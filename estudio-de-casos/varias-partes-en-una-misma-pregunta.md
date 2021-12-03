# Varias partes en una misma pregunta

## Archivo XML de referencia

{% file src="../.gitbook/assets/preguntas-Aules-Varias partes-20200524-0928.xml" %}

## ¿Qué son las partes?

Podríamos decir que una **parte** es un elemento de la pregunta que se califica de forma independiente al resto.

{% hint style="info" %}
Las distintas partes de una pregunta se referencian en el enunciado con {#i} siendo i el número de la parte. El mismo identificador se incluirá en la parte correspondiente.
{% endhint %}

![](<../.gitbook/assets/image (21).png>)

{% hint style="danger" %}
En el enunciado el marcador va entre llaves y en la parte ya no se ponen las llaves
{% endhint %}

{% hint style="success" %}
En la parte, los campos de respuesta se indican con {\_0}, {\_1}, ... Podremos incluir tantos campos de entrada como deseemos. Marcado en verde en la imagen anterior.
{% endhint %}

## Varios campos de entrada en una parte

&#x20;Podemos incluir varios campos de entrada en una parte si deseamos calificarlos conjuntamente.

![](<../.gitbook/assets/image (22).png>)

{% hint style="success" %}
La respuesta correcta se introduce como array (entre corchetes) y con los campos de entrada en orden: primero respuesta correcta del \_0_,_ luego la del \_1,...
{% endhint %}

{% hint style="warning" %}
En este caso, por defecto se corregirá conjuntamente la parte, es decir, la parte estará toda bien o toda mal: en caso de introducir incorrectamente uno de los valores la respuesta será incorrecta sin disponerse de información de qué parte es la que está mal.
{% endhint %}

{% hint style="success" %}
En un ejemplo como el anterior es más interesante incluir dos partes que se muestren en la misma línea, con el fin de obtener la corrección de cada campo de entrada independientemente del otro
{% endhint %}

## Varias partes en una misma línea

{% hint style="info" %}
Para mostrar el código HTML con el editor por defecto de Moodle basta pulsar dos botones.
{% endhint %}

![](<../.gitbook/assets/image (24).png>)

```
<div style="display:inline-block;">{#1}</div>
```

Hará que las partes se muestren "inline", es decir, en la misma línea. Al corregir la pregunta, las partes se comprueban de forma independiente una de la otra, con lo que tenemos más información de cuál es correcta y cuál no.

![](<../.gitbook/assets/image (23).png>)
