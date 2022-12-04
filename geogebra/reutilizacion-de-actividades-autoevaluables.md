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

Nous allons introduire dans un cours <mark style="color:red;">**Aules/Moodle**</mark> une question Formulas qui comprend l'[activité d'auto-évaluation suivante sur les problèmes de nombres](https://www.geogebra.org/m/Az5bY5zR) (auteur Javier Cayetano Rodríguez).

![](<../.gitbook/assets/image (80).png>)

## Modèle de question : fichier XML

Nous utiliserons la question suivante comme **modèle** pour importer l'activité d'auto-évaluation.

{% file src="../.gitbook/assets/preguntas-Aules-Geogebra autoevaluable plantilla-20200710-1049.xml" %}

## Brève explication de son fonctionnement (pas indispensable pour comprendre).

{% hint style="danger" %}
**L'éditeur Moodle doit être en texte brut** ou le code de la question peut "casser".
{% endhint %}

1. Grâce à la bibliothèque [jQuery](https://jquery.com/), nous capturons la valeur de la note d'activité (variable SCORMRawScore) et la transmettons à l'espace réservé {\_0} de la partie 1 : nous utilisons un Listener qui s'exécute avec l'applet GeoGebra.
2. Nous cachons tous les éléments avec name='elqueseoculta'. Dans ce cas, le seul qui existe est placeholder {\_0} de la partie 1.
3. Nous avons défini un critère de correction pour la partie 1 afin que le score de la question corresponde à la valeur de {\_0} <mark style="color:red;">**par un.**</mark>

```javascript
<p> Ici, les instructions que nous estimons appropriées peuvent être copiées.</p>
<br>

<script src="https://cdn.geogebra.org/apps/deployggb.js"></script>
<script type="text/javascript" src="https://code.jquery.com/jquery-3.1.0.min.js"></script>

<div id="ggbApplet"></div>

<script>

//Ce premier script cachera tous les éléments html dont le nom est "elquesoculta"
$(document).ready(function(){
    jQuery ("*[name='elqueseoculta']").hide();
 });

</script>

<script>

//Pour prendre la valeur précédente si la question a déjà été traitée, elle n'est pas utilisée dans cette question
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
// ajouter ici du code à exécuter au démarrage de l'applet
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
// si nous enregistrons le fichier dans le cloud, l'id du matériau ira ici
"material_id":"b5ckap8z",
//"ggbBase64":"changer pour base64",
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

Référence des **paramètres** appliqués lors du chargement de la construction GeoGebra : [PARAMETERS](https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters).

Référence de l'**API** GeoGebra : [API](https://wiki.geogebra.org/en/Reference:GeoGebra\_Apps\_API).

## Adapter une question à notre modèle

{% hint style="danger" %}
**L'éditeur Moodle doit être en texte brut** ou le code de la question peut "casser".
{% endhint %}

Nous aurons besoin de plusieurs paramètres, qui sont ce que nous allons inclure dans le code du modèle :

* [x] Vérifier que l'activité **enregistre le score dans SCORMRawScore** : on ouvre l'activité avec GeoGebra et on voit que la variable est dans la question.

![](../.gitbook/assets/verSCORMRawScore.gif)

* [x] **Code d'activité** GeoGebra : il se trouve dans l'adresse Web de la question. Dans ce cas, il s'agit de Az5bY5zR.

![](<../.gitbook/assets/image (50).png>)

* [x] **Taille de l'applet** : dans ce cas, elle mesure 675 pixels de large (width) et 417 pixels de haut (height).

![](../.gitbook/assets/tamaño.gif)

{% hint style="success" %}
En modifiant ces trois paramètres dans la question fournie comme modèle, nous aurons la question d'auto-évaluation GeoGebra prête.
{% endhint %}

![](../.gitbook/assets/edicion.gif)

## Pièces jointes

L'activité est donnée ci-dessous en tant que question Formulas et en tant que package SCORM. Notez la différence de taille entre l'un et l'autre format : avec ce que cette question occupe dans SCORM, on peut avoir plus de 40 questions au format Formulas.

{% file src="../.gitbook/assets/preguntas-Aules-Geogebra autoevaluable plantilla-20200710-1045.xml" %}

{% file src="../.gitbook/assets/Scorm.zip" %}
