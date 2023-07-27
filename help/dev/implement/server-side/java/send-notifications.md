---
title: Envíe notificaciones de visualización o clics a [!DNL Adobe Target] uso del SDK de Java
description: Aprenda a utilizar sendNotifications() para enviar notificaciones de visualización o de clic a [!DNL Adobe Target] para medición e informes.
feature: APIs/SDKs
exl-id: 9231b480-f50f-40d1-ab06-0b9f2a2d79e3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 2%

---

# Envío de notificaciones (Java)

## Descripción

`sendNotifications()` se utiliza para enviar notificaciones de visualización o clics a [!DNL Adobe Target] para medición e informes.

>[!NOTE]
>
>Cuando un `execute` el objeto con parámetros requeridos está dentro de la propia solicitud, la impresión se incrementará automáticamente para las actividades calificadas.

Los métodos del SDK que incrementarán una impresión automáticamente son:

* `getOffers()`
* `getAttributes()`

Cuando un `prefetch` se pasa dentro de la solicitud, la impresión no se incrementa automáticamente para las actividades con mboxes dentro de `prefetch` objeto. `sendNotifications()` debe utilizarse para experiencias previamente recuperadas para incrementar impresiones y conversiones.

## Método

### crear

```javascript {line-numbers="true"}
ResponseStatus TargetClient.sendNotifications(TargetDeliveryRequest request)
```

## Ejemplo

Primero, vamos a construir el [!DNL Target Delivery API] solicitud de recuperación previa de contenido para `home` y `product1` mboxes.

### Precarga

```javascript {line-numbers="true"}
List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("home").index(1));
mboxRequests.add((MboxRequest) new MboxRequest().name("product1").index(2));
PrefetchRequest prefetchMboxesRequest = new PrefetchRequest().setMboxes(mboxRequests)

// Next, we fetch the offers via Target Java SDK getOffers() API
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```

Una respuesta correcta contendrá un [!UICONTROL API de envío de Target] objeto response, que contiene contenido recuperado previamente para los mboxes solicitados. Una muestra `targetResponse.response` puede tener el siguiente aspecto:

### Respuesta

```javascript {line-numbers="true"}
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

Observe el mbox `name` y `state` , así como la variable `eventToken` , en cada una de las [!DNL Target] opciones de contenido. Estos deben proporcionarse en la `sendNotifications()` solicitud, en cuanto se muestre cada opción de contenido. Supongamos que el `product1` mbox se ha mostrado en un dispositivo que no es de explorador. La solicitud de notificaciones tendrá este aspecto:

### Solicitud

```javascript {line-numbers="true"}
TargetDeliveryRequest mboxNotificationRequest = TargetDeliveryRequest.builder().notifications(new ArrayList() {{
    add(new Notification()
            .id("1")
            .timestamp(System.currentTimeMillis())
            .type(MetricType.DISPLAY)
            .mbox(new NotificationMbox()
                    .name("product1")
                    .state("J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
            )
            .tokens(Arrays.asList(new String[]{"t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="}))
    );
}}).build();
```

Tenga en cuenta que hemos incluido el estado de mbox y el token de evento correspondiente al [!DNL Target] entregada en la respuesta de recuperación previa. Una vez creada la solicitud de notificaciones, podemos enviarla a [!DNL Target] mediante `sendNotifications()` Método de API:

### Respuesta

```javascript {line-numbers="true"}
ResponseStatus notificationResponse = targetJavaClient.sendNotifications(mboxNotificationRequest);
```
