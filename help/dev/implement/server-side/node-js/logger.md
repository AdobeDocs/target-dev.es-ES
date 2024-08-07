---
title: Inicialice el SDK  [!DNL Adobe Target] Node.js para registrar solicitudes
description: Obtenga información sobre cómo registrar solicitudes en el SDK de  [!DNL Adobe Target] Node.js.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# Registrador (Node.js)

## Descripción

Al [inicializar el SDK](initialize-sdk.md), el objeto `options.logger` es un objeto opcional. Sin embargo, para depurar de forma eficaz cuando se produce un problema, se debe proporcionar un objeto `logger` al inicializar el SDK.

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
