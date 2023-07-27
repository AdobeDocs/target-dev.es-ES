---
title: Uso [!UICONTROL getOffers()] in [!DNL Adobe Target] al utilizar el SDK de Node.js
description: Aprenda a utilizar [!UICONTROL getOffers()] para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 22%

---

# [!UICONTROL Obtener ofertas] (Node.js)

## Descripción

`[!UICONTROL getOffers()]` se utiliza para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].


## Método

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parámetros

El `options` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- |--- | --- | --- | --- |
| Solicitud | Objeto | Sí | Ninguna | Se ajusta a [[!DNL Target] API de envío](/help/dev/implement/delivery-api/overview.md) solicitud |
| visitorCookie | Cadena | No | Ninguna | Cookie ECID (VisitorId) |
| targetCookie | Cadena | No | Ninguna | [!DNL Target] cookie |
| targetLocationHint | Cadena | No | Ninguna | [!DNL Target] indicio de ubicación |
| consumerId | Cadena | No | Ninguna | consumerIds para [!UICONTROL Analytics for Target] Vinculación (A4T) |
| CustomerIds | Matriz | No | Ninguna | ID de cliente en formato compatible con VisitorId |
| sessionId | Cadena | No | Ninguna | Se utiliza para vincular varios [!DNL Target] solicitudes |
| visitante | Objeto | No | new VisitorId | Proporcione una instancia de VisitorId externa |

## Promesa

`Promise` devuelto tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| de eventos | Objeto | [[!UICONTROL API de envío de Target]](/help/dev/implement/delivery-api/overview.md) solicitud |
| respuesta | Objeto | [[!UICONTROL API de envío de Target]](/help/dev/implement/delivery-api/overview.md) respuesta |
| visitorState | Objeto | Objeto que debe pasarse a la API de visitante `getInstance()` |
| targetCookie | Objeto | [!DNL Target] cookie |
| targetLocationHintCookie | Objeto | [!DNL Target] cookie de indicio de ubicación |
| analyticsDetails | Matriz | Carga útil de Analytics, en caso de uso de Analytics en el lado del cliente |
| responseTokens | Matriz | Una lista de [Tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trazar | Matriz | Datos de seguimiento agregados para todos los mboxes o vistas de solicitud |
| status | Objeto | Un objeto que contiene el estado de la respuesta. |
| decisioningMethod | Cadena | Determina qué método de toma de decisiones utilizar ([en el dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), del lado del servidor, híbrido) |

`targetCookie` y `targetLocationHintCookie` Los objetos utilizados para devolver datos al explorador tienen la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| name | Cadena | Nombre de la cookie |
| value | Cualquiera | Valor de la cookie, el se convertirá en cadena |
| maxAge | Número | El `maxAge` es una opción conveniente para configurar las caducidades en relación con el tiempo actual en segundos |

El `status` el objeto utilizado para indicar el estado de la respuesta de destinatario tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| status | Número | Código de estado HTTP |
| message | Cadena | Un mensaje sobre la respuesta. Por ejemplo, puede indicar si se ha decidido la respuesta [en el dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) o del lado del servidor |
| remoteMboxes | Matriz | Cuando el método de toma de decisiones es `on-device`, se proporciona una matriz de nombres de mbox que no se han podido decidir completamente en el dispositivo. En otras palabras, un [[!UICONTROL API de envío de Target]](/help/dev/implement/delivery-api/overview.md) se necesita la solicitud de. |

## Ejemplo

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    context: {channel: "web"},
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
}};

const response = await targetClient.getOffers({ request });
```
