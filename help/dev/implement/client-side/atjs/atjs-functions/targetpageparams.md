---
keywords: targetPageParams, targetpageparams, pageParams, pageparams, parámetros de página, at.js, funciones, función, targetPageParams0
description: Utilice la función [!UICONTROL targetPageParams()] de la biblioteca JavaScript  [!DNL Adobe Target] at.js para adjuntar parámetros al mbox global desde fuera del código de la solicitud.
title: ¿Cómo se utiliza la función [!UICONTROL targetPageParams()]?
feature: at.js
exl-id: 274e4d1f-843a-443b-ad98-7139dc4a13f8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 68%

---

# [!UICONTROL targetPageParams()]

Este método permite adjuntar parámetros al mbox global desde fuera del código de la solicitud.

Esta función resulta muy útil para incluir el mismo conjunto de parámetros en varias llamadas de mbox. El cliente debe definir la función. Debería devolver una matriz de parámetros que se pasarán solamente a la solicitud de mbox global. Esta función se puede definir antes de que se cargue at.js o en **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** > **[!UICONTROL Library Header]**.

Puede pasar parámetros a target-global-mbox mediante la función `[!UICONTROL targetPageParams()]` de cualquiera de estas formas:

* Una lista delimitada por Y comerciales
* Una matriz
* Un objeto JSON

## Ejemplos

Una lista delimitada por Y comerciales (los valores deben tener codificación de dirección URL):

```javascript {line-numbers="true"}
function targetPageParams() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Matriz (los valores no necesitan tener codificación de dirección URL):

```javascript {line-numbers="true"}
targetPageParams = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (los valores no necesitan tener codificación de dirección URL):

```javascript {line-numbers="true"}
targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
        "age": 26, 
        "country": { 
          "city": "San Francisco" 
        } 
      } 
  }; 
};
```
