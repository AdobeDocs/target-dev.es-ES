---
title: Cómo usar solicitudes asincrónicas en el SDK de  [!DNL Adobe Target] Python
description: Descubra cómo el SDK de  [!DNL Target] Python admite solicitudes asincrónicas, lo que puede reducir el tiempo de destino efectivo a cero.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 4%

---

# Solicitudes asincrónicas (Python)

## Descripción

Una ventaja de la integración del lado del servidor es que puede aprovechar el enorme ancho de banda y recursos informáticos disponibles en el lado del servidor mediante el paralelismo. [!DNL Target] El SDK de Python admite solicitudes asincrónicas, lo que puede reducir el tiempo de destino efectivo a cero.

## Métodos compatibles

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## Ejemplo

Una aplicación de ejemplo que use el módulo async/await de `asyncio` en Python 3.9+ podría tener el siguiente aspecto:

### Python

```python {line-numbers="true"}
async def execute_mboxes(self, mboxes):
    context = Context(channel=ChannelType.WEB)
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }
    return await asyncio.to_thread(target_client.get_offers, get_offers_options)

async def get_target_delivery_response(mboxes):
    target_delivery_response = await execute_mboxes(mboxes)
    response = Response(target_delivery_response.get("response").to_str(), status=200, mimetype='application/json')
    return response

mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
return asyncio.run(get_target_delivery_response(mboxes)
```

En este ejemplo se supone que está utilizando Python 3.9+. Si usa una versión anterior de Python, aún puede enviar solicitudes asincrónicas pasando `options.callback` a `get_offers`. Consulte la aplicación Flask de ejemplo para obtener más detalles sobre la ejecución asincrónica mediante devoluciones de llamada o asíncrona/espera, [aquí](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py).
