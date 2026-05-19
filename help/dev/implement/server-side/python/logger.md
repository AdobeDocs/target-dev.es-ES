---
title: Inicialice  [!DNL Adobe Target] Python SDK para registrar solicitudes
description: Aprenda a registrar solicitudes en  [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
TQID: https://experienceleague.adobe.com/9LSln8V3QIG9GTok2yTTnKvhlpQhaed3a-qJyA4jErg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 97
ht-degree: 3%

---

# Registrador (Python)

## Descripción

Al [inicializar SDK](initialize-sdk.md), el objeto `options["logger"]` es un objeto opcional. De forma predeterminada, se creará un registrador de nivel INFO en el espacio de nombres `adobe.target`. Sin embargo, para personalizar el nivel de registro o depurar de forma eficaz cuando se produce un problema, se puede proporcionar un objeto `logger` al inicializar SDK.

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
