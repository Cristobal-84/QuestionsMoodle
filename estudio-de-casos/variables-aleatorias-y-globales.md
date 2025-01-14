# Variables aléatoires et globales

## Pourquoi les variables

Les variables sont des paramètres que nous pouvons utiliser à la fois pour générer du caractère aléatoire dans nos questions et pour **effectuer des calculs intermédiaires**. \*\*\*\*

Elles sont définies au début de la question et sont probablement les éléments les plus importants de toute la question.

![](<../.gitbook/assets/Editar\_una\_pregunta\_de\_fórmulas (1).png>)

Dans la question d'introduction vue dans "[Premiers pas](../untitled.md#pregunta-en-xml)", nous avons défini deux variables aléatoires : a et b, afin que la formulation de la question change pour chacun des élèves.

{% hint style="danger" %}
Entre la définition de l'une et l'autre variable il faut introduire le séparateur " ; " ou la vérification des variables aléatoires  échouera.
{% endhint %}

## Variables aléatoires

{% hint style="info" %}
Plusieurs choix :

**Intervalles :**

a={1:6}; #La variable a prendra des valeurs entières aléatoires entre 1 et 5 (la dernière valeur n'est pas prise).

b={4:12:2}; #La variable b prendra des valeurs aléatoires entre 4 et 10 avec un incrément de 2 (c'est à dire qu'elle ne prendra que des valeurs paires).

**Valeurs :**

c={1,3,5,7}; #La variable c prendra une valeur au hasard parmi celles fournies entre virgules (elle vaudra 1 ou 3 ou 5 ou 7).
{% endhint %}

{% hint style="success" %}
Des combinaisons d'intervalles et de valeurs isolées peuvent être saisies.

d={-7:0,1:8}; #d prendra une valeur entre -7 et -1 ou entre 1 et 7, c'est-à-dire qu'il prendra une valeur entre -7 et 7 et ne pourra pas être nul.
{% endhint %}

## Variables globales

Les variables globales peuvent être utilisées pour effectuer des **calculs intermédiaires** et permettre aux **fonctions** implémentées dans Moodle Formulas d'être appliquées à des variables aléatoires. [Liste des fonctions utilisables](https://dynamiccourseware.org/course/view.php?id=31\&section=4).

![](<../.gitbook/assets/image (114).png>)

Dans la première ligne, nous réattribuons la valeur de b par une condition et dans la seconde, nous avons défini une nouvelle aire variable comme le produit des deux autres.

Les variables globales peuvent être utilisées à la fois dans l'énoncé de la question et dans la vérification des réponses ou dans le feedback donnée à l'élève.

{% hint style="danger" %}
En esta parte de la pregunta **2^3 NO ES 8.**

Las **potencias** se pueden hacer usando pow(2,3)=2\*\*3=8.
{% endhint %}

{% hint style="success" %}
Permiten establecer la lógica de la resolución de la pregunta.
{% endhint %}

## Variables en el enunciado

Para referirnos a las variables en el enunciado de la pregunta, tenemos que **introducirlas entre llaves**.

En el ejemplo de [Primeros pasos](../untitled.md#pregunta-en-xml) se observa que incluyendo las variables entre llaves...

![](<../.gitbook/assets/image (72).png>)

{% hint style="info" %}
Cada vez que se genera la pregunta, Moodle sustituye los valores de cada variable por los valores numéricos generados.
{% endhint %}

![](<../.gitbook/assets/image (61).png>)

![](<../.gitbook/assets/image (88).png>)

{% hint style="success" %}
Las variables se pueden utilizar tanto en el **enunciado** como en la **respuesta correcta** o en el **feedback** que se da al alumno.
{% endhint %}

## Variables en la respuesta

![](<../.gitbook/assets/image (120).png>)

{% hint style="success" %}
Será útil calcular la respuesta correcta en "Variables globales" y en el campo en que se introduce la respuesta correcta únicamente hacer referencia a la variable ya creada.
{% endhint %}
