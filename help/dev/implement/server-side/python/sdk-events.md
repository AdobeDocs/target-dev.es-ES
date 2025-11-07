---
title: Suscribirse a eventos en  [!DNL Adobe Target] Python SDK
description: Obtenga información sobre cómo suscribirse a varios eventos que se producen dentro de Python SDK mediante el objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Eventos de SDK (Python)

## Descripción

Al [inicializar SDK](initialize-sdk.md), el diccionario `options["events"]` es un objeto opcional con claves de nombre de evento y valores de función de devolución de llamada. Se puede utilizar para suscribirse a varios eventos que se producen dentro de SDK. Por ejemplo, el evento `client_ready` se puede utilizar con una función de devolución de llamada que se invocará cuando SDK esté listo para las llamadas de método.

Cuando se llama a la función `callback`, se pasa un objeto de evento. Cada evento tiene un `type` correspondiente al nombre del evento y algunos eventos incluyen propiedades adicionales con información relevante.

## Solicitud

| Nombre del evento (tipo) | Descripción | Propiedades de evento adicionales |
| --- | --- | --- |
| client_ready | Se emite cuando el artefacto se ha descargado y el SDK está listo para las llamadas get_offers. Se recomienda cuando se utiliza el método de toma de decisiones en el dispositivo. | Ninguna |
| artifact_download_succeeded | Se emite cada vez que se descarga un nuevo artefacto. | artifact_payload, artifact_location |
| artifact_download_failed | Se emite cada vez que un artefacto no se puede descargar. | artifact_location, error |

## Ejemplo

### Python

```python {line-numbers="true"}
def client_ready_callback():
    # make get_offers requests

def artifact_download_succeeded(event):
    print("The artifact was successfully downloaded from {}".format(event.artifact_location))
    # optionally do something with event.artifact_payload, like persist it

def artifact_download_failed(event):
    print("The artifact failed to download from {} with the following error: {}"
          .format(event.artifact_location, str(event.error)))

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback,
        "artifact_download_succeeded": artifact_download_succeeded,
        "artifact_download_failed": artifact_download_failed
    }
}
target_client = target_client.create(client_options)
```
