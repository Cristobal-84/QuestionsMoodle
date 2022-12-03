# Preguntas de opción múltiple

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Aules-Preguntas de opción múltiple-20200525-1832.xml" %}

![](<../.gitbook/assets/image (55).png>)

![](<../.gitbook/assets/image (45).png>)

![](<../.gitbook/assets/image (115).png>)

## Las listas...

Una lista es una colección ordenada de elementos, en Fórmulas todos ellos del mismo tipo (normalmente números o cadenas de texto).

```
opciones=["a","b","c","d"];
```

{% hint style="success" %}
Podemos hacer referencia a cada uno de los elementos de la lista mediante:

opciones\[i], siendo i el subíndice de la posición del elemento (el primer elemento está en la posición cero).

Así, en el caso anterior se cumplirá que opciones\[1] es "b" y opciones\[3] vale "d".
{% endhint %}

## Preguntas de opción múltiple

{% hint style="info" %}
**Lista desplegable:** {\_0:opciones:MCE}

**Botones de radio:** {\_0:opciones}
{% endhint %}

## Respuesta correcta

En el campo destinado a la respuesta correcta introduciremos el **subíndice del elemento de la lista** que es el correcto.
