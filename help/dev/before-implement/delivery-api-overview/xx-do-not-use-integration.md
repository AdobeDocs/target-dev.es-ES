---
title: Integración con Experience Cloud
description: Integración con Experience Cloud
keywords: api de envío
source-git-commit: f16903556954d2b1854acd429f60fbf6fc2920de
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 7%

---

<!-- The content on this page was originally pulled from the legacy Delivery API doc site, and was subsequently found to be an outdated version of information now found on [Implement > Server-side > Integration > A4T Reporting](../../implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md) and [Implement > Server-side > Integration > AAM Segments](../../implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md). Therefore sunsetting this page, but not deleting it from the repo immediately, pending a more thorough examination to avoid inadvertently deleting relevant content. -->


# Integración con Experience Cloud

## Adobe Analytics for Target (A4T)

Cuando se activa una llamada a la API de envío de Target desde el servidor, Adobe Target devuelve la experiencia de ese usuario y, además de eso, Adobe Target devuelve la carga útil de Adobe Analytics al que llama o la reenvía automáticamente a Adobe Analytics. Para enviar información de actividad de Target a Adobe Analytics en el servidor, hay que cumplir algunos requisitos previos:

1. La actividad se configura en la IU de Adobe Target con Adobe Analytics como fuente de informes y las cuentas están habilitadas para A4T
1. El ID de visitante de Adobe Marketing Cloud lo genera el usuario de la API y está disponible cuando se activa la llamada a la API de envío de Target

### Adobe Target reenvía automáticamente la carga útil de Analytics

Adobe Target puede reenviar automáticamente la carga útil de Analytics a Adobe Analytics a través del servidor si se proporcionan los siguientes identificadores:

1. `supplementalDataId`: el ID que se utiliza para unir Adobe Analytics y Adobe Target
1. `trackingServer`: el servidor de Adobe Analytics Para que Adobe Target y Adobe Analytics unan correctamente los datos, es necesario pasar el mismo `supplementalDataId` a Adobe Target y a Adobe Analytics.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "supplementalDataId" : "23423498732598234",
          "trackingServer": "ags041.sc.omtrdc.net",
          "logging": "server_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

### Recuperar carga útil de Analytics de Adobe Target

Los consumidores de la API de envío de Adobe Target pueden recuperar la carga útil de Adobe Analytics para un mbox correspondiente, de modo que el consumidor pueda enviar la carga útil a Adobe Analytics mediante la [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Cuando se activa una llamada de Adobe Target del lado del servidor, pase `client_side` al campo `logging` en la solicitud. A su vez, esto devolverá una carga útil si el mbox está presente en una actividad que utiliza Analytics como fuente de informes.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "logging": "client_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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

Una vez que haya especificado `logging` = `client_side`, recibirá la carga útil en el campo `mbox` como se muestra a continuación.

```
{
    "status": 200,
    "requestId": "4b8855a5-8354-4ac4-8ae7-c551f7c0bb8a",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",

                    }
                ],
                "analytics": {
                    "payload": {
                        "pe": "tnt",
                        "tnta": "285408:0:0|2"
                    }
                }
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>",
                        "type": "html",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>",
                        "type": "html",
                    }
                ]
            }
        ]
    }
}
```

Si la respuesta de Target contiene algo en la propiedad `analytics` -> `payload`, reenvíela tal cual a Adobe Analytics. Analytics sabe cómo procesar esta carga útil. Esto se puede hacer en una solicitud de GET con el siguiente formato:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Parámetros y variables de cadena de consulta

| Nombre del campo | Requerido | Descripción |
| --- | --- | --- |
| `rsid` | Sí | La ID del grupo de informes |
| `pe` | Sí | Evento de página. Siempre establecido en `tnt` |
| `tnta` | Sí | Carga útil de Analytics devuelta por el servidor de Target en `analytics` -> `payload` -> `tnta` |
| `mid` | ID de visitante de Marketing Cloud |

### Valores de encabezado obligatorios

| Nombre del encabezado | Valor del encabezado |
| --- | --- |
| Host | Servidor de recopilación de datos de Analytics (p. ej.: adobeags421.sc.omtrdc.net) |

### Ejemplo de llamada de obtención HTTP de inserción de datos de A4T

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```

## Adobe Audience Manager

Los segmentos de Adobe Audience Manager AAM () también se pueden aprovechar mediante las API de envío de Adobe Target. AAM Para aprovechar los segmentos de, se deben proporcionar los siguientes campos:

| Nombre del campo | Requerido | Descripción |
| --- | --- | --- |
| `locationHint` | Sí | AAM Sugerencia de ubicación DCS se utiliza para determinar qué extremo de DCS de DCS de DCS se visita para recuperar el perfil. Debe ser >= 1. |
| `marketingCloudVisitorId` | Sí | ID de visitante de Marketing Cloud |
| `blob` | Sí | AAM AAM Se utiliza un blob de para enviar datos adicionales a los usuarios de la aplicación de correo electrónico No debe estar en blanco y tener un tamaño &lt;= 1024. |

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "audienceManager": {
          "locationHint": 9,
          "blob": "32fdghkjh34kj5h43"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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
