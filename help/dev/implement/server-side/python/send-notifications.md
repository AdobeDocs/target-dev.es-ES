---
title: Enviar notificaciones de clic o visualización a [!DNL Adobe Target] usando el SDK de Python
description: Aprenda a utilizar sendNotifications() para enviar notificaciones de clic o visualización a [!DNL Adobe Target] para la medición y la creación de informes.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 8%

---

# Envío de notificaciones (Python)

## Descripción

`send_notifications()` se usa para enviar notificaciones de clics o visualizaciones a [!DNL Adobe Target] para la medición y generación de informes.

>[!NOTE]
>
>Cuando un objeto `execute` con parámetros requeridos se encuentra dentro de la propia solicitud, la impresión se incrementará automáticamente para las actividades calificadas.

Los métodos del SDK que incrementarán una impresión automáticamente son:

* `get_offers()`
* `get_attributes()`

Cuando se pasa un objeto `prefetch` dentro de la solicitud, la impresión no se incrementa automáticamente para las actividades con mboxes dentro del objeto `prefetch`. `Send_notifications()` debe usarse para experiencias previamente recuperadas para incrementar impresiones y conversiones.

## Método

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## Parámetros

`options` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- | --- | --- | --- | --- |
| de eventos | DeliveryRequest | Sí | Ninguna | Se ajusta a la solicitud [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | no | Ninguna | Cookie [!DNL Target] |
| target_location_hint | str | no | Ninguna | [!DNL Target] sugerencia de ubicación |
| consumer_id | str | no | Ninguna | Al vincular varias llamadas, se deben proporcionar ID de consumidor diferentes |
| customer_ids | list[CustomerId] | no | Ninguna | Una lista de ID de cliente en formato compatible con VisitorId |
| session_id | str | no | Ninguna | Se utiliza para vincular varias solicitudes |
| callback | exigible | no | Ninguna | Si se administra la solicitud de forma asíncrona, la llamada de retorno se invoca cuando la respuesta está lista |
| err_callback | exigible | no | Ninguna | Si se administra la solicitud de forma asíncrona, se invoca la devolución de llamada de error cuando se produce una excepción |

## Devuelve

`Returns` a `TargetDeliveryResponse` si se llama sincrónicamente (predeterminado), o a `AsyncResult` si se llama con una llamada de retorno. `TargetDeliveryResponse` tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| respuesta | DeliveryResponse | Se ajusta a la respuesta [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | dict | Cookie [!DNL Target] |
| target_location_hint_cookie | dict | [!DNL Target] cookie de indicio de ubicación |
| analytics_details | list[AnalyticsResponse] | [!DNL Analytics] carga útil, en caso de uso de [!DNL Analytics] del lado del cliente |
| trazar |  | list[dict] | Datos de seguimiento agregados para todos los mboxes o vistas de solicitud |
| response_tokens | list[dict] | Una lista de [&#x200B; tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=es) |
| meta | dict | Metadatos de toma de decisiones adicionales para su uso con la toma de decisiones en el dispositivo |

## Ejemplo

En primer lugar, vamos a generar la solicitud [!UICONTROL Target Delivery API] para recuperar previamente contenido para los mboxes `home` y `product1`.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

Una respuesta correcta contendrá un objeto de respuesta [!UICONTROL Target Delivery API], que incluye contenido recuperado previamente para los mboxes solicitados. Un objeto `target_response["response"]` de ejemplo (con formato de diccionario) puede aparecer de la siguiente manera:

### Python

```python {line-numbers="true"}
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

Observe los campos mbox `name` y `state`, así como el campo `eventToken`, en cada una de las opciones de contenido de Target. Se deben proporcionar en la solicitud `send_notifications()`, en cuanto se muestre cada opción de contenido. Supongamos que el mbox `product1` se ha mostrado en un dispositivo que no es de explorador. La solicitud de notificaciones aparecerá de la siguiente manera:

### Python

```python {line-numbers="true"}
notification_mbox = NotificationMbox(name="product1",
                                     state="J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
notification = Notification(
    id="1",
    type=MetricType.DISPLAY,
    timestamp=1621530726000,  # Epoch time in milliseconds
    mbox=notification_mbox,
    tokens=["t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="]
)
notification_request = DeliveryRequest(notifications=[notification])
```

Tenga en cuenta que hemos incluido el estado de mbox y el token de evento correspondiente a la oferta [!DNL Target] entregada en la respuesta de recuperación previa. Una vez creada la solicitud de notificaciones, podemos enviarla a [!DNL Target] mediante el método de API `send_notifications()`:

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
