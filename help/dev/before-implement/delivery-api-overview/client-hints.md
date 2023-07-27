---
title: Sugerencias del cliente de API de envío de Adobe Target
description: ¿Cómo utilizo Client Hints en la [!DNL Adobe Target] ¿API de envío?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Client Hints y la [!UICONTROL API de envío de Adobe Target]

Las Client Hints deben enviarse a [!DNL Adobe Target] en la solicitud de ofertas.

Por lo general, se recomienda enviar todas las Client Hints disponibles a [!DNL Target]. Para obtener más información, consulte [User-agent y Client Hints](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) en el [Implementación de cliente](../../implement/client-side/overview.md) sección.

## Llamadas directas de API de envío

### Desde el explorador

En este caso, el explorador enviará Client Hints de baja entropía a [!DNL Target] automáticamente mediante encabezados de solicitud. Sin embargo, existen un par de limitaciones a nivel de explorador con esta implementación. Primero: no se enviarán encabezados de Client Hints desde el explorador a menos que se realice la solicitud a través de https. Segundo: las Client Hints no se enviarán en la primera solicitud a [!DNL Target] en la página. Los encabezados de Client Hints solo se enviarán en la segunda solicitud y todas las solicitudes a partir de entonces. Esto significa que la segmentación y personalización de audiencias no pueden ser realizadas por [!DNL Target] en la primera visita a la página. Para evitar ambas limitaciones, recomendamos encarecidamente utilizar la API de sugerencias del cliente del agente de usuario en el explorador para recopilar las sugerencias del cliente directamente y enviarlas en la carga útil de solicitud.

### Desde un servidor

En este caso, las Client Hints deben reenviarse manualmente desde el explorador a [!DNL Target] en la solicitud de API de envío.

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
