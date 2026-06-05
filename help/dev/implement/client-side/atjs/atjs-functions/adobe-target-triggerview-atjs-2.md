---
keywords: adobe.target.triggerView, triggerView, triggerview, vista de déclencheur, at.js, funciones, función, viewName, viewname, nombre de vista, adobe.target.triggerView1
description: Utilice la función adobe.target.triggerView() para la biblioteca JavaScript  [!DNL Adobe Target] at.js para su uso en aplicaciones de una sola página (SPA). (at.js 2.x)
title: ¿Cómo utilizo la función adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
TQID: https://experienceleague.adobe.com/pBC1GRKG0mxeaZ1hfaByKv2tu-XScrSJfm7lUw-3yKw
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 19%

---

# adobe.target.triggerView (viewName, options): at.js 2.x

Se puede llamar a esta función cada vez que se carga una página nueva o cuando se vuelve a procesar un componente de una página. `adobe.target.triggerView()` debe implementarse para aplicaciones de una sola página (SPA) a fin de usar el [!UICONTROL Compositor de experiencias visuales] (VEC) para crear actividades de [!UICONTROL Prueba A/B] y [!UICONTROL Segmentación de experiencias] (XT). Si `[!UICONTROL adobe.target.triggerView()]` no está implementado en el sitio, el VEC no se puede usar para SPA. Para obtener más información, consulte [Implementación de aplicación de una sola página](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Esta función se introdujo en at.js 2.*x*. Esta función no está disponible para la versión 1.*x* de at.js.

| Parámetro | Tipo | ¿Requerido? | Descripción |
| --- | --- | --- | --- |
| Nombre de vista | Cadena | Sí | Pase cualquier nombre como tipo de cadena que desee que represente la vista. Este nombre de vista aparece en el panel [!UICONTROL Modificaciones] del VEC para que los especialistas en marketing creen acciones y ejecuten sus actividades [!UICONTROL Prueba A/B] y [!UICONTROL Segmentación de experiencias] XT. |
| opciones | Objeto | No |  |
| opciones > página | Booleano | No | **VERDADERO:** el valor predeterminado de la página es verdadero. Cuando la página es “page=true”, las notificaciones se envían al back-end [!DNL Target] para incrementar el recuento de impresiones.<P>Siempre se envía una notificación de forma predeterminada cuando se llama a `[!UICONTROL triggerView]`, excepto cuando options > page se establece en false.<P>**FALSO:** Cuando la página es page=false, las notificaciones no se envían para incrementar el recuento de impresiones. Este método debe utilizarse cuando desee volver a procesar un componente en una página con una oferta.<P>**Nota**: las ofertas de código personalizado del VEC no se vuelven a procesar cuando se llama a `[!UICONTROL triggerView()]` con `{page: false}` como opción. |

## Ejemplo: True

Llamada de `[!UICONTROL triggerView()]` para enviar una notificación al back-end de [!DNL Target] para incrementar las impresiones de actividad y otras métricas.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Ejemplo: False

Llamada de `[!UICONTROL triggerView()]` para no tener notificaciones enviadas al backend de [!DNL Target] para el recuento de impresiones.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Ejemplo: Promesa encadenada con `getoffers()` y `applyOffers()`

Para ejecutar `triggerView()` cuando se resuelva la promesa `getOffers()`, es importante ejecutar `triggerView()` en el bloque final, como se muestra en el ejemplo siguiente. Esto es necesario para que el VEC detecte `Views` en el modo de creación.

```javascript {line-numbers="true"}
adobe.target.getOffers({
    'request': {
        'prefetch': {
            'views': [{
                'parameters': {}
            }]
        }
    }
}).then(function(response) {
    // Apply Offers
    adobe.target.applyOffers({
        response: response
    });
}).catch(function(error) {
    console.log("AT: getOffers failed - Error", error);
}).finally(() => {
    // Trigger View call, assuming pageView is defined elsewhere
    adobe.target.triggerView(pageView, {
        page: true
    });
    console.log('AT: View triggered on : ' + pageView);
});
```

## Ejemplo: compatibilidad óptima para `triggerView()` con la extensión [!UICONTROL Ayuda de edición visual de Adobe]

Tenga en cuenta lo siguiente al usar la extensión [Ayuda de edición visual de Adobe](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}:

Debido a las nuevas directivas de Manifiesto V3 de [!DNL Googl]e para las extensiones [!DNL Chrome], la extensión [!UICONTROL Ayuda de edición visual] debe esperar el evento `DOMContentLoaded` antes de cargar las bibliotecas [!DNL Target] en el VEC. Este retraso podría hacer que las páginas web activen la llamada a `triggerView()` antes de que las bibliotecas de creación estén listas, lo que ocasionaría que la vista no se rellene al cargar.

Para mitigar este problema, use un agente de escucha para el evento de página `load`.

Esta es una implementación de ejemplo:

```javascript
function triggerViewIfLoaded() {
    adobe.target.triggerView("homeView");
}

if (document.readyState === "complete") {
    // If the page is already loaded
    triggerViewIfLoaded();
} else {
    // If the page is not yet loaded, set up an event listener
    window.addEventListener("load", triggerViewIfLoaded);
}
```


