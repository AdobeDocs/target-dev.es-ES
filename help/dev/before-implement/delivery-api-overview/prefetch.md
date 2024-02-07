---
title: Precarga de API de envío de Adobe Target
description: ¿Cómo utilizo la recuperación previa de en [!UICONTROL API de envío de Adobe Target]?
keywords: api de envío
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 803723d95d50cc39101d1646232446fbb0254385
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Precarga

La recuperación previa permite a clientes como aplicaciones móviles y servidores recuperar contenido para varios mboxes o vistas en una solicitud, almacenarlo en la caché local y notificarlo más tarde [!DNL Target] cuando el usuario visita esos mboxes o vistas.

Al utilizar la recuperación previa, es importante estar familiarizado con los siguientes términos:

| Nombre del campo | Descripción |
| --- | --- |
| `prefetch` | Lista de mboxes y vistas que deben recuperarse, pero que no deben marcarse como visitadas. El [!DNL Target] Edge devuelve un valor `eventToke`n para cada mbox o vista que exista en la matriz de recuperación previa. |
| `notifications` | Lista de mboxes y vistas que se recuperaron previamente y que deben marcarse como visitados. |
| `eventToken` | Un token cifrado con hash que se devuelve cuando se recupera previamente el contenido. Este token debe enviarse de vuelta a [!DNL Target] en el `notifications` matriz. |

## Mboxes de recuperación previa

Los clientes, como las aplicaciones y los servidores móviles, pueden recuperar previamente varios mboxes para un usuario determinado dentro de una sesión y almacenarlos en la caché para evitar múltiples llamadas a [!UICONTROL API de envío de Adobe Target].

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
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
    "prefetch": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      },
      {
        "name" : "SummerShoesOffer",
        "index" : 2
      },
      {
        "name" : "SummerDressOffer",
        "index" : 3
      }      
    ]
  }
}'
```

Dentro de `prefetch` , añada uno o más `mboxes` que desee recuperar previamente de a la vez para un usuario dentro de una sesión. Una vez que los haya recuperado previamente. `mboxes` recibirá la siguiente respuesta:

```
{
    "status": 200,
    "requestId": "5efee0d8-3779-4b12-a74e-e04848faf191",
    "client": "demo",
    "id": {
        "tntId": "abcdefghijkl00023.1_1"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "mboxes": [
            {
                "index": 1,
                "name": "SummerOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            }
        ]
    }
}
```

Dentro de la respuesta, verá el `content` campo que contiene la experiencia que se mostrará al usuario en un `mbox`. Esto resulta muy útil cuando se almacena en caché en el servidor, para que cuando un usuario interactúe con la aplicación web o móvil dentro de una sesión y visite un `mbox` en cualquier página concreta de la aplicación, la experiencia se puede entregar desde la caché en lugar de hacer otra [!UICONTROL API de envío de Adobe Target] llamada. Sin embargo, cuando se entrega una experiencia al usuario desde el `mbox`, a `notification` se enviarán mediante una llamada de API de envío para que se registre la impresión. Esto se debe a la respuesta de `prefetch` Las llamadas de se almacenan en caché, lo que significa que el usuario no ha visto las experiencias en el momento de la `prefetch` la llamada se realiza. Para obtener más información sobre `notification` proceso, consulte [Notificaciones](notifications.md).

## Recuperar previamente mboxes con métricas de clickTrack al usar [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics para Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html){target=_blank} (A4T) es una integración de soluciones cruzadas que le permite crear actividades basadas en [!DNL Analytics] métricas de conversión y segmentos de audiencia de.

El siguiente fragmento de código es una respuesta de una recuperación previa de un mbox que contiene `clickTrack` métricas a notificar [!DNL Analytics] que se ha hecho clic en una oferta:

```
{
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "<mboxName>",
        "options": [
           ...
        ],
        "metrics": [
          {
            "type": "click",
            "eventToken": "<eventToken>",
             "analytics": {
               "payload": {
                 "pe": "tnt",
                 "tnta": "..."
               }
             }
          },
          }
        ],
        "analytics": {
          "payload": {
            "pe": "tnt",
            "tnta": "347565:1:0|2,347565:1:0|1"
          }
        }
      }
    ]
  }
}
```

>[!NOTE]
>
>La recuperación previa de un mbox contiene [!DNL Analytics] carga útil solo para actividades cualificadas. La recuperación previa de métricas de éxito para actividades no calificadas aún provoca incoherencias en los informes.

## Recuperar vistas previamente

SPA Las vistas admiten aplicaciones de una sola página () y aplicaciones móviles de forma más fluida. SPA Las vistas se pueden ver como un grupo lógico de elementos visuales que, juntos, constituyen una experiencia de visualización o una experiencia móvil de un usuario o una experiencia móvil de un usuario. Ahora, a través de la API de entrega, VEC crea actividades AB y XT con modificaciones en [SPA Vistas para la](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) ahora se puede recuperar previamente.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=a3e7368c62d944c0855d424cd7a03ab0' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "window": {
      "width": 1819,
      "height": 842
    },
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "prefetch": {
    "views": [{}]
  }
}'
```

SPA La llamada de ejemplo anterior recuperará previamente todas las vistas creadas mediante el VEC de para actividades AB y XT que se mostrarán para la web `channel`. Observe en la llamada que queremos recuperar previamente todas las vistas de las actividades AB o XT con las que trabaja un visitante `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` que está visitando el `url`:`https://target.enablementadobe.com/react/demo/#/` es apto para.

```
{
    "status": 200,
    "requestId": "14ce028e-d2d2-4504-b3da-32740fa8dd61",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "views": [
            {
                "id": 228,
                "name": "checkout-express",
                "key": "checkout-express",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV:nth-of-type(1) > DIV.mb-3:eq(2)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > FORM:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(3)",
                                "content": "<span style=\"color:#000080;\"><strong>*We charge an additional fee of $12.34 for faster delivery. If you choose express delivery get 15% off on your next order.</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 5,
                "name": "home",
                "key": "home",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
                                "content": "<span style=\"color:#800000;\"><strong>Trending Items</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 6,
                "name": "products",
                "key": "products",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setStyle",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > DIV.heading:eq(0) > BUTTON.btn:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > BUTTON:nth-of-type(1)",
                                "content": {
                                    "background-color": "rgba(191,0,0,1)",
                                    "priority": "important"
                                }
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            }
        ]
    }
}
```

En el `content` campos de la respuesta, observe metadatos como `type`, `selector`, `cssSelector`, y `content`, que se utilizan para presentar la experiencia al usuario final cuando este visita la página. Tenga en cuenta que la variable `prefetched` el contenido se puede almacenar en caché y procesar para el usuario cuando sea necesario.
