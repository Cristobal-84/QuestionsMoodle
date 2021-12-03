---
description: >-
  Guía de uso y ejemplos de uso de Moodle para la evaluación de contenidos
  matemáticos.
---

# Empezamos

{% hint style="warning" %}
ESTA DOCUMENTACIÓN SE ELABORÓ DURANTE EL VERANO DE 2020 Y NO SE ACTUALIZA
{% endhint %}

{% hint style="success" %}
Actualmente:

* Puede no funcionar correctamente.
* Puede haber otras formas más sencillas de hacer lo que aquí se expone.
{% endhint %}

## ¿Qué se puede encontrar en esta página?

Experiencias de uso de Moodle para la creación y evaluación de actividades de Matemáticas.

Este libro pretende ser una guía no exhaustiva para la creación de materiales de Matemáticas autoevaluables para Moodle.

## ¿Qué se necesita?

Será necesaria una instalación de Moodle y el plugin Fórmulas de Moodle.

Este plugin puede encontrarse en [https://moodle.org/plugins/qtype\_formulas](https://moodle.org/plugins/qtype\_formulas).

La instalación de plugins en Moodle requiere de permisos de administrador. Usuarios individuales **no pueden instalar** plugins. Asegúrate de que tu administrador lo ha instalado o solicita su instalación.

Puedes comprobar si dispones de la pregunta Fórmulas si creas una nueva pregunta y aparece la opción de Fórmulas en los tipos de pregunta que puedes seleccionar:&#x20;

![](.gitbook/assets/pantallaconpregunta.png)

## ¿A quién va dirigido?

Como profesor de Matemáticas en Secundaria y Bachillerato, me centraré en ejemplos y preguntas adaptadas al nivel en que imparto docencia.&#x20;

No obstante, el método de trabajo y las propuestas de actividades serán lo suficientemente generales para que puedan ser utilizadas en un curso de Moodle de cualquier nivel. Las preguntas de tipo fórmulas son aptas tanto para matemáticas como para cualquier área en que pueda ser interesante utilizar preguntas que empleen notación matemática o sean susceptibles de ser generadas mediante valores aleatorios.

{% hint style="info" %}
La elaboración de este tipo de preguntas es costoso tanto en tiempo como en conocimientos: hay que superar una curva de aprendizaje y ser resiliente para no abandonar.&#x20;
{% endhint %}

{% hint style="success" %}
El tiempo que se invierte en la preparación de la pregunta se recupera con la corrección automática.&#x20;
{% endhint %}

{% hint style="success" %}
La pregunta que recibirá cada alumno será diferente a la del resto, lo que dificulta la copia.
{% endhint %}

{% hint style="danger" %}
Este libro no pretende ser un banco de preguntas ni un catálogo directamente aplicable al aula. Únicamente es una guía para facilitar el aprendizaje del uso de las preguntas de tipo fórmulas en Moodle.
{% endhint %}

> ### Largo es el camino de la enseñanza por medio de teorías, breve y eficaz por medio de ejemplos (Séneca)

## ¿Qué tipos de pregunta se pueden realizar con Fórmulas?

En este vídeo (en inglés) se observan varios de ejemplos de pregunta. También se puede ver algo del código que es necesario escribir para llegar al resultado que se muestra.

{% embed url="https://youtu.be/brWP7LRjPS0" %}

Además de las mostradas en el vídeo, que son las más sencillas de realizar, también es posible incluir preguntas que:

* Tengan elementos de opción múltiple:

{% tabs %}
{% tab title="Desplegable" %}
![](<.gitbook/assets/image (6).png>)
{% endtab %}

{% tab title="Botones de radio" %}
![](<.gitbook/assets/image (8).png>)
{% endtab %}
{% endtabs %}

* Generen gráficos dinámicamente: por ejemplo, la gráfica de una función.

{% tabs %}
{% tab title="Gráficos dinámicos de Desmos" %}
![](<.gitbook/assets/image (1).png>)
{% endtab %}

{% tab title="Gráficos dinámicos de JSXGraph (recomendado)" %}
![](<.gitbook/assets/image (2).png>)
{% endtab %}

{% tab title="Aleatoriedad a través del color" %}
![](<.gitbook/assets/image (28).png>)
{% endtab %}
{% endtabs %}

* Generen gráficos que permitan respuestas gráficas por parte del alumnado: por ejemplo, del tipo "arrastra los puntos para que la recta que los une sea y=mx+n", con m y n diferentes para cada alumno.

{% tabs %}
{% tab title="Vectores" %}
![](<.gitbook/assets/image (3).png>)
{% endtab %}

{% tab title="Rectas" %}
![](<.gitbook/assets/image (4).png>)
{% endtab %}

{% tab title="Respuesta abierta" %}
![](<.gitbook/assets/image (5).png>)
{% endtab %}
{% endtabs %}

## ¿Qué hacer cuando las cosas no funcionan?

En los momentos de atasco, en que una pregunta no funciona y no sabemos qué ocurre. Todo parece estar bien escrito, el código es el correcto, pero da error o no funciona como debiera.

Has buscado y leído la documentación, has buscado ejemplos parecidos, has hecho cursos gratuitos de Javascript y de HTML...

Puedes obtener ayuda en [el foro de Moodle quiz (en inglés)](https://moodle.org/mod/forum/view.php?id=737). Si es problema el idioma, puedes escribir en español y traducir con el traductor de Google. Se entenderá aunque no sea un inglés perfecto.

Es importante que documentes bien la pregunta:

* Incluye tu archivo XML.
* Explica bien qué quieres hacer, qué has hecho y qué problema encuentras.

{% hint style="info" %}
No olvides que quien te trata de ayudar lo hace desinteresadamente y te está regalando su tiempo.&#x20;
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
