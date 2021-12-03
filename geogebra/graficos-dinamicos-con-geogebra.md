# Gráficos dinámicos con GeoGebra

## ¿Qué queremos hacer?

Se trata de mostrar gráficos de GeoGebra que se generen en base a ciertas variables (aleatorias o no) establecidas en la pregunta de Fórmulas.&#x20;

Vamos a resolver la misma pregunta que ya hicimos en [Gráficos dinámicos de JSXGraph](../consideraciones-antes-de-empezar-con-esto/graficos-dinamicos-de-jsxgraph.md).

{% hint style="success" %}
Utilizando GeoGebra no necesitaremos crear la construcción gráfica programáticamente (escribiendo código): podemos **crear las construcciones directamente desde la interfaz gráfica** de GeoGebra o reutilizar construcciones de [www.geogebra.org](https://www.geogebra.org).
{% endhint %}

![](<../.gitbook/assets/image (96).png>)

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Aules-Plano cartesiano 3 puntos GeoGebra-20200718-1247 (1) (1).xml" %}

## Archivo de GeoGebra

{% hint style="info" %}
Será conveniente crearlo en base a las **mismas variables que aparezcan en la pregunta de Fórmulas** para poder pasar fácilmente los valores entre la pregunta de Fórmulas y el applet de GeoGebra.
{% endhint %}

{% file src="../.gitbook/assets/3puntos.ggb" %}

![](<../.gitbook/assets/image (95).png>)

![](../.gitbook/assets/pant3ptos.png)

{% hint style="info" %}
Los puntos A, B y C se han creado en base a los parámetros: A=(a1,a2), ...
{% endhint %}

## Obtener el id del archivo de GeoGebra

{% hint style="info" %}
Puede crearse el archivo directamente en la nube o bien trabajar en local. En el primer caso, el id se obtiene directamente de la dirección web del navegador.
{% endhint %}

{% tabs %}
{% tab title="Archivo creado en la nube" %}
Se obtiene el id directamente de la dirección web del navegador.

![](<../.gitbook/assets/image (92).png>)
{% endtab %}

{% tab title="Archivo creado en local" %}
Una vez creado el archivo, se **exporta como página web**:

![](<../.gitbook/assets/image (93).png>)

Esto sube el archivo a la nube y podremos encontrarlo en la pestaña de Recursos.
{% endtab %}
{% endtabs %}

## Como ajustar el tamaño del applet

Hay varias opciones, resulta cómodo guardar el archivo con la vista que queremos que aparezca en el applet.

![Captura de la pantalla de GeoGebra previa a exportación](<../.gitbook/assets/image (94).png>)

{% hint style="success" %}
Si ocultamos la vista algebraica y la barra de entrada, y hacemos que el tamaño de la ventana sea el que queremos que tenga la gráfica en Moodle, la construcción que se sube a la nube no necesita más ajustes.
{% endhint %}

## Enfoque general

La estrategia que seguiremos es:

1. Introduciremos el gráfico de GeoGebra en la pregunta de Fórmulas.
2. Modificaremos los parámetros del gráfico para que sean los que se generan aleatoriamente en la pregunta de Fórmulas.

## Plantilla de referencia

Al igual que hemos hecho en la reutilización de actividades autoevaluables, utilizaremos una plantilla para  evitar tener que escribir demasiado código Javascript.

En este caso incluyo la pregunta en XML, que se podrá utilizar como plantilla.

{% file src="../.gitbook/assets/preguntas-Aules-Plano cartesiano 3 puntos GeoGebra-20200718-1247 (1).xml" %}

## Adaptar la pregunta a otros archivos de GeoGebra

{% hint style="info" %}
Teniendo una pregunta funcional, lo más cómodo será adaptarla para crear nuevas preguntas a partir de ella.
{% endhint %}

```javascript
//ESTE SERÍA EL ENUNCIADO QUE SE MUESTRA SOBRE EL GRÁFICO
<p> A la vista del gráfico que se muestra: </p>

<script src="https://cdn.geogebra.org/apps/deployggb.js"></script>


<div id="ggbApplet"></div>

<script>

//Variables de dibujo del applet QUE HAY QUE EDITAR
  var a1={a1}; //Para no tener que poner llaves en el código del script
  var a2={a2};
  var b1={b1};
  var b2={b2};
  var c1={c1};
  var c2={c2};


var parameters = {
"id": "ggbApplet",
"width":612, //AQUÍ HAY QUE INTRODUCIR EL ANCHO DE LA CONSTRUCCIÓN
"height":608, //AQUÍ VA EL ALTO DE LA CONSTRUCCIÓN
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
"preventFocus":true,
"showZoomButtons":true,
"capturingThreshold":3,
// add code here to run when the applet starts
"appletOnLoad":function(api){

              //Ajustamos los valores iniciales del dibujo COGIENDO LAS VARIABLES DE MOODLE
//Aquí podríamos ejecutar comandos en la construcción de GeoGebra
              api.setValue('a1',a1);
              api.setValue('a2',a2);
              api.setValue('b1',b1);
              api.setValue('b2',b2);
              api.setValue('c1',c1);
              api.setValue('c2',c2);

},
"showFullscreenButton":true,
"scale":1,
"disableAutoScale":false,
"autoHeight":true,
"allowUpscale":false,
"clickToLoad":false,
"appName":"classic",
"showSuggestionButtons":false,
"buttonRounding":1,
"buttonShadows":false,
"language":"es",
// si guardamos el archivo en la nube, aquí irá el material id
"material_id":"vbstt5ue", //AQUÍ HAY QUE INTRODUCIR EL ID DEL ARCHIVO GEOGEBRA
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
```

{% hint style="success" %}
En la función que se ejecuta en "AppletOnLoad", podemos ejecutar comandos de GeoGebra para adaptar la construcción a nuestro gusto.&#x20;

La documentación de la API se encuentra en: [https://wiki.geogebra.org/en/Reference:GeoGebra\_Apps\_API](https://wiki.geogebra.org/en/Reference:GeoGebra\_Apps\_API)
{% endhint %}

{% hint style="info" %}
Descripción de los parámetros de carga del applet en: [https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters](https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters)
{% endhint %}
