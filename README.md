---
description: >-
  Guide d'utilisation et exemples d'utilisation de Moodle pour l'évaluation de
  contenus mathématiques.
---

# On commence



{% hint style="warning" %}
CETTE DOCUMENTATION A ÉTÉ RÉALISÉE PENDANT L'ÉTÉ 2020 ET N'EST PAS À JOUR
{% endhint %}

{% hint style="success" %}
Actuellement :

* Cela peut ne pas fonctionner correctement.
* Il peut y avoir d'autres moyens plus simples de faire ce qui est exposé ici.
{% endhint %}

## Que peut-on trouver sur cette page ?

Expériences d'utilisation de Moodle pour la création et l'évaluation d'activités mathématiques.

Ce livret se veut un guide non exhaustif pour la création de matériel d'auto-évaluation en mathématiques pour Moodle.

## Que vous faut-il ?

Une installation de Moodle et du plugin Moodle Formulas sera nécessaire.

Ce plugin peut être trouvé sur [https://moodle.org/plugins/qtype\_formulas](https://moodle.org/plugins/qtype\_formulas).

L'installation de plugins dans Moodle nécessite des autorisations d'administrateur. Les utilisateurs individuels **ne peuvent pas installer** de plugins. Assurez-vous que votre administrateur l'a installé ou demandez son installation.

Vous pouvez vérifier si vous avez le type de question Formulas si vous créez une nouvelle question et que l'option Formulas apparaît dans les types de questions que vous pouvez sélectionner :

![](.gitbook/assets/pantallaconpregunta.png)

## A qui s'adresse-t-elle ?

En tant que professeur de mathématiques au collège et au lycée, je me concentrerai sur des exemples et des questions adaptés au niveau auquel j'enseigne.

Cependant, la méthode de travail et les propositions d'activités seront suffisamment générales pour pouvoir être utilisées dans un cours Moodle de tout niveau. Les questions de type Formulas conviennent aussi bien aux mathématiques qu'à tout domaine dans lequel il peut être intéressant d'utiliser des questions utilisant des notations mathématiques ou susceptibles d'être générées par des valeurs aléatoires.

{% hint style="info" %}
L'élaboration de ce type de questions est coûteuse en temps et en connaissances : il faut surmonter une courbe d'apprentissage et être résilient pour ne pas abandonner.
{% endhint %}

{% hint style="success" %}
Le temps investi dans la préparation de la question est récupéré avec la correction automatique.
{% endhint %}

{% hint style="success" %}
La question que chaque élève recevra sera différente des autres, ce qui rend la fraude difficile.
{% endhint %}

{% hint style="danger" %}
Ce livre n'a pas vocation à être une banque de questions ou un catalogue directement applicable en classe. Il s'agit uniquement d'un guide pour faciliter l'apprentissage de l'utilisation des questions de type Formulas dans Moodle.
{% endhint %}

> #### Le chemin de l'enseignement à travers les théories est long,  court et efficace à travers des exemples (Sénèque)

## Quels types de questions peuvent être posées avec les Formulas ?

Dans cette vidéo (en anglais, sous-titres et traduction automatique disponibles), vous pouvez voir plusieurs exemples de questions. Vous pouvez également voir une partie du code qui doit être écrit pour obtenir le résultat affiché.

{% embed url="https://youtu.be/brWP7LRjPS0" %}

En plus de celles présentées dans la vidéo, qui sont les plus simples à réaliser, il est également possible dans ces questions :

* D'avoir des éléments à choix multiples :

{% tabs %}
{% tab title="Menu déroulant" %}
![](<.gitbook/assets/image (28).png>)
{% endtab %}

{% tab title="Boutons radio" %}
![](<.gitbook/assets/image (4).png>)
{% endtab %}
{% endtabs %}

* De générer dynamiquement des graphes : par exemple, le graphe d'une fonction.

{% tabs %}
{% tab title="Graphiques dynamiques Desmos" %}
![](<.gitbook/assets/image (11).png>)
{% endtab %}

{% tab title="Graphiques dynamiques JSXGraph (recommandé)" %}
![](<.gitbook/assets/image (24).png>)
{% endtab %}

{% tab title="Le hasard par la couleur hasard" %}
![](<.gitbook/assets/image (76).png>)
{% endtab %}
{% endtabs %}

* De générer des graphes permettant des réponses graphiques par les élèves : par exemple du type « faire glisser les points pour que la droite qui les relie soit y=mx+n », avec m et n différents pour chaque élève.

{% tabs %}
{% tab title="Vecteurs" %}
![](<.gitbook/assets/image (98).png>)
{% endtab %}

{% tab title="Droites" %}
![](<.gitbook/assets/image (118).png>)
{% endtab %}

{% tab title="Réponse ouverte" %}
![](<.gitbook/assets/image (10).png>)
{% endtab %}
{% endtabs %}

## Que faire quand ça ne va pas ?

Dans les moments de blocage, lorsqu'une question ne fonctionne pas et que nous ne savons pas ce qui se passe. Tout semble bien écrit, le code est correct, mais il donne une erreur ou ne fonctionne pas comme il se doit.

Vous avez recherché et lu la documentation, vous avez recherché des exemples similaires, vous avez suivi des cours Javascript et HTML gratuits ...

Vous pouvez obtenir de l'aide sur le [forum Quiz de Moodle (en anglais)](https://moodle.org/mod/forum/view.php?id=737). Si la langue pose problème, vous pouvez écrire en français et traduire avec le traducteur Google. Il sera compris même si ce n'est pas un anglais parfait.

Il est important de bien documenter votre question sur le forum :

* Incluez votre fichier XML.
* Expliquez bien ce que vous voulez faire, ce que vous avez fait et quel(s) problème(s) vous rencontrez.

{% hint style="info" %}
N'oubliez pas que celui qui essaie de vous aider le fait de manière désintéressée et vous donne de son temps.
{% endhint %}

{% hint style="danger" %}
Évitez de demander des choses qui peuvent être trouvées en faisant une simple recherche sur Google ou qui ont déjà été répondues dans le forum : utilisez d'abord le moteur de recherche.
{% endhint %}

{% hint style="success" %}
Vous avez demandé et ils vous ont répondu : soyez reconnaissants et commentez la réponse. La personne qui a répondu mérite de savoir si sa réponse a été utile.
{% endhint %}

## Garantie que ce que je dis est correct et que c'est la meilleure façon de le faire

Aucune.

Ce document vise uniquement à recueillir comment je fais les choses ou comment je pense qu'elles peuvent être faites.

Bien sûr, tout ce que je dis ici n'est pas correct et ce n'est pas non plus la meilleure façon de le faire. C'est simplement ainsi que je considère aujourd'hui, avec ce que je connais sur le sujet, que certaines choses peuvent être faites. Rien de plus.

J'offre la même garantie que ce que je facture pour cela : ZÉRO.
