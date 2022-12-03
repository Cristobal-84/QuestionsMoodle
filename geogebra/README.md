# GeoGebra

## Qu'est-ce que GeoGebra ?

Parmi ceux arrivés jusqu'ici, je ne pense pas qu'il y ait quelqu'un qui lit ceci qui ne connaisse pas GeoGebra.

{% hint style="success" %}
[GeoGebra ](https://www.geogebra.org)possède une **interface bien connue** **et documentée** : les constructions géométriques peuvent être faites sans avoir besoin de programmer en Javascript.
{% endhint %}

{% hint style="success" %}
GeoGebra a une **importante communauté** et un grand nombre de [matériaux librement partagés](https://www.geogebra.org/materials).
{% endhint %}

## Plusieurs possibilités

Lors d'une intégration de GeoGebra dans Moodle Formulas, nous avons plusieurs options : en fonction du nombre de paramètres que nous voulons synchroniser entre GeoGebra et Aules. Du plus simple (et moins fonctionnel) au plus laborieux :

1. Pregunta con aleatoriedad generada por GeoGebra y corregida por GeoGebra en que únicamente registramos la puntuación obtenida por el alumno: va a ser muy útil para reutilizar actividades autoevaluables de GeoGebra en Aules.
2. Pregunta con aleatoriedad generada por Aules y registro de la respuesta del estudiante.

Caben todas las posibilidades intermedias de registro de datos.

## Integración en Moodle

Con el plugin Fórmulas, podremos incluir applets de GeoGebra como parte de las preguntas de Moodle. Tendremos la posibilidad de mostrar únicamente el applet, mostrar el applet con valores de parámetros establecidos por Moodle (gráficos aleatorios en cada ejecución de la pregunta) e incluso capturar respuestas gráficas derivadas de la interacción con el applet.

{% hint style="success" %}
Integraremos las **construcciones dentro de preguntas**, con lo que podrán formar parte de cuestionarios.
{% endhint %}

{% hint style="info" %}
Podremos crear preguntas que incluyan aleatoriedad y **registrar las respuestas del usuario** (no únicamente la puntuación obtenida).
{% endhint %}

{% hint style="danger" %}
La preparación de estas preguntas es laboriosa y no es sencilla ya que hay que utilizar código html y Javascript.
{% endhint %}

Comenzaremos por las más fáciles de preparar...
