# Questions avec réponses graphiques avec GeoGebra

## Que voulons-nous faire ?

Nous voulons afficher une applet GeoGebra dans la question Moodle et capturer l'interaction de l'utilisateur avec le graphique.

Par exemple :

![](<../.gitbook/assets/image (89).png>)

Nous demandons à l'utilisateur de déplacer les points de sorte que :

* Un point se trouve a des coordonnées données (elles changent à chaque fois que la question est exécutée).
* L'un des côtés du triangle qui en résulte a une longueur donnée (il change à chaque fois que la question est exécutée).
* Le triangle doit avoir une aire donnée (elle change à chaque exécution de la question).
* Vous devez indiquer le périmètre du triangle que vous avez tracé avec une erreur absolue de 2 unités.

## Stratégie à suivre

Nous allons intégrer l'applet GeoGebra comme nous l'avons fait dans la [section précédente](graficos-dinamicos-con-geogebra.md).

Puisque nous devons maintenant **sauvegarder et récupérer la construction** que l'utilisateur a faite, nous stockerons les valeurs des variables qui définissent la réponse **dans autant de placeholders que nécessaire**. Plus tard, **nous masquerons les** **placeholders** à l'aide de jQuery afin qu'ils ne soient pas visibles pour l'utilisateur.

Dans ce cas, nous allons stocker les coordonnées des trois points, nous aurons donc besoin de 6 placeholders (cases de réponse) pour stocker l'état de l'applet.

Chaque fois que nous chargeons la question (ou chargeons l'applet), nous vérifierons s'il y a des valeurs stockées à partir des réponses précédentes, pour dessiner le graphique avec les valeurs initiales ou avec celles précédemment données par l'utilisateur.

{% hint style="success" %}
Une fois résolu comment transmettre les données de Moodle Formulas à GeoGebra et inversement, nous avons résolu le problème.
{% endhint %}

{% hint style="success" %}
De plus, puisque nous pouvons récupérer la valeur de n'importe quelle variable GeoGebra stockée dans l'applet, **nous pouvons donc utiliser n'importe quelle fonction GeoGebra pour évaluer** le travail effectué dans l'applet.
{% endhint %}

## Aperçu de la question pendant le développement

Dans un aperçu de la question, sans masquer tous les placeholders que nous avons utilisés, nous aurions les éléments suivants :

![](../.gitbook/assets/vistapreviasinocultar.gif)

![](<../.gitbook/assets/image (51).png>)

Bien qu'il ne soit pas difficile de calculer l'aire et les longueurs des côtés à partir des coordonnées, nous avons choisi de les calculer dans GeoGebra et de les importer directement dans Moodle. Cela simplifiera beaucoup la correction.

## Fichier XML de référence

{% file src="../.gitbook/assets/preguntas-Aules-Geogebra proof of concept v1-20200728-2052.xml" %}

## Code de la question

```javascript
//Tout ce qui porte le nom "esqueseoculta" sera masqué lors de l'exécution de la question
<p name="elqueseoculta">Mes informations : A({a1},{a2}), B ({b1},{b2}) et C({c1},{c2}) </p>
 
 
<p>Déplacez les points sur le graphique de sorte que :</p>
<ul>
<li>Le point A soit aux coordonnées \( ({d1},{d2}) \).</li>
<li>Un des côtés du triangle ait pour longueur \( {L}~u\).</li>
<li>L'aire du triangle soit \( {area}~u^2 \).</li>
</ul>
<small>Vous pouvez zoomer avec la molette de la souris ou déplacer le graphique en cliquant sur l'arrière-plan puis en le faisant glisser</small>

<script src="https://cdn.geogebra.org/apps/deployggb.js"></script>
<script type="text/javascript" src="https://code.jquery.com/jquery-3.1.0.min.js"></script>

<div id="ggbApplet"></div>

<script>
//Ce premier script va masquer tous les éléments html dont le nom est "elquesoculta"
$(document).ready(function(){
    jQuery ("*[name='elqueseoculta']").hide();
 });

</script>

<script>
//Pour reprendre la valeur précédente si la question a déjà été répondue
//Il est également utilisé pour initialiser la construction lors de la première exécution.
function compruebaRespuesta(part,placeholder,variable){
    var resp=jQuery( "input[name*='_"+part.toString()+"_"+placeholder.toString()+"']" ).val();
    if (resp=="") {return variable;}
   else {return parseFloat(resp);}
}

//Variables du dessin de l'applet. Elles correspondent aux variables définies dans Moodle
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
// ajouter ici du code à exécuter au démarrage de l'applet
"appletOnLoad":function(api){

              //On ajuste les valeurs initiales du dessin

              api.setValue('a1',compruebaRespuesta(0,0,a1));
//Définissez a1 sur la valeur  placeholder 0=partie1, 0 = premier placeholder de la partie ou,
//s'il est vide, définissez sur a1 (variable aléatoire Moodle) -
//il aurait été plus facile de ne pas randomiser le graphique en incluant directement
//api.setValue('a1',compruebaRespuesta(0,0,3)); et la coordonnée x de A commencerait toujours
//à la valeur 3 si elle n'a pas été déplacée auparavant par l'utilisateur

              api.setValue('a2',compruebaRespuesta(0,1,a2));
              api.setValue('b1',compruebaRespuesta(1,0,b1));
              api.setValue('b2',compruebaRespuesta(1,1,b2));
              api.setValue('c1',compruebaRespuesta(1,2,c1));
              api.setValue('c2',compruebaRespuesta(1,3,c2));          

              //Fonction permettant de lier les paramètres de l'applet aux cases de réponse Aules _(nº de parte de la pregunta -1)_nº de placeholder

              function updateListener(objName) { 
 //ces commandes sont celles qui transmettent les valeurs de l'applet aux placeholder
                                
                              jQuery( "input[name*='_0_0']" ).val(api.getValue('a1'));
                              jQuery( "input[name*='_0_1']" ).val(api.getValue('a2'));
                              jQuery( "input[name*='_1_0']" ).val(api.getValue('b1'));
                              jQuery( "input[name*='_1_1']" ).val(api.getValue('b2'));                              
                              jQuery( "input[name*='_1_2']" ).val(api.getValue('c1'));
//_1_2 correspond à la partie 2(=1+1), le troisième placeholder de cette partie (le premier a un
//index nul). Nous y stockons la variable c1 de l'applet.   
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
// si nous sauvegardons le fichier dans le cloud, l'id du matériau ira ici.
"material_id":"p6tbqcav",
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
{#2}
{#3}
{#4}
```

## Masquer les placeholder

{% hint style="info" %}
Tout ce que vous avez à faire est de leur attribuer name="elqueseoculta" dans n'importe quelle balise \<html>.

Dans ce cas, cela a été fait dans un paragraphe, bien que cela puisse être avec \<span>, \<div>...
{% endhint %}

![](<../.gitbook/assets/image (85).png>)

{% hint style="info" %}
Dans la dernière partie, un placeholder a été masqué (que nous avons utilisé pour "récupérer" la valeur du périmètre du triangle de l'applet) et un autre a été laissé à l'utilisateur :
{% endhint %}

![](<../.gitbook/assets/image (8).png>)

## Corriger la réponse

Dans la première partie, il suffit de comparer la valeur des deux coordonnées du point A avec la valeur connue de la réponse donnée par les variables d1 et d2.

{% hint style="success" %}
Dans la première partie, il suffit de comparer la valeur des deux coordonnées du point A avec la valeur connue de la réponse donnée par les variables d1 et d2.
{% endhint %}

{% hint style="warning" %}
Ce n'est pas le plus correct, mais puisque **nous allons corriger à l'aide de critères de qualification**, dans cette question, nous ne nous sommes pas souciés de rechercher analytiquement les coordonnées des points qui sont des solutions à l'activité.
{% endhint %}

{% hint style="danger" %}
Si nous cliquons sur "Remplir avec les bonnes réponses" et vérifions, nous obtiendrons une mauvaise réponse car nous n'avons pas défini d'exemple de réponse correcte dans le champ Réponse\*.
{% endhint %}

{% hint style="success" %}
La réponse donnée sera correcte si \_4 (longueur de BC) est égale à L (longueur que nous avons demandée pour un des côtés dans l'énoncé) ou si \_5 (longueur de AC) est égale à L ou si \_6 l'est.
{% endhint %}

![](<../.gitbook/assets/image (104).png>)
