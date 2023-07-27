---
keywords: servidor, api, sdk, node.js, nodejs, node.js, api de recommendations, api, api, servidor1
description: Obtenga información acerca de [!DNL Adobe Target] API de envío del lado del servidor, SDK y [!DNL Target Recommendations] API.
title: ¿Dónde puedo obtener información? [!DNL Target] ¿API de envío del lado del servidor y SDK?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 14%

---

# Servidor: implementación [!DNL Target]

Información acerca de [!DNL Adobe Target] API de envío del lado del servidor, SDK y [!DNL Target Recommendations] API.

El proceso siguiente se produce en una implementación del lado del servidor de [!DNL Target]:

1. Un dispositivo cliente realiza una solicitud de una experiencia a través del servidor.
1. El servidor envía esa solicitud a [!DNL Target].
1. [!DNL Target] devuelve la respuesta al servidor.
1. El servidor toma la decisión sobre la experiencia que debe ofrecerse al dispositivo cliente para que se procese.

No es necesario que la experiencia se muestre en un explorador. La experiencia se puede mostrar en un correo electrónico o quiosco, a través de un asistente de voz o a través de otro dispositivo no visual o no basado en un explorador. Dado que su servidor se encuentra entre el cliente y [!DNL Target], este tipo de implementación también es ideal si necesita mayor control y seguridad o si tiene procesos backend complejos que desee ejecutar en el servidor.

>[!NOTE]
>
>Un visitante por primera vez solo se puede inicializar en el lado del cliente. Un visitante por primera vez *no puede* se inicialice en el lado del servidor. Esto se debe al ECID, que depende de la cookie demdex de terceros y, por lo tanto, debe inicializarse mediante la API de visitante.js en una implementación en la que participe el explorador.

Las secciones siguientes proporcionan más información sobre las distintas API y SDK del lado del servidor:

## API de envío del servidor

Vínculo: [API de envío del servidor](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

A través de [!DNL Target] API de envío, puede:

* SPA Ofrezca experiencias en toda la web, incluidos los canales web y móviles, así como en dispositivos IoT no basados en el explorador, como televisores conectados, quioscos o pantallas digitales en tienda.
* Ofrezca experiencias desde cualquier plataforma o aplicación del lado del servidor que pueda realizar llamadas HTTP/S.
* Ofrezca experiencias coherentes y personalizadas a un visitante, independientemente del canal o los dispositivos que el visitante utilizó para interactuar con su negocio.
* Almacene en caché las experiencias de un visitante dentro de una sesión en su servidor para poder evitar múltiples llamadas a la API y lograr así un mejor rendimiento.
* Se integra perfectamente con los productos de Adobe Experience Cloud, como Adobe Analytics, Adobe Audience Manager AAM () y el servicio de ID de Experience Cloud desde el servidor.

## SDK del lado del servidor

El [!DNL Adobe Target] La documentación del SDK del lado del servidor le ayuda a implementar [!DNL Target] en sus servidores en el idioma que elija.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Pasante [!DNL Adobe Target]Los SDK del lado del servidor de, puede:

* Ejecutar y ejecutar **indicación de características**, **despliegues**, y **Experimentos A/B** en **latencia cercana a cero**.
* Ofrecer experiencias a través de **web**, incluido **SPA**, y **canales móviles**, así como no basadas en explorador **Dispositivos con Internet de las cosas (IoT)** como un televisor conectado, un quiosco o una pantalla digital en la tienda.
* Entrega **Experiencias personalizadas impulsadas por el aprendizaje automático (ML)** a un usuario, independientemente del canal o dispositivo que este haya utilizado en su negocio.
* **Integración perfecta con Adobe Experience Cloud** productos como **Adobe Analytics**, **Adobe Audience Manager**, y el **Servicio de ID de Experience Cloud** del lado del servidor.

Consulte la [Primeros pasos](sdk-guides/getting-started/getting-started.md) para aprender a ejecutar una sencilla función de marcación de casos de uso mediante [toma de decisiones en el dispositivo](sdk-guides/on-device-decisioning/overview.md).

Consulte nuestra [Aplicaciones de ejemplo](sdk-guides/sample-apps/sample-apps.md) ¡para divertirte y jugar!

## [!DNL Target Recommendations] API

Vínculo: [API de Recommendations de Target](https://developers.adobetarget.com/api/recommendations) y [Información general de API de Adobe Recommendations](../../before-administer/recs-api/overview.md).

Las API de Recommendations le permiten interactuar mediante programación con [!DNL Target] servidores de recommendations. Estas API se pueden integrar con una serie de pilas de aplicaciones para realizar funciones que normalmente se realizan a través de [!DNL Target] interfaz de usuario.
