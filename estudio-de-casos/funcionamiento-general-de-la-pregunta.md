# Introducción de contenido matemático

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Aules-Visualizar contenido matemático-20200521-2111.xml" %}

![](<../.gitbook/assets/image (81).png>)

En muchas ocasiones necesitamos introducir contenido matemático en nuestros enunciados.&#x20;

La solución se llama $$\LaTeX{}$$, que permite la introducción de todo tipo de fórmulas matemáticas.

Para introducir contenido en $$\LaTeX$$existen **varias opciones.**

## Mediante el editor de Moodle

![](<../.gitbook/assets/image (103).png>)

&#x20;Ofrece ecuaciones predefinidas que podemos seleccionar y adaptar a nuestras necesidades. Al pulsar en salvar ecuación, la introduce con los signos \\( ... \\) que indican a Moodle que entre medias estamos escribiendo código $$\LaTeX$$.&#x20;

![](<../.gitbook/assets/image (31).png>)

{% hint style="warning" %}
Esa ecuación mostrará $$\frac{a}{b+c}$$ y no sustituirá el valor de las variables a, b, c.
{% endhint %}

{% hint style="success" %}
Si queremos que se muestre el valor numérico de las variables, tendríamos que incluirlas entre llaves:

\\( \frac\{{a\}}\{{b}+{c\}} \\)
{% endhint %}

{% hint style="success" %}
Para mostrar fracciones es mucho más interesante el comando \dfrac{numerador}{denominador} que el comando por defecto del editor \frac. Ya que el primero mantiene el tamaño de los números de la fracción y no los reduce.

( \frac{a}{b+c} = \dfrac{a}{b+c} \\)

$$\frac{a}{b+c} = \dfrac{a}{b+c}$$&#x20;
{% endhint %}

## Introduciendo directamente código $$\LaTeX$$&#x20;

La forma de indicar a Moodle que introduciremos  $$\LaTeX$$ es:

```
\( código LaTeX \) mostrará el contenido en la misma línea
```

{% hint style="info" %}
El resultado de \\( (a+b)^{2} \\) no es la suma de los cuadrados. Mostrará:
{% endhint %}

> El resultado de $$(a + b)^{2}$$ no es la suma de los cuadrados.

```
\[ código LaTeX \] mostrará el contenido centrado en la línea siguiente
```

{% hint style="info" %}
El resultado de \\\[ (a+b)^{2} \\] no es la suma de los cuadrados. Mostrará:
{% endhint %}

> El resultado de                &#x20;
>
> $$(a+b)^2$$&#x20;
>
> no es la suma de los cuadrados

Existe multitud de información en la red acerca del uso de expresiones de $$\LaTeX$$. Algunas formas de generar contenido son:

* Editor online: [https://www.codecogs.com/latex/eqneditor.php?lang=es-es](https://www.codecogs.com/latex/eqneditor.php?lang=es-es)
* Copiando / pegando desde la calculadora gráfica de Desmos.

![](../.gitbook/assets/DESMOS.gif)

* Capturando el código desde el navegador (si se genera en un sitio a través de Mathjax), como por ejemplo desde Moodle:

{% hint style="info" %}
En algunos casos, haciendo clic derecho sobre una fórmula podemos mostrar el código $$\LaTeX$$
{% endhint %}

![](<../.gitbook/assets/Sin título (1).png>)

![](<../.gitbook/assets/Sin título1.png>)

## Algunos consejos

{% hint style="success" %}
Para evitar problemas con variables que se sustituyen en el enunciado por su valor numérico por culpa de las llaves de $$\LaTeX$$, como ocurre en el ejemplo anterior con el 5 del numerador de la fracción: **elegir nombres de variable** ligeramente distintos al nombre de las incógnitas que aparecerán en las ecuaciones.
{% endhint %}

{% hint style="info" %}
La función poly() de Moodle Fórmulas resuelve muchos dolores de cabeza con los signos de las variables:

Por ejemplo, al escribir \\( {a}x^2+{b}x+{c}=0\\) en una pregunta con valores aleatorios podríamos obtener:

$$1x^2+-3x+-4=0$$ si a=1, b=-3, c=-4

Para que la ecuación se muestre correctamente, podemos usar la función poly(), referenciada en [https://moodleformulas.org/course/view.php?id=31\&section=49](https://moodleformulas.org/course/view.php?id=31\&section=49).

En variables globales: ec=poly("x",\[a,b,c]); y al introducir {ec} en el enunciado obtendremos el polinomio adecuadamente formateado.
{% endhint %}

{% hint style="info" %}
Podemos introducir operaciones o funciones que se aplican a las variables introduciendo un = dentro de las {}.

En la ecuación anterior podríamos haber introducido directamente {=poly("x",\[a,b,c])} en el enunciado.
{% endhint %}

