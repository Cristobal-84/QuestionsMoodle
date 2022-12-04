# Réutilisation des activités d'auto-évaluation

## Quelles sont ces activités ?

Ce sont des constructions GeoGebra qui ont été écrites de telle sorte qu'elles calculent un score et peuvent être intégrées dans une activité SCORM.

{% hint style="danger" %}
Elles doivent inclure les variables :

* **SCORMMaxScore** : qui enregistre le score maximum de l'activité.
* **SCORMRawScore** : qui enregistre le score obtenu par l'étudiant.
{% endhint %}

Plusieurs exemples de ces activités peuvent être trouvés sur la page GeoGebra. Des exemples magnifiques sont ceux de [Javier Cayetano](https://www.geogebra.org/u/javier+cayetano).

## Avantages d'introduire ces activités comme une question <mark style="color:red;">Aules/Moodle</mark> et non comme un SCORM.

Ce type d'activité peut être inclus dans <mark style="color:red;">**Aules/Moodle**</mark> en tant qu'activité SCORM via **eXeLearning** : [lien vers un tutoriel vidéo](https://www.youtube.com/watch?v=1F9pFOCnZAY).

L'introduction d'une **activité en tant que package SCORM** :

* est très simple avec eXeLearning,
* s'affiche sur la page d'accueil du cours,
* généré une note est dans le carnet de notes.

Une seule activité d'auto-évaluation peut être saisie (pour autant que je sache) dans chaque package SCORM.

![](<../.gitbook/assets/image (47).png>)

L'introduction d'une **activité en tant que question Formulas** :

* ne requiert aucun programme externe,
* est quelque chose "de plus" compliqué,
* peut être inclus dans la **banque de questions**, de sorte qu'il peut être facilement catégorisé,
* peut être inclus dans les **questionnaires**,
* occupe beaucoup moins d'espace de stockage dans le cours (il y a une limite à la taille d'un cours pour une restauration ultérieure),
* si elle comprend des variables aléatoires, **il est possible de stocker la réponse de l'utilisateur** (bien que selon la programmation de l'activité, cela puisse être compliqué) et pas seulement la note obtenue.

## Que voulons-nous faire ?

Vamos a introducir en un curso de Aules una pregunta de Fórmulas que incluya la [siguiente actividad autoevaluable de Problemas de Números](https://www.geogebra.org/m/Az5bY5zR) (autor Javier Cayetano Rodríguez).

![](<../.gitbook/assets/image (80).png>)

## Plantilla de pregunta: Archivo XML

Utilizaremos la siguiente pregunta como **plantilla** para importar la actividad autoevaluable.

{% file src="../.gitbook/assets/preguntas-Aules-Geogebra autoevaluable plantilla-20200710-1049.xml" %}

## Breve explicación sobre su funcionamiento (no necesario entender)

{% hint style="danger" %}
El editor de Moodle debe estar en texto plano o puede que se "estropee" el código de la pregunta.
{% endhint %}

1. A través de la biblioteca [jQuery](https://jquery.com/), capturamos el valor de la calificación de la actividad (variable SCORMRawScore) y lo pasamos al placeholder {\_0} de la Parte 1: utilizamos un Listener que se ejecuta con el applet de GeoGebra.
2. Ocultamos todos los elementos con name='elqueseoculta'. En este caso el único que hay es el placeholder {\_0} de la parte 1.
3. Establecemos un criterio de corrección para la parte 1 de modo que la puntuación de la pregunta corresponda con el valor de {\_0} en tanto por uno.

```javascript
<p> Aquí podrían copiarse las instrucciones que consideremos oportunas.</p>
<br>

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

//Para tomar el valor anterior si es que la pregunta ya se ha contestado, no se usa en esta pregunta
function compruebaRespuesta(part,placeholder,variable){
    var resp=jQuery( "input[name*='_"+part.toString()+"_"+placeholder.toString()+"']" ).val();
    if (resp=="") {return variable;}
   else {return parseFloat(resp);}
}



var parameters = {
"id": "ggbApplet",
"width":800,
"height":547,
"showMenuBar":false,
"showAlgebraInput":false,
"showToolBar":false,
"showToolBarHelp":false,
"showResetIcon":true,
"enableLabelDrags":false,
"enableShiftDragZoom":false,
"enableRightClick":false,
"errorDialogsActive":false,
"useBrowserForJS":false,
"allowStyleBar":false,
"preventFocus":false,
"showZoomButtons":false,
"capturingThreshold":3,
// add code here to run when the applet starts
"appletOnLoad":function(api){
                  function updateListener(objName) {                                     
                              jQuery( "input[name*='_0_0']" ).val(api.getValue('SCORMRawScore'));
                              
                                                                
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
"material_id":"b5ckap8z",
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
```

Referencia de los **parámetros** que se aplican al cargar la construcción de GeoGebra: [PARÁMETROS](https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters).

Referencia del **API** de GeoGebra: [API](https://wiki.geogebra.org/en/Reference:GeoGebra\_Apps\_API).

## Adaptar una pregunta a nuestra plantilla

{% hint style="danger" %}
El **editor de Moodle debe estar en texto plano** o puede que se "estropee" el código de la pregunta.
{% endhint %}

Necesitaremos varios parámetros, que son los que vamos a incluir en el código de la plantilla:

* [x] Comprobar que la actividad **guarda la puntuación en SCORMRawScore**: abrimos la actividad con GeoGebra y vemos que está la variable en la pregunta.

![](../.gitbook/assets/verSCORMRawScore.gif)

* [x] **Código de la actividad** de GeoGebra: está en la dirección web de la pregunta. En este caso es Az5bY5zR.

![](<../.gitbook/assets/image (50).png>)

* [x] **Tamaño del Applet**: en este caso es de 675 pixeles de ancho (width) y 417 de alto (height).

![](../.gitbook/assets/tamaño.gif)

{% hint style="success" %}
Con la edición de estos tres parámetros en la pregunta suministrada como plantilla, tendremos lista la pregunta autoevaluable de GeoGebra.
{% endhint %}

![](../.gitbook/assets/edicion.gif)

## Archivos adjuntos

Se incluye a continuación la actividad como pregunta de Fórmulas y como paquete SCORM. Obsérvese la diferencia de tamaño entre uno y el otro formato: con lo que ocupa esta pregunta en SCORM, podemos más de 40 preguntas en formato de Fórmulas.

{% file src="../.gitbook/assets/preguntas-Aules-Geogebra autoevaluable plantilla-20200710-1045.xml" %}

{% file src="../.gitbook/assets/Scorm.zip" %}
