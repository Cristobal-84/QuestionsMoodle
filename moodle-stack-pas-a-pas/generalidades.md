# Généralités

Tout d'abord, voyons quelques généralités sur les questions STACK.

## Maxima CAS

Les questions STACK utilisent le moteur de calcul symbolique [Maxima](https://maxima.sourceforge.io/) (légèrement modifié) ce qui signifie que nous aurons un environnement de programmation mathématique qui simplifiera grandement la logique des questions. Nous aurons, par exemple, des fonctions pour :

* Résoudre des équations ou des systèmes d'équations.
* Des types de données variés : listes, ensembles, matrices, ...
* Operativa con matrices: determinante, inversa, traspuesta, ...
* Condiciones lógicas (if/else), bucles, ...
* Funciones para comprobar si dos expresiones son algebraicamente equivalentes, si una expresión está factorizada, si un número es igual a otro con una cierta tolerancia...

## Familiarizarse con Máxima

La forma más rápida, pero no más recomendable, es usar una versión online de Máxima: [http://maxima.cesga.es/](http://maxima.cesga.es/)

La forma más recomendable, es instalar Máxima en local y utilizar el entorno gráfico de WxMaxima para hacer nuestras pruebas. Las instrucciones de instalación se pueden encontrar en [este enlace](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/CAS/STACK-Maxima\_sandbox.md).

{% hint style="info" %}
No hay que olvidarse de editar las primeras líneas del Sandbox de acuerdo con nuestro sistema operativo.
{% endhint %}

{% hint style="success" %}
La documentación de Máxima puede encontrarse en [aquí](https://maxima.sourceforge.io/docs/manual/es/maxima.html) y la de las funciones específicas de STACK en [este enlace](https://github.com/maths/moodle-qtype\_stack/blob/master/doc/en/CAS/index.md).
{% endhint %}

![WxMaxima instalado en local](<../.gitbook/assets/image (16).png>)

## La filosofía de STACK

En las preguntas podremos diferenciar tres procesos independientes:

1. Validación de la respuesta del usuario: podemos establecer el tipo de respuesta que esperamos y validarla previamente a valorar si es o no correcta.
2. Comprobación de la respuesta: realizaremos diversas pruebas a la respuesta para establecer si es o no correcta. En principio podemos hacer tantas pruebas como queramos.
3. Feedback: dependiendo de los resultados de las pruebas que hagamos, podemos dar feedback personalizado al usuario.
