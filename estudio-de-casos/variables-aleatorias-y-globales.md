# Variables aléatoires et globales

## Pourquoi les variables

Las variables son parámetros que podemos utilizar tanto para **generar aleatoriedad** en nuestras preguntas como para **realizar cálculos intermedios**. \*\*\*\*

Se definen al principio de la pregunta y son, probablemente, los elementos más importantes de toda la pregunta.

![](<../.gitbook/assets/Editar\_una\_pregunta\_de\_fórmulas (1).png>)

En la pregunta de introducción vista en [Primeros pasos](../untitled.md#pregunta-en-xml) hemos definido dos variables aleatorias: a y b para que el enunciado de la pregunta cambie para cada uno de los alumnos.

{% hint style="danger" %}
Entre la definición de una y otra variable hay que introducir **;** o dará error al comprobar.
{% endhint %}

## Variables aleatorias

{% hint style="info" %}
Varias opciones:

**Intervalos:**

a={1:6}; #La variable a tomará valores aleatorios enteros entre 1 y 5 (el último valor no se coge)

b={4:12:2}; #La variable b tomará valores aleatorios entre 4 y 10 con un incremento de 2 (es decir, únicamente tomará los valores pares)

**Valores:**

c={1,3,5,7}; #La variable c tomará un valor aleatorio de los suministrados entre comas (valdrá 1 o 3 o 5 o 7).
{% endhint %}

{% hint style="success" %}
Se pueden introducir combinaciones de intervalos y valores aislados.

d={-7:0,1:8}; #d tomará un valor entre -7 y -1 o entre 1 y 7, es decir, toma un valor entre -7 y 7 y no puede valer cero.
{% endhint %}

## Variables globales

Las variables globales pueden utilizarse para realizar **cálculos intermedios** y permiten **aplicar funciones** implementadas en Moodle Fórmulas sobre las variables aleatorias. [Lista de funciones utilizables](https://moodleformulas.org/course/view.php?id=31\&section=1).

![](<../.gitbook/assets/image (114).png>)

En la primera línea reasignamos el valor de b mediante un condicional y en la segunda hemos definido una nueva variable area como producto de las otras dos.

Las variables globales se pueden usar tanto en el enunciado de la pregunta como en la comprobación de las respuestas o en el feedback que se da al alumno.

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
