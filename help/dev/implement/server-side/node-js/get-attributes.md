---
title: Cómo utilizar solicitudes asincrónicas en [!DNL Adobe Target] SDK de Node.js
description: Descubra cómo [!DNL Target] El SDK de Node.js admite solicitudes asincrónicas, lo que puede reducir el tiempo de destino efectivo a cero.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 18%

---

# Obtener atributos (Node.js)

## Descripción

`[!UICONTROL getAttributes()]` se utiliza para recuperar experimentación y experiencias personalizadas de [!DNL Target] y extraer valores de atributo.

## Método

### getAttributes

```js {line-numbers="true"}
TargetClient.getAttributes(mboxNames: Array, options: Object): Promise
```

## Parámetros

| Nombre | Tipo | Requerido | Valor predeterminado |
| --- | --- | --- |--- |
| mboxNames | Matriz | Sí | Ninguna |
| opciones | Objeto | No | Ninguna |

## Promesa

El `Promise` devuelto por `TargetClient.getAttributes()` resuelve un objeto con los métodos siguientes:

| Método | Tipo de devolución | Descripción |
| --- | --- | --- |
| getValue(mboxName, key) | Cualquiera | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| asObject(mboxName) | Objeto | Devuelve un objeto json simple con pares de valor clave |
| getResponse() | [Respuesta de getOffers](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | Devuelve el objeto de respuesta normalmente devuelto por `getOffers` |

## Ejemplo

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);
const offerAttributes = await targetClient.getAttributes(["demo-engineering-flags"]);


//returns just the value of searchProviderId from the mbox offer
const searchProviderId = offerAttributes.getValue("demo-engineering-flags", "searchProviderId");

//returns a simple JSON object representing the mbox offer
const engineeringFlags = offerAttributes.asObject("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

const assetUrl = `http://${engineeringFlags.cdnHostname}/path/to/asset`;
```
