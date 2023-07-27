---
title: Uso de getOffers() en [!DNL Adobe Target] al usar el SDK de Python de
description: Aprenda a utilizar getOffers() para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 13%

---

# Obtener ofertas (Python)

## Descripción

`get_offers()` se utiliza para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].


## Método

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## Parámetros

El `options` dict tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- | --- | --- | --- | --- |
| de eventos | DeliveryRequest | Sí | Ninguna | Se ajusta a [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) solicitud |
| target_cookie | str | no | Ninguna | [!DNL Target] cookie |
| target_location_hint | str | no | Ninguna | [!DNL Target] indicio de ubicación |
| consumer_id | str | no | Ninguna | Al vincular varias llamadas, se deben proporcionar ID de consumidor diferentes |
| customer_ids | lista[CustomerId] | no | Ninguna | Una lista de ID de cliente en formato compatible con VisitorId |
| session_id | str | no | Ninguna | Se utiliza para vincular varias solicitudes |
| callback | exigible | no | Ninguna | Si se administra la solicitud de forma asíncrona, la llamada de retorno se invoca cuando la respuesta está lista |
| err_callback | exigible | no | Ninguna | Si se administra la solicitud de forma asíncrona, se invoca la devolución de llamada de error cuando se produce una excepción |

## Devuelve

Devuelve un `TargetDeliveryResponse` si se llama sincrónicamente (predeterminado), o un `AsyncResult` si se llama con una llamada de retorno. `TargetDeliveryResponse` tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| respuesta | DeliveryResponse | Se ajusta a [[!UICONTROL API de envío de Target]](/help/dev/implement/delivery-api/overview.md) respuesta |
| target_cookie | dict | [!DNL Target] cookie |
| target_location_hint_cookie | dict | [!DNL Target] cookie de indicio de ubicación |
| analytics_details | lista[AnalyticsResponse] | Carga útil de Analytics, en caso de uso de Analytics por parte del cliente |
| trazar | lista[dict] | Datos de seguimiento agregados para todos los mboxes o vistas de solicitud |
| response_tokens | lista[dict] | Una lista de[Tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| meta | dict | Metadatos de toma de decisiones adicionales para su uso con la toma de decisiones en el dispositivo |

`target_cookie` y `target_location_hint_cookie` Los objetos utilizados para devolver datos al explorador tienen la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| name | str | Nombre de la cookie |
| value | any | Valor de la cookie, el valor se convertirá en cadena |
| max_age | int | El `max_age option` es una comodidad para la configuración de caduca en relación con el tiempo actual en segundos |

El `meta` el objeto utilizado para indicar el estado de la respuesta de destinatario tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| decisioning_method | str | Qué método de toma de decisiones se ha utilizado: en el dispositivo o del lado del servidor |
| remote_mboxes | list`[str]` | Cuando el método de toma de decisiones es `on-device`, se proporciona una matriz de nombres de mbox que no se han podido decidir completamente en el dispositivo. En otras palabras, un [[!UICONTROL API de envío de Target]](/help/dev/implement/delivery-api/overview.md) se necesita la solicitud de. |
| remote_views | list`[str]` | Cuando el método de toma de decisiones es en el dispositivo, se proporciona una matriz de nombres de vista que no se pudieron decidir completamente en el dispositivo. En otras palabras, un [[!UICONTROL API de envío de Target]](/help/dev/implement/delivery-api/overview.md) se necesita la solicitud de. |

## Ejemplo

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }

    target_delivery_response = target_client.get_offers(get_offers_options)


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
