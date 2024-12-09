---
keywords: adobe.target.triggerView, triggerView, triggerview, vista de déclencheur, at.js, funciones, función, viewName, viewname, nombre de vista, adobe.target.triggerView1
description: Utilice la función adobe.target.triggerView() para la biblioteca JavaScript SPA  [!DNL Adobe Target] at.js para su uso en aplicaciones de una sola página (). (at.js 2.x)
title: ¿Cómo utilizo la función adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: fe4e607173c760f782035a10f52936d96e9db300
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 21%

---

# adobe.target.triggerView (viewName, options): at.js 2.x

Se puede llamar a esta función cada vez que se carga una página nueva o cuando se vuelve a procesar un componente de una página. SPA `adobe.target.triggerView()` debe implementarse para aplicaciones de una sola página () a fin de usar el [!UICONTROL Visual Experience Composer] (VEC) para crear actividades [!UICONTROL A/B Test] y [!UICONTROL Experience Targeting] (XT). SPA Si `[!UICONTROL adobe.target.triggerView()]` no está implementado en el sitio, el VEC no se puede usar para la creación de informes de VEC (VECoVECoVECoVECoVECoVECo. Para obtener más información, consulte [Implementación de aplicación de una sola página](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Esta función se introdujo en at.js 2.*x*. Esta función no está disponible para la versión 1 de at.js.*x*.

| Parámetro | Tipo | ¿Requerido? | Descripción |
| --- | --- | --- | --- |
| Nombre de vista | Cadena | Sí | Pase cualquier nombre como tipo de cadena que desee que represente la vista. Este nombre de vista aparece en el panel [!UICONTROL Modifications] del VEC para que los especialistas en marketing creen acciones y ejecuten sus actividades [!UICONTROL A/B Test] y [!UICONTROL Experience Targeting] XT. |
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

## Ejemplo: Compatibilidad óptima para `triggerView()` con [!UICONTROL Adobe Visual Editing Helper extension]

Tenga en cuenta lo siguiente al usar la extensión [Ayuda de edición visual de Adobe](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}:

Debido a las nuevas directivas de manifiesto V3 de [!DNL Googl]e para las extensiones [!DNL Chrome], [!UICONTROL Visual Editing Helper extension] debe esperar el evento `DOMContentLoaded` antes de cargar las bibliotecas [!DNL Target] en el VEC. Este retraso podría hacer que las páginas web activen la llamada a `triggerView()` antes de que las bibliotecas de creación estén listas, lo que ocasionaría que la vista no se rellene al cargar.

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


