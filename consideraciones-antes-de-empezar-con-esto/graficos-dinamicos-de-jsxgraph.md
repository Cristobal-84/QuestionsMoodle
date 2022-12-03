---
description: >-
  ACTUALMENTE (10-06-2021) EN LA INSTALACIÓN DE MOODLE DE LA COMUNIDAD
  VALENCIANA ESTÁ DISPONIBLE EL FILTRO JSXGRAPH, LO QUE SIMPLIFICA LA
  UTILIZACIÓN DE JSXGRAPH EN LAS PREGUNTAS DE FORMULAS.
---

# Gráficos dinámicos de JSXGraph

{% hint style="danger" %}
Se recomienda utilizar el filtro de JSXGraph en caso de estar disponible, ya que simplifica la integración de JSXGraph y Moodle.
{% endhint %}

## ¿Qué queremos hacer?

Se trata de generar **gráficos en base a parámetros aleatorios**, de modo que el gráfico que se muestre cada vez que se genera una nueva pregunta sea diferente para cada alumno.

En este caso queremos crear una gráfica que incluya:

* Ejes cartesianos visibles entre -10 y 10 en ambos ejes.
* Tres puntos:&#x20;
  * A aleatorio en el primer cuadrante.
  * B aleatorio en el segundo cuadrante.
  * C sobre el eje y negativo.

Se pedirá que el alumno introduzca las coordenadas de los puntos.

## Archivo XML de referencia

![](<../.gitbook/assets/image (107).png>)

{% file src="../.gitbook/assets/preguntas-Aules-Plano cartesiano 3 puntos-20200531-1303.xml" %}

## Qué es JSXGraph

Es una librería de Javascript que utilizaremos para realizar gráficos a partir de las variables de la pregunta de fórmulas.

La documentación de la librería se encuentra en [https://jsxgraph.uni-bayreuth.de/wp/index.html](https://jsxgraph.uni-bayreuth.de/wp/index.html)

{% hint style="info" %}
Para personalizar los gráficos y utilizar **todas las opciones** será necesario explorar la documentación de referencia de la librería en [https://jsxgraph.org/docs/index.html](https://jsxgraph.org/docs/index.html)
{% endhint %}

{% hint style="success" %}
En un principio y, **para comenzar a familiarizarse con ella**, es recomendable reutilizar fragmentos de código de la Wiki en [https://jsxgraph.org/wiki/index.php/Main\_Page](https://jsxgraph.org/wiki/index.php/Main\_Page)
{% endhint %}

{% hint style="info" %}
Partiendo de una **pregunta funcional** que incluya una gráfica, es relativamente sencillo **adaptarla** para presentar otra representación gráfica.
{% endhint %}

## Scripts

Introduciremos las gráficas a través de **scripts** que se ejecutarán o en el enunciado de la pregunta o en las partes.

Los scripts son **fragmentos de código Javascript** que permitirán la elaboración de gráficos programáticamente.

{% hint style="info" %}
Los gráficos se generan mediante código Javascript.
{% endhint %}

Por ejemplo, para generar el punto (-3,1) haríamos algo del estilo a:

```
var p = board.create('point',[-3,1]);
```

## Scripts en pregunta Fórmulas

{% hint style="danger" %}
Recuerda que el **editor de texto por defecto de Moodle** puede hacer que el código se vuelva inutilizable. Ver [Preguntas "menos sencillas"](./#el-editor-de-texto-de-moodle-estropea-el-codigo).
{% endhint %}

Veamos cómo se ha hecho la pregunta de ejemplo de este apartado. He comentado el código para que se vea paso a paso lo que se va haciendo.

```javascript
//Generamos un div para meter dentro la gráfica.
//este div configura el tamaño de la gráfica y su posición
//luego explicaremos el nombre del div: es importante que no se repita

<div id='{MB}' class="jxgbox" style="width:400px; height:400px;margin-left:1px; margin-right:auto;"></div>

//Referencia a la biblioteca que vamos a utilizar

<script type="text/javascript" src="https://jsxgraph.uni-bayreuth.de/distrib/jsxgraphcore.js"></script>

//Este es el script que rellena el contenedor de la gráfica

<script type="text/javascript">
  
  //No necesario, pero es cómodo para no tener que andar con las {} para referirnos
  //a las variables que hemos definido en la pregunta
  
  var a1={a1}; //Para no tener que poner llaves en el código del script
  var a2={a2};
  var b1={b1};
  var b2={b2};
  var c1={c1};
  var c2={c2};

  //Esta primera variable es la que forma el área de trazado y coloca los ejes.
  //siempre debe estar y el nombre debe ser el mismo que el del div del principio
  //además, el div no puede repetirse entre gráficas del mismo cuestionario
  //por eso se aleatoriza el nombre y sería conveniente editar algo entre preguntas
  //para que fuese imposible que coincidiera entre preguntas distintas
  
  var brd = JXG.JSXGraph.initBoard('{MB}', {
    boundingbox: [-10.5, 10.5, 10.5, -10.5],
    axis:true,
    grid: true,
    showCopyright: false,
    shownavigation:false,
    zoom: {
      enabled: false,
      wheel: false
    },
    pan: {
      enabled: false,
      needTwoFingers: false
    }
  });
  
  //Podemos establecer opciones generales para toda la construcción
  
  brd.options.point.showInfobox=false;
  brd.options.point.withlabel=true;
  brd.options.point.visible=true;
   

  //Creamos los puntos
  
  var ptoA=brd.create('point', [a1,a2], {
    name: 'A',
    withlabel:true,
    visible:true,
    label:{autoposition:true},
    fixed:true
  });
     
   var ptoB=brd.create('point', [b1,b2], {
    name: 'B',
    withlabel:true,
    visible:true,
    label:{autoposition:true},
    fixed:true
  });

 var ptoC=brd.create('point', [c1,c2], {
    name: 'C',
    withlabel:true,
    visible:true,
    label:{autoposition:true},
    fixed:true
  });
   
//Actualización de la visualización  

brd.update(); 

</script>

```

Los scripts se introducen con `<script>` y se cierran con `<\script>`.

## Adaptar preguntas

Vamos a intentar hacer una pregunta que muestre:

* Dos puntos A (en el origen) y B en OX positivo.
* Un tercer punto C ubicado en el primer cuadrante que forme triángulo acutángulo.
* El triánguno que forman.
* La altura del triángulo correspondiente al vértice C con línea discontinua.

Para ello necesitaremos construir cuatro segmentos además de los tres puntos.

![](<../.gitbook/assets/image (12).png>)

Visitando la wiki de JSXGraph ([https://jsxgraph.org/wiki/index.php/Main\_Page](https://jsxgraph.org/wiki/index.php/Main\_Page)) y buscando por **segment** podemos ver varios ejemplos de segmentos: el primero de ellos se adapta a lo que buscamos. Copiamos y pegamos en nuestro código.

![](<../.gitbook/assets/image (69).png>)

{% hint style="warning" %}
Tendremos que ver que:

* [x] Coincide la identicación del board con el nuestro: antes de .create debe estar el nombre de la variable con que hemos creado el "Board".
* [ ] Los puntos por los que pasa coinciden con los nuestros. En este caso cambiaremos p0 y p1 por ptoA y ptoB, para el lado AB.
* [ ] El nombre lo borraremos ya que no nos interesa en este momento o directamente cambiamos withLabel a false y ya no se mostrará la etiqueta.
* [ ] La línea de código siempre tiene que terminar en ;
{% endhint %}

&#x20;Con esto tenemos a continuación de los tres puntos:

```javascript
<div id='{MB}' class="jxgbox" style="width:400px; height:400px;margin-left:1px; margin-right:auto;"></div>


<script type="text/javascript" src="https://jsxgraph.uni-bayreuth.de/distrib/jsxgraphcore.js"></script>



<script type="text/javascript">
  

  
  var a1=0; //Para no tener que poner llaves en el código del script
  var a2=0;
  var b1={b1};
  var b2=0;
  var c1={c1};
  var c2={c2};

  
  var brd = JXG.JSXGraph.initBoard('{MB}', {
    boundingbox: [-1, 10.5, 10.5, -1], //cambiamos los ejes para un mejor encuadre
    axis:true,
    grid: false, //no necesitamos la cuadrícula
    showCopyright: false,
    shownavigation:false,
    zoom: {
      enabled: false,
      wheel: false
    },
    pan: {
      enabled: false,
      needTwoFingers: false
    }
  });
  
  //Podemos establecer opciones generales para toda la construcción
  
  brd.options.point.showInfobox=true; //Para que al parar el ratón sobre un 
                                      //punto se vean las coordenadas
  brd.options.point.withlabel=false; //No queremos que se vean los nombres
  brd.options.point.visible=true;
   

  //Creamos los puntos
  var ptoA=brd.create('point', [a1,a2], {
    name: 'A', //realmente no es necesario ponerle nombre
    fixed:true
  });
     
  var ptoB=brd.create('point', [b1,b2], {
    name: 'B', 
    fixed:true //si no indicamos que es fijo
  });

  var ptoC=brd.create('point', [c1,c2], {
    name: 'C', 
    fixed:false //el punto podría moverse y no nos interesa en este caso
  });
 
  //Lado AB (el código puede ir en línea)
  var AB= brd.create('segment', [ptoA, ptoB], {withLabel:false, name:''});

  //Lado BC   
  var BC= brd.create('segment', [ptoB, ptoC], {withLabel:false, name:''});

  //Lado AC (o puede distribuirse en varias líneas)  
  var AC = brd.create('segment', [ptoA, ptoC], {
    withLabel: false,
    name: ''
  });
  
  //Altura del triángulo (será otro segmento)
  var altura = brd.create('segment', [ptoC,[c1,0]], {
    withLabel: false,
    name: '',
    dash:3 //hace que el segmento sea a trazos
  });

  brd.update(); 

</script>


```

{% hint style="success" %}
Simplemente trazando cuatro segmentos tenemos una pregunta totalmente diferente.

Únicamente hemos adaptado el código que ya teníamos y hemos incluido los elementos que necesitábamos.
{% endhint %}

{% hint style="danger" %}
JSXGraph es una biblioteca de geometría dinámica, por lo que **los elementos que creamos pueden moverse** si no los fijamos.

En este ejemplo no hemos fijado el vértice superior del triángulo y el usuario podría moverlo. Tenemos un comportamiento del gráfico totalmente indeseado.

Hay que comprobar que la construcción no tenga un "dinamismo" que no debiera.
{% endhint %}

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Aules-Hallar área de triángulo conocidos los vértices en cartesianas-20200531-2116.xml" %}

## Ayudas para la redacción de este tipo de preguntas

{% hint style="warning" %}
Redactar una pregunta con tanto código directamente en el editor de Moodle y que al previsualizar todo funcione como debe es altamente improbable.

Con que falte una coma o haya cualquier errata, no se mostrará el gráfico.
{% endhint %}

{% hint style="success" %}
Resultará interesante utilizar algún editor de código que nos permita visualizar la construcción conforme la hacemos.

Con esto tendremos varias ventajas. Entre ellas:

* El editor resalta con colores la sintaxis y ayuda a leer el código.
* En caso de equivocarnos, veremos en tiempo real que la construcción no funciona.
{% endhint %}

Algunas de las opciones que se pueden usar son:

{% embed url="https://codepen.io/DavidGaliana/pen/rNOXXRV" %}

{% embed url="https://jsfiddle.net/DavidGaliana/jtgeboah/" %}

Puesto que a la hora de realizar la construcción no nos importa demasiado el valor de las variables que se aleatorizan y definen en Fórmulas, es cómodo asignar valores fijos para realizar la construcción:

```javascript
  var a1 = 0; //Después introduciremos aquí las variables de la pregunta
  var a2 = 0; //Ya sean aleatorias o globales
  var b1 = 8;
  var b2 = 0;
  var c1 = 5;
  var c2 = 6;
```

Al pasar  el script a Moodle asignaremos las variables del script, pero sabiendo que el script funciona correctamente:

```javascript
  var a1 = {a1}; //Para que tome el valor declarado en la pregunta de Moodle
  var a2 = {a2}; 
  var b1 = {b1};
  var b2 = {b2};
  var c1 = {c1};
  var c2 = {c2};
```

## Un mundo de posibilidades

{% hint style="success" %}
Con elementos muy sencillos se puede crear **todo tipo de gráficos** para preguntas STEM.
{% endhint %}

{% hint style="info" %}
Hay **multitud de ejemplos** de gráficos en la Wiki de JSXGraph y en la propia referencia de la biblioteca.
{% endhint %}

{% hint style="warning" %}
En un principio, parece complicado mostrar gráficos dinámicos pero se trata más de **saber qué bloque de código incluir** de acuerdo a nuestras necesidades que de ser programador de Javascript.&#x20;
{% endhint %}

{% hint style="success" %}
La biblioteca JSXGraph está **muy bien documentada**.
{% endhint %}
