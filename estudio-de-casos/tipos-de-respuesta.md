# Tipos de respuesta

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Preguntas-Comunicarse con Moodle-20200524-1316.xml" %}

![](<../.gitbook/assets/image (71).png>)

## Comportamiento acumulativo

Conforme descendemos en la lista, la respuesta admite todas las posibilidades de la anterior + las opciones propias del tipo.

Así, la respuesta numérica admitirá todas las entradas de la respuesta número.

### Número

Permite la introducción de números únicamente.

### Numérico

Permite la introducción, además, de operaciones elementales: suma, resta, multiplicación, división y potencias.

{% hint style="success" %}
El tipo numérico será el apropiado cuando preguntemos por una fracción. Admitirá por respuesta 13/2.
{% endhint %}

{% hint style="info" %}
Este tipo de respuesta es muy útil cuando queremos **"liberar" al alumno de la operativa** y centrarnos en conceptos. Por ejemplo: si preguntamos la velocidad media al recorrer 120 km en 2 horas y no nos preocupa que el alumno sepa dividir 120 entre 2; podemos **dar por válida una respuesta que sea 120/2** usando el tipo numérico.
{% endhint %}

### Fórmula numérica

Admite, además, funciones como puede ser sqrt(2)= $$\sqrt{2}$$&#x20;

### Fórmula algebraica

En este caso admitimos respuestas que incluyan variables. Por ejemplo: 3x+4

## Respuesta correcta

Para las respuestas tipo número, numérica y fórmula numérica, la respuesta correcta será un **número.**

Para la fórmula algebraica la respuesta es una **cadena de texto** (variable tipo String). Esto condicionará de forma importante el comportamiento de las preguntas en que se pida una fórmula algebraica.

{% hint style="success" %}
Podemos usar la pregunta tipo fórmula algebraica para admitir respuestas como "introduce NO", cuando no tiene solución la ecuación, por ejemplo.
{% endhint %}

Dada su singularidad, dedicaré la siguiente página a desarrollar en detalle las preguntas de tipo fórmula algebraica.

