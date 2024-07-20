---
title: API de envío de Adobe Target que identifica visitantes
description: ¿Cómo puedo identificar al usuario dentro de  [!DNL Adobe Target]?
keywords: api de envío
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 7%

---

# Identificación de visitantes

Existen varias maneras de identificar a un visitante dentro de [!DNL Adobe Target].

Target utiliza tres identificadores:

| Nombre del campo | Descripción |
| --- | --- |
| `tntId` | `tntId` es el identificador principal de [!DNL Target] para un usuario. Puede proporcionar este identificador o [!DNL Target] lo generará automáticamente si la solicitud no contiene uno. |
| `thirdPartyId` | El `thirdPartyId` es el identificador de su compañía para el usuario que puede enviar con cada llamada. Cuando un usuario inicia sesión en el sitio de una empresa, esta generalmente crea un ID vinculado a la cuenta del visitante, la tarjeta de fidelidad, el número de pertenencia u otros identificadores aplicables para esa empresa. |
| `marketingCloudVisitorId` | `marketingCloudVisitorId` se usa para combinar y compartir datos entre distintas soluciones de Adobe. Se requiere `marketingCloudVisitorId` para las integraciones con Adobe Analytics y Adobe Audience Manager. |
| `customerIds` | Junto con la ID de visitante Experience Cloud, se pueden usar [ID de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) adicionales y un estado autenticado para cada visitante. |

## [!DNL Target] ID

El identificador [!DNL Target] o `tntId` se puede ver como un identificador de dispositivo. [!DNL Target] genera automáticamente este(a) `tntId` si no se proporciona(n) en la solicitud. A partir de entonces, las solicitudes posteriores deberán incluir este(a) `tntId` para que se entregue el contenido adecuado a un dispositivo utilizado por el usuario.

```http {line-numbers="true"}
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

La llamada de ejemplo anterior demuestra que no es necesario pasar un `tntId`. En este escenario, [!DNL Target] genera un `tntId` y lo proporciona en la respuesta, como se muestra a continuación:

```URI {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "demo",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  ...
}
```

El `tntId` generado es `10abf6304b2714215b1fd39a870f01afc.28_20`. Tenga en cuenta que este(a) `tntId` debe usarse al llamar al [!UICONTROL Adobe Target Delivery API] para el mismo usuario en varias sesiones.

## ID de visitante de Marketing Cloud

`marketingCloudVisitorId` es un identificador universal y persistente que identifica a los visitantes en todas las soluciones del Experience Cloud. Cuando su organización implementa el servicio de ID, este ID le permite identificar el mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud como Adobe Target, Adobe Analytics o Adobe Audience Manager. Tenga en cuenta que `marketingCloudVisitorId` es necesario al aprovechar e integrar con Analytics y Audience Manager.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "marketingCloudVisitorId": "10527837386392355901041112038610706884"
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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

La llamada de ejemplo anterior muestra cómo se pasa a Adobe Target un(a) `marketingCloudVisitorId` que se recuperó del servicio de ID de Experience Cloud. En este escenario, [!DNL Target] genera un `tntId`, ya que no se pasó a la llamada original, que se asignará al `marketingCloudVisitorId` proporcionado, tal como se ve en la respuesta siguiente.

## ID de terceros

Si su organización utiliza un ID para identificar a su visitante, puede usar `thirdPartyID` para entregar contenido. Sin embargo, debe proporcionar `thirdPartyID` por cada [!UICONTROL Adobe Target Delivery API] llamada que realice.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "thirdPartyId": "B234A029348"
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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

La llamada de ejemplo anterior muestra un `thirdPartyId`, que es un ID persistente que su empresa utiliza para identificar a un usuario final, independientemente de si está interactuando con su empresa desde canales web, móviles o de IoT. En otras palabras, `thirdPartyId` hará referencia a los datos de perfil de usuario que se pueden utilizar en todos los canales. En este escenario, [!DNL Target] genera un `tntId`, ya que no se pasó a la llamada original, que se asignará al `thirdPartyId` proporcionado tal como se ve en la respuesta siguiente.

```
{
    "status": 200,
    "requestId": "55de9886-bd14-4dee-819c-7d1633b79b90",
    "client": "demo",
    "id": {
        "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20",
        "thirdPartyId": "B234A029348"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    ...
}
```

## Customer ID

[Los ID de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) se pueden agregar y asociar con un ID de visitante de Experience Cloud. Siempre que se envíe `customerIds`, también se debe proporcionar `marketingCloudVisitorId`. Además, se puede proporcionar un estado de autenticación junto con cada `customerId` para cada visitante. Se puede tener en cuenta el siguiente estado de autenticación:

| Estado de autenticación | Estado de usuario |
| --- | --- |
| `unknown` | Desconocido o nunca autenticado. Este estado se puede utilizar para escenarios como un visitante que ha aterrizado en el sitio haciendo clic en un anuncio en pantalla. |
| `authenticated` | El usuario está autenticado con una sesión activa en su sitio web o aplicación. |
| `logged_out` | El usuario estaba autenticado pero ha cerrado sesión activamente. El usuario quería desconectarse del estado autenticado. El usuario ya no quiere que se le trate como autenticado. |

Tenga en cuenta que solo cuando el ID de cliente está en estado `authenticated` Target hará referencia a los datos de perfil de usuario almacenados y vinculados al ID de cliente. Si el ID del cliente tiene el estado `unknown` o `logged_out`, se omitirá el ID de cliente y los datos de perfil de usuario que se puedan asociar a él no se aprovecharán para la segmentación de audiencia.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "customerIds": [{
          "id": "134325423",
          "integrationCode" : "crm_data",
          "authenticatedState" : "authenticated"
        }]
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
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

La llamada de ejemplo anterior muestra cómo enviar un(a) `customerId` con un(a) `authenticatedState`. Al enviar un `customerId`, se requieren `integrationCode`, `id` y `authenticatedState`, así como `marketingCloudVisitorId`. `integrationCode` es el alias del [archivo de atributos del cliente](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=es) que usted proporcionó a través de CRS.

## Perfil combinado

Puede combinar `tntId`, `thirdPartyID` y `marketingCloudVisitorId` en la misma solicitud. En esta situación, Adobe Target mantendrá la asignación de todos estos ID y los anclará a un visitante. Descubra cómo se combinan y sincronizan los perfiles [en tiempo real](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) con los diferentes identificadores.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "tntId": "d359234570e044f14e1faeeba02d6ab23439914e.28_78",
        "thirdPartyId":"23423432"
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

La llamada de ejemplo anterior muestra cómo se puede combinar `tntId`, `thirdPartyID` y `marketingCloudVisitorId` en la misma solicitud. Los tres ID también se devuelven en la respuesta.
