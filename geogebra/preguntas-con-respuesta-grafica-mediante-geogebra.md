# Questions avec réponses graphiques avec GeoGebra

## Que voulons-nous faire ?

Nous voulons afficher une applet GeoGebra dans la question Moodle et capturer l'interaction de l'utilisateur avec le graphique.

Par exemple :

![](<../.gitbook/assets/image (89).png>)

Nous demandons à l'utilisateur de déplacer les points de sorte que :

* Un punto quede en unas coordenadas dadas (cambian cada vez que se ejecuta la pregunta).
* Uno de los lados del triángulo resultante tenga una longitud dada (cambia cada vez que se ejecuta la pregunta).
* El triángulo debe tener un área dada (cambia cada vez que se ejecuta la pregunta).
* Debe indicar el perímetro del triángulo que ha dibujado con un error absoluto de 2 unidades.

## Estrategia a seguir

Incrustaremos el applet de GeoGebra tal y como lo hemos hecho en el [apartado anterior](graficos-dinamicos-con-geogebra.md).

Puesto que ahora necesitamos **guardar y recuperar la construcción** que ha hecho el usuario, almacenaremos los valores de las variables que definen la respuesta **en tantos placeholders como necesitemos**. Posteriormente **ocultaremos los placeholders** mediante jQuery para que no sean visibles para el usuario.

En este caso, guardaremos las coordenadas de los tres puntos por lo que necesitaremos 6 placeholders (cajas de respuesta) para almacenar el estado del applet.

Cada vez que carguemos la pregunta (o se cargue el applet), comprobaremos si hay valores almacenados de respuestas previas, para dibujar el gráfico con los valores iniciales o con los dados previamente por el usuario.

{% hint style="success" %}
Una vez resuelto como pasar datos de Moodle Fórmulas a GeoGebra y al revés, ya tenemos resuelto el problema.
{% endhint %}

{% hint style="success" %}
Además, como podemos recuperar el valor de cualquier variable de GeoGebra almacenado en el applet, por lo que **podemos hacer uso de cualquier función de GeoGebra para evaluar** el trabajo realizado en el applet.
{% endhint %}

## Vista previa de la pregunta durante el desarrollo

En una vista previa de la pregunta, sin ocultar todos los placeholders que hemos utilizado, tendríamos lo siguiente:

![](../.gitbook/assets/vistapreviasinocultar.gif)

![](<../.gitbook/assets/image (51).png>)

A pesar de que no resulta complicado calcular el área y las longitudes de los lados a partir de las coordenadas, hemos optado por calcularlas en GeoGebra e importarlas directamente a Moodle. Esto simplificará mucho la corrección.

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Aules-Geogebra proof of concept v1-20200728-2052.xml" %}

## Código de la pregunta

```javascript
//Todo lo que tenga por nombre "esqueseoculta" se ocultará al ejecutar la pregunta
<p name="elqueseoculta">Info mía: A({a1},{a2}), B ({b1},{b2}) y C({c1},{c2}) </p>
 
 
<p>Mueve los puntos del gráfico para que:</p>
<ul>
<li>El punto A esté en las coordenadas \( ({d1},{d2}) \).</li>
<li>Uno de los lados del triángulo tenga longitud \( {L}~u\).</li>
<li>El área del triángulo sea de \( {area}~u^2 \).</li>
</ul>
<small>Puedes hacer zoom con la rueda del ratón y desplazar la gráfica haciendo clic sobre el fondo de la misma y arrastrando</small>

<script src="https://cdn.geogebra.org/apps/deployggb.js"></script>
<script type="text/javascript" src="https://code.jquery.com/jquery-3.1.0.min.js"></script>

<div id="ggbApplet"></div>

<script>
//Este primer script oculará todos los elementos html cuyo nombre sea "elquesoculta"
$(document).ready(function(){
    jQuery ("*[name='elqueseoculta']").hide();
 });

</script>

<script>
//Para tomar el valor anterior si es que la pregunta ya se ha contestado
//También sirve para inicializar la construcción en la primera ejecución
function compruebaRespuesta(part,placeholder,variable){
    var resp=jQuery( "input[name*='_"+part.toString()+"_"+placeholder.toString()+"']" ).val();
    if (resp=="") {return variable;}
   else {return parseFloat(resp);}
}

//Variables de dibujo del applet. Corresponden con las variables definidas en Moodle
var a1={a1}; var a2={a2};
var b1={b1}; var b2={b2};
var c1={c1}; var c2={c2};



var parameters = {
"id": "ggbApplet",
"width":700,
"height":600,
"showMenuBar":false,
"showAlgebraInput":false,
"showToolBar":false,
"showToolBarHelp":false,
"showResetIcon":true,
"enableLabelDrags":false,
"enableShiftDragZoom":true,
"enableRightClick":false,
"errorDialogsActive":false,
"useBrowserForJS":false,
"allowStyleBar":false,
"preventFocus":false,
"showZoomButtons":false,
"capturingThreshold":3,
// add code here to run when the applet starts
"appletOnLoad":function(api){

              //Ajustamos los valores iniciales del dibujo

              api.setValue('a1',compruebaRespuesta(0,0,a1));
//Asigna a a1 el valor del placeholder 0=parte1, 0=primer placeholder de la parte o, si
//estuviera vacío le asignará el valor a1 (variable aleatoria de Moodle) - 
//hubiera sido más sencillo no aleatorizar el gráfico incluyendo directamente
//api.setValue('a1',compruebaRespuesta(0,0,3)); y la coordenada x de A siempre empezaría
//en el valor 3 si no lo ha movido antes el usuario

              api.setValue('a2',compruebaRespuesta(0,1,a2));
              api.setValue('b1',compruebaRespuesta(1,0,b1));
              api.setValue('b2',compruebaRespuesta(1,1,b2));
              api.setValue('c1',compruebaRespuesta(1,2,c1));
              api.setValue('c2',compruebaRespuesta(1,3,c2));          

              //Función para vincular los parámetros del applet con las cajas de respuesta de Aules _(nº de parte de la pregunta -1)_nº de placeholder

              function updateListener(objName) { 
 //estas órdenes son las que pasan los valores del applet a los placeholder
                                
                              jQuery( "input[name*='_0_0']" ).val(api.getValue('a1'));
                              jQuery( "input[name*='_0_1']" ).val(api.getValue('a2'));
                              jQuery( "input[name*='_1_0']" ).val(api.getValue('b1'));
                              jQuery( "input[name*='_1_1']" ).val(api.getValue('b2'));                              
                              jQuery( "input[name*='_1_2']" ).val(api.getValue('c1'));
//_1_2 corresponde a la parte 2(=1+1), tercer placeholder de dicha parte(el primero tiene
//índice cero). Ahí almacenamos la variable c1 del applet.   
                              jQuery( "input[name*='_1_3']" ).val(api.getValue('c2'));
                              jQuery( "input[name*='_1_4']" ).val(api.getValue('a'));
                              jQuery( "input[name*='_1_5']" ).val(api.getValue('b'));
                              jQuery( "input[name*='_1_6']" ).val(api.getValue('c'));
                              jQuery( "input[name*='_2_0']" ).val(api.getValue('t1'));
                              jQuery( "input[name*='_3_1']" ).val(api.getValue('peri'));
                                   
}
              api.registerUpdateListener(updateListener);
},
"showFullscreenButton":true,
"scale":1,
"disableAutoScale":true,
"autoHeight":true,
"allowUpscale":false,
"clickToLoad":false,
"appName":"classic",
"showSuggestionButtons":false,
"buttonRounding":1,
"buttonShadows":false,
"language":"es",
// si guardamos el archivo en la nube, aquí irá el material id
"material_id":"p6tbqcav",
//"ggbBase64":"cambiar por base64",
};

var views = {'is3D': 0,'AV': 0,'SV': 0,'CV': 0,'EV2': 0,'CP': 0,'PC': 0,'DA': 0,'FI': 0,'macro': 0};
var applet = new GGBApplet(parameters, '5.0', views);

window.addEventListener("load", function() {
                    applet.inject('ggbApplet');
                    });

</script>

<br>
{#1}
{#2}
{#3}
{#4}
```

## Ocultar los placeholder

{% hint style="info" %}
Bastará con asignarles name="elqueseoculta" en cualquier etiqueta \<html>.

En este caso se ha hecho en un párrafo, aunque podría ser con \<span>, \<div>...
{% endhint %}

![](<../.gitbook/assets/image (85).png>)

{% hint style="info" %}
En la última parte se ha ocultado un placeholder (que hemos utilizado para "recoger" el valor del perímetro del triángulo del applet) y se ha dejado otro para el usuario:
{% endhint %}

![](<../.gitbook/assets/image (8).png>)

## Corregir la respuesta

En la primera parte basta comparar el valor de las dos coordenadas del punto A con el valor conocido de la respuesta dado por las variables d1 y d2.

{% hint style="success" %}
En la parte 2 necesitamos 7 placeholders por lo que la respuesta correcta deben ser 7 números.
{% endhint %}

{% hint style="warning" %}
No es lo más correcto, pero como **vamos a corregir utilizando criterios de calificación**, en esta pregunta no nos hemos preocupado en buscar analíticamente las coordenadas de los puntos que son solución de la actividad.
{% endhint %}

{% hint style="danger" %}
Si pulsamos en "Rellenar con las respuestas correctas" y comprobamos, obtendremos una respuesta errónea ya que no hemos establecido una respuesta correcta de ejemplo en el campo de Respuesta\*.
{% endhint %}

{% hint style="success" %}
La respuesta dada será correcta si \_4 (longitud de BC) es igual a L (longitud que hemos pedido para uno de los lados en el enunciado) o si \_5 (longitud de AC) es igual a L o si \_6 lo es.
{% endhint %}

![](<../.gitbook/assets/image (104).png>)
