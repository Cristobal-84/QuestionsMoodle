# Graphiques dynamiques avec GeoGebra

## Que voulons-nous faire ?

Il s'agit de montrer des graphiques GeoGebra générés en fonction de certaines variables (aléatoires ou non) établies dans la question Formulas.

Nous allons résoudre la même question que celle déjà posée dans les [graphiques dynamiques de JSXGraph](../consideraciones-antes-de-empezar-con-esto/graficos-dinamicos-de-jsxgraph.md).

{% hint style="success" %}
En utilisant GeoGebra, nous n'aurons pas besoin de créer la construction graphique par programmation (en écrivant du code) : nous pouvons **créer les constructions directement depuis l'interface graphique** de GeoGebra ou réutiliser les constructions de[ www.geogebra.org](https://www.geogebra.org/).
{% endhint %}

![](<../.gitbook/assets/image (23).png>)

## Fichier XML de référence

{% file src="../.gitbook/assets/preguntas-Aules-Plano cartesiano 3 puntos GeoGebra-20200718-1247 (1).xml" %}

## Fichier GeoGebra

{% hint style="info" %}
Il sera pratique de le créer en se basant sur les **mêmes variables qui apparaissent dans la question Formulas** pour pouvoir passer facilement les valeurs entre la question Formulas et l'applet GeoGebra.
{% endhint %}

{% file src="../.gitbook/assets/3puntos.ggb" %}

![](<../.gitbook/assets/image (60).png>)

![](../.gitbook/assets/pant3ptos.png)

{% hint style="info" %}
Les points A, B et C ont été créés sur la base des paramètres : A=(a1,a2), ...
{% endhint %}

## Obtenir l'id du fichier GeoGebra

{% hint style="info" %}
Le fichier peut être créé directement dans le cloud ou on peut travailler localement. Dans le premier cas, l'identifiant est obtenu directement à partir de l'adresse Web du navigateur.
{% endhint %}

{% tabs %}
{% tab title="Fichier créé dans le cloud" %}
L'identifiant est obtenu directement à partir de l'adresse Web du navigateur.

![](<../.gitbook/assets/image (92).png>)
{% endtab %}

{% tab title="Fichier créé localement" %}
Une fois le fichier créé, il est **exporté sous forme de page Web**.

![](<../.gitbook/assets/image (15).png>)

Cela télécharge le fichier sur le cloud et nous pouvons le trouver dans l'onglet Ressources.
{% endtab %}
{% endtabs %}

## Comment ajuster la taille de l'applet

Il existe plusieurs options, il est pratique d'enregistrer le fichier avec la vue que l'on souhaite voir apparaître dans l'applet.

![Capture d'écran GeoGebra avant l'export](<../.gitbook/assets/image (14).png>)

{% hint style="success" %}
Si nous masquons la vue algébrique et la barre de saisie, et faisons de la taille de la fenêtre ce que nous voulons que le graphique soit dans Moodle, la construction qui est téléchargée sur le cloud ne nécessite aucun autre ajustement.
{% endhint %}

## Approche générale

La stratégie que nous suivrons est :

1. Nous introduirons le graphe GeoGebra dans la question Formulas.
2. Nous modifierons les paramètres du graphique pour qu'ils soient ceux qui sont générés aléatoirement dans la question Formulas.

## Modèle de référence

Tout comme nous l'avons fait en réutilisant les activités d'auto-évaluation, nous utiliserons un modèle pour éviter d'avoir à écrire trop de code Javascript.

Dans ce cas, j'inclus la question en XML, qui peut être utilisée comme modèle.

{% file src="../.gitbook/assets/preguntas-Aules-Plano cartesiano 3 puntos GeoGebra-20200718-1247 (1) (1).xml" %}

## Adapter la question à d'autres fichiers GeoGebra

{% hint style="info" %}
Ayant une question fonctionnelle, le plus confortable sera de l'adapter pour en créer de nouvelles.
{% endhint %}

```javascript
//ICI SERAIT L'ÉNONCÉ AFFICHÉ SUR LE GRAPHIQUE
<p> À la vue du graphique présenté : </p>

<script src="https://cdn.geogebra.org/apps/deployggb.js"></script>


<div id="ggbApplet"></div>

<script>

//Variables du dessin de l'applet À MODIFIER
  var a1={a1}; //Pour éviter d'avoir à mettre des accolades dans le code du script
  var a2={a2};
  var b1={b1};
  var b2={b2};
  var c1={c1};
  var c2={c2};


var parameters = {
"id": "ggbApplet",
"width":612, //ICI VOUS DEVEZ ENTRER LA LARGEUR DE LA CONSTRUCTION
"height":608, //ICI VOUS DEVEZ ENTRER LA HAUTEUR DE LA CONSTRUCTION
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
// ajouter ici du code à exécuter au démarrage de l'applet
"appletOnLoad":function(api){

              //On ajuste les valeurs initiales du dessin COLLECTANT LES VARIABLES DE MOODLE
//Ici, nous pourrions exécuter des commandes dans la construction GeoGebra
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
// si nous sauvegardons le fichier dans le cloud, l'id du matériau ira ici
"material_id":"vbstt5ue", //ICI VOUS DEVEZ ENTRER L'ID DU FICHIER GEOGEBRA
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
```

{% hint style="success" %}
Dans la fonction exécutée dans "AppletOnLoad", nous pouvons exécuter des commandes GeoGebra pour adapter la construction à notre goût.

La documentation de l'API se trouve à : [API](https://wiki.geogebra.org/en/Reference:GeoGebra\_Apps\_API).
{% endhint %}

{% hint style="info" %}
Description des paramètres de chargement de l'applet dans : [PARAMETERS](https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters).
{% endhint %}

