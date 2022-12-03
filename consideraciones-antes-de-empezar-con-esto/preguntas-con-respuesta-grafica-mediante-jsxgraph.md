---
description: >-
  ACTUALMENTE (10-06-2021) EN LA INSTALACIÓN DE MOODLE DE LA COMUNIDAD
  VALENCIANA ESTÁ DISPONIBLE EL FILTRO JSXGRAPH, LO QUE SIMPLIFICA LA
  UTILIZACIÓN DE JSXGRAPH EN LAS PREGUNTAS DE FORMULAS.
---

# Preguntas con respuesta gráfica mediante JSXGraph



{% hint style="danger" %}
Se recomienda utilizar el filtro de JSXGraph en caso de estar disponible, ya que simplifica la integración de JSXGraph y Moodle.
{% endhint %}

## ¿Qué queremos hacer?

Se trata de crear una pregunta en se pida al usuario que mueva dos puntos para que el vector que representan sea un vector aleatorio dado.

![](<../.gitbook/assets/image (97).png>)

### Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Preguntas-Arrastrar puntos para dibujar vector dado-20200617-1152.xml" %}

{% hint style="danger" %}
Recuerda que el **editor de texto por defecto de Moodle** puede hacer que el código se vuelva inutilizable. Ver [Preguntas "menos sencillas"](./#el-editor-de-texto-de-moodle-estropea-el-codigo).
{% endhint %}

## Referencias

La información aquí mostrada se ha extraído básicamente de tres proyectos cofinanciados por la Unión Europea:

* Proyecto COMPASS: [https://moodle.compasspro.eu/](https://moodle.compasspro.eu/)
* Proyecto SCORE: [https://moodle.scorepro.eu/](https://moodle.scorepro.eu/)
* Proyecto ITEMS: [https://moodle.itemspro.eu/](https://moodle.itemspro.eu/)

A través de los enlaces se puede acceder a los cursos de Moodle donde se encuentran los materiales generados en dichos proyectos.

## Particularidades y limitaciones de Aules

Este tipo de preguntas aporta una nueva funcionalidad a las preguntas de tipo Fórmulas, para la que no estaban inicialmente pensadas. Ello obliga a generar código Javascript más complicado que el que se ha utilizado hasta ahora.

{% hint style="info" %}
La idea es adaptar el código de una pregunta funcional para generar nuevas preguntas.&#x20;

No será necesario comprender el código al 100%.
{% endhint %}

{% hint style="warning" %}
Posiblemente la pregunta STACK sería más apropiada para este uso pero como no disponemos de ella en Aules, utilizaremos la pregunta Fórmulas.
{% endhint %}

## Esquema general de la pregunta

Habrá que definir varias cosas:

1. Un Script que permita conectar la vista gráfica con la respuesta del estudiante almacenada en Moodle.
2. Un Script para mostrar la vista gráfica. Será muy parecido al utilizado para mostrar gráficos dinámicos pero incorporará información para establecer los parámetros que deseamos pasar como respuesta a Aules.

Como variables aleatorias únicamente tendremos las coordenadas del vector buscado:

![](<../.gitbook/assets/image (109).png>)

En el enunciado de la pregunta tendremos:

```javascript
//Cargamos la librería JSXGraph.
<script type="text/javascript" src="https://jsxgraph.uni-bayreuth.de/distrib/jsxgraphcore.js"></script>

//Cargamos la librería jquery
<script type="text/javascript" src="https://code.jquery.com/jquery-3.1.0.min.js"></script>

//Este script será común a cualquier pregunta con respuestas gráficas
//No cambiaremos nada de una a otra pregunta
<script type="text/javascript">
    var JSXQuestion = function (elmID, jsxCode, debug) {
        var thiz = this;
        thiz.elm = document.getElementById(elmID);
        thiz.inputs = $(thiz.elm).closest(".qtext").children(".formulaspart").find("input");
        $(thiz.elm).closest(".qtext").children(".formulaspart").children("formulaspartoutcome").hide();
        if (debug !== true) {
            thiz.inputs.hide();
        }
        thiz.solved = $(thiz.inputs[0]).prop('readonly');


        thiz.set = function (idx, val) {
            if (!thiz.solved && thiz.inputs && thiz.inputs[idx]) {
                thiz.inputs[idx].value = Math.round(val * 100) / 100;
            }
        };
        thiz.get = function (idx) {
            if (thiz.inputs && thiz.inputs[idx]) {
                var n = parseFloat(thiz.inputs[idx].value);
                if (isNaN(n)) {
                    return null
                }
                return n;
            }
            return null;
        };

        thiz.brd = null;
        jsxCode(thiz);

        thiz.reload = function () {
            jsxCode(thiz);
        };
    };
</script>


//Enunciado de la pregunta
    <p> Mueve los puntos para representar un vector que tenga por coordenadas \(({v1},{v2})\).</p>
<br>
   
    
//Contenedor para la gráfica 
//Hay que cambiar el id para que no coincida entre diferentes pregunats de un mismo cuestionario   
<div id="box1" class="jxgbox" style="width:300px; height:150px;margin-left:auto; margin-right:auto;"></div>

//Código de la gráfica
<script type="text/javascript">
    $(function () {
        var jsxCode = function (main) {
            var width = 400;
            var height = 400;
            main.elm.setAttribute("style", "width:" + width + "px; height:" + height + "px;margin-left:auto; margin-right:auto;");

            if (main.brd != null) JXG.JSXGraph.freeBoard(main.brd);
            main.brd = JXG.JSXGraph.initBoard(main.elm.id, {
                boundingbox: [0, 10, 10, 0],
                showCopyright: false,
                showNavigation: false
            });
            var brd = main.brd;
            var grid = brd.create('grid', []);

//Este es uno de los puntos que forman el vector
//Primero miramos si hay alguna respuesta almacenada y, sin no, inicializamos
            
            var tx = main.get(0);
            if (tx === null) {
                tx = Math.random() * 3 + 1;
            }
            var ty = main.get(1);
            if (ty === null) {
                ty = Math.random() * 3 + 1;
            }

//Dibujamos el punto, que estará fijo una vez se haya contestado a la pregunta
            var t = brd.create('point', [tx, ty], {
                fixed: main.solved,
                name: "",
                snapToGrid:true,
                showInfobox:false
            });

//Este es el segundo de los puntos que forman el vector
            var sx = main.get(2);
            if (sx === null) {
                sx = Math.random() * 3 + 1;
            }
            var sy = main.get(3);
            if (sy === null) {
                sy = Math.random() * 3 + 1;
            }

            var s = brd.create('point', [sx, sy], {
                fixed: main.solved,
                name: "",
                snapToGrid:true,
                showInfobox:false
            });

//Dibujamos el vector que une los puntos            
            var lin = brd.create('segment',[t,s], 
 {touchLastPoint: true,lastArrow: {type: 2,size: 6}});

//Función que pasará las coordenadas de los puntos a las variables _0, _1, _2, _3
            var check = function () {
                main.set(0, t.X());
                main.set(1, t.Y());
                main.set(2, s.X());
                main.set(3, s.Y())
            }
            
            check();
            
//Pasamos el valor de la variable cada vez que se muevan los puntos           
            t.on('drag', function () {
                check();
            });
            s.on('drag', function () {
                check();
            });
            
            brd.update();
        };

//Esto siempre será igual. Únicamente habrá de modificarse el "box1" por el 
//id que tenga el div (no pueden coincidir entre preguntas diferentes)
        new JSXQuestion("box1", jsxCode, false);
    });
    
</script>
```

Con esto, tendremos una gráfica con un vector $$\vec{v}=\vec{ts}$$ . Cada vez que se mueven los puntos que definen el vector, automáticamente se graban las coordenadas de los puntos en las variables de respuesta del estudiante:

* \_0=Coordenada x del punto t.
* \_1=Coordenada y del punto t.
* \_2=Coordenada x del punto s.
* \_3=Coordenada y del punto s.

Nos quedará comprobar si la respuesta es correcta o no.

### Calificación de la respuesta

![](<../.gitbook/assets/image (36).png>)

{% hint style="info" %}
Puesto que es una actividad de respuesta abierta, usaremos el **criterio de calificación** para evaluar la respuesta.
{% endhint %}

{% hint style="success" %}
El valor indicado en **Respuesta\* es una respuesta válida cualquiera** (únicamente sirve para mostrar al alumno la respuesta correcta si así decidimos hacerlo en la configuración del cuestionario)
{% endhint %}

La comprobación será (ambas deben verificarse al mismo tiempo):

* Coordenada x del extremo (\_2) - Coordenada x del origen (\_0) = Coordenada x del vector (v1)
* Coordenada y del extremo (\_3) - Coordenada y del origen (\_1) = Coordenada y del vector (v2)

## Adaptar preguntas

Basándonos en la pregunta anterior vamos a **crear una pregunta** que muestre los ejes cartesianos, dos puntos, la recta que los une y, dada una ecuación en forma continua, nos pida mover los puntos para que la recta mostrada corresponda con la ecuación.

![](<../.gitbook/assets/image (65).png>)

{% hint style="success" %}
Esencialmente esta pregunta es **muy parecida** a la anterior: el usuario interacciona con **dos puntos** y realizamos comprobaciones para ver si dichos puntos cumplen con una serie de condiciones.
{% endhint %}

### Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Preguntas-Arrastrar puntos para dibujar recta continua-20200617-1348.xml" %}

{% hint style="danger" %}
Recuerda que el **editor de texto por defecto de Moodle** puede hacer que el código se vuelva inutilizable. Ver [Preguntas "menos sencillas"](./#el-editor-de-texto-de-moodle-estropea-el-codigo).
{% endhint %}

### Estrategia para definir la pregunta

* Generamos un **nombre aleatorio para el contenedor de la gráfica**, para no preocuparnos por la coincidencia de nombres entre distintas preguntas.
* Generamos un **punto y un vector aleatorios** que definirán la recta objetivo.
* Calculamos, a partir de estos, otro punto que utilizaremos **únicamente** para incluir como respuesta correcta en la parte.
* **Comprobaremos** la respuesta **sustituyendo directamente** en la ecuación de la recta los dos puntos introducidos por el usuario.
* También comprobaremos que los dos puntos sean **diferentes** para evitar dar por válidas preguntas en que los dos puntos son coincidentes.

![](<../.gitbook/assets/image (41).png>)

{% hint style="info" %}
Obsérvese que para pasar ecuaciones en $$\LaTeX$$ a través de variables es necesario escapar las \ (introduciendo otra \ previa).&#x20;

Los numeradores de la ecuación continua se han generado mediante la función **poly()** para no tener que estar pendientes del signo de p1 y p2 y evitar expresiones del tipo x--3 (signo menos duplicado).

Para generar la ecuación se ha usado la función **join()** para enlazar cadenas de texto y la función **str()** para convertir valores numéricos a cadenas de texto.
{% endhint %}

En el enunciado de la pregunta:

```javascript
<script type="text/javascript" src="https://jsxgraph.uni-bayreuth.de/distrib/jsxgraphcore.js"></script>
<script type="text/javascript" src="https://code.jquery.com/jquery-3.1.0.min.js"></script>
<script type="text/javascript">
    var JSXQuestion = function(elmID, jsxCode, debug) {
        var thiz = this;
        thiz.elm = document.getElementById(elmID);
        thiz.inputs = $(thiz.elm).closest(".qtext").children(".formulaspart").find("input");
        $(thiz.elm).closest(".qtext").children(".formulaspart").children("formulaspartoutcome").hide();
        if (debug !== true) {
            thiz.inputs.hide();
        }
        thiz.solved = $(thiz.inputs[0]).prop('readonly');


        thiz.set = function(idx, val) {
            if (!thiz.solved && thiz.inputs && thiz.inputs[idx]) {
                thiz.inputs[idx].value = Math.round(val * 100) / 100;
            }
        };
        thiz.get = function(idx) {
            if (thiz.inputs && thiz.inputs[idx]) {
                var n = parseFloat(thiz.inputs[idx].value);
                if (isNaN(n)) {
                    return null
                }
                return n;
            }
            return null;
        };

        thiz.brd = null;
        jsxCode(thiz);

        thiz.reload = function() {
            jsxCode(thiz);
        };
    };
</script>

//Hasta aquí es exactamente igual que la anterior

<p>Mueve los puntos para que la recta representada corresponda con la ecuación</p> {ecuacion}
<br>

//Aquí únicamente cambiamos el nombre del contenedor (aleatorizado)
<div id="{MB}" class="jxgbox" style="width:400px; height:400px;margin-left:auto; margin-right:auto;"></div>

<script type="text/javascript">
    $(function() {
        var jsxCode = function(main) {
            var width = 400;
            var height = 400;
            main.elm.setAttribute("style", "width:" + width + "px; height:" + height + "px;margin-left:auto; margin-right:auto;");

            if (main.brd != null) JXG.JSXGraph.freeBoard(main.brd);
            main.brd = JXG.JSXGraph.initBoard(main.elm.id, {
                boundingbox: [-10, 10, 10, -10],
                showCopyright: false,
                axis: true, //ahora sí que queremos los ejes
                showNavigation: false
            });
            var brd = main.brd;
            var grid = brd.create('grid', []);

            var tx = main.get(0);
            if (tx === null) {
                tx = Math.random() * 3 + 1;
            }
            var ty = main.get(1);
            if (ty === null) {
                ty = Math.random() * 3 + 1;
            }

            var t = brd.create('point', [tx, ty], {
                fixed: main.solved,
                name: "",
                snapToGrid: true,
                showInfobox: true,
            });

            var sx = main.get(2);
            if (sx === null) {
                sx = Math.random() * 3 + 1;
            }
            var sy = main.get(3);
            if (sy === null) {
                sy = Math.random() * 3 + 1;
            }

            var s = brd.create('point', [sx, sy], {
                fixed: main.solved,
                name: "",
                snapToGrid: true,
                showInfobox: true
            });

            var lin = brd.create('line', [t, s],{fixed: main.solved} );

//Igual que antes, únicamente cambia que ahora dibujamos una recta y no un vector

            var check = function() {
                main.set(0, t.X());
                main.set(1, t.Y());
                main.set(2, s.X());
                main.set(3, s.Y())
            }
            check();
            t.on('drag', function() {
                check();
            });
            s.on('drag', function() {
                check();
            });
            brd.update();
        };

        new JSXQuestion("{MB}", jsxCode, false);
    });
</script>
```

### Calificar la respuesta

![](<../.gitbook/assets/image (13).png>)

{% hint style="success" %}
* El punto "t" debe verificar la ecuación.
* El punto "s" debe verificar la ecuación.
* Los puntos "t" y "s" no pueden coincidir.

&#x20;( (\_0-p1)/v1==(\_1-p2)/v2 )&&( (\_2-p1)/v1==(\_3-p2)/v2 )&&(\_0!=\_2&&\_1!=\_3)
{% endhint %}

{% hint style="info" %}
**Prácticamente con el mismo código** hemos hecho una pregunta aparentemente muy diferente.
{% endhint %}

## Pregunta de respuesta abierta

Queremos preparar una pregunta que pida al usuario que interaccione con una serie de puntos para que el resultado sea una función que verifique una serie de condiciones:

![](<../.gitbook/assets/image (30).png>)

### Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Preguntas-Crear gráficamente función que cumpla restricciones-20200618-1306.xml" %}

### Estrategia para definir la pregunta

* La pregunta debe capturar **8 entradas del usuario** (la coordenada y de cada uno de los puntos)
* Introduciremos **aleatoriedad mediante varios parámetros** a, b, c, d, e; algunos de los cuales hemos acabado por fijar para no complicar demasiado la casuística resultante.
* El código será muy parecido a las preguntas anteriores, solamente que incluye más puntos.
* Generaremos las variables sol1 hasta sol7 que serán una posible respuesta correcta.

![](<../.gitbook/assets/image (62).png>)

En texto de la parte:

```javascript
<script type="text/javascript" src="https://jsxgraph.uni-bayreuth.de/distrib/jsxgraphcore.js"></script>
<script type="text/javascript" src="https://code.jquery.com/jquery-3.1.0.min.js"></script>

<script type="text/javascript">
var JSXQuestion = function (elmID, jsxCode, debug) {
        var thiz = this;
        thiz.elm = document.getElementById(elmID);
        thiz.inputs = $(thiz.elm).closest(".formulaspart").find("input");
        $(thiz.elm).closest(".formulaspart").children("formulaspartoutcome").hide();
        if (debug !== true) {
            thiz.inputs.hide();
        }
        thiz.solved = $(thiz.inputs[0]).prop('readonly');


        thiz.set = function (idx, val) {
            if (!thiz.solved && thiz.inputs && thiz.inputs[idx]) {
                thiz.inputs[idx].value = Math.round(val * 100) / 100;
            }
        };
        thiz.get = function (idx) {
            if (thiz.inputs && thiz.inputs[idx]) {
                var n = parseFloat(thiz.inputs[idx].value);
                if (isNaN(n)) {
                    return null
                }
                return n;
            }
            return null;
        };

        thiz.brd = null;
        jsxCode(thiz);

        thiz.reload = function () {
            jsxCode(thiz);
        };
    };
</script>

//Hasta aquí es idéntico a las preguntas anteriores

<div id="{MB}" class="jxgbox" style="width:400px; height:400px;margin-left:1px; margin-right:auto;"></div>

<script type="text/javascript">
    $(function () {
        var jsxCode = function (main) {
            main.brd = JXG.JSXGraph.initBoard(main.elm.id, {
                boundingbox:[-1,10,10,-10], showNavigation:false, showCopyright:false, grid:false, axis:true, zoom: {enabled:false,wheel: false}, pan: {enabled:false, needTwoFingers: false}  
            }); //Únicamente queremos ver las x positivas
            var brd = main.brd;

brd.options.point.showInfobox=true;

 
//Los 8 valores que queremos "capturar" (el primero será el _0...)
var t0y = main.get(0);if (t0y === null) {t0y =0; }
var t1y = main.get(1);if (t1y === null) {t1y = 0; }
var t2y = main.get(2);if (t2y === null) {t2y = 0; }
var t3y = main.get(3);if (t3y === null) {t3y = 0; }
var t4y = main.get(4);if (t4y === null) {t4y = 0; }
var t5y = main.get(5);if (t5y === null) {t5y = 0; }
var t6y = main.get(6);if (t6y === null) {t6y = 0; }
var t7y = main.get(7);if (t7y === null) {t7y = 0; }


//Dibujamos los puntos 
var p0 = brd.create('point', [0,t0y], {snapToGrid:true, snapSizeX:0.5, snapSizeY:0.5, fixed: main.solved});
var p1 = brd.create('point', [1,t1y], {snapToGrid:true, snapSizeX:0.5, snapSizeY:0.5, fixed: main.solved});
var p2 = brd.create('point', [2,t2y], {snapToGrid:true, snapSizeX:0.5, snapSizeY:0.5, fixed: main.solved});
var p3 = brd.create('point', [3,t3y], {snapToGrid:true, snapSizeX:0.5, snapSizeY:0.5, fixed: main.solved});
var p4 = brd.create('point', [4,t4y], {snapToGrid:true, snapSizeX:0.5, snapSizeY:0.5, fixed: main.solved});
var p5 = brd.create('point', [5,t5y], {snapToGrid:true, snapSizeX:0.5, snapSizeY:0.5, fixed: main.solved});
var p6 = brd.create('point', [6,t6y], {snapToGrid:true, snapSizeX:0.5, snapSizeY:0.5, fixed: main.solved});
var p7 = brd.create('point', [7,t7y], {snapToGrid:true, snapSizeX:0.5, snapSizeY:0.5, fixed: main.solved});

//Limitamos el movimiento de los puntos al eje y
brd.on('move', function(){
        p0.moveTo([0, p0.Y()]);
        p1.moveTo([1, p1.Y()]);
        p2.moveTo([2, p2.Y()]);
        p3.moveTo([3, p3.Y()]);
        p4.moveTo([4, p4.Y()]);
        p5.moveTo([5, p5.Y()]);
        p6.moveTo([6, p6.Y()]);
        p7.moveTo([7, p7.Y()]);
});

//Dibujamos los segmentos que unen los puntos (no queremos que se muevan al arrastrarlos con el ratón)
var s01=brd.create('segment', [p0,p1],{fixed:true});
var s02=brd.create('segment', [p1,p2],{fixed:true});
var s03=brd.create('segment', [p2,p3],{fixed:true});
var s04=brd.create('segment', [p3,p4],{fixed:true});
var s05=brd.create('segment', [p4,p5],{fixed:true});
var s06=brd.create('segment', [p5,p6],{fixed:true});
var s07=brd.create('segment', [p6,p7],{fixed:true});


//Función que traslada los valores de comprobación a las variables (_0, _1,...) de Moodle
var check =  function(){
        main.set(0, p0.Y());
        main.set(1, p1.Y());
        main.set(2, p2.Y());
        main.set(3, p3.Y());
        main.set(4, p4.Y());
        main.set(5, p5.Y());
        main.set(6, p6.Y());
        main.set(7, p7.Y());
        }
        
        check();

//Cada vez que el usuario mueva un puneto, actualizamos la respuesta
p0.on('drag', function () {
                check();
            });
p1.on('drag', function () {
                check();
            });
p2.on('drag', function () {
                check();
            });
p3.on('drag', function () {
                check();
            });
p4.on('drag', function () {
                check();
            });
p5.on('drag', function () {
                check();
            });
p6.on('drag', function () {
                check();
            });
p7.on('drag', function () {
                check();
            });


brd.update();
          
        };

        new JSXQuestion("{MB}", jsxCode, false);
    });
</script>
```

### Calificar la respuesta

Dado que hay que realizar numerosas comprobaciones, va a ser útil utilizar las **variables de calificación**:

{% hint style="success" %}
Para visualizar las variables de calificación hay que pulsar en **Ver más...** al final de la parte.
{% endhint %}

1. Comprobamos aisladamente las condiciones y
2. Calificamos imponiendo que se cumplan todas las condiciones simultáneamente

![](<../.gitbook/assets/image (99).png>)
