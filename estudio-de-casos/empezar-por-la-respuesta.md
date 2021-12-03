# Empezar por la respuesta

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Aules-Ecuación segundo grado-20200525-1726.xml" %}

![](<../.gitbook/assets/image (38).png>)

## Enunciado de la pregunta

Resolver la ecuación de 2º grado ax^2+bx+c=0 donde queremos que las soluciones sean enteras y queremos que los coeficientes a, b y c también sean enteros.&#x20;

Las raíces deben estar en el intervalo \[-5,5] y no ser nulas.

## ¿Por qué no montar la pregunta a partir de las soluciones?

Podemos seguir el siguiente esquema:

* Definimos dos variables aleatorias x1 y x2, que serán las soluciones de la ecuación.
* Como queremos que x1≠x2, reasignamos el valor de una de las variables en caso de coincidencia.
* Generamos la ecuación a partir de ec=a\*(x-x1)(x-x2)=0.
* Como habrá dos campos de respuesta, haremos que sea indiferente el orden en que se introducen las respuestas.



![](<../.gitbook/assets/image (35).png>)

![](<../.gitbook/assets/image (36).png>)

![](<../.gitbook/assets/image (37).png>)

Al establecer el criterio de calificación como:

```
(_0==x1&&_1==x2)||(_1==x1&&_0==x2)
```

{% hint style="success" %}
"**Si** caja de respuesta \_0 es igual a x1 **y** \_1 es igual a x2 **o si** \_1 es igual a x1 **y** \_0 es igual a x2, entonces la respuesta es correcta"
{% endhint %}

&#x20;__ Conseguimos que sea correcta la respuesta en un orden o en otro.
