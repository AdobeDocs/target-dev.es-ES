---
title: Inicialice el SDK  [!DNL Adobe Target] Node.js para registrar solicitudes
description: Obtenga información sobre cómo registrar solicitudes en el SDK  [!DNL Adobe Target] Node.js.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
TQID: https://experienceleague.adobe.com/tC6xT-eAHOO17h1BK-PwWTBmwg3Dy0Wj8KYrV3W-VR4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 83
ht-degree: 2%

---

# Registrador (Node.js)

## Descripción

Al [inicializar SDK](initialize-sdk.md), el objeto `options.logger` es un objeto opcional. Sin embargo, para depurar correctamente cuando se produce un problema, se debe proporcionar un objeto `logger` al inicializar SDK.

Se espera que el objeto `logger` tenga un método `debug()` y un método `error()`. Cuando se proporcione un registrador apropiado, como `console`, se registrarán [!DNL Target] solicitudes y respuestas.

## Ejemplo

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  logger: console
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
    }
};

const response = await targetClient.getOffers({ request, targetCookie });
```

Debería ver las solicitudes y respuestas que se imprimen en la consola.
