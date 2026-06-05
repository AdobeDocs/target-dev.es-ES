---
title: Usar [!UICONTROL getOffers()] en [!DNL Adobe Target] al usar el SDK de Node.js
description: Aprenda a usar [!UICONTROL getOffers()] para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
TQID: https://experienceleague.adobe.com/WRGy74F1kUobRl1Pakse0VnXt3cT3-ntCljm4bHtiZ4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 20%

---

# [!UICONTROL Obtener ofertas] (Node.js)

## Descripción

`[!UICONTROL getOffers()]` se usa para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].


## Método

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parámetros

El objeto `options` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- |--- | --- | --- | --- |
| Solicitud | Objeto | Sí | Ninguna | Se ajusta a la solicitud de la [[!DNL Target] API de envío](/help/dev/implement/delivery-api/overview.md) |
| visitorCookie | Cadena | No | Ninguna | Cookie ECID (VisitorId) |
| targetCookie | Cadena | No | Ninguna | Cookie [!DNL Target] |
| targetLocationHint | Cadena | No | Ninguna | [!DNL Target] sugerencia de ubicación |
| consumerId | Cadena | No | Ninguna | consumerIds para la vinculación de [!UICONTROL Analytics for Target] (A4T) |
| CustomerIds | Matriz | No | Ninguna | ID de cliente en formato compatible con VisitorId |
| sessionId | Cadena | No | Ninguna | Se usa para vincular varias solicitudes [!DNL Target] |
| visitante | Objeto | No | new VisitorId | Proporcione una instancia de VisitorId externa |

## Promesa

`Promise` devuelto tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| de eventos | Objeto | [[!UICONTROL Solicitud de API de envío de destino]](/help/dev/implement/delivery-api/overview.md) |
| respuesta | Objeto | Respuesta de la [[!UICONTROL API de envío de destino]](/help/dev/implement/delivery-api/overview.md) |
| visitorState | Objeto | Objeto que se debe pasar a la API de visitante `getInstance()` |
| targetCookie | Objeto | Cookie [!DNL Target] |
| targetLocationHintCookie | Objeto | [!DNL Target] cookie de indicio de ubicación |
| analyticsDetails | Matriz | Carga útil de Analytics, en caso de uso de Analytics en el lado del cliente |
| responseTokens | Matriz | Una lista de [tokens de respuesta] (¿https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trazar | Matriz | Datos de seguimiento agregados para todos los mboxes o vistas de solicitud |
| status | Objeto | Un objeto que contiene el estado de la respuesta. |
| decisioningMethod | Cadena | Determina qué método de toma de decisiones usar ([en el dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), del lado del servidor, híbrido) |

Los objetos `targetCookie` y `targetLocationHintCookie` utilizados para devolver datos al explorador tienen la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| name | Cadena | Nombre de la cookie |
| value | Cualquiera | Valor de la cookie, el se convertirá en cadena |
| maxAge | Número | La opción `maxAge` es una conveniencia para configurar las caducidades en relación con el tiempo actual en segundos |

El objeto `status` utilizado para indicar el estado de la respuesta de destino tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| status | Número | Código de estado HTTP |
| message | Cadena | Un mensaje sobre la respuesta. Por ejemplo, puede indicar si la respuesta se decidió [en el dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) o en el lado del servidor |
| remoteMboxes | Matriz | Cuando el método de toma de decisiones es `on-device`, se proporciona una matriz de nombres de mbox que no se pudieron decidir completamente en el dispositivo. En otras palabras, se necesita una solicitud de la [[!UICONTROL API de envío de Target]](/help/dev/implement/delivery-api/overview.md). |

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
