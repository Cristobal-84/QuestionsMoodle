# GeoGebra

## Qu'est-ce que GeoGebra ?

Parmi ceux arrivés jusqu'ici, je ne pense pas qu'il y ait quelqu'un qui lit ceci qui ne connaisse pas GeoGebra.

{% hint style="success" %}
[GeoGebra ](https://www.geogebra.org)possède une **interface bien connue** **et documentée** : les constructions géométriques peuvent être faites sans avoir besoin de programmer en Javascript.
{% endhint %}

{% hint style="success" %}
GeoGebra a une **importante communauté** et un grand nombre de [matériaux librement partagés](https://www.geogebra.org/materials).
{% endhint %}

## Plusieurs possibilités

Lors d'une intégration de GeoGebra dans Moodle Formulas, nous avons plusieurs options : en fonction du nombre de paramètres que nous voulons synchroniser entre GeoGebra et <mark style="color:red;">**Aules/Moodle**</mark>. Du plus simple (et moins fonctionnel) au plus laborieux :

1. Question avec valeurs aléatoires générée par GeoGebra et corrigée par GeoGebra dans laquelle on n'enregistre que le score obtenu par l'élève : elle sera très utile pour réutiliser les activités d'auto-évaluation GeoGebra dans <mark style="color:red;">**Aules/Moodle**</mark>.
2. Question avec valeurs aléatoires générée par <mark style="color:red;">**Aules/Moodle**</mark> et enregistrement de la réponse de l'élève.

Toutes les possibilités d'enregistrement de données intermédiaires sont possibles.

## Intégration Moodle

Avec le plugin Formulas, nous pourrons inclure des applets GeoGebra dans les questions Moodle. Nous aurons la possibilité d'afficher uniquement l'applet, d'afficher l'applet avec des valeurs de paramètres définies par Moodle (graphiques aléatoires à chaque exécution de la question) et même de capturer des réponses graphiques dérivées de l'interaction avec l'applet.

{% hint style="success" %}
Nous allons intégrer les **constructions dans les questions**, afin qu'elles puissent faire partie des questionnaires.
{% endhint %}

{% hint style="info" %}
Nous pouvons créer des questions aléatoires et **enregistrer les réponses de l'utilisateur** (et pas seulement le score obtenu).
{% endhint %}

{% hint style="danger" %}
La préparation de ces questions est laborieuse et pas facile puisqu'il faut utiliser du code html et Javascript.
{% endhint %}

On va commencer par le plus simple à préparer ...
