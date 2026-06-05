---
title: Implementar la configuración proxy en el SDK  [!DNL Adobe Target] Node.js
description: Aprenda a configurar la configuración proxy [!UICONTROL TargetClient] en el SDK [!DNL Adobe Target] Node.js.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
TQID: https://experienceleague.adobe.com/kaE-ZEOTteaVp5kWSHiVYCvEiHuQHSMqeWRq6r-mJaA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 84
ht-degree: 0%

---

# Configuración de proxy (Node.js)

Para configurar un proxy para las solicitudes HTTP del nodo SDK, anule la API de recuperación utilizada por SDK durante la inicialización.

El siguiente es un ejemplo básico que muestra cómo anular `fetchApi` durante la inicialización de `TargetClient` para agregar un proxy:

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

Tenga en cuenta que esto solo funciona para las versiones de nodo 18.2 o posterior, en las que `undici.fetch` es el `fetch` predeterminado para el nodo.
Visite el [repositorio de muestras de Node SDK](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
para obtener ejemplos de configuración proxy de versiones anteriores del nodo y más información.
