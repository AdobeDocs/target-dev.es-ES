---
title: Inicialice el [!DNL Adobe Target] SDK de Python para registrar solicitudes
description: Obtenga información sobre cómo registrar solicitudes en [!DNL Adobe Target] SDK de Python.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Registrador (Python)

## Descripción

Cuándo [inicialización del SDK](initialize-sdk.md), el `options["logger"]` object es un objeto opcional. De forma predeterminada, se creará un registrador de nivel INFO en la variable `adobe.target` namespace. Sin embargo, para personalizar el nivel de registro o depurar correctamente cuando se produce un problema, `logger` se puede proporcionar al inicializar el SDK.

El `logger` se espera que el objeto tenga un `debug()` y un `error()` método. Cuando se proporciona un registrador adecuado, [!DNL Target] las solicitudes y respuestas se registrarán.

## Ejemplo

### Python

```python {line-numbers="true"}
logger = logging.getLogger("org.logger")
logger.setLevel(logging.DEBUG)

client_options = {
  "client": "acmeclient",
  "organization_id": "1234567890@AdobeOrg",
  "logger": logger
}
target_client = TargetClient.create(client_options)
```

Debería ver las solicitudes y respuestas que se imprimen en la consola.
