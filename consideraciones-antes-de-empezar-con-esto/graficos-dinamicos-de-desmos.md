# Gráficos dinámicos de Desmos

## ¿Qué queremos hacer?

Se trata de generar **gráficos en base a parámetros aleatorios**, de modo que el gráfico que se muestre cada vez que se genera una nueva pregunta sea diferente para cada alumno.

En este caso vamos a generar una función con tres trozos y se pedirá al alumno la ecuación de los tres trozos y las abscisas en que cambia la rama.

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Preguntas-Función a trozos hallar ecuación-20200527-0819.xml" %}

![](<../.gitbook/assets/image (105).png>)

![](<../.gitbook/assets/image (78).png>)

![](<../.gitbook/assets/image (26).png>)

{% hint style="warning" %}
Ahora que empieza a haber  más código en las preguntas, será conveniente ir buscando algún editor de código que resalte por colores para simplificar la redacción y lectura de lo que hacemos.
{% endhint %}

Enunciado de la pregunta:

```javascript
<h4>Completa:</h4><p>Recuerda que puedes hacer zoom (rueda del ratón) para acercar o alejar la gráfica.</p>

<script src="https://www.desmos.com/api/v1.4/calculator.js?apiKey=dcb31709b452b1cf9dc26972add0fda6"></script>

<div id="calculator" style="width: 600px; height: 400px;"></div>

<script>
    var elt = document.getElementById('calculator');
    var calculator = Desmos.GraphingCalculator(elt, {
        expressions: false,
        settingsMenu: false,
        zoomButtons: false
    });
  
  // PRIMER TROZO
    calculator.setExpression({
        id: 'graph1',
        latex: 'y=-{a}\\left \\{ x<{b}  \\right \\}',
        color: Desmos.Colors.BLUE
    });
  
    calculator.setExpression({
        id: 'pointB',
        latex: 'B=({b},-{a})',
        pointStyle: Desmos.Styles.POINT,
        dragMode: Desmos.DragModes.NONE,
        color: Desmos.Colors.PURPLE
    });
   
     // SEGUNDO TROZO 
    calculator.setExpression({
        id: 'graph2',
        latex: 'y={a}*x+{b}\\left \\{ {b}<x<{c}  \\right \\}',
        color: Desmos.Colors.BLUE
    });
    calculator.setExpression({
        id: 'pointC',
        latex: 'C=({b},{a}*{b}+{b})',
        pointStyle: Desmos.Styles.OPEN,
        dragMode: Desmos.DragModes.NONE,
        color: Desmos.Colors.PURPLE
    });
    calculator.setExpression({
        id: 'pointD',
        latex: 'D=({c},{a}*{c}+{b})',
        pointStyle: Desmos.Styles.OPEN,
        dragMode: Desmos.DragModes.NONE,
        color: Desmos.Colors.PURPLE
    });
 
   //TERCER TROZO		

    calculator.setExpression({
        id: 'graph3',
        latex: 'y={a}\\left \\{ x>{c}  \\right \\}',
        color: Desmos.Colors.BLUE
    });
 
   calculator.setExpression({
        id: 'pointE',
        latex: 'E=({c},{a})',
        pointStyle: Desmos.Styles.POINT,
        dragMode: Desmos.DragModes.NONE,
        color: Desmos.Colors.PURPLE
    });
  
</script>

<br> \(f(x) = \begin{cases} f(x) &amp; si &amp; a \leq x \\ g(x) &amp; si &amp; a &lt; x &lt; b \\ h(x) &amp; si &amp; b \leq x \end{cases} \) <br><br> a=
<div style="display:inline-block;">{#1}</div> b=
<div style="display:inline-block;">{#2}</div><br> f(x)=
<div style="display:inline-block;">{#3}</div><br> g(x)=
<div style="display:inline-block;">{#4}</div><br> h(x)=
<div style="display:inline-block;">{#5}</div>



```

Resumiendo lo que se ha hecho en la pregunta:

1. Enunciado
2. Conectar mediante un script con la API de la calculadora gráfica Desmos.
3. Definir un contenedor de tamaño 600x400 para alojar la gráfica.
4. Mediante otro script, rellenar ese contenedor mediante puntos y rectas definidas en base a las variables a, b, c definidas en la pregunta.

![](<../.gitbook/assets/image (121).png>)

{% hint style="success" %}
Las variables se deben pasar a la API de Desmos entre llaves (igual que cuando queremos que aparezcan con su valor numérico en un enunciado).
{% endhint %}

Por último, se ha escrito la función a trozos en $$\LaTeX$$y se ha hecho 5 partes para recopilar cada uno de los 5 campos de respuesta.&#x20;

{% hint style="info" %}
En un principio, la idea debería ser adaptar una pregunta de este tipo para representar otra gráfica cualquiera.
{% endhint %}

Para ello, bastará consultar la [documentación de la API de Desmos](https://www.desmos.com/api/v1.5/docs/index.html) y añadir o eliminar fragmentos de código según nuestras necesidades.

{% hint style="danger" %}
Esta pregunta **no es apta para utilizar directamente con alumnos** ya que, en ocasiones, las ramas se solapan y da la sensación de que hay una discontinuidad en el punto de unión.&#x20;

Modificadla antes de utilizarla para no confundir al alumnado. Bastaría dibujar primero la rama central para que al dibujar la de la izquierda, que acaba con el punto relleno, quede visible en caso de coincidir.
{% endhint %}

![](<../.gitbook/assets/image (42).png>)

## Y por qué al principio del documento no se recomiendan estos gráficos

Por varias razones:

* Desmos es una empresa privada que, hoy por hoy presta sus servicios gratis. Mañana pueden decidir dejar de dar soporte a su API o, simplemente, pueden decidir cobrar por el servicio.
* Existen alternativas de código abierto, gratuitas, mantenidas por universidades europeas y que permiten una mayor funcionalidad.
