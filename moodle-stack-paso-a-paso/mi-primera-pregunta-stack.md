# Mi primera pregunta STACK

## Archivo xml

{% file src="../.gitbook/assets/preguntas-DemoStack-12022021-Superficie estancia-20220420-2123.rar" %}
Comprimido en .rar y en formato xml de Moodle
{% endfile %}

## Descripción de la pregunta

Se trata de preparar una pregunta muy sencilla en que se pida calcular el área de una estancia rectangular (puede ser una cocina, un comedor, una habitación o una terraza).

* Las dimensiones deben estar entre 5 y 10 metros.
* De momento, no pediremos unidades en la respuesta del usuario.
* En el enunciado, se mostrarán, por un lado, las dimensiones en formato $$\LaTeX$$ y por otro como texto sin formato.

## Explicación paso a paso de la pregunta

### Variables

![](<../.gitbook/assets/image (56).png>)

{% hint style="info" %}
Uno de los puntos fuertes de las preguntas STACK es la posibilidad de **aleatorización**.&#x20;

En [esta página](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/CAS/Random.md) están las funciones que tenemos disponibles para aleatorizar.
{% endhint %}

En este caso hemos utilizado la función `rand(lista)` para elegir aleatoriamente un elemento de la lista y la función `rand_with_step(límite inferior, límite superior, paso)` para elegir un número que esté entre 5 y 10 (ambos incluidos) y avanzando de  uno en uno.

Los caracteres especiales (o con tilde en "habitación") se deben escribir como:

![](<../.gitbook/assets/image (2).png>)

Como última variable hemos elegido tans1 ("teacher answer 1") que almacena el valor de la respuesta correcta a la pregunta.

{% hint style="info" %}
En las preguntas de ejemplo (que están en el [curso demostración de STACK](https://github.com/maths/moodle-qtype\_stack/blob/master/samplequestions/STACK-demo.mbz), que se puede descargar y restaurar en cualquier instalación de Moodle) se suele utilizar TANS para la respuesta del profesor.

En caso de que usemos preguntas previamente preparadas para elaborar nuevas preguntas, puede ahorrar tiempo utilizar variables con nombres genéricos para las respuestas finales ya que, en la comprobación de la respuesta y en el feedback, se utilizará varias veces la "respuesta correcta".
{% endhint %}

### Enunciado

![](<../.gitbook/assets/image (119).png>)

{% hint style="success" %}
Para escribir variables en el enunciado podemos utilizar:

* `{#nombre_variable#}` mostrará el valor de la variable como texto sin formato. Si la variable es una cadena de texto, la mostrará como texto plano entre comillas.
* `{@nombre_variable@}` mostrará el valor de la variable como código $$\LaTeX$$. Si la variable es una cadena de texto, la mostrará como texto plano sin las comillas.
{% endhint %}

{% hint style="danger" %}
**MUY IMPORTANTE**

Cada ver que queramos incluir un **campo de respuesta** (hueco para que el usuario pueda responder), habremos de introducir **SIEMPRE LOS DOS**:

* `[[input:nombre_campo]]` donde queramos que aparezca el campo de respuesta
* `[[validation:nombre_campo]]` donde queramos que aparezca la validación de la respuesta. Notar que se trata de una validación del formato de la respuesta (decimal / no decimal, numérica, expresión algebraica...)

Donde queramos que aparezca la **corrección** de la validez de la respuesta del usuario (generalmente comparando con la respuesta correcta) tendremos que introducir:

* `[[feedback:nombre_feedback]]`
{% endhint %}

{% hint style="info" %}
Téngase en cuenta que:

* Podremos incluir más de un campo de **feedback** para un campo de respuesta (input).
* Podrá haber campos de respuesta sin **feedback**.
* Podrá haber un único **feedback** para varios campos de respuesta.
{% endhint %}

![Resultado que vería el usuario](<../.gitbook/assets/image (38).png>)

### Notas de la pregunta

En las preguntas que incluyen **aleatoriedad**, Moodle STACK nos pedirá que rellenemos el campo notas de la pregunta para poder guardar la pregunta.

La nota de la pregunta debe ser un texto que sea **diferente para cada una de las variantes de la pregunta**. STACK considerará que dos preguntas son la misma si sus notas de la pregunta son iguales.

{% hint style="info" %}
Es conveniente definir **notas de la pregunta que nos ayuden a identificar fácilmente a qué variante de cada pregunta corresponden** ya que, cuando despleguemos las variantes de cada pregunta, la forma de identificarlas será a través de la nota de la pregunta.
{% endhint %}

![](<../.gitbook/assets/image (111).png>)

{% hint style="success" %}
Las notas de la pregunta tendrán que incluir algunas de las variables aleatorizadas que hemos utilizado.
{% endhint %}

### Características del campo de entrada

![](<../.gitbook/assets/image (59).png>)

{% hint style="info" %}
Por **cada uno de los inputs** que tengamos en la pregunta, tendremos una pestaña **Entrada** para configurar dicho campo de entrada.
{% endhint %}

Veamos cómo configurar los campos más importantes:

* **Tipo de entrada**: permite elegir el tipo de entrada que esperamos del usuario. Documentación detallada [aquí](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/Authoring/Inputs.md). \
  Las que utilizaremos habitualmente son:

![](../.gitbook/assets/image.png)

1. Algebraica: admite expresiones algebraicas formadas por números y variables. Aunque no esperemos variables, es también válida para números.
2. Numerical: únicamente serán válidas las respuestas numéricas. También admite operaciones entre números cuyo resultado sea un número. Puede configurarse para admitir determinados tipos de número y no operaciones. Documentación detallada [aquí](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/Authoring/Numerical\_input.md).

* **Respuesta modelo**: aquí incluiremos una posible respuesta correcta a la pregunta. Es el valor que se introduce como respuesta correcta al pulsar en el botón `Rellenar con las respuestas correctas` de la vista previa de la pregunta. NO ES EL VALOR QUE SE UTILIZA PARA DECIDIR SI ES CORRECTA O NO LA RESPUESTA DEL USUARIO.
* **Prohibir flotantes**: en caso de que esté marcado como Sí, la respuesta del usuario no podrá incluir decimales de coma flotante (números decimales) y únicamente serán válidas respuestas con **números fraccionarios**. MUY ÚTIL EN MATEMÁTICA ELEMENTAL EN QUE NO DESEAMOS RESULTADOS DECIMALES.
* **Requerir mínima expresión**: fuerza a que las fracciones estén simplificadas. En caso contrario, da un aviso de que deben estarlo. EN LUGAR DE UTILIZAR ESTA OPCIÓN, NORMALMENTE SERÁ PREFERIBLE EVALUAR LA SIMPLIFICACIÓN CUANDO PUNTUEMOS LA PREGUNTA.
* **Comprobar tipo**: en caso de estar activado, muestra un mensaje de error al usuario en caso de que la expresión introducida no sea del tipo esperado y definido en el tipo de variable que sea la Respuesta modelo.
* **Verificar respuesta** y **Mostrar validación**: permiten mostrar al usuario su respuesta en un formato habitual. Por ejemplo, las fracciones, potencias y raíces se muestran de la forma estándar. NORMALMENTE, LA VALIDACIÓN COMPACTA SERÁ LA QUE MÁS SE UTILICE YA QUE SE MUESTRA EN LA MISMA LÍNEA DE LA RESPUESTA Y ES BASTANTE MÁS SENCILLA.

![Ejemplo de validación incluyendo lista de variables](<../.gitbook/assets/image (63).png>)

![Ejemplo de validación Compacta](<../.gitbook/assets/image (79).png>)

### Árbol de respuestas potenciales

La documentación relativa a esta parte de la pregunta se puede encontrar [aquí](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/Authoring/Feedback.md).

![](<../.gitbook/assets/image (40).png>)

{% hint style="info" %}
Aquí será donde:

* Haremos todas las comprobaciones que deseemos a la respuesta del usuario.
* Asignaremos la puntuación que consideremos dependiendo del resultado de dichas comprobaciones.
* Ofreceremos retroalimentación al usuario dependiendo del resultado de las comprobaciones que hagamos.&#x20;
{% endhint %}

En nuestra pregunta, únicamente verificamos que la respuesta del usuario(`Sans` que en este caso hemos llamado `ans1`) sea algebraicamente equivalente a la respuesta correcta (`Tans` que en este caso hemos llamado `tans1`). En caso de que así sea, que se asigna el 100% de la puntuación (1) y en caso contrario, se asigna una puntuación de cero. No ofrecemos retroalimentación.

Un campo importante a configurar es **PRT Feedback Style** ya que determinará qué información se ofrece al usuario tras la corrección. De momento lo dejaremos en Standard. Veremos más adelante, en otras preguntas, qué tipos de feedback podemos utilizar.

### Resultado de la pregunta

![](<../.gitbook/assets/image (5).png>)

### Despliegue de variantes y tests

![](<../.gitbook/assets/image (96).png>)

{% hint style="info" %}
Cuando las preguntas incluyen aleatoriedad, Moodle ofrece la posibilidad (y encarecidamente recomienda) la generación de **variantes**, que son cada una de las versiones de la pregunta que se mostrarán a los alumnos.
{% endhint %}

El despliegue de variantes nos permitirá tener **control sobre la aleatoriedad** que se genera en las preguntas ya que podremos eliminar aquellas variantes cuya combinación de variables aleatorias no sea de nuestro agrado (valores que se repiten, resultados fraccionarios indeseados...).

![](<../.gitbook/assets/image (57).png>)

En nuestra pregunta hay potencialmente 4 tipos de estancia por 5 anchos diferentes por 5 largos diferentes, lo que da un total de 100 variantes distintas. Nosotros desplegaremos 30.

![](<../.gitbook/assets/image (49).png>)

Aquí podremos eliminar las variantes que no nos "gusten" haciendo click en la Papelera.

Para terminar la pregunta, únicamente nos faltará generar un **caso de prueba**.

{% hint style="info" %}
Los **casos de prueba** sirven para identificar variantes que no funcionan correctamente.
{% endhint %}

En este caso, generaremos un caso de prueba elemental en que se verifique que si la respuesta del usuario (ans1) es igual a la respuesta modelo (tans1) se asigne una puntuación del 100% del valor de la pregunta.

![](<../.gitbook/assets/image (93).png>)

Con esto, en la pantalla en que se observan las variantes desplegadas, se puede realizar el test a todas las variantes (Run all tests on deployed variants):

![](<../.gitbook/assets/image (48).png>)
