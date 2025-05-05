---
title: Notificaciones de API de envío de Adobe Target
description: ¿Cómo se activan las notificaciones mediante [!UICONTROL Adobe Target Delivery API]?
keywords: api de envío
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Notificaciones

Las notificaciones deben activarse cuando se ha visitado o procesado un mbox o una vista de recuperación previa para el usuario final.

Para que las notificaciones se activen en el mbox o la vista correctos, asegúrese de realizar un seguimiento de `eventToken` correspondiente para cada mbox o vista. Es necesario activar las notificaciones con el `eventToken` correcto para los mboxes o vistas correspondientes para que los informes se reflejen correctamente.

## Notificaciones para mboxes de recuperación previa

Se pueden enviar una o varias notificaciones a través de una sola llamada de envío. Determine si la métrica de la que debe realizarse el seguimiento es un `click` o `display` para cada mbox para que el `type` de la notificación se pueda reflejar correctamente. Además, pase un `id` por cada notificación para que se pueda determinar si una notificación se envió correctamente a través de [!UICONTROL &#x200B; Adobe Target Delivery API]. `timestamp` también es importante que se reenvíe a [!DNL Target] para indicar cuándo se produjo `click` o `display` en un mbox determinado con fines de creación de informes.

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
    "id": {
      "tntId": "abcdefghijkl00023.1_1"
    },
    "context": {
      "channel": "web",
      "browser" : {
        "host" : "demo"
      },
      "address" : {
        "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
      },
      "screen" : {
        "width" : 1200,
        "height": 1400
      }
    },
      "notifications": [
      {
      "id" : "SummerOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerShoesOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerShoesOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerDressOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerDressOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
    } 
    ]
  }'
```

La llamada de ejemplo anterior dará como resultado una respuesta que indica que la solicitud `notifications` se procesó correctamente.

```
{
  "status": 200,
  "requestId": "36014eed-4772-4c48-a9e2-e532762b6a85",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "notifications": [
      {
          "id": "SummerOfferNotification"
      },
      {
          "id": "SummerDressOfferNotification"
      },
      {
          "id": "SummerShoesOfferNotification"
      }
  ]
}
```

Si todos los `notifications` enviados a [!DNL Target] se procesan correctamente, aparecerán en la matriz `notifications` de la respuesta. Sin embargo, si falta `notifications` `id`, ese(a) `notification` en particular no se realizó. En este escenario, se podría establecer una lógica de reintento hasta que se recupere una respuesta correcta `notification`. Asegúrese de que la lógica de reintentos tenga un tiempo de espera especificado para que la llamada de API no se bloquee y cause retrasos de rendimiento.

## Notificaciones para vistas recuperadas previamente

Se pueden enviar una o varias notificaciones a través de una sola llamada de envío. Determine si la métrica de la que debe realizarse el seguimiento es `click` o `display` para cada mbox para que el tipo de notificación se pueda reflejar correctamente. Además, pase un `id` por cada notificación para que se pueda determinar si una notificación se envió correctamente a través de [!UICONTROL Adobe Target Delivery API]. La marca de tiempo también es importante para reenviarse a [!DNL Target] a fin de indicar cuándo se produjo `click` o `display` en una vista determinada con fines de generación de informes.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "notifications": [{
      "id": "228",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "checkout-express",
      }
    },
    {
      "id": "5",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "home",
      }
    },
    {
      "id": "6",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "products",
      }
    }
  ]
}'
```

La llamada de ejemplo anterior dará como resultado una respuesta que indica que la solicitud `notifications` se procesó correctamente.

```
{
    "status": 200,
    "requestId": "85cc7394-c19a-4398-9b8b-bbee1e4c4579",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "notifications": [
        {
            "id": "5"
        },
        {
            "id": "6"
        },
        {
            "id": "228"
        }
    ]
}
```

Si todos los `notifications` enviados a [!DNL Target] se procesan correctamente, aparecerán en la matriz `notifications` de la respuesta. Sin embargo, si falta un(a) `notifications` `id`, esa notificación en particular no se realizó. En esta situación, se podría establecer una lógica de reintento hasta que se recupere una respuesta de notificación correcta. Asegúrese de que la lógica de reintentos tenga un tiempo de espera especificado para que la llamada de API no se bloquee y cause retrasos de rendimiento.
