---
title: Suscribirse a eventos en el SDK  [!DNL Adobe Target] Node.js
description: Obtenga información sobre cómo suscribirse a varios eventos que se producen en el SDK de Node.js mediante el objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---

# Eventos de SDK (Node.js)

## Descripción

Al [inicializar SDK](initialize-sdk.md), el objeto `options.events` es un objeto opcional con claves de nombre de evento y valores de función de devolución de llamada. Se puede utilizar para suscribirse a varios eventos que se producen dentro de SDK. Por ejemplo, el evento `clientReady` se puede usar con una función de devolución de llamada que se invocará cuando SDK esté listo para las llamadas de método.

Cuando se llama a la función de llamada de retorno, se pasa un objeto de evento. Cada evento tiene un `type` correspondiente al nombre del evento. Algunos eventos incluyen propiedades adicionales con información pertinente.

## Solicitud

| Nombre del evento (tipo) | Descripción | Propiedades de evento adicionales |
| --- | --- | --- |
| clientReady | Se emite cuando el artefacto se ha descargado y el SDK está listo para `getOffers` llamadas. Se recomienda cuando se utiliza el método de toma de decisiones en el dispositivo. |  |
| artifactDownloadSucceeded | Se emite cada vez que se descarga un nuevo artefacto. | artifactPayload, artifactLocation |
| artifactDownloadFailed | Se emite cada vez que un artefacto no se puede descargar. | artifactLocation, error |

## Ejemplo

### Node.js

```js {line-numbers="true"}
const targetClient = TargetClient.create({
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device",
    events: {
        clientReady: onTargetClientReady,
        artifactDownloadSucceeded: onArtifactDownloadSucceeded,
        artifactDownloadFailed: onArtifactDownloadFailed
    }
});

function onTargetClientReady() {
    // make getOffers requests
    targetClient.getOffers({...})            
}

function onArtifactDownloadSucceeded(event) {
    console.log(`The artifact was successfully downloaded from '${event.artifactLocation}'`);
    // optionally do something with event.artifactPayload, like persist it
}

function onArtifactDownloadFailed(event) {
    console.log(`The artifact failed to download from '${event.artifactLocation}' with the following error message: ${event.error.message}`);
}
```
