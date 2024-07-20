---
title: Enviar notificaciones de clic o visualización a [!DNL Adobe Target] mediante el SDK de Java
description: Aprenda a utilizar sendNotifications() para enviar notificaciones de clic o visualización a [!DNL Adobe Target] para la medición y la creación de informes.
feature: APIs/SDKs
exl-id: 9231b480-f50f-40d1-ab06-0b9f2a2d79e3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 2%

---

# Envío de notificaciones (Java)

## Descripción

`sendNotifications()` se usa para enviar notificaciones de clics o visualizaciones a [!DNL Adobe Target] para la medición y generación de informes.

>[!NOTE]
>
>Cuando un objeto `execute` con parámetros requeridos se encuentra dentro de la propia solicitud, la impresión se incrementará automáticamente para las actividades calificadas.

Los métodos del SDK que incrementarán una impresión automáticamente son:

* `getOffers()`
* `getAttributes()`

Cuando se pasa un objeto `prefetch` dentro de la solicitud, la impresión no se incrementa automáticamente para las actividades con mboxes dentro del objeto `prefetch`. `sendNotifications()` debe usarse para experiencias previamente recuperadas para incrementar impresiones y conversiones.

## Método

### crear

```javascript {line-numbers="true"}
ResponseStatus TargetClient.sendNotifications(TargetDeliveryRequest request)
```

## Ejemplo

En primer lugar, vamos a generar la solicitud [!DNL Target Delivery API] para recuperar previamente contenido para los mboxes `home` y `product1`.

### Precarga

```javascript {line-numbers="true"}
List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("home").index(1));
mboxRequests.add((MboxRequest) new MboxRequest().name("product1").index(2));
PrefetchRequest prefetchMboxesRequest = new PrefetchRequest().setMboxes(mboxRequests)

// Next, we fetch the offers via Target Java SDK getOffers() API
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```

Una respuesta correcta contendrá un objeto de respuesta [!UICONTROL Target Delivery API], que incluye contenido recuperado previamente para los mboxes solicitados. Un objeto `targetResponse.response` de ejemplo puede tener el siguiente aspecto:

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

Observe los campos mbox `name` y `state`, así como el campo `eventToken`, en cada una de las opciones de contenido de [!DNL Target]. Se deben proporcionar en la solicitud `sendNotifications()`, en cuanto se muestre cada opción de contenido. Supongamos que el mbox `product1` se ha mostrado en un dispositivo que no es de explorador. La solicitud de notificaciones tendrá este aspecto:

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

Observe que hemos incluido el estado de mbox y el token de evento correspondiente a la oferta [!DNL Target] entregada en la respuesta de recuperación previa. Una vez creada la solicitud de notificaciones, podemos enviarla a [!DNL Target] mediante el método de API `sendNotifications()`:

### Respuesta

```javascript {line-numbers="true"}
ResponseStatus notificationResponse = targetJavaClient.sendNotifications(mboxNotificationRequest);
```
