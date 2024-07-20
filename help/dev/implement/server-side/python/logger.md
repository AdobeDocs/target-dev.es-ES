---
title: Inicialice el SDK de  [!DNL Adobe Target] Python para registrar solicitudes
description: Obtenga información sobre cómo registrar solicitudes en el SDK de  [!DNL Adobe Target] Python.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Registrador (Python)

## Descripción

Al [inicializar el SDK](initialize-sdk.md), el objeto `options["logger"]` es un objeto opcional. De forma predeterminada, se creará un registrador de nivel INFO en el espacio de nombres `adobe.target`. Sin embargo, para personalizar el nivel de registro o depurar correctamente cuando se produce un problema, se puede proporcionar un objeto `logger` al inicializar el SDK.

Se espera que el objeto `logger` tenga un método `debug()` y un método `error()`. Cuando se proporcione un registrador apropiado, se registrarán [!DNL Target] solicitudes y respuestas.

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
