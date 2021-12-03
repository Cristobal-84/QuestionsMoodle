# Fórmula algebraica

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Aules-Opera los monomios (ax+b)(cx+d)-20200524-1904.xml" %}

## Algunas consideraciones...

{% hint style="info" %}
La respuesta de tipo fórmula algebraica realiza comprobaciones numéricas en muchos valores de la(s) variable(s).
{% endhint %}

Ello da lugar a una importante limitación de este tipo de respuesta:

{% hint style="danger" %}
Dará por válida cualquier expresión matemáticamente equivalente a la respuesta correcta.
{% endhint %}

Adicionalmente  a los campos a cumplimentar en el resto de tipos de respuesta hay que tener en cuenta que:

* La respuesta correcta es una **cadena de texto** (entre comillas).
* En **variables locales** de la parte hay que definir el rango de valores de comprobación de la(s) variable(s). En los puntos de comprobación debe ser posible realizar la operación (cuidado con denominadores nulos, logaritmos de números negativos...)
* El único **criterio de calificación** que acepta es el **error absoluto**.
* Los **errores numéricos** son importantes: si elegimos error absoluto==0 puede que la respuesta se corrija incorrectamente debido a errores numéricos con las operaciones de coma flotante. Como referencia un error absoluto < un valor entre 1E-6 y 1E-10 puede ser razonable con carácter general.&#x20;

![](<../.gitbook/assets/image (33).png>)

![](<../.gitbook/assets/image (32).png>)

{% hint style="success" %}
Los condicionales, cuando utilicemos cadenas de texto, se pueden realizar con la función **pick()**. Documentación en [https://moodleformulas.org/course/view.php?id=31\&section=48](https://moodleformulas.org/course/view.php?id=31\&section=48)
{% endhint %}

![](<../.gitbook/assets/image (34).png>)
