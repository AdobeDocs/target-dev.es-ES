---
keywords: parámetros de mbox globales, targetPageParams, cadena de consulta, matriz, json, dtm
description: Aprenda a utilizar la función [!UICONTROL targetPageParams] para pasar información adicional de contexto o destino al  [!DNL Adobe Target] mbox global.
title: ¿Cómo paso parámetros a un mbox global?
feature: at.js
exl-id: 2a6be3e4-a618-4812-9e87-b01789705c40
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 61%

---

# Pasar parámetros a un mbox global

La función de JavaScript `targetPageParams` se usa para pasar parámetros al mbox global en [!DNL Adobe Target]. Esto es necesario en cualquier escenario donde se pase información adicional de contexto/destino a [!DNL Target].

Por ejemplo, en una actividad de Recommendations, use los parámetros para representar el producto o la categoría actual que se está viendo.

El código para llamar a la función de JavaScript debe ir antes que el mbox global en la página, independientemente de si el mbox global se activa como parte de at.js o se incluye manualmente en el código de página.

>[!NOTE]
>
>Si desea agregar parámetros a todos los mboxes de la página, no solo al mbox global, utilice la función [targetPageParamsAll()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md).

Puede pasar parámetros a `target-global-mbox` mediante la función `targetPageParams()` de cualquiera de estas formas:

* Una matriz
* Un objeto JSON
* Una lista delimitada por Y comerciales

Use estos tres métodos para verificar que los parámetros se estén pasando correctamente. También podría verificar el paso de parámetros con [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html).

Debe definir la función de JavaScript antes de añadir el mbox global a la página. El nombre debe ser `targetPageParams`.

## Cadena de consulta

```
p1=v1&p2=v2&p3=hello%20world
```

* Nombre: `targetPageParams`
* Valor devuelto: parámetros delimitados por “&amp;”, con valores de parámetro codificados con la dirección URL.

  Ejemplo:

  En este ejemplo, p3 tiene el valor `hello world`, que está codificado con la dirección URL.

Veamos el siguiente código de página de ejemplo:

```html {line-numbers="true"}
<html> 
  <head> 
    <title>Title here..</title> 
    <script type="text/javascript"> 
        function targetPageParams() { 
          return "p1=v1&p2=v2&p3=hello%20world";
        } 
    </script> 
    <script src="mbox.js" type="text/javascript"></script> 
  </head> 
  <body>Body here... 
  </body> 
</html>
```

Este ejemplo envía los siguientes datos al edge de mbox:

* p1=v1
* p2=v2
* p3=hello world

## Matriz

```javascript {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return ["a=1", "b=2", "c=hello world"]; 
}; 
```

Los valores no necesitan tener codificación de dirección URL. Por ejemplo, si un valor contiene un espacio, no es necesario codificar el espacio.

Este ejemplo envía los siguientes datos al edge de mbox:

* a=1
* b=2
* c=hello world

## JSON

JSON es una manera eficaz de pasar parámetros. [!DNL Target] utiliza las claves de objeto JSON para acoplar estructuras complejas en parámetros simples.

```json {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
                  "memberStatus": Gold, 
                  "country": { 
                                "city": "San Francisco" 
                            } 
              } 
  }; 
}; 
```

Los valores no necesitan tener codificación de dirección URL. Por ejemplo, “San Francisco” no requiere que se codifique el espacio. Un espacio es suficiente.

Este ejemplo envía los siguientes datos al edge de mbox:

* a=1
* b=2
* `profile.memberStatus`=Oro
* `profile.country.city`=San Francisco
