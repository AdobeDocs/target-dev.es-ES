---
keywords: servidor, api, sdk, node.js, nodejs, node.js, api de recommendations, api, api, servidor1
description: Obtenga información acerca de las  [!DNL Adobe Target] API de envío del lado del servidor, SDK y [!DNL Target Recommendations] API de.
title: ¿Dónde puedo obtener información acerca de  [!DNL Target] API de envío del lado del servidor y los SDK?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
TQID: https://experienceleague.adobe.com/x5WKb9Eenz2bw-idOnxlpWdtiivTx05n38sNXEt3DNc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a6cc21b9-1a36-4fa6-9c61-4acd04d9c88c
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 45af56b5ac64eb1db67c1bfdfecd6887dce990ff
workflow-type: tm+mt
source-wordcount: 825
ht-degree: 9%

---

# Servidor: implementar [!DNL Target]

Información sobre [!DNL Adobe Target] API de envío del lado del servidor, SDK y [!DNL Target Recommendations] API.

>[!NOTE]
>
>Si su implementación utiliza at.js y [!DNL AppMeasurement] en el lado del cliente, debe utilizar la [!UICONTROL API de envío de Target] y los SDK del lado del servidor que se describen a continuación.
>
>Si su implementación usa [!UICONTROL Adobe Experience Platform Web SDK], debería usar la [[!UICONTROL API de servidor de Adobe Experience Platform] [!UICONTROL Edge Network]](https://experienceleague.adobe.com/es/docs/experience-platform/edge-network-server-api/overview){target=_blank}.

El proceso siguiente se produce en una implementación del lado del servidor de [!DNL Target]:

1. Un dispositivo cliente realiza una solicitud de una experiencia a través del servidor.
1. El servidor envía esa solicitud a [!DNL Target].
1. [!DNL Target] devuelve la respuesta al servidor.
1. El servidor toma la decisión sobre la experiencia que debe ofrecerse al dispositivo cliente para que se procese.

No es necesario que la experiencia se muestre en un explorador. La experiencia se puede mostrar en un correo electrónico o quiosco, a través de un asistente de voz o a través de otro dispositivo no visual o no basado en un explorador. Dado que su servidor se encuentra entre el cliente y [!DNL Target], este tipo de implementación también es ideal si necesita mayor control y seguridad o si tiene procesos backend complejos que desee ejecutar en el servidor.

>[!NOTE]
>
>Un visitante por primera vez solo se puede inicializar en el lado del cliente. Un visitante por primera vez *no se puede* inicializar en el servidor. Esto se debe al ECID, que depende de la cookie demdex de terceros y, por lo tanto, debe inicializarse mediante la API de visitante.js en una implementación en la que participe el explorador.

Las secciones siguientes proporcionan más información sobre las distintas API y SDK del lado del servidor:

## API de envío del servidor

Vínculo: [API de envío del servidor](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

A través de la API de entrega [!DNL Target], puede:

* Ofrezca experiencias en toda la web, incluidas las SPA y los canales móviles, así como dispositivos de IoT no basados en explorador, como televisores conectados, quioscos o pantallas digitales en tienda.
* Ofrezca experiencias desde cualquier plataforma o aplicación del lado del servidor que pueda realizar llamadas HTTP/S.
* Ofrezca experiencias coherentes y personalizadas a un visitante, independientemente del canal o los dispositivos que el visitante utilizó para interactuar con su negocio.
* Almacene en caché las experiencias de un visitante dentro de una sesión en su servidor para poder evitar múltiples llamadas a la API y lograr así un mejor rendimiento.
* Se integra perfectamente con los productos de Adobe Experience Cloud, como Adobe Analytics, Adobe Audience Manager (AAM) y el servicio Experience Cloud ID desde el servidor.

## SDK del lado del servidor

La documentación de SDK del lado del servidor [!DNL Adobe Target] le ayuda a implementar [!DNL Target] en sus servidores en el idioma que elija.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Mediante los SDK del lado del servidor de [!DNL Adobe Target], puede:

* Ejecute **marcas de características**, **despliegues** y **experimentos A/B** con **latencia cercana a cero**.
* Ofrezca experiencias en **la web**, incluidos **SPA** y **canales móviles**, así como dispositivos con **Internet de las cosas (IoT)** que no usen explorador, como un televisor conectado, un quiosco o una pantalla digital en la tienda.
* Ofrezca **experiencias personalizadas impulsadas por el aprendizaje automático** a un usuario, sin importar el canal o el dispositivo que el usuario haya interactuado con su empresa.
* **Integre sin problemas con productos de Adobe Experience Cloud** como **Adobe Analytics**, **Adobe Audience Manager** y el **servicio de Experience Cloud ID** desde el servidor.

Consulte la página [Introducción](sdk-guides/getting-started/getting-started.md) para obtener información sobre cómo ejecutar un caso de uso de indicador de funciones simple mediante [toma de decisiones en el dispositivo](sdk-guides/on-device-decisioning/overview.md).

¡Eche un vistazo a nuestras [aplicaciones de ejemplo](sdk-guides/sample-apps/sample-apps.md) para divertirse y jugar!

## [!DNL Target Recommendations] API

Vínculo: [API de Target Recommendations](https://developers.adobetarget.com/api/recommendations) y [Información general de la API de Adobe Recommendations](../../before-administer/recs-api/overview.md).

Las API de Recommendations le permiten interactuar mediante programación con [!DNL Target] servidores de recomendaciones. Estas API se pueden integrar con una serie de pilas de aplicaciones para realizar funciones que normalmente se realizan a través de la interfaz de usuario [!DNL Target].

## [!DNL Platform Edge Network] llamadas de API sin un SDK {#platform-edge-api-user-agent}

[!UICONTROL Adobe Experience Platform Web SDK] y otras integraciones de SDK compatibles incluyen un valor `User-Agent` similar al explorador en los encabezados de solicitud HTTP al llamar a [!DNL Experience Platform Edge Network]. Las integraciones del lado del servidor que usen la [API de Interact](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/server-api/interact){target=_blank} pública sin SDK deben proporcionar este encabezado explícitamente.

Para las llamadas a la API de Interact que no sean de SDK, cumpla los siguientes requisitos:

* Incluya un `User-Agent` válido, similar a un explorador, en los encabezados de solicitud HTTP. Un valor de visitante o usuario-agente solo en el cuerpo de la solicitud JSON no cumple los requisitos de detección de bots para este patrón de integración.
* No utilice valores de marcador de posición o que no sean del explorador, por ejemplo, `MyApp/1.0`, ya que estos valores pueden dar como resultado la clasificación de bots.
* No se requiere un nombre de SDK o una versión de SDK para las llamadas públicas a la API de Edge. Para este escenario, el elemento requerido es un encabezado HTTP `User-Agent` válido.

Cuando [!DNL Target] clasifica una solicitud como tráfico de bots, la personalización puede fallar o parecer intermitente porque la búsqueda de perfiles, la evaluación de segmentos y el contenido personalizado para actividades como [!UICONTROL Recommendations] y [!UICONTROL Segmentación automática] están suprimidos, como se describe a continuación.

Obtenga más información acerca de la implementación con SDK en la [[!DNL Adobe Experience Platform Web SDK] descripción general](https://experienceleague.adobe.com/es/docs/target-dev/developer/client-side/aep/aep-web-sdk-overview){target=_blank}.

**Ejemplo de solicitud de API de Interact (los encabezados deben incluir `User-Agent`):**

```http
POST https://edge.adobedc.net/ee/v2/interact?dataStreamId=YOUR_DATASTREAM_ID&requestId=YOUR_REQUEST_ID
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.5 Safari/605.1.15
Accept: */*
Content-Type: text/plain; charset=UTF-8
```
