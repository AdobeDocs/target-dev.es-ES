---
title: Cómo usar solicitudes asincrónicas en el SDK de  [!DNL Adobe Target] Python
description: Descubra cómo el SDK de  [!DNL Target] Python admite solicitudes asincrónicas, lo que puede reducir el tiempo de destino efectivo a cero.
feature: APIs/SDKs
exl-id: fafb9e28-5ac5-41c1-8e7f-f40550b6749f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 16%

---

# Obtener atributos (Python)

## Descripción

`get_attributes()` se usa para recuperar experimentación y experiencias personalizadas de [!DNL Target] y extraer valores de atributos.


## Método

### getAttributes

```python {line-numbers="true"}
target_client_instance.get_attributes(mbox_names, options)
```

## Parámetros

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- | --- | --- | --- | --- |
| mbox_names | list[str] | Sí | Ninguna | Una lista de nombres de mbox |
| opciones | dict | No | Ninguna | Se usan las mismas opciones para [Obtener ofertas](get-offers.md) |

## AttributesProvider

El `AttributesProvider` devuelto por `target_client.get_attributes()` tiene los siguientes métodos:

| Método | Tipo de devolución | Descripción |
| --- | --- | --- |
| get_value(mbox_name, key) | any | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| as_object(mbox_name) | dict | Devuelve un objeto json simple con pares de valor clave |
| get_response() | [TargetDeliveryResponse](https://github.com/adobe/target-python-sdk/blob/main/target_python_sdk/types/target_delivery_response.py) | Devuelve el objeto de respuesta normalmente devuelto por `get_offers` |

## Ejemplo

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_attributes_options = {
      "request": delivery_request
    }

    attributes_provider = target_client.get_attributes(["demo-engineering-flags"], get_attributes_options)
    # returns just the value of searchProviderId from the demo-engineering-flags mbox offer
    search_provider_id = attributes_provider.get_value("demo-engineering-flags", "searchProviderId")

    # returns a simple dict object representing the demo-engineering-flags mbox offer
    engineering_flags = attributes_provider.as_object("demo-engineering-flags")
    """  the value of engineeringFlags looks like this
        {
            "cdnHostname": "cdn.cloud.corp.net",
            "searchProviderId": 143,
            "hasLegacyAccess": false
        }
    """

    asset_url = "http://{}/path/to/asset".format(engineering_flags.get("cdnHostname"))


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
