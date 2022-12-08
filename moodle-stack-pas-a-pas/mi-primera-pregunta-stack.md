# Ma première question STACK

## Fichier XML

{% file src="../.gitbook/assets/preguntas-DemoStack-12022021-Superficie estancia-20220420-2123.rar" %}
Compression au format .rar du fichier XML Moodle
{% endfile %}

## Description de la question

Il s'agit de préparer une question très simple qui demande de calculer l'aire d'une pièce rectangulaire (cela peut être une cuisine, une salle à manger, une chambre ou une terrasse).

* Les dimensions doivent être comprises entre 5 et 10 mètres.
* Pour l'instant, nous ne demanderons pas d'unités dans la réponse de l'utilisateur.
* Dans le relevé, les dimensions seront affichées au format $$\LaTeX$$ d'une part et en texte brut d'autre part.

## Explication étape par étape de la question

### Variables

![](<../.gitbook/assets/image (56).png>)

{% hint style="info" %}
L'un des points forts des questions STACK est la possibilité de **randomisation**.

Sur [cette page](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/CAS/Random.md) se trouvent les fonctions dont nous disposons pour randomiser.
{% endhint %}

Dans ce cas, nous avons utilisé la fonction`rand(lista)` pour choisir au hasard un élément de la liste et la fonction `rand_with_step(límite inferior, límite superior, paso)` pour choisir un nombre compris entre 5 et 10 (les deux inclus) et avancer de un en un.

Les caractères spéciaux (ou avec l'accent dans "habitación") doivent être écrits comme suit :

![](<../.gitbook/assets/image (2).png>)

Comme dernière variable, nous avons choisi tans1 ("teacher answer 1") qui stocke la valeur de la bonne réponse à la question.

{% hint style="info" %}
Dans les exemples de questions (qui se trouvent dans le [cours de démonstration STACK](https://github.com/maths/moodle-qtype\_stack/blob/master/samplequestions/STACK-demo.mbz), qui peut être téléchargé et restauré sur n'importe quelle installation Moodle), TANS est souvent utilisé pour la réponse de l'enseignant.

Dans le cas où nous utilisons des questions préalablement préparées pour créer de nouvelles questions, cela peut faire gagner du temps d'utiliser des variables avec des noms génériques pour les réponses finales puisque, dans la vérification des réponses et dans le feedback, la "bonne réponse" sera utilisée plusieurs fois.
{% endhint %}

## Enoncé

![](<../.gitbook/assets/image (119).png>)

{% hint style="success" %}
Pour écrire des variables dans l'instruction, nous pouvons utiliser :

* `{#nombre_variable#}` affichera la valeur de la variable sous forme de texte brut. Si la variable est une chaîne de texte, elle sera affichée sous forme de texte brut entre guillemets.
* `{@nombre_variable@}` affichera la valeur de la variable sous forme de code $$\LaTeX$$. Si la variable est une chaîne de texte, elle sera affichée sous forme de texte brut sans les guillemets.
{% endhint %}

{% hint style="danger" %}
TRÈS IMPORTANT

Chaque fois que nous voulons inclure un **champ de réponse** (un espace pour que l'utilisateur réponde), nous devons **TOUJOURS introduire LES DEUX** champs suivants :

* `[[input:nombre_campo]]` où nous voulons que le champ de réponse apparaisse,
* `[[validation:nombre_campo]]` où nous voulons que la validation de la réponse apparaisse. Notez qu'il s'agit d'une validation du format de la réponse (décimal/non décimal, numérique, expression algébrique...).

Là où nous voulons que la correction de la validité de la réponse de l'utilisateur apparaisse (généralement en la comparant à la bonne réponse) nous devrons introduire :

* `[[feedback:nombre_feedback]]`
{% endhint %}

{% hint style="warning" %}
Veuillez noter que :

* Nous pouvons inclure plus d'un champ de **feedback** pour un champ de réponse (input).
* Il peut y avoir des champs de réponse sans **feedback**.
* Il peut y avoir un seul **feedback** pour plusieurs champs de réponse.
{% endhint %}

![Résultat que l'utilisateur verrait](<../.gitbook/assets/image (38).png>)

## Annotation

Dans les questions qui incluent des variables aléatoires, Moodle STACK nous demandera de remplir le champ annotation de question avant de pouvoir sauvegarder la question.

Le but d'une annotation de question est de distinguer les différentes versions aléatoires d'une question. L'annotation de question doit donc être un texte **différente pour chacune des variantes de la question**. STACK considèrera que deux versions d'une question sont égales si, et seulement si, leurs annotations de question sont égales.

{% hint style="info" %}
Il est pratique de définir **des annotations de question qui nous aident à identifier facilement à quelle variante de chaque question elles correspondent** puisque, lorsque nous afficherons les variantes de chaque question, la façon de les identifier se fera par l'annotation de question.
{% endhint %}

![](<../.gitbook/assets/image (111).png>)

{% hint style="success" %}
Les annotations de questions devront inclure certaines des variables aléatoires que nous avons utilisées.
{% endhint %}

## Fonctionnalités du champ de saisie (Input)

![](<../.gitbook/assets/image (59).png>)

{% hint style="info" %}
Pour **chacun des input** que nous avons dans la question, nous aurons un onglet **Input** pour configurer ledit champ de saisie.
{% endhint %}

Voyons comment configurer les champs les plus importants :

* **Type d'input :** vous permet de choisir le type d'entrée que nous attendons de l'utilisateur. Documentation détaillée [ici](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/Authoring/Inputs.md).

Ceux que nous utiliserons généralement sont :

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
* Ofreceremos retroalimentación al usuario dependiendo del resultado de las comprobaciones que hagamos.
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
