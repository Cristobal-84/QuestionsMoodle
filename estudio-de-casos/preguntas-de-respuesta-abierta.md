# Preguntas de respuesta abierta

## ¿Qué queremos hacer?

Se trata de comprobar si la respuesta proporcionada verifica unas ciertas restricciones.

Un ejemplo de pregunta podría ser:&#x20;

> Busca dos números distintos que cumplan simultáneamente las siguientes condiciones:
>
> 1. Ambos están en el intervalo \[10,20].
> 2. Uno de ellos es múltiplo de 2.
> 3. El otro es múltiplo de 3.
> 4. La suma de ambos es >30.

## Archivo XML de referencia&#x20;

{% file src="../.gitbook/assets/preguntas-Aules-Respuesta abierta-20200524-1026.xml" %}

## Variables de calificación

Podemos hacer comprobaciones lógicas de las entradas del usuario utilizando las variables de calificación y los criterios de calificación.

{% hint style="info" %}
Dentro de la parte, hay que pulsar en Ver más... para que se visualicen las opciones de variables de calificación
{% endhint %}

![](<../.gitbook/assets/image (73).png>)

Dentro de variables de calificación, introduciremos las comprobaciones que deseamos realizar.

```
primernumentre10y20=(_0>=10)&&(_0<=20);
primernummult2=_0%2==0;
segundonumentre10y20=(_1>=10)&&(_1<=20);
segundonummult3=_1%3==0;
sumamayora30=(_0+_1)>30;
```

{% hint style="info" %}
Asignamos valores a las variables mediante operadores lógicos y de comparación.

El valor de cada una de estas variables será 1 ó 0.
{% endhint %}

![](<../.gitbook/assets/image (44).png>)

## Criterios de calificación

En **criterios de calificación** podemos incluir nuestro criterio. En este caso hemos decidido que la pregunta puntúe un 100% si ambos números cumplen todas las restricciones y 0 en caso contrario.

```
primernumentre10y20 &&
primernummult2 &&
segundonumentre10y20 &&
segundonummult3 &&
sumamayora30
```

![](<../.gitbook/assets/image (116).png>)

{% hint style="warning" %}
Puesto que los operadores de comprobación dan resultado 1 si la comprobación se cumple, podemos operar entre las variables teniendo en cuenta que 1 = cierto y 0=falso.

Así, podríamos haber establecido el criterio de calificación como:

primernumeroentre10y20 \* primernummult2 \* ...

Multiplicamos valores que valen 1 o 0 -> Da 1 (=cierto) si todos son ciertos
{% endhint %}

### Puntuación parcial de los distintos criterios

También podríamos haber considerado el criterio de que cada una de las variables de calificación tuviera una contribución a la puntuación de la pregunta.

Por ejemplo:&#x20;

* 30% si el primer número es 10≤n≤20 y múltiplo de 2.
* 30 % si el segundo número es 10≤n≤20 y múltiplo de 3.
* 40 % restante si la suma de ambos es >30.

Para conseguir esto bastaría hacer, en **Criterios de calificación**:

```
0.3*(primernumentre10y20&&primernummult2)+
0.3*(segundonumentre10y20&&segundonummult3)+
0.4*sumamayora30
```

#### Archivo XML de referencia&#x20;

{% file src="../.gitbook/assets/preguntas-Aules-Respuesta abierta-20200524-1106.xml" %}
Respuesta abierta con crédito parcial
{% endfile %}
