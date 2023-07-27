---
title: API de envío de Adobe Target que identifica visitantes
description: ¿Cómo puedo identificar a un usuario dentro de? [!DNL Adobe Target]?
keywords: api de envío
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 9%

---

# Identificación de visitantes

Existen varias formas de identificar a un visitante en [!DNL Adobe Target].

Target utiliza tres identificadores:

| Nombre del campo | Descripción |
| --- | --- |
| `tntId` | El `tntId` es el identificador principal de [!DNL Target] para un usuario. Puede proporcionar este ID o [!DNL Target] La generará automáticamente si la solicitud no contiene ninguna. |
| `thirdPartyId` | El `thirdPartyId` es el identificador de su empresa del usuario que puede enviar con cada llamada. Cuando un usuario inicia sesión en el sitio de una empresa, esta generalmente crea un ID vinculado a la cuenta del visitante, la tarjeta de fidelidad, el número de pertenencia u otros identificadores aplicables para esa empresa. |
| `marketingCloudVisitorId` | El `marketingCloudVisitorId` se utiliza para combinar y compartir datos entre distintas soluciones de Adobe. El `marketingCloudVisitorId` es necesario para las integraciones con Adobe Analytics y Adobe Audience Manager. |
| `customerIds` | Junto con el ID de visitante de Experience Cloud, se [ID de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) y se puede utilizar un estado autenticado para cada visitante. |

## [!DNL Target] ID

El [!DNL Target] ID o `tntId` puede verse como un ID de dispositivo. Esta `tntId` se genera automáticamente mediante [!DNL Target] si no se proporciona en la solicitud. A partir de entonces, las solicitudes posteriores deben incluir esto `tntId` para que el contenido correcto se envíe a un dispositivo utilizado por el usuario.

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

La llamada de ejemplo anterior demuestra que un `tntId` no necesita que se pase. En este escenario, [!DNL Target]  genera un `tntId` y proporciónelo en la respuesta, como se muestra a continuación:

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

El generado `tntId` es `10abf6304b2714215b1fd39a870f01afc.28_20`. Tenga en cuenta esto `tntId` necesita utilizarse al llamar a la función [!UICONTROL API de envío de Adobe Target] para el mismo usuario entre sesiones.

## ID de visitante de Marketing Cloud

El `marketingCloudVisitorId` es un ID universal y persistente que identifica a los visitantes en todas las soluciones del Experience Cloud. Cuando su organización implementa el servicio de ID, este ID le permite identificar el mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud como Adobe Target, Adobe Analytics o Adobe Audience Manager. Tenga en cuenta que las `marketingCloudVisitorId` es necesario al aprovechar e integrar con Analytics y Audience Manager.

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

La llamada de ejemplo anterior muestra cómo `marketingCloudVisitorId` que se recuperó del servicio de ID de Experience Cloud se pasa a Adobe Target. En este escenario, [!DNL Target] genera un `tntId` ya que no se pasó a la llamada original, que se asignará a la proporcionada `marketingCloudVisitorId` como se observa en la respuesta que figura a continuación.

## ID de terceros

Si su organización utiliza un ID para identificar a su visitante, puede utilizar `thirdPartyID` para entregar contenido. Sin embargo, debe proporcionar la variable `thirdPartyID` para cada [!UICONTROL API de envío de Adobe Target] Llamada que haces.

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

La llamada de ejemplo anterior muestra un `thirdPartyId`, que es un ID persistente que su empresa utiliza para identificar a un usuario final, independientemente de si está interactuando con su empresa desde canales web, móviles o de IoT. En otras palabras, la variable `thirdPartyId` hará referencia a los datos de perfil de usuario que se pueden utilizar en todos los canales. En este escenario, [!DNL Target] genera un `tntId`, ya que no se pasó a la llamada original, que se asignará a la proporcionada `thirdPartyId` como se observa en la respuesta que figura a continuación.

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

[ID de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) se puede agregar y asociar con un ID de visitante de Experience Cloud. Siempre que envíe `customerIds` el `marketingCloudVisitorId` también debe proporcionarse. Además, se puede proporcionar un estado de autenticación junto con cada `customerId` para cada visitante. Se puede tener en cuenta el siguiente estado de autenticación:

| Estado de autenticación | Estado de usuario |
| --- | --- |
| `unknown` | Desconocido o nunca autenticado. Este estado se puede utilizar para escenarios como un visitante que ha aterrizado en el sitio haciendo clic en un anuncio en pantalla. |
| `authenticated` | El usuario está autenticado con una sesión activa en su sitio web o aplicación. |
| `logged_out` | El usuario estaba autenticado pero ha cerrado sesión activamente. El usuario quería desconectarse del estado autenticado. El usuario ya no quiere que se le trate como autenticado. |

Tenga en cuenta que solo cuando el ID de cliente está en `authenticated` El estado hará referencia a los datos de perfil de usuario almacenados y vinculados al id de cliente. Si el ID del cliente está en `unknown` o `logged_out` , el id de cliente se ignorará y los datos de perfil de usuario que puedan asociarse a él no se aprovecharán para la segmentación de audiencia.

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

La llamada de ejemplo anterior muestra cómo enviar un `customerId` con un `authenticatedState`. Al enviar un `customerId`, el `integrationCode`, `id`, y `authenticatedState` así como el `marketingCloudVisitorId` son obligatorios. El `integrationCode` es el alias del [archivo de atributos del cliente](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=es) ha proporcionado mediante CRS.

## Perfil combinado

Se puede combinar `tntId`, `thirdPartyID`, y `marketingCloudVisitorId` en la misma solicitud. En esta situación, Adobe Target mantendrá la asignación de todos estos ID y los anclará a un visitante. Descubra cómo son los perfiles [combinado y sincronizado en tiempo real](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) uso de los distintos identificadores.

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

La llamada de ejemplo anterior muestra cómo se puede combinar `tntId`, `thirdPartyID`, y `marketingCloudVisitorId` en la misma solicitud. Los tres ID también se devuelven en la respuesta.
