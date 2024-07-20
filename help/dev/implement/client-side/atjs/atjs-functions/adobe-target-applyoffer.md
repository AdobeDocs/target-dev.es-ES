---
keywords: adobe.target.applyOffer, applyOffer, applyoffer, aplicar oferta, at.js, funciones, función, $8
description: Utilice la función [!UICONTROL adobe.target.applyOffer()] para la biblioteca JavaScript  [!DNL Adobe Target] at.js para aplicar el contenido de respuesta.
title: ¿Cómo se utiliza la función [!UICONTROL adobe.target.applyOffer()]?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 69%

---

# [!UICONTROL adobe.target.applyOffer(options)]

Esta función es para aplicar el contenido de respuesta con [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer` requiere el parámetro `mbox`. Si no se especifica un nombre de mbox, se produce un error.

El parámetro de opciones es obligatorio y tiene la siguiente estructura:

| Clave | Tipo | Requerido | Descripción |
|--- |--- |--- |--- |
| mbox | Cadena | Sí | El nombre de mbox<br />con at.js 1.3.0 (y versiones posteriores) Target exige que se use la clave mbox. Esta clave se ha requerido en el pasado, pero Target impone ahora su uso para garantizar que Target tenga la validación adecuada y los clientes usen la función correctamente. |
| selector | Cadena o elemento DOM | No | Elemento HTML o selector de CSS utilizado para identificar el elemento HTML donde Target debería colocar el contenido de la oferta. Si no se proporciona un selector, Target supone que el elemento HTML debe utilizar un HEAD HTML. |
| Oferta | Matriz | Sí | Las acciones de una matriz que deben aplicarse al elemento. |

## Ejemplo

El siguiente ejemplo muestra el uso de `[!UICONTROL getOffer]` y `[!UICONTROL applyOffer]` juntos:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "mbox",   
  "success": function(offers) {           
        adobe.target.applyOffer( {  
           "mbox": "mbox", 
           "offer": offers  
        } ); 
  },   
  "error": function(status, error) {           
      if (console && console.log) { 
        console.log(status); 
        console.log(error); 
      } 
  }, 
 "timeout": 5000 
}); 
```
