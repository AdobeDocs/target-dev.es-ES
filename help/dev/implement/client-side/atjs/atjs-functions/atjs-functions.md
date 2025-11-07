---
keywords: at.js, funciones, biblioteca javascript
description: Vea una lista de funciones que se pueden usar con las versiones 1.x y 2.x de la biblioteca JavaScript at.js en  [!DNL Adobe Target].
title: ¿Qué funciones puedo utilizar con at.js?
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 58%

---

# Funciones de at.js

Lista de funciones que se pueden usar con la biblioteca JavaScript at.js [!DNL Adobe Target]. Para obtener más información y ejemplos, haga clic en los vínculos de la columna Función.

| Función | Detalles |
| --- | --- |
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | Esta función activa una solicitud para obtener una oferta [!DNL Target]. Use con `adobe.target.applyOffer()` para procesar la respuesta o use su propia administración de éxito. |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x) | Esta función le permite recuperar varias ofertas pasando varios mboxes. Además, se pueden recuperar varias ofertas para todas las vistas de actividades activas.<P>**Nota:** Esta función se introdujo en at.js 2.x. Esta función no está disponible para la versión 1 de at.js.*x*. |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | Esta función es para aplicar el contenido de respuesta. |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x) | Esta función permite aplicar más de una oferta recuperada por [!UICONTROL adobe.target.getOffers()].<P>**Nota:** Esta función se introdujo en at.js 2.x. Esta función no está disponible para la versión 1 de at.js.*x*. |
| [[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x) | Se puede llamar a esta función cada vez que se carga una página nueva o cuando se vuelve a procesar un componente de una página.<P> Esta función debe implementarse para aplicaciones de una sola página (SPA) a fin de usar el [!UICONTROL Visual Experience Composer] (VEC) para crear actividades [!UICONTROL A/B Test] y [!UICONTROL Experience Targeting] (XT). |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | Esta función activa una solicitud para informar sobre las acciones de los usuarios, como clics y conversiones. No proporciona ninguna actividad en la respuesta. |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x) | Ejecuta una solicitud y aplica la oferta al DIV más cercano con nombre de clase mboxDefault.<P>**Nota:** Esta función está disponible para las versiones 1 de at.js.Solamente *x*. Esta función quedó obsoleta con el lanzamiento de at.js 2.x. Esta función devuelve el contenido predeterminado si se utiliza con at.js 2.x. |
| [[!UICONTROL mboxDefine(options)] y [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x) | Defina y actualice un mbox.<P>**Nota:** Esta función está disponible para las versiones 1 de at.js.Solamente *x*. Esta función quedó obsoleta con el lanzamiento de at.js 2.x. Esta función devuelve el contenido predeterminado si se utiliza con at.js 2.x. |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | Puede anular la configuración de la biblioteca at.js mediante `[!UICONTROL targetGlobalSettings()]`, en lugar de hacerlo en la interfaz de usuario de [!DNL Target Standard/Premium], o mediante las API de REST.<ul><li>Proveedores de datos: Esta configuración permite a los clientes recopilar información de proveedores de datos de terceros, como Demandbase, BlueKai y servicios personalizados, así como pasar la información a Target como parámetros mbox y la solicitud mbox global.</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | Este método permite adjuntar parámetros al mbox global desde fuera del código de la solicitud. |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | Este método permite adjuntar parámetros a todos los mboxes desde fuera del código de la solicitud. |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x) | Ofrece una forma estándar de registrar una extensión determinada.<P>**Nota:** Esta función está disponible para las versiones 1 de at.js.Solamente *x*. Esta función quedó obsoleta con el lanzamiento de at.js 2.x. Esta función devuelve el contenido predeterminado si se utiliza con at.js 2.x. |
| [[!UICONTROL at.js custom events]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | Los eventos personalizados de at.js le permiten saber cuándo una solicitud o una oferta de mbox tiene éxito o falla. |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0) | Esta función envía una notificación a [!DNL Target] edge cuando se procesa una experiencia sin usar `[!UICONTROL adobe.target.applyOffer()]` o `[!UICONTROL adobe.target.applyOffers()]`.<P>**Nota**: Esta función se ha introducido en at.js 2.1.0 y estará disponible para todas las versiones superiores a 2.1.0. |
