---
title: Envíe notificaciones de visualización o clics a [!DNL Adobe Target] uso del SDK de Node.js
description: Aprenda a utilizar sendNotifications() para enviar notificaciones de visualización o de clic a [!DNL Adobe Target] para medición e informes.
feature: APIs/SDKs
exl-id: 84bb6a28-423c-457f-8772-8e3f70e06a6c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 4%

---

# Enviar notificaciones (Node.js)

## Descripción

`[!UICONTROL sendNotifications()]` se utiliza para enviar notificaciones de visualización o clics a [!DNL Adobe Target] para medición e informes.

>[!NOTE]
>
>Cuando un `execute` el objeto con parámetros requeridos está dentro de la propia solicitud, la impresión se incrementará automáticamente para las actividades calificadas.

Los métodos del SDK que incrementarán una impresión automáticamente son:

* `getOffers()`
* `getAttributes()`

Cuando un `prefetch` se pasa dentro de la solicitud, la impresión no se incrementa automáticamente para las actividades con mboxes dentro de `prefetch` objeto. `sendNotifications()` debe utilizarse para experiencias previamente recuperadas para incrementar impresiones y conversiones.

## Método

### crear

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

### Parámetros

`options` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Valor predeterminado |
| --- | --- | --- | --- |
| de eventos | Objeto | Sí | Ninguna |

## Ejemplo

Primero, vamos a crear el ID de TargetSolicitud de API de envío para recuperar previamente contenido para `home` y `product1` mboxes.

### Node.js

```js {line-numbers="true"}
const prefetchMboxesRequest = {
  prefetch: {
    mboxes: [
      { name: "home" },
      { name: "product1" }
    ]
  }
};
// Next, we fetch the offers via Target Node.js SDK getOffers() API
const targetResponse = await targetClient.getOffers({ request: prefetchMboxesRequest });
```

Una respuesta correcta contendrá un [!UICONTROL API de envío de Target] objeto response, que contiene contenido recuperado previamente para los mboxes solicitados. Una muestra `targetResponse.response` puede aparecer de la siguiente manera:

### Node.js

```js {line-numbers="true"}
{
  "status": 200,
  "requestId": "e8ac2dbf5f7d4a9f9280f6071f24a01e",
  "id": {
    "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "adobetargetmobile",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "home",
        "options": [
          {
            "type": "html",
            "content": "HOME OFFER",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      },
      {
        "index": 1,
        "name": "product1",
        "options": [
          {
            "type": "html",
            "content": "TEST OFFER 1",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      }
    ]
  }
}
```

Observe el mbox `name` y `state` , así como la variable `eventToken` , en cada una de las [!DNL Target] opciones de contenido. Estos deben proporcionarse en la `sendNotifications()` solicitud, en cuanto se muestre cada opción de contenido. Supongamos que el `product1` mbox se ha mostrado en un dispositivo que no es de explorador. La solicitud de notificaciones aparecerá de la siguiente manera:

### Node.js

```js {line-numbers="true"}
const mboxNotificationRequest = {
  notifications: [{
    id: "1",
    timestamp: Date.now(),
    type: "display",
    mbox: {
      name: "product1",
      state: "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    },
    tokens: [ "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" ]
  }]
};
```

Tenga en cuenta que hemos incluido el estado de mbox y el token de evento correspondiente al [!DNL Target] entregada en la respuesta de recuperación previa. Una vez creada la solicitud de notificaciones, podemos enviarla a [!DNL Target] a través de `sendNotifications()` Método de API:

### Node.js

```js {line-numbers="true"}
const notificationResponse = await targetClient.sendNotifications({ request: mboxNotificationRequest });
```
