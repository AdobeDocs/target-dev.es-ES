---
title: Sugerencias del cliente de API de envío de Adobe Target
description: ¿Cómo utilizo Client Hints en la API de  [!DNL Adobe Target] envío?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/ijbOsWitZdNHpjNduh8xtPyEYdw2tsWz2rB6jZ5JbQA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094id: ff2b9b37-92e0-45fc-b853-379d44c08c89
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 282
ht-degree: 0%

---

# Sugerencias del cliente y la [!UICONTROL API de envío de Adobe Target]

Las Client Hints deben enviarse a [!DNL Adobe Target] en la solicitud de ofertas.

En general, se recomienda enviar todas las Client Hints disponibles a [!DNL Target]. Para obtener más información, consulte [User-agent y Client Hints](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) en la sección [Implementación del lado del cliente](../../implement/client-side/overview.md).

## Llamadas directas de API de envío

### Desde el explorador

En este caso, el explorador enviará Client Hints de baja entropía a [!DNL Target] automáticamente a través de encabezados de solicitud. Sin embargo, existen un par de limitaciones a nivel de explorador con esta implementación. Primero: no se enviarán encabezados de Client Hints desde el explorador a menos que se realice la solicitud a través de https. Segundo: las Client Hints no se enviarán en la primera solicitud a [!DNL Target] en la página. Los encabezados de Client Hints solo se enviarán en la segunda solicitud y todas las solicitudes a partir de entonces. Esto significa que [!DNL Target] no puede realizar la segmentación y personalización de audiencias en la primera visita a la página. Para evitar ambas limitaciones, recomendamos encarecidamente utilizar la API de sugerencias del cliente del agente de usuario en el explorador para recopilar las sugerencias del cliente directamente y enviarlas en la carga útil de solicitud.

### Desde un servidor

En este caso, las Client Hints deben reenviarse manualmente desde el explorador a [!DNL Target] en la solicitud de API de entrega.

```
curl -X POST 'http://mboxedge28.tt.omtrdc.net/rest/v1/delivery?client=myClientCode&sessionId=abcdefghijkl00014' -d '{
  "context": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36",
    "clientHints": {
      "Sec-CH-UA-Model": "iPhone",
      "Sec-CH-UA-Mobile": true,
      "Sec-CH-UA-Platform": "iOS",
      "Sec-CH-UA": "[ { \"brand\": \"Chromium\", \"version\": \"91\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99\" } ]",
      "Sec-CH-UA-Full-Version-List": "[ { \"brand\": \"Chromium\", \"version\": \"91.1.1.1\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99.1.1.1\" } ]",
      "Sec-CH-UA-Platform-Version": "10.0.0",
      "Sec-CH-UA-Arch": "x86",
      "Sec-CH-UA-Bitness": "64"
    }
  },
  "execute": {
    "mboxes": [{
      "name": "home",
      "index": 1
    }]
  }
}'
```

## Formato

Los encabezados Sec-CH-UA y Sec-CH-UA-Full-Version-List de Client Hints tienen un formato diferente al de los resultados de la API del explorador de Client Hints (navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues). La API de entrega acepta ambos formatos. La API de entrega normaliza los valores en el formato utilizado en los encabezados de solicitud, lo que es importante tener en cuenta al acceder a Client Hints en los scripts de perfil.
