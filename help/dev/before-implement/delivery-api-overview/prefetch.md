---
title: Precarga de API de envío de Adobe Target
description: ¿Cómo se usa la recuperación previa en [!UICONTROL Adobe Target Delivery API]?
keywords: api de envío
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 4ff2746b8b485fe3d845337f06b5b0c1c8d411ad
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Precarga

La recuperación previa permite a clientes como aplicaciones móviles y servidores recuperar contenido para varios mboxes o vistas en una solicitud, almacenarlo en la caché local y, posteriormente, notificar a [!DNL Target] cuando el visitante visite esos mboxes o vistas.

Al utilizar la recuperación previa, es importante estar familiarizado con los siguientes términos:

| Nombre del campo | Descripción |
| --- | --- |
| `prefetch` | Lista de mboxes y vistas que deben recuperarse, pero que no deben marcarse como visitadas. El Edge [!DNL Target] devuelve un `eventToken` para cada mbox o vista que exista en la matriz de recuperación previa. |
| `notifications` | Lista de mboxes y vistas que se recuperaron previamente y que deben marcarse como visitados. |
| `eventToken` | Un token cifrado con hash que se devuelve cuando se recupera previamente el contenido. Este token debe enviarse a [!DNL Target] en la matriz `notifications`. |

## Mboxes de recuperación previa

Los clientes, como las aplicaciones móviles y los servidores, pueden recuperar previamente varios mboxes para un visitante determinado dentro de una sesión y almacenarlos en la caché para evitar múltiples llamadas a [!UICONTROL Adobe Target Delivery API].

```shell shell-session
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

Dentro del campo `prefetch`, agregue uno o más `mboxes` que quiera recuperar previamente al menos una vez para un visitante dentro de una sesión. Después de recuperar previamente esos `mboxes`, recibe la siguiente respuesta:

```JSON {line-numbers="true"}
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

Dentro de la respuesta, verá el campo `content` que contiene la experiencia que se mostrará al visitante en relación con un(a) `mbox` determinado(a). Esto es muy útil cuando se almacena en caché en el servidor para que cuando un visitante interactúe con su aplicación web o móvil en una sesión y visite un(a) `mbox` en cualquier página particular de su aplicación, la experiencia se pueda entregar desde la caché en lugar de realizar otra llamada de [!UICONTROL Adobe Target Delivery API]. Sin embargo, cuando se entrega una experiencia al visitante desde `mbox`, se envía un `notification` a través de una llamada de API de entrega para que se produzca el registro de impresiones. Esto se debe a que la respuesta de `prefetch` llamadas se almacena en caché, lo que significa que el visitante no ha visto las experiencias en el momento en que se produce la llamada a `prefetch`. Para obtener más información acerca del proceso `notification`, consulte [Notificaciones](notifications.md).

## Recuperar previamente mboxes con métricas `clickTrack` al usar [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics for Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es){target=_blank} (A4T) es una integración de soluciones cruzadas que le permite crear actividades basadas en [!DNL Analytics] métricas de conversión y segmentos de audiencia.

El siguiente fragmento de código es una respuesta de una recuperación previa de un mbox que contiene `clickTrack` métricas para notificar a [!DNL Analytics] que se hizo clic en una oferta:

```JSON {line-numbers="true"}
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
>La recuperación previa de un mbox contiene la carga útil [!DNL Analytics] solo para actividades calificadas. La recuperación previa de métricas de éxito para actividades no calificadas aún provoca incoherencias en los informes.

## Recuperar vistas previamente

SPA Las vistas admiten aplicaciones de una sola página () y aplicaciones móviles de forma más fluida. SPA Las vistas se pueden ver como un grupo lógico de elementos visuales que, juntos, constituyen una experiencia de visualización o una experiencia móvil de un usuario o una experiencia móvil de un usuario. SPA Ahora, a través de la API de entrega, se pueden recuperar previamente las actividades [[!UICONTROL A/B Test]](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=es){target=_blank} y [[!UICONTROL Experience Targeting]](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=es){target=_blank} (X)T creadas por VEC con modificaciones en [Vistas para el](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

```shell  {line-numbers="true"}
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

SPA La llamada de ejemplo anterior recupera previamente todas las vistas creadas a través del VEC de para las actividades [!UICONTROL A/B Test] y XT que se mostrarán en la web `channel`. Observe que la llamada recupera previamente todas las vistas de las actividades [!UICONTROL A/B Test] o XT para las que califica un visitante con `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` que visita `url`:`https://target.enablementadobe.com/react/demo/#/`.

```JSON  {line-numbers="true"}
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

En los campos `content` de la respuesta, anote metadatos como `type`, `selector`, `cssSelector` y `content`, que se utilizan para representar la experiencia en el visitante cuando un usuario visita su página. Tenga en cuenta que el contenido de `prefetched` se puede almacenar en caché y representar para el usuario cuando sea necesario.
