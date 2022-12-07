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

## La filosofía de STACK

En las preguntas podremos diferenciar tres procesos independientes:

1. Validación de la respuesta del usuario: podemos establecer el tipo de respuesta que esperamos y validarla previamente a valorar si es o no correcta.
2. Comprobación de la respuesta: realizaremos diversas pruebas a la respuesta para establecer si es o no correcta. En principio podemos hacer tantas pruebas como queramos.
3. Feedback: dependiendo de los resultados de las pruebas que hagamos, podemos dar feedback personalizado al usuario.
