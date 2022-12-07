# Généralités

Tout d'abord, voyons quelques généralités sur les questions STACK.

## Maxima CAS

Les questions STACK utilisent le moteur de calcul symbolique [Maxima](https://maxima.sourceforge.io/) (légèrement modifié) ce qui signifie que nous aurons un environnement de programmation mathématique qui simplifiera grandement la logique des questions. Nous aurons, par exemple, des fonctions pour :

* Résoudre des équations ou des systèmes d'équations.
* Types de données variés : listes, ensembles, matrices, ...
* Opérations sur les matrices : déterminant, inverse, transposée, ...
* Conditions logiques (if/else), boucles, ...
* Fonctions pour vérifier si deux expressions sont algébriquement équivalentes, si une expression est factorisée, si un nombre est égal à un autre avec une certaine tolérance...

## Faites connaissance avec Maxima

Le moyen le plus rapide, mais pas le plus recommandé, consiste à utiliser une [version en ligne de Maxima](http://maxima.cesga.es/).

La méthode la plus recommandée consiste à installer Maxima localement et à utiliser l'environnement graphique WxMaxima pour effectuer nos tests. Les instructions d'installation peuvent être trouvées sur [ce lien](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/CAS/STACK-Maxima\_sandbox.md).

{% hint style="info" %}
N'oubliez pas de modifier les premières lignes de la Sandbox selon notre système d'exploitation.
{% endhint %}

{% hint style="success" %}
La documentación de Máxima puede encontrarse en [aquí](https://maxima.sourceforge.io/docs/manual/es/maxima.html) y la de las funciones específicas de STACK en [este enlace](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/CAS/index.md).
{% endhint %}

![WxMaxima instalado en local](<../.gitbook/assets/image (16).png>)

## La philosophie STACK

Dans les questions, nous pouvons distinguer trois processus indépendants :

1. Validation de la réponse de l'utilisateur : nous pouvons établir le type de réponse que nous attendons et le valider avant d'évaluer s'il elle est correct ou non.
2. Vérification de la réponse : nous effectuerons divers tests sur la réponse pour établir si elle est correcte ou non. En principe, nous pouvons faire autant de tests que nous voulons.
3. Feedback : en fonction des résultats des tests que nous effectuons, nous pouvons donner un feedback personnalisé à l'utilisateur.
