---
title: Envíe notificaciones de visualización o clics a [!DNL Adobe Target] utilizar .NET SDK
description: Aprenda a utilizar sendNotifications() para enviar notificaciones de visualización o de clic a [!DNL Adobe Target] para medición e informes.
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---

# Enviar notificaciones (.NET)

## Descripción

`SendNotifications()` se utiliza para enviar notificaciones de visualización o clics a [!DNL Adobe Target] para medición e informes.

>[!NOTE]
>
>Cuando un `Execute` el objeto con parámetros requeridos está dentro de la propia solicitud, la impresión se incrementará automáticamente para las actividades calificadas.

Los métodos del SDK que incrementarán una impresión automáticamente son:

* `GetOffers()`
* `GetAttributes()`

Cuando un `Prefetch` se pasa dentro de la solicitud, la impresión no se incrementa automáticamente para las actividades con mboxes dentro de `Prefetch` objeto. `SendNotifications()` debe utilizarse para experiencias previamente recuperadas para incrementar impresiones y conversiones.

## Método

### Crear 

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## Ejemplo

Primero, vamos a construir el [!UICONTROL API de envío de Target] solicitud de recuperación previa de contenido para `home` y `product1` mboxes.

### \.NET

```dotnet {line-numbers="true"}
var mboxRequests = new List<MboxRequest>
    {
        new (index: 1, name: "home"),
        new (index: 2, name: "product1"),
    };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetPrefetch(new PrefetchRequest(mboxes: mboxRequests))
    .Build();

// Next, we fetch the offers via Target .NET SDK GetOffers() API
var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```

Una respuesta correcta contendrá un [!DNL Target Delivery API] objeto response, que contiene contenido recuperado previamente para los mboxes solicitados. Una muestra `targetResponse.Response` puede aparecer de la siguiente manera:

### \.NET

```dotnet {line-numbers="true"}
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

Tenga en cuenta `mbox` nombre y `state` , así como la variable `eventToken` , en cada una de las [!DNL Target] opciones de contenido. Estos deben proporcionarse en la `SendNotifications()` solicitud, en cuanto se muestre cada opción de contenido. Supongamos que el `product1` mbox se ha mostrado en un dispositivo que no es de explorador. La solicitud de notificaciones aparecerá de la siguiente manera:

### \.NET

```dotnet {line-numbers="true"}
var mboxNotifications = new List<Notification>
{
    new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
        mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
        tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
}; 

var mboxNotificationRequest = new TargetDeliveryRequest.Builder()
    .SetNotifications(mboxNotifications)
    .Build();
```

Tenga en cuenta que hemos incluido el estado de mbox y el token de evento correspondiente a [!DNL Target] entregada en la respuesta de recuperación previa. Una vez creada la solicitud de notificaciones, podemos enviarla a [!DNL Target] a través de `SendNotifications()` Método de API:

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
