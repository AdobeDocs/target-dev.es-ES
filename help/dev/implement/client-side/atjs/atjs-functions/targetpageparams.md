---
keywords: targetPageParams, targetpageparams, pageParams, pageparams, parámetros de página, at.js, funciones, función, targetPageParams0
description: Utilice la función [!UICONTROL targetPageParams()] para que la biblioteca JavaScript  [!DNL Adobe Target] at.js adjunte parámetros al mbox global desde fuera del código de solicitud.
title: ¿Cómo utilizo la función [!UICONTROL targetPageParams()]?
feature: at.js
exl-id: 274e4d1f-843a-443b-ad98-7139dc4a13f8
TQID: https://experienceleague.adobe.com/xaSxd1biZ8G-LmgYN4YW9BZ2lDyjZyPHOOlfnbXC2jU
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 66%

---

# [!UICONTROL targetPageParams()]

Este método permite adjuntar parámetros al mbox global desde fuera del código de la solicitud.

Esta función resulta muy útil para incluir el mismo conjunto de parámetros en varias llamadas de mbox. El cliente debe definir la función. Debería devolver una matriz de parámetros que se pasarán solamente a la solicitud de mbox global. Esta función puede definirse antes de que se cargue at.js o en **[!UICONTROL Administración]** > **[!UICONTROL Implementación]** > **[!UICONTROL Editar]** > **[!UICONTROL Encabezado de biblioteca]**.

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


