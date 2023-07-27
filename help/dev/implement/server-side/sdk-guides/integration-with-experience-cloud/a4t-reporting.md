---
title: Integración con los informes de A4T de Experience Cloud
description: Integración con Experience Cloud, informes de A4T, integración de Analytics para Target
keywords: api de entrega, lado del servidor, lado del servidor, integración, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 7%

---

# Creación de informes en Analytics for Target (A4T)

[!DNL Adobe Target] admite la creación de informes de A4T tanto para la toma de decisiones en el dispositivo como para las actividades de Target del lado del servidor. Existen dos opciones de configuración para activar la creación de informes de A4T:

* [!DNL Adobe Target] reenvía automáticamente la carga útil de analytics a [!DNL Adobe Analytics], o
* El usuario solicita la carga útil de Analytics desde [!DNL Adobe Target]. ([!DNL Adobe Target] devuelve el [!DNL Adobe Analytics] carga útil de vuelta al llamador).

>[!NOTE]
>
>La toma de decisiones en el dispositivo solo admite informes de A4T de los cuales [!DNL Adobe Target] reenvía automáticamente la carga útil de analytics a [!DNL Adobe Analytics]. Recuperación de la carga útil de Analytics de [!DNL Adobe Target] no es compatible.

## Requisitos previos

1. Configure la actividad en [!DNL Adobe Target] IU con [!DNL Adobe Analytics] como fuente de informes y asegúrese de que las cuentas están habilitadas para A4T.
1. El usuario de la API genera el ID de visitante de Adobe Marketing Cloud y garantiza que este ID esté disponible cuando se ejecuta la solicitud de Target.

## [!DNL Adobe Target] reenvía automáticamente la carga útil de Analytics

[!DNL Adobe Target] puede reenviar automáticamente la carga útil de analytics a [!DNL Adobe Analytics] si se proporcionan los siguientes identificadores:

1. `supplementalDataId`: ID que se utiliza para vincular entre [!DNL Adobe Analytics] y [!DNL Adobe Target]. Para que [!DNL Adobe Target] y [!DNL Adobe Analytics] para unir correctamente los datos, siga el mismo procedimiento `supplementalDataId` debe pasarse a ambos [!DNL Adobe Target] y [!DNL Adobe Analytics].
1. `trackingServer`: La [!DNL Adobe Analytics] Servidor.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "server_side",
        supplementalDataId: "7D3AA246CC99FD7F-1B3DD2E75595498E",
        trackingServer: "jimsbrims.sc.omtrds.net"
      }
    }, 
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .trackingServer("jimsbrims.sc.omtrds.net")
        .logging(LoggingType.SERVER_SIDE)
        .supplementalDataId("7D3AA246CC99FD7F-1B3DD2E75595498E");
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## El usuario recupera la carga útil de Analytics de [!DNL Adobe Target]

Un usuario puede recuperar los [!DNL Adobe Analytics] carga útil para un mbox determinado y, a continuación, enviarla a [!DNL Adobe Analytics] a través de [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Cuando un [!DNL Adobe Target] se ha activado la solicitud, pase `client_side` a la `logging` en la solicitud. Esto devolverá una carga útil si el mbox especificado está presente en una actividad que utiliza Analytics como fuente de informes.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const targetClient = TargetClient.create(CONFIG);
targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "client_side"
      }
    },  
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .logging(LoggingType.CLIENT_SIDE);
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Una vez especificado `logging = client_side`, recibirá la carga útil en el campo mbox.

Si la respuesta de Target contiene algo en `analytics -> payload` propiedad, reenvíela tal como está [!DNL Adobe Analytics]. [!DNL Adobe Analytics] sabe cómo procesar esta carga útil. Esto se puede hacer en una solicitud de GET con el siguiente formato:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Parámetros y variables de cadena de consulta

| Nombre del campo | Requerido | Descripción |
| --- | --- | --- |
| `rsid` | Sí | La ID del grupo de informes |
| `pe` | Sí | Evento de página. Siempre establecido en `tnt` |
| `tnta` | Sí | Carga útil de Analytics devuelta por el servidor de Target en `analytics -> payload -> tnta` |
| `mid` | Sí | ID de visitante de Marketing Cloud |

### Valores de encabezado obligatorios

| Nombre del encabezado | Valor de encabezado |
| --- | --- |
| Host | Servidor de recopilación de datos de Analytics (p. ej.: `adobeags421.sc.omtrdc.net`) |

### Ejemplo de llamada de obtención HTTP de inserción de datos de A4T

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```
