---
keywords: targetPageParamsAll, targetpageparamsall, PageParamsAll, pageparamsall, parámetros de página, at.js, funciones, función, targetPageParamsAll0
description: Utilice el [!UICONTROL targetPageParamsAll()] para la función [!DNL Adobe Target] Biblioteca JavaScript de at.js para adjuntar parámetros a todos los mboxes desde fuera del código de la solicitud.
title: ¿Cómo utilizo el [!UICONTROL targetPageParamsAll()] ¿Función?
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 55%

---

# [!UICONTROL targetPageParamsAll()]

Este método permite adjuntar parámetros a todos los mboxes desde fuera del código de la solicitud.

Resulta muy útil para incluir el mismo conjunto de parámetros en varias llamadas de mbox. El cliente debe definir la función. Debería devolver una matriz de parámetros que se pasarán a todas las solicitudes de mbox de la página. Esta función puede definirse antes de que at.js se cargue o en **[!UICONTROL Administration]** > **[!UICONTROL Implementación]** > **[!UICONTROL Editar]** > **[!UICONTROL Configuración de código]** > **[!UICONTROL Encabezado de biblioteca]**.

Puede pasar parámetros a target-global-mbox mediante el complemento [!UICONTROL targetPageParamsAll()] funciona de cualquiera de las siguientes maneras:

* Una lista delimitada por Y comerciales
* Una matriz
* Un objeto JSON

## Ejemplos

Una lista delimitada por Y comerciales (los valores deben tener codificación de dirección URL):

```javascript {line-numbers="true"}
function targetPageParamsAll() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Matriz (los valores no necesitan tener codificación de dirección URL):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (los valores no necesitan tener codificación de dirección URL):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
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
