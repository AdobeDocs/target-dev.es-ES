---
keywords: Versiones de at.js, versiones de at.js, notas de la versión
description: Vea los detalles sobre los cambios realizados en cada versión de la biblioteca JavaScript  [!DNL Adobe Target] at.js.
title: ¿Qué se incluye en cada versión de at.js?
feature: at.js
exl-id: 609dacba-2ab8-45e9-b189-928d59938c98
source-git-commit: aa6f6593a6979666101d8754dde3e02fb6a21e33
workflow-type: tm+mt
source-wordcount: '5018'
ht-degree: 64%

---

# Detalles de las versiones de at.js

Detalles sobre los cambios realizados en cada versión de la biblioteca JavaScript de at.js. [!DNL Adobe Target].

>[!IMPORTANT]
>
>[!DNL Adobe Target] admite at.js 1.*x* y at.js 2.*x*.
>
>at.js 1.*x* ha entrado en modo de mantenimiento. El equipo [!DNL Target] publica correcciones de errores y parches de seguridad cuando es necesario.
>
>El equipo [!DNL Target] proporciona soporte completo para at.js 2.*x* y publica correcciones de errores, parches de seguridad, funciones y optimización del rendimiento de forma continua.
>
>Debe actualizar a las versiones más recientes de cualquiera de las dos 1.*x* o 2.*x* para obtener correcciones de errores y parches de seguridad para problemas detectados en cualquier versión menor anterior de la versión principal correspondiente.

Las etiquetas de [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) son el método preferido para actualizar at.js. Los desarrolladores de extensiones añaden continuamente nuevas funciones a sus extensiones y suelen corregir errores. Estas actualizaciones se incluyen en las versiones nuevas de una extensión y se pueden descargar en el catálogo de Adobe Experience Platform como actualizaciones. Para obtener más información, consulte [Actualizaciones de extensiones](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/extensions/extension-upgrade.html) en la guía de *Información general sobre etiquetas*.

## Versión 2.11.8 de at.js (31 de marzo de 2025)

* Se ha resuelto una vulnerabilidad identificada por CodeQL en la validación de sufijos de cadena para evitar casos extremos durante las operaciones de cambio de tamaño y movimiento. (TNT-51516)

## Versión 2.11.7 de at.js (26 de febrero de 2025)

* Se corrigió el registro de telemetría cuando `localStorage` no está disponible. La telemetría estaba ocasionando un problema a algunos clientes que tenían `localStorage` deshabilitado en sus navegadores.

## Versión 2.11.6 de at.js (lunes, 29 de septiembre de 2024)

* Se ha corregido un problema que impedía que [!DNL Target] funcionara correctamente con ofertas de redireccionamiento dentro de [!UICONTROL Visual Experience Composer] (VEC) o [!UICONTROL Form-Based Experience Composer].

## Versión 2.11.5 de at.js (jueves, 14 de agosto de 2024)

* Se ha implementado el almacenamiento en caché para las operaciones de lectura y escritura de cookies a fin de reducir la sobrecarga de análisis y manipulación de cadenas costosas y repetidas.
* Se ha implementado la API más reciente de parámetros de búsqueda de URL cuando está disponible, ya que es más rápido que analizar y manipular cadenas manualmente.

## Versión 2.11.4 de at.js (jueves, 24 de enero de 2024)

* Se ha actualizado at.js para evitar que se envíen datos geográficos no válidos a la API de entrega.

## Versión 2.11.3 de at.js (miércoles, 21 de noviembre de 2023)

* Se ha corregido un problema que impedía que se enviaran tokens de respuesta en `at-content-rendering-failed` eventos.

## Versión 2.11.2 de at.js (viernes, 26 de octubre de 2023)

* Se ha corregido un problema que provocaba incoherencias en los tokens de respuesta enviados en eventos personalizados.

## Versión 2.11.1 de at.js (sábado, 13 de octubre de 2023)

* Se ha corregido un problema que provocaba errores no capturados mientras una página que ejecutaba at.js estaba en modo quirks.

## Versión 2.11.0 de at.js (miércoles, 10 de octubre de 2023)

* Se agregó compatibilidad para establecer [!DNL Adobe Experience Platform] (AEP) `sandboxId` y `sandboxName` personalizados en `targetGlobalSettings`, que se pasa a la API de entrega en `getOffer/getOffers` llamadas.
* Corrección DOM de sombreado para encadenar `:eq()` en selectores.

## Versión 2.10.3 de at.js (miércoles, 12 de septiembre de 2023)

* Se ha corregido un problema que activaba incorrectamente el evento personalizado `at-content-rendering-succeeded` cuando no se representaba ninguna oferta. El evento correcto, `at-content-rendering-no-offers`, se ha activado.
* Se agregaron `eventToken` y `responseTokens` al objeto de error para el evento personalizado `at-content-rendering-failed`.

## Versión 2.10.2 de at.js (7 de marzo de 2023)

* Se ha corregido un problema que provocaba que la función `trackEvent` devolviera siempre un error.

## Versión 2.10.1 de at.js (2 de febrero de 2023)

* Se ha corregido un error por el que las actividades que implicaban reglas de audiencia que contenían parámetros con puntos en sus nombres no devolvían la experiencia esperada, para la toma de decisiones en el dispositivo.
* Se ha corregido un error introducido en at.js 2.6.0 en el que at.js activaba una llamada de entrega, incluso cuando mboxDisable estaba habilitado.

## Versión 2.10.0 de at.js (martes, 19 de septiembre de 2022)

* Se ha agregado compatibilidad con cookies de terceros.

## Versión 2.9.0 de at.js (27 de mayo de 2022)

* Se ha añadido la compatibilidad con [User Agent Client Hints](user-agent-and-client-hints.md).
* Se ha corregido un error por el cual varias solicitudes de mbox en la misma página tenían ID de impresión diferentes.

## Versión 2.8.1 de at.js (28 de enero de 2022)

* Se ha corregido que `pageLoad` no se asignara a target-global-mbox en el modo de ejecución híbrido de On Device Decisioning (ODD).
* Se ha corregido un problema con los detalles de análisis para la solicitud de mbox.
* Se han actualizado las dependencias de desarrollo para corregir las vulnerabilidades de seguridad.

## Versión 2.8.0 de at.js (7 de enero de 2022)

La biblioteca JavaScript de at.js de [!DNL Target] ahora recopila datos de uso de funcionalidades y telemetría de rendimiento. Los datos personales no se recopilan. La exclusión de esta funcionalidad está disponible al configurar `telemetryEnabled` en falso en `targetGlobalSettings`. Para obtener más información, consulte [telemetryEnabled en targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).

## Versión 2.7.0 de at.js (28 de octubre de 2021)

Esta versión incluye la siguiente mejora:

* Se ha añadido compatibilidad con [Web Components](https://developer.mozilla.org/es/docs/Web/Web_Components). Esta versión de at.js es necesaria para crear y probar experiencias y ofertas personalizadas en elementos personalizados y en elementos dentro de elementos personalizados. Esta funcionalidad se incluye en la versión de [!DNL Target Standard/Premium] 21.10.5.

## at.js 1.8.3 (21 de septiembre de 2021)

Esta versión incluye los siguientes cambios:

* Se eliminaron los módulos Adobe Experience Platform Launch `reactor-window` y `reactor-document` para garantizar que la versión de Platform Launch funcione correctamente para los clientes que tienen establecidos `window.default` o `document-default`.
* at.js 1.8.3 ahora establece explícitamente `Samesite=None` y `Secure` para garantizar que las cookies de dominio de terceros se establezcan correctamente.

## at.js 2.6.1 (16 de agosto de 2021)

* Corrección de errores para el mensaje “No hay artefactos en caché disponibles para el modo híbrido” al utilizar la toma de decisiones en el dispositivo.

## at.js 2.6.0 (16 de julio de 2021)

* Se ha agregado un atributo seguro a las cookies cada vez que la configuración `secureOnly` de at.js se establece en `true`.
* Los tokens de respuesta ya están disponibles al utilizar `triggerView()`.
* Se ha corregido un problema relacionado con el evento `CONTENT_RENDERING_NO_OFFERS`. Ahora este evento se activa correctamente siempre que no haya contenido devuelto de [!DNL Target].
* [!UICONTROL Analytics for Target] (A4T) Los detalles de las métricas de clic se devuelven correctamente al usar solicitudes `prefetch`.
* La generación UUID ya no utiliza `Math.random()`, sino que depende de `window.crypto`.
* La caducidad de la cookie `sessionId` se amplía correctamente en cada llamada de red.
* La inicialización de la caché de la vista Aplicación de una sola página (SPA) ahora se administra correctamente y respeta la configuración de `viewsEnabled`. Al establecer `viewsEnabled` en el valor `false`, ahora se deshabilita la función `triggerView()`. Consulte [Orden de las operaciones para la carga inicial de la página](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md#order).

## at.js 2.5.0 (13 de mayo de 2021)

Esta versión de at.js incluye las siguientes mejoras y cambios:

* [Compatibilidad de decisiones en el dispositivo](/help/dev/implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md) para at.js.
* [Vista previa de vínculos](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) Compatibilidad con actividades de Automated Personalization

Esta versión también elimina la compatibilidad con Microsoft Internet Explorer 10 y versiones posteriores.

## at.js 2.4.1 (23 de marzo de 2021)

Esta versión de at.js es de mantenimiento e incluye las siguientes mejoras y correcciones:

* Se ha corregido un problema por el que `targetPageParams` se incluía en las solicitudes de mbox. `targetPageParams` solo debe incluirse en las solicitudes de `pageLoad`. (TNT-40247)
* Ventana optimizada y referencias globales de documento en la extensión de Adobe Experience Platform. (TNT-37124)

## at.js 2.4.0 (14 de enero de 2021)

Esta versión de at.js es de mantenimiento e incluye las siguientes correcciones:

* Añade compatibilidad con el perfil unificado/ID de plataforma a customerIds de la API de entrega.
* Corrige la inyección de etiquetas de estilo no válida.

## at.js 2.3.3 (13 de noviembre de 2020)

Esta versión de at.js es de mantenimiento e incluye las siguientes correcciones:

* Se ha corregido un problema relacionado con el rastreo de clics de mbox y A4T. Con 0n-click, [!DNL Target] activó una llamada a la API de entrega con los parámetros de mbox y mbox correctos. Sin embargo, el SDID no coincidió con el de la llamada a [!DNL Analytics], por lo que no hubo vinculación de visitas ni conversión. (TNT-38372)

## at.js 2.3.2 (24 de julio de 2020)

Esta versión de at.js es de mantenimiento e incluye las siguientes correcciones:

* Se ha corregido un error cuando un script o código añade la propiedad predeterminada a la ventana o al documento.

## at.js 1.8.2 (15 de junio de 2020)

Esta versión de at.js es de mantenimiento e incluye las siguientes correcciones:

* Se ha corregido un problema que se producía al usar CNAME y la anulación de perímetros, at.js 1.*x* podría crear incorrectamente el dominio del servidor, lo que provocaba que la solicitud de [!DNL Target] diera error. (TNT-35064)

## Versiones de at.js 2.3.1 (15 de junio de 2020)

Esta versión de at.js es de mantenimiento e incluye las siguientes mejoras y correcciones:

* Se ha hecho que la configuración `deviceIdLifetime` sea reemplazable mediante [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md). (TNT-36349)
* Se ha corregido un problema que se producía al usar CNAME y la anulación de perímetros, at.js 2.*x* podría crear incorrectamente el dominio del servidor, lo que provocaba que la solicitud de [!DNL Target] diera error. (TNT-35065)
* Se corrigió un problema que se producía al usar la extensión [!DNL Target] v2 y la extensión [!UICONTROL Adobe Analytics Launch], [!DNL Target] retrasó la llamada [!DNL Analytics] `sendBeacon`. (TNT-36407, TNT-35990, TNT-36000)

## Versión 2.3.0 de at.js (jueves, 25 de marzo de 2020)

Esta versión de at.js es de mantenimiento e incluye las siguientes mejoras y correcciones:

* Compatibilidad con la configuración de nonces de Política de seguridad de contenido en etiquetas SCRIPT y STYLE anexadas al DOM de página al aplicar ofertas [!DNL Target] entregadas. Los clientes pueden establecer `targetGlobalSettings.cspScriptNonce` y `targetGlobalSettings.cspStyleNonce` para que at.js pueda establecer las nonces de etiqueta de estilo y script correspondientes en las ofertas aplicadas. Consulte [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) para obtener más información.
* Se ha corregido un problema que se producía al compilar at.js con el compilador de cierre de Google para la implementación de Google Tag Manager.
* Se cambió el nombre de la cookie de comprobación at.js de `check` a `at_check` para evitar conflictos con las implementaciones de los clientes.

## Versión 1.8.1 de at.js (jueves, 25 de marzo de 2020)

Esta versión de at.js es de mantenimiento e incluye las siguientes mejoras y correcciones:

* Se cambió el nombre de la cookie de comprobación at.js de `check` a `at_check` para evitar conflictos con las implementaciones de los clientes.

## Versión 2.2.0 de at.js (viernes, 10 de octubre de 2019)

Esta versión de at.js incluye las siguientes mejoras y correcciones:

* Se corrigió un problema en el cual el rastreo de clics no informaba de las conversiones en [!DNL Analytics for Target] (A4T) cuando el código [!DNL Adobe Analytics] no estaba presente en los elementos de la página.
* Rendimiento mejorado al usar el servicio Experience Cloud ID (ECID) 4.4 y at.js 2.2 en sus páginas web.
* Anteriormente, el ECID realizaba dos llamadas de bloqueo antes de que at.js pudiera recuperar experiencias. Esto se ha reducido a una sola llamada, lo que mejora significativamente el rendimiento.
* Se ha corregido un procesamiento de vista previa incorrecto, en el que los tokens de evento de ofertas predeterminadas no se incluían en las notificaciones enviadas.

>[!NOTE]
>
>Actualice la extensión de ECID a la versión 4.4 para aprovechar esta mejora de rendimiento.

* La versión 2.2 de at.js también proporciona una nueva configuración denominada `serverState`. Esta configuración se puede usar para optimizar el rendimiento de la página cuando se implementa una integración híbrida de [!DNL Target]. La integración híbrida significa que está utilizando at.js v2.2 o posterior del lado del cliente y la API de entrega o un SDK [!DNL Target] del lado del servidor para ofrecer experiencias. `serverState` permite a at.js v2.2 o posterior aplicar experiencias directamente desde el contenido recuperado en el servidor y devuelto al cliente como parte de la página que se está sirviendo. Para obtener más información, consulte &quot;serverState&quot; en [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverstate).

## Versión 1.8.0 de at.js (viernes, 10 de octubre de 2019)

Esta versión de at.js incluye las siguientes mejoras y correcciones:

* Rendimiento mejorado al usar el servicio Experience Cloud ID (ECID) 4.4 y at.js 1.8 en sus páginas web.
* Anteriormente, el ECID realizaba dos llamadas de bloqueo antes de que at.js pudiera recuperar experiencias. Esto se ha reducido a una sola llamada, lo que mejora significativamente el rendimiento.

>[!NOTE]
>
>Actualice la extensión de ECID a la versión 4.4 para aprovechar esta mejora de rendimiento.

## Versión 2.1.1 de at.js (24 de julio de 2019)

Esta versión de at.js es de mantenimiento e incluye las siguientes mejoras y correcciones:

(Los números entre paréntesis son para uso interno de Adobe).

* Se ha corregido un problema que hacía que se activaran varios avisos al utilizar la métrica Rastreo de clics en la página Objetivos y configuración del Compositor de experiencias visuales (VEC). (TNT-32812)
* Se ha corregido un problema que causaba que `triggerView()` no procesara ofertas más de una vez. (TNT-32780)
* Se ha corregido un problema con `triggerView()` al garantizar que la solicitud contenga información de Experience Cloud ID (ECID). (TNT-32776)
* Se ha corregido un problema que impedía que se activara la notificación `triggerView()` aunque no hubiera vistas guardadas. (TNT-32614)
* Se ha corregido un problema que provocaba un error debido al uso de decodeURIcomponent, que causaba problemas cuando la dirección URL contenía un parámetro de cadena de consulta incorrecto. (TNT-32710)
* El indicador de señalización ahora se establece como “true” en el contexto de las solicitudes de envío enviadas mediante la API `Navigator.sendBeacon()`. (TNT-32683)
* Se ha corregido un problema que impedía que las ofertas de recomendaciones se mostraran en sitios web para algunos clientes. Los clientes podían ver el contenido de la oferta en la llamada de API de entrega, pero la oferta no se aplicaba al sitio web. (TNT-32680)
* Se ha corregido un problema que provocaba que el rastreo de clics en varias experiencias no funcionara según lo esperado. (TNT-32644)
* Se ha corregido un problema que impedía que at.js aplicara la segunda métrica después de que fallara la representación de la primera. (TNT-32628)
* Se ha corregido un problema al pasar `mbox3rdPartyId` con la función `targetPageParams` que provocaba que la carga útil de la solicitud no estuviera presente en los parámetros de consulta ni en la carga útil de la misma. (TNT-32613)
* Se ha corregido un problema que provocaba que las respuestas de notificación de clics y visualización se bloquearan en exploradores basados en Chromium (incluido Google Chrome). (TNT-32290)

## Versión 2.1.0 de at.js (3 de junio de 2019)

Esta versión incorpora las siguientes funciones y mejoras:

* **Compatibilidad de Adobe Opt-In**: Adobe Opt-in es una forma de simplificar las integraciones de soluciones de Adobe con plataformas de administración de consentimiento. Para obtener más información sobre Adobe Opt-in, consulte [Privacidad y Reglamento General de Protección de Datos (RGPD)](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

* **Compatible con CSP estándar del sector**: at.js ya no utiliza eval() para ejecutar JavaScript.

* **Registro de análisis del lado del cliente**: Proporcione a los clientes control total sobre cómo desean enviar datos de análisis a [!DNL Adobe Analytics], ya sea en el lado del cliente o en el lado del servidor.

  Para obtener más información, consulte [Registro del lado del cliente [!DNL Analytics] 2}.](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html#client-side)

* **Enviar notificaciones**: Permita que los desarrolladores envíen notificaciones cuando su código procese una experiencia en lugar de utilizar `applyOffer()` o `applyOffers()`.

  Para obtener más información, consulte [adobe.target.sendNotifications(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md).

* **El tamaño de at.js disminuyó ~24%**: El tamaño de at.js se reduce en ~24%. El menor tamaño de archivo mejora el rendimiento de carga de página y reduce el tiempo para descargar at.js en la página.

## Versión 2.0.1 de at.js (19 de marzo de 2019)

Esta es una versión de mantenimiento e incluye las siguientes mejoras y correcciones:

(Los números entre paréntesis son para uso interno de Adobe).

* Se ha corregido una condición de carrera en el código de sondeo DOM que provocaba excepciones de JavaScript para ciertos clientes. (TNT-31869)
* Se han desunido las notificaciones que visualizaban los controladores de eventos de rastreo de clics. Inicialmente, [!DNL Target] no enviaba notificaciones si no se podían adjuntar controladores de eventos de clic pertenecientes a una vista representada. [!DNL Target] ahora envía una notificación de vista incluso cuando no se encuentran elementos de clic. (TNT-31969)
* Se ha corregido un problema que provocaba que el indicador de redireccionamiento de eventos de solicitud se defina siempre como verdadero. (TNT-31907)
* Se ha corregido un problema que provocaba que la acción de reorganizar VEC se registrara como éxito, incluso cuando faltaban elementos. (TNT-31924)
* Se ha corregido un problema que causaba que las notificaciones para determinados clientes no contenderan el token de propiedad de permisos de Enterprise. (TNT-31999)

## Versión 1.7.1 de at.js (19 de marzo de 2019)

Esta es una versión de mantenimiento e incluye la siguiente corrección:

(Los números entre paréntesis son para uso interno de Adobe).

* Se ha corregido una condición de carrera en el código de sondeo DOM que provocaba excepciones de JavaScript para ciertos clientes. (TNT-31869)

## Versión 2.0.0 de at.js

at.js 2 proporciona conjuntos de funciones enriquecidos que equipan su empresa para ejecutar personalizaciones en tecnologías de próxima generación del lado del cliente. Esta nueva versión se centra en actualizar at.js para tener interacciones armoniosas con aplicaciones de una sola página (SPA).

Estos son algunos de los beneficios de utilizar at.js 2.x que no están disponibles en versiones anteriores:

* La capacidad de almacenar en caché todas las ofertas al cargar la página para reducir el número de llamadas al servidor a una sola llamada.
* Importante mejora de las experiencias de los usuarios finales en su sitio porque las ofertas se muestran inmediatamente a través de la caché sin ningún tiempo de retraso que introducen las llamadas tradicionales al servidor.
* Código sencillo de una línea y configuración de desarrollador única para permitir que sus especialistas en marketing creen y ejecuten actividades A/B y Experiencia (XT) a través del Compositor de experiencias visuales (VEC) en sus aplicaciones de una sola página.

at.js 2.x presenta las siguientes funciones nuevas:

* getOffers()
* applyOffers()
* triggerView()

Las siguientes funciones han quedado obsoletas con la introducción de at.js 2.x:

* mboxCreate()
* mboxDefine
* registerExtension()

Para obtener más información, consulte [Actualización de at.js 1.x a at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) y [funciones at.js](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).

>[!NOTE]
>
>Si necesita soporte de Adobe Opt-in para el [Reglamento General de Protección de Datos](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) (RGPD), actualmente debe utilizar at.js 1.7.0, o at.js 2.1.0 o posterior.

## Versión 1.7.0 de at.js

at.js 1.7.0 ofrece soporte con Adobe Opt-In. Adobe Opt-In es una forma de simplificar las integraciones de soluciones de Adobe con plataformas de administración de consentimiento.

Para obtener más información sobre Adobe Opt-in, consulte [Privacidad y Reglamento General de Protección de Datos](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) (RGPD).

Esta versión también corrige un problema en el cual [!DNL Target] podría anular los parámetros de URL de redireccionamiento con parámetros procedentes de la dirección URL de redireccionamiento.

>[!NOTE]
>
>Si necesita soporte con Adobe Opt-in para el RGPD, actualmente debe utilizar at.js 1.7.0, at.js 2.1.0 o posterior.

## Versión 1.6.4 de at.js

La versión at.js 1.6.4 es una versión de mantenimiento y aborda el siguiente problema:

* Se ha corregido una condición de carrera que se manifestaba en Microsoft Internet Explorer 11 y que provocaba que se aplicaran ofertas duplicadas.

## Versión 1.6.3 de at.js

La versión 1.6.3 de at.js incluye las siguientes correcciones y mejoras:

* Los selectores eluden el CSS si contienen ID o clases de CSS que comiencen con un dígito, dos guiones o un guion seguido por un dígito (por ejemplo, n.º 123). (TNT-31061)
* Se ha corregido un problema introducido con at.js 1.6.2 en el que las ofertas del Compositor de experiencias visuales (VEC) de diferentes actividades y aplicables al mismo selector de CSS no respetaban la prioridad de la actividad. (TNT-31052)
* Se ha corregido un problema con el tiempo de espera de una promesa en entornos en los que no había compatibilidad nativa con las promesas. (TNT-30974)
* Los problemas se registran y comunican correctamente mediante el evento fallido de representación de contenido. Es posible que anteriormente JavaScript haya informado que se ejecutó correctamente, incluso si no era así. (TNT-30599)

## Versión 1.6.2 de at.js

Esta es una versión de mantenimiento y aborda el siguiente problema:

* Se ha solucionado un problema que en algunos sitios de clientes conducía a un bucle infinito “asíncrono”.

>[!WARNING]
>
>Además, la versión 1.6.2 de at.js también contiene todas las mejoras y correcciones incluidas en las versiones 1.6.1 y 1.6.0 de at.js. Estas versiones ya no están disponibles para descargar. Le recomendamos que actualice a la versión 1.6.2 si usa 1.6.1 o 1.6.0

Estas son las mejoras y correcciones que se incluyeron en la versión 1.6.1 de at.js:

* Se ha solucionado un problema en at.js 1.6.0 que hacía que las experiencias de las recomendaciones se duplicaran en Microsoft Internet Explorer 11. (TNT-30593)
* at.js ahora garantiza que la lógica de anulación de bordes compruebe la existencia de una cookie de clúster de perímetro para evitar un número de perímetro diferente si un usuario salta los perímetros durante una sesión. (TNT-30563)
* Se ha solucionado un problema que impedía que at.js ejecutara acciones posteriores si el contenido HTML contenía un código JS no válido. at.js ahora registra el error y presenta las acciones restantes sin problemas. (TNT-30546)
* Se han realizado cambios para que haya una excepción cuando una página de redirección se vuelve a calificar para una actividad de redireccionamiento. (TNT-30532)
* Se ha solucionado un problema que impedía que el tiempo de espera de solicitud correcto se propagara desde la solicitud de la API getOffer(). (TNT-30498)
* Se ha solucionado un problema que impedía que at.js 1.6.0 guardara cookies al usar el protocolo de archivo. (TNT-30454)
* Se ha corregido un problema que hacía que pareciera que no todas las experiencias se entregaban con redirecciones al usar [!DNL Analytics for Target] (A4T). (TNT-30444)
* Se ha corregido un problema que provocaba que la página se ocultara después de que la llamada a [!DNL Target] se realizara correctamente. (TNT-30358)

Estas son las mejoras y correcciones que se incluyeron en la versión 1.6.0 de at.js:

* Ahora se admiten automáticamente ofertas de redireccionamiento en la integración de [!UICONTROL Analytics for Target] (A4T). Se ha eliminado la solución del lado del cliente. (TNT-30247)
* El enrutamiento de perímetro del lado del cliente ahora está habilitado de forma predeterminada. (TNT-30261)
* Se ha solucionado un problema con la representación de la acción del Compositor de experiencias visuales (VEC) cuando hay dependencias entre las acciones. (TNT-30248)

## Versión 1.5.0 de at.js

Ya está disponible la versión 1.5.0 de at.js.

* Los detalles del evento `at-request-succeeded` contienen el indicador de redirección. Este indicador se puede utilizar para determinar si la página se redirigirá a una URL diferente. Si desea conocer la URL, suscríbase a `at-content-rendering-redirect`. (TNT-29834)
* Se solucionó un problema que provocaba que `window.targetGlobalSettings.enabled` fallara con una excepción de tiempo de ejecución si se establecía en Falso. (TNT-29829)
* Se solucionó un problema que provocaba que la página fallara al cargarse en el Compositor de experiencias visuales (VEC) si se incluía código personalizado en una solicitud mbox global y se utilizaba ocultación de texto. (TNT-29795)
* Se añadió compatibilidad con `screenOrientation`, `devicePixelRatio` y `webGLRenderer`. Estos nuevos parámetros de solicitud [!DNL Target] se usan para iPhone X y otros dispositivos modernos. Para obtener más información, consulte [Móvil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html). (TNT-29781)
* Se solucionó un problema por el cual no siempre se enviaba la sugerencia de ubicación de Adobe Audience Manager (AAM). (TNT-29695)
* En los navegadores compatibles, at.js 1.5.0 cambia a MutationObserver para el sondeo de selectores. Las versiones anteriores a at.js 1.0.0 utilizaban un polyfill MutationObserver que resultó problemático. Para evitar problemas de polyfill, la versión 1.5.0 utiliza el siguiente pseudocódigo a fin de decidir el mecanismo de programación que debe utilizarse:

  ```
  if MutationObserver is supported
    scheduler = MutationObserver
  else if document is visible
    scheduler = requestAnimationFrame
  else
    scheduler = setTimeout
  ```

## Versión 1.3.0 de at.js

Ya está disponible la versión 1.3.0 de at.js.

* Los siguientes eventos nuevos sirven para ayudar a rastrear, depurar y personalizar la interacción con at.js:

   * LIBRARY_LOADED
   * REQUEST_START
   * CONTENT_RENDERING_START
   * CONTENT_RENDERING_NO_OFFERS
   * CONTENT_RENDERING_REDIRECT

  Para obtener más información, consulte [Eventos personalizados de at.js](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md).

* Puede aumentar una solicitud at.js con parámetros adicionales que provengan de los proveedores de datos. Los proveedores de datos deben añadirse a `window.targetGlobalSettings` en `dataProviders key`.

  Para obtener más información, consulte [Proveedores de datos](atjs-functions/targetglobalsettings.md#data-providers).

* Las solicitudes at.js ahora usan GET, pero cambiarán a POST cuando el tamaño de la URL exceda los 2048 caracteres. Hay una nueva propiedad llamada `urlSizeLimit` donde puede aumentar el límite de tamaño si es necesario. Este cambio permite que [!DNL Target] alinee at.js con AppMeasurement, que usa la misma técnica.
* [!DNL Target] exige ahora que se use la clave `mbox` en la función `adobe.target.applyOffer(options)`. Esta clave se ha requerido en el pasado, pero [!DNL Target] impone ahora su uso para garantizar que [!DNL Target] tenga la validación adecuada y que los clientes usen la función correctamente.
* at.js ha mejorado la funcionalidad de seguimiento de eventos y clics. at.js utiliza `navigator.sendBeacon()` para enviar datos de seguimiento de eventos y se volverá a utilizar XHR sincrónico cuando no se admita `navigator.sendBeacon()`. Este reutilización afecta principalmente a Internet Explorer 10 y 11 y algunas versiones de Safari. Safari añadirá compatibilidad para `navigator.sendBeacon()` en la próxima versión de iOS 11.3.
* Ahora, at.js puede presentar ofertas incluso cuando una página se abre en pestañas de fondo. Algunos clientes de [!DNL Target] encontraron un problema cuando `requestAnimationFrame()` se deshabilitó debido al comportamiento de regulación del explorador para las fichas de fondo.
* Esta versión agrega muchas mejoras de rendimiento, incluyendo pilas de llamadas más cortas al inspeccionar un perfil de la CPU de Chrome.
* at.js 1.3.0 ya no admite la publicación de contenido en Microsoft Internet Explorer 9. Para ver una lista de los exploradores compatibles, consulte [Exploradores compatibles](/help/dev/before-implement/supported-browsers.md). En el futuro, todas las solicitudes se ejecutarán a través de `XMLHttpRequest` con compatibilidad con CORS sin solicitudes JSONP. Este cambio mejora mucho la seguridad.

## Versión 1.2.3 de at.js

Ya está disponible la versión 1.2.3 de at.js.

* Incorpora compatibilidad con ofertas JSON. Las ofertas JSON solo se admiten en actividades creadas con el Compositor de experiencias basadas en formularios. En estos momentos, la única forma de utilizar las ofertas JSON es mediante llamadas directas a API. Consulte [Creación ofertas JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html).

## Versión 1.2.2 de at.js

Ya está disponible la versión 1.2.2 de at.js.

* Se ha corregido un problema que devolvía un error de JavaScript cuando la biblioteca [!DNL Target] se cargaba en una página mediante el modo QUIRKS. (TNT-28312)
* Se ha corregido un problema que provocaba que el rastreo de clics de [!DNL Target] interrumpiera las llamadas de recopilación de datos de [!DNL Analytics]. (TNT-28261)
* Se ha corregido un problema que provocaba que `getOffer() params` fallara cuando `targetPageParams()` devolvía una cadena vacía. (TNT-28359)
* Se ha corregido un problema con la generación del ID de sesión al utilizar x-solamente. (TNT-28361)

## Versión 1.2.1 de at.js

Ya está disponible la versión 1.2.1 de at.js.

* Se ha corregido un problema que se producía cuando el rastreo de clics en un vínculo con target=&quot;_blank&quot; impedía que [!DNL Target] abriera el vínculo en una pestaña nueva.

## Versión 1.2.0 de at.js

La versión 1.2 de at.js ya está disponible como una versión de mantenimiento que contiene principalmente correcciones de errores.

* Se ha corregido un problema que impedía utilizar acciones predeterminadas en casos especiales de rastreo de clics. (TNT-28089)
* Se ha corregido un problema producido al rastrear clics en un vínculo con `target="_blank"`, y que impedía que [!DNL Target] abriera el vínculo en una pestaña nueva. (TNT-28072)
* Se pueden usar direcciones IP como dominio de la cookie. (TNT-28002)
* Se ha corregido un problema que causaba parpadeo en las ofertas de redireccionamiento con un mbox global u otros mboxes regionales. (TNT-27978)
* Se ha corregido un problema en la configuración de la actividad [!UICONTROL Experience Targeting] que fallaba dentro del VEC al cambiar entre Examinar y Componer. (TNT-27942)
* Se ha corregido la gestión incorrecta en clases de estilo de parpadeo para elementos de rastreo de clics. (TNT-27896)
* Se ha corregido un problema que causaba que los parámetros de mbox global se mezclaran con todos los parámetros de mbox. (TNT-27846)
* Se han realizado cambios para garantizar que at.js gestione adecuadamente Handlebars, Mustache y otras bibliotecas de creación de plantillas del lado del cliente. (TNT-27831)
* Se han realizado cambios para asegurar que `sdidParamExpiry` se inicialice apropiadamente y se pase al API de visitante. Esto es una regresión que se ha añadido a `at.js 1.1.0`. Las versiones anteriores de at.js no se ven afectadas. Solo afecta a los clientes que utilizan ofertas de redireccionamiento y A4T. (TNT-27791)
* Se han realizado cambios para garantizar que `SCRIPT` se ejecute independientemente del tipo de atributo utilizado. (TNT-27865)

## Versión 1.1.0 de at.js

**Fecha:** 2 de agosto de 2017

En la versión 1.1 de at.js se incluyen las siguientes mejoras y correcciones:

* Se ha añadido la gestión de tokens de respuesta. Para obtener más información, consulte [Tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html).
* Se ha resuelto un problema para que `document.currentScript polyfill` no interfiera con Angular 1.X.
* Se han realizado cambios para asegurar que el rastreo de clics no interfiera con la propiedad Visibilidad. Los elementos de rastreo de clics se marcan con la clase CSS `at-element-click-tracking` en vez de con `at-element-marker`.

## Versión 1.0.0 de at.js

**Fecha:** 7 de julio de 2017

En la versión 1.0 de at.js se incluyen las siguientes mejoras y correcciones:

* Compatibilidad con la carga asíncrona de at.js para cargar las páginas más rápido.
* Soporte para el ocultamiento previo el contenido de la página al cargar at.js de forma asíncrona.
* Mejores mensajes de error cuando se deshabilita el envío de contenido.
* Mejoras de rendimiento al enviar varias actividades.
* Compatibilidad con YUI Compressor.
* Realización de informes de errores/fallos para eventos personalizados durante el envío de actividades.
* Corrección de problemas de rendimiento en Microsoft Internet Explorer 11.
* Corrección para la función `getOffer()`, que generaba un error en algunos sitios web.
* Cargar la biblioteca [!DNL Target] de forma asincrónica. Para obtener más información, consulte [Preguntas más frecuentes de at.js](/help/dev/implement/client-side/atjs/target-atjs-faq.md).

## Versión 0.9.7 de at.js

**Fecha:** 22 de mayo de 2017

En la versión 0.9.7 de at.js se incluyen las siguientes mejoras y correcciones:

* Se ha corregido un problema relacionado con una clave de recurso que faltaba en acciones `insertAfter` e `insertBefore` en el Compositor de experiencias visuales (VEC). Estos problemas estaban relacionados con la migración de ofertas visuales a plantillas de ofertas.

## Versión 0.9.6 de at.js

**Fecha:** 13 de abril de 2017

En la versión 0.9.6 de at.js se incluyen las siguientes mejoras y correcciones:

* Compatibilidad con ofertas de redireccionamiento para A4T. Una vez que descargue e instale la versión 0.9.6 de at.js, podrá usar ofertas de redireccionamiento en actividades que usen [!UICONTROL Adobe Analytics as the Reporting Source for Target] (A4T). Aparte de la versión 0.9.6 de at.js, existen otros requisitos mínimos que su implementación debe cumplir para utilizar ofertas de redireccionamiento y A4T. Para obtener más información y otros detalles importantes adicionales que debe conocer, consulte las [preguntas más frecuentes de A4T sobre las ofertas de redireccionamiento](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html).
* Antes de at.js 0.9.6, cuando la API de visitantes estaba presente en la página y la opción `visitorApiTimeout` era demasiado agresiva, [!DNL Target] podía encontrar una situación en la que no se enviara ningún dato ECID en la solicitud [!DNL Target]. Esto podía conllevar problemas como visitas no retenidas en [!DNL Analytics] al usar A4T.

  Este comportamiento se ha cambiado en at.js 0.9.6, incluso si `visitorApiTimeout` se establece en, por ejemplo, 1 ms, [!DNL Target] intentará recopilar los datos del SDID, los servidores de seguimiento y los ID de clientes, y enviarlos en la solicitud [!DNL Target].

* Se ha añadido la opción `selectorsPollingTimeout`. Para obtener más información, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* Se ha cambiado el formato de la respuesta de `getOffer()`. Para obtener más información, consulte [adobe.target.getOffer(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md).
* Se ha añadido el registro en la consola de declaraciones `<!DOCTYPE>` no admitidas.
* Se corrigió un problema en el cual los complementos [!DNL Target Classic] no se aplicaban correctamente cuando se enviaban varias ofertas predeterminadas a un único mbox. (TGT-22664)
* Se ha mejorado el establecimiento de cookies para los dominios de nivel superior (TLD) de dos letras con la finalidad de garantizar que la cookie de mbox se establezca correctamente en dichos dominios (por ejemplo, test.no, autodrives.ca, etc.).
* El algoritmo para extraer el dominio de nivel superior que debería usarse al guardar cookies ha cambiado en la versión 0.9.6 de at.js. Debido a ello, no es posible guardar cookies en direcciones que utilicen IP. La mayoría de las veces se usan direcciones IP con fines de prueba, pero como solución alternativa se pueden utilizar entradas DNS o ajustar el archivo de anfitriones en un cuadro local.
* Se ha corregido la gestión de las acciones mover y reorganizar cuando las propiedades son valores de cadena, no números enteros.

## Versión 0.9.4 de at.js

**Fecha:** 19 de enero de 2017

* Los nombres de mbox ahora pueden contener caracteres especiales, incluido el símbolo &amp;.

  Para obtener una lista de caracteres especiales permitidos, consulte [Configuración de at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

* Se ha añadido la opción de configuración `secureOnly` que indica si at.js debería utilizar solo HTTPS o se le debería permitir alternar entre HTTP y HTTPS según el protocolo de la página. Se trata de un ajuste avanzado que se establece en False de manera predeterminada y puede anularse mediante `targetGlobalSettings`.
* La opción Compatibilidad con navegadores anteriores está disponible en la versión 0.9.3 (y anteriores) de at.js. Esta opción se ha eliminado en la versión 0.9.4 de at.js.

## Versión 0.9.3 de at.js

**Fecha:** 10 de octubre de 2016

* Garantiza que las llamadas de mbox se realicen en Microsoft Internet Explorer 11 si los navegadores heredados están desactivados en la configuración de at.js.
* Garantiza que se procese el contenido predeterminado si una oferta remota dinámica falla (por ejemplo, si la URL es incorrecta y devuelve un error 404).
* Garantiza que los elementos se revelen rápidamente si los selectores de rastreo de clics de VEC no se encuentran en DOM.

## Versión 0.9.2 de at.js

**Fecha:** 21 de septiembre de 2016

* Se ha añadido la opción de configuración `optoutEnabled` para habilitar o deshabilitar la exclusión de Device Graph. Si esta opción se establece en `true` y el visitante ha excluido el seguimiento, su navegador no hará llamadas de mbox. Device Graph está aún en versión beta. Esta configuración está establecida en `false` de manera predeterminada, pero se debe establecer en `true` si usa Device Graph.
* Se ha añadido compatibilidad con `CustomEvent` para el mecanismo de notificación. Antes, el mecanismo de notificación de los eventos de at.js no se podía usar desde las API Standard del DOM, como `document.addEventListener()`. Ahora puede usar `document.addEventListener()` para suscribirse a los eventos de at.js, como eventos de solicitud y eventos de representación de contenido.
* Se ha arreglado un error relacionado con las ofertas creadas en el Compositor de experiencias visuales (VEC). Antes de esta versión, [!DNL Target] ocultaba los selectores y los mostraba solo cuando coincidían todos ellos. En la versión 0.9.2 de at.js [!DNL Target] muestra los selectores en cuanto coinciden.

## Versión 0.9.1 de at.js

**Fecha:** 14 de julio de 2016

* Proporciona a at.js un tiempo de espera para el servicio de ID de visitante. Es independiente del propio tiempo de espera del servicio.
* Corrige un problema en la versión 0.9.0 que afectaba a las implementaciones que usaban at.js en algunas páginas y mbox.js (ahora obsoleto) en otras.
* Si usa [!DNL Adobe Analytics] como fuente de informes de la actividad, no es necesario que especifique un servidor de seguimiento durante la creación de la actividad en las versiones 61 (o posterior) de mbox.js y 0.9.1 (o posterior) de at.js. La biblioteca at.js envía automáticamente los valores del servidor de seguimiento a [!DNL Target]. Durante la creación de la actividad, puede dejar vacío el campo Servidor de seguimiento de la página Objetivos y configuración.

## Versión 0.9.0 de at.js

Versión **[!DNL Target]:** 16.6.1

**Fecha:** 23 de junio de 2016

* Corrige un problema de pantalla blanca que surgía al usar las ofertas del VEC. Todo aquel que utilice at.js debe actualizar a esta nueva versión.
* Nueva API `registerExtension`.

  Esta nueva API proporciona a los desarrolladores acceso a ciertos módulos de jQuery utilizados en at.js para desarrollar extensiones (es decir, complementos) para la biblioteca. Este cambio conlleva varias implicaciones. Solo afectan a los usuarios que usan estas características:

   * La API `getSettings()` se ha eliminado, pero las mismas funciones están disponibles en `registerExtension()`.
   * La API `getTracking()` se ha eliminado, pero las mismas funciones están disponibles en `registerExtension()`.

   * Las extensiones existentes (por ejemplo, AngularJS) se deben actualizar para usar el método `registerExtension()`.

* Nueva API de notificación de at.js.

  El objetivo de este sistema de notificación es proporcionar más información sobre lo que at.js está haciendo en la página y cuándo hay problemas. Un problema común del VEC es que un lanzamiento de TI modifica la página, un selector del VEC se interrumpe y la prueba deja de entregar el contenido correctamente. Uno de los objetivos de este sistema de notificación es poner en conocimiento de la página este problema de entrega con el fin de que los desarrolladores puedan acceder a la información para pasarla a un sistema como [!DNL Adobe Analytics] y de que se puedan enviar alertas a los propietarios del negocio con el aviso de que la prueba se ha interrumpido.

* Método de la nueva API.`targetGlobalSettings()`

  En lugar de definir la configuración en la interfaz de usuario de [!DNL Target Standard/Premium], puede anular la configuración de la biblioteca at.js o usar las API de REST.

## Versión 0.8.0 de at.js

**Fecha:** 5 de mayo de 2016.

Esta es la primera fecha de lanzamiento oficial de la biblioteca at.js.

at.js es una nueva biblioteca de implementación para [!DNL Target] diseñada tanto para implementaciones web típicas como para aplicaciones de una sola página.

at.js reemplaza a mbox.js para [!DNL Adobe Target]implementaciones.

Entre otros beneficios, at.js mejora los tiempos de carga de página en implementaciones web, mejora la seguridad y proporciona mejores opciones de implementación en aplicaciones de una sola página.

at.js contiene los componentes que se incluían en target.js, de modo que ya no hay más una llamada a target.js.

Al implementar at.js, tenga en cuenta lo siguiente:

* Las versiones anteriores a Internet Explorer 8 no son compatibles.
* La implementación asíncrona significa que las integraciones heredadas como el complemento [!UICONTROL Test&Target to SiteCatalyst] pueden no funcionar.
* No se admiten [!DNL Target] complementos que hagan referencia a objetos y métodos de mbox.js.
* Todas las llamadas a [!DNL Target] se realizan mediante una solicitud XMLHTTPRequest y el contenido se devuelve mediante JSON.
