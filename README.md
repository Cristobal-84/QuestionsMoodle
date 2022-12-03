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
{% tab title="Desplegable" %}
![](<.gitbook/assets/image (28).png>)
{% endtab %}

{% tab title="Botones de radio" %}
![](<.gitbook/assets/image (4).png>)
{% endtab %}
{% endtabs %}

* De générer dynamiquement des graphes : par exemple, le graphe d'une fonction.

{% tabs %}
{% tab title="Gráficos dinámicos de Desmos" %}
![](<.gitbook/assets/image (11).png>)
{% endtab %}

{% tab title="Gráficos dinámicos de JSXGraph (recomendado)" %}
![](<.gitbook/assets/image (24).png>)
{% endtab %}

{% tab title="Aleatoriedad a través del color" %}
![](<.gitbook/assets/image (76).png>)
{% endtab %}
{% endtabs %}

* De générer des graphes permettant des réponses graphiques par les élèves : par exemple du type « faire glisser les points pour que la droite qui les relie soit y=mx+n », avec m et n différents pour chaque élève.

{% tabs %}
{% tab title="Vectores" %}
![](<.gitbook/assets/image (98).png>)
{% endtab %}

{% tab title="Rectas" %}
![](<.gitbook/assets/image (118).png>)
{% endtab %}

{% tab title="Respuesta abierta" %}
![](<.gitbook/assets/image (10).png>)
{% endtab %}
{% endtabs %}

## Que faire quand ça ne va pas ?

En los momentos de atasco, en que una pregunta no funciona y no sabemos qué ocurre. Todo parece estar bien escrito, el código es el correcto, pero da error o no funciona como debiera.

Has buscado y leído la documentación, has buscado ejemplos parecidos, has hecho cursos gratuitos de Javascript y de HTML...

Puedes obtener ayuda en [el foro de Moodle quiz (en inglés)](https://moodle.org/mod/forum/view.php?id=737). Si es problema el idioma, puedes escribir en español y traducir con el traductor de Google. Se entenderá aunque no sea un inglés perfecto.

Es importante que documentes bien la pregunta:

* Incluye tu archivo XML.
* Explica bien qué quieres hacer, qué has hecho y qué problema encuentras.

{% hint style="info" %}
No olvides que quien te trata de ayudar lo hace desinteresadamente y te está regalando su tiempo.
{% endhint %}

{% hint style="danger" %}
Evita preguntar por cosas que se encuentran haciendo una simple búsqueda en Google o que se han respondido anteriormente en el foro: usa el buscador primero.
{% endhint %}

{% hint style="success" %}
Has preguntado y te han respondido: sé agradecido y comenta la respuesta. La persona que ha respondido merece saber si su respuesta ha sido útil.
{% endhint %}

## Garantía de que lo que digo es correcto y de que es la mejor forma de hacerlo

Ninguna.

Este documento únicamente pretende recoger cómo hago yo las cosas o cómo creo que se pueden hacer.

Por supuesto que no todo lo que diga aquí es correcto ni es la mejor forma de hacerlo. Simplemente es cómo considero yo hoy, con lo que sé del tema, que se pueden hacer ciertas cosas. Nada más.

Ofrezco la misma garantía que lo que cobro por hacer esto: CERO.
