---
title: Implemente la configuración proxy en [!DNL Adobe Target] SDK de Node.js
description: Obtenga información sobre cómo configurar el [!UICONTROL TargetClient] configuración de proxy en [!DNL Adobe Target] SDK de Node.js.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Configuración de proxy (Node.js)

Para configurar un proxy para las solicitudes HTTP del SDK del nodo, anule la API de recuperación utilizada por el SDK durante la inicialización.

El siguiente es un ejemplo básico que muestra cómo anular `fetchApi` durante la `TargetClient` inicialización para añadir un proxy:

```javascript {line-numbers="true"}
const { ProxyAgent } = require("undici");

const proxyAgent = new ProxyAgent("your proxy address here");

const fetchImpl = (url, options) => {
  const fetchOptions = options;
  fetchOptions.dispatcher = proxyAgent;
  return fetch(url, fetchOptions);
};

client = TargetClient.create({
    ...,
    fetchApi: fetchImpl
});
```

Tenga en cuenta que esto solo funciona para las versiones de nodo 18.2+, en las que `undici.fetch` es el valor predeterminado `fetch` para el nodo.
Visite la [Repositorio de ejemplos del SDK de nodos](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
para obtener ejemplos de configuración proxy de versiones anteriores del nodo y más información.
