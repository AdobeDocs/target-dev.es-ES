---
title: Identificación de usuarios y agrupamiento
description: Identificación de usuarios y agrupamiento
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 3%

---

# Identificación de usuarios y agrupamiento

## Identificación de usuario

Hay varias maneras de identificar a un usuario dentro de [!DNL Adobe Target]. [!UICONTROL Target] utiliza los identificadores siguientes:

| Nombre del campo | Descripción |
| --- | --- |
| `tntID` | `tntId` es el identificador principal de [!DNL Target] para un usuario. Puede proporcionar este identificador o [!DNL Target] lo generará automáticamente si la solicitud no contiene uno. |
| `thirdPartyId` | El `thirdPartyId` es el identificador de su compañía para el usuario, el cual puede enviar con cada llamada. Cuando un usuario inicia sesión en el sitio de una empresa, esta generalmente crea un ID vinculado a la cuenta del visitante, la tarjeta de fidelidad, el número de pertenencia u otros identificadores aplicables para esa empresa. |
| `marketingCloudVisitorId` | `marketingCloudVisitorId` se usa para combinar y compartir datos entre distintas soluciones de Adobe. Se requiere marketingCloudVisitorId para las integraciones con Adobe Analytics y Adobe Audience Manager. |
| `customerIds` | Junto con la ID de visitante Experience Cloud, también se pueden usar [ID de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=es) adicionales y un estado autenticado para cada visitante. |

## [!DNL Target] ID (tntID)

El identificador [!DNL Target], o `tntId`, puede considerarse un identificador de dispositivo. [!DNL Adobe Target] genera automáticamente este(a) `tntId` si no se proporciona(n) en la solicitud. Las solicitudes posteriores deben incluir este(a) `tntId` para que se pueda entregar el contenido correcto a un dispositivo que use el mismo usuario.

La siguiente llamada de ejemplo muestra una situación en la que `tntId` no se pasa a [!DNL Target].

>[!BEGINTABS]

>[!TAB SDK de Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
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

>[!TAB SDK de Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

En ausencia de `tntId`, [!DNL Adobe Target] genera un `tntId` y lo proporciona en la respuesta de la siguiente manera.

```json {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "acmeclient",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.35_0"
  },
  "edgeHost": "mboxedge35.tt.omtrdc.net",
  ...
}
```

En este ejemplo, el `tntId` generado es `10abf6304b2714215b1fd39a870f01afc.35_0`. Tenga en cuenta que este(a) `tntId` debe(n) usarse para el mismo usuario en todas las sesiones.

## ID de terceros (thirdPartyId)

Si su organización utiliza un ID para identificar a su visitante, puede usar `thirdPartyID` para entregar contenido. Un `thirdPartyID` es un ID persistente que su empresa utiliza para identificar a un usuario final, independientemente de si interactúa con su empresa desde canales web, móviles o de IoT. En otras palabras, `thirdPartyId` hace referencia a datos de perfil de usuario que se pueden utilizar en todos los canales. Sin embargo, debe proporcionar `thirdPartyID` por cada llamada a la API de entrega de [!DNL Adobe Target] que realice.

La siguiente llamada de ejemplo muestra el uso de un `thirdPartyId`.

>[!BEGINTABS]

>[!TAB SDK de Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      thirdPartyId: "B234A029348"
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

>[!TAB SDK de Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .thirdPartyId("B234A029348");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

En este escenario, [!DNL Adobe Target] generará un `tntId`, ya que no se pasó a la llamada original, que se asignará al `thirdPartyId` proporcionado.

## ID de visitante de Marketing Cloud (marketingCloudVisitorId)

`marketingCloudVisitorId` es un identificador universal y persistente que identifica a los visitantes en todas las soluciones de Adobe Experience Cloud. Cuando su organización implementa el servicio de ID, este ID le permite identificar el mismo visitante del sitio y sus datos en diferentes soluciones de Experience Cloud, incluidas [!DNL Adobe Target], Adobe Analytics y Adobe Audience Manager. Tenga en cuenta que `marketingCloudVisitorId` es necesario al integrar [!DNL Target] con [!DNL Adobe Analytics] y [!DNL Adobe Audience Manager].

La siguiente llamada de ejemplo muestra cómo se pasa a [!DNL Target] un(a) `marketingCloudVisitorId` que se recuperó del servicio de ID de Experience Cloud.

>[!BEGINTABS]

>[!TAB SDK de Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId: "10527837386392355901041112038610706884"
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

>[!TAB SDK de Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

En este escenario, [!DNL Target] generará un `tntId`, ya que no se pasó a la llamada original, que se asignará al `marketingCloudVisitorId` proporcionado.

## ID del cliente (customerIds)

[Los ID de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=es) se pueden agregar o asociar a un ID de visitante de Experience Cloud. Siempre que se envíe `customerIds`, también se debe proporcionar `marketingCloudVisitorId`. Además, se puede proporcionar un estado de autenticación junto con cada `customerId` para cada visitante. Se pueden utilizar los siguientes estados de autenticación:

| Estado de autenticación | Estado de usuario |
| --- | --- |
| `unknown` | Desconocido o nunca autenticado. Este estado se puede utilizar en escenarios como aquellos en los que un visitante llega a un sitio haciendo clic en un anuncio en pantalla. |
| `authenticated` | El usuario está autenticado con una sesión activa en su sitio web o aplicación. |
| `logged_out` | El usuario estaba autenticado pero ha cerrado sesión activamente. El usuario tenía la intención de desconectarse del estado autenticado. El usuario ya no quiere que se le trate como autenticado. |

Tenga en cuenta que solo cuando `customerId` se encuentra en un estado autenticado, [!DNL Target] hará referencia a los datos de perfil de usuario que se almacenan y vinculan al customerId. Si `customerId` tiene un estado desconocido o `logged_out`, se omitirá y los datos de perfil de usuario que puedan estar asociados con ese(a) `customerId` no se aprovecharán para la segmentación de audiencia.

>[!BEGINTABS]

>[!TAB SDK de Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId : "10527837386392355901041112038610706884",
      customerIds: [{
        id: "134325423",
        integrationCode : "crm_data",
        authenticatedState : "authenticated"
      }]
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

>[!TAB SDK de Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

CustomerId customerId = new CustomerId()
  .id("134325423")
  .integrationCode("crm_data")
  .authenticatedState(AuthenticatedState.AUTHENTICATED);
VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884")
  .customerIds(Arrays.asList(customerId));
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

El ejemplo anterior muestra cómo enviar un `customerId` con un `authenticatedState`. Al enviar un `customerId`, se requieren `integrationCode`, `id` y `authenticatedState`, así como `marketingCloudVisitorId`. `integrationCode` es el alias del [archivo de atributos del cliente](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=es) que usted proporcionó a través de CRS.

## Perfil combinado

Puede combinar `tntId`, `thirdPartyID` y `marketingCloudVisitorId` en la misma solicitud. En este escenario, [!DNL Adobe Target] mantendrá la asignación de todos estos ID y los anclará a un visitante. Descubra cómo se combinan y sincronizan los perfiles [en tiempo real](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=es) con los diferentes identificadores.

>[!BEGINTABS]

>[!TAB SDK de Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId: "B234A029348",
      marketingCloudVisitorId : "10527837386392355901041112038610706884"
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

>[!TAB SDK de Java]

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

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

El ejemplo anterior muestra cómo se puede combinar `tntId`, `thirdPartyID` y `marketingCloudVisitorId` en la misma solicitud.

## Agrupamiento

Los usuarios se agrupan para ver una experiencia según la configuración de las actividades de [!DNL Adobe Target]. En [!DNL Adobe Target], el agrupamiento es:

* **Determinístico**: MurmurHash3 se usa para garantizar que el usuario esté agrupado y vea la variación correcta cada vez, siempre y cuando el ID de usuario sea coherente.
* **Adhesivo**: [!DNL Adobe Target] almacena la variación que el usuario ve en el perfil de usuario para garantizar que se muestre la variación de manera consistente a ese usuario en todas las sesiones y canales. Las variaciones y la permanencia están garantizadas al utilizar la toma de decisiones en el lado del servidor. Cuando se utiliza la toma de decisiones en el dispositivo, no se garantiza la permanencia.

## Flujo de trabajo de bloques de extremo a extremo

Antes de sumergirse en el algoritmo de agrupamiento real, es importante resaltar que se utilizan pasos similares tanto para seleccionar actividades en función de su porcentaje de asignación de tráfico, como para seleccionar una experiencia dentro de una actividad.

### Pasos de selección de actividad

1. Generar un ID de dispositivo, normalmente un UUID
1. Obtener el código de cliente
1. Obtención del ID de actividad
1. Obtener la sal, que suele ser una cadena como &quot;actividad&quot;
1. Calcular el hash con MurmurHash3
1. Obtener el valor absoluto del hash
1. Dividir el valor absoluto de hash por 10000
1. Divida el resto por 10000, lo que debería producir un valor entre 0 y 1
1. Multiplicar el resultado por 100 %
1. Compare el porcentaje de asignación de tráfico de actividad con el porcentaje obtenido. Si el porcentaje de asignación de tráfico es menor, se selecciona la actividad. De lo contrario, la actividad se omitirá.

### Pasos de selección de experiencias

1. Generar un ID de dispositivo, normalmente un UUID
1. Obtener el código de cliente
1. Obtención del ID de actividad
1. Coge la sal, que suele ser una cuerda como &quot;experiencia&quot;
1. Calcular el hash con MurmurHash3
1. Obtener el valor absoluto del hash
1. Dividir el valor absoluto de hash por 10000
1. Divida el resto por 10000, lo que debería producir un valor entre 0 y 1
1. Multiplique el resultado por el número total de experiencias dentro de la actividad
1. Redondea el resultado. Esto debería generar el índice de experiencia.

### Ejemplo

Supongamos lo siguiente:

* Cliente C con código de cliente `acmeclient`
* Actividad A con ID `1111` y tres experiencias `E1`, `E2`, `E3`
* Las experiencias tienen la siguiente distribución: `E1` - 33%, `E2` - 33%, `E3` - 34%

El flujo de selección tiene este aspecto:

1. Id. de dispositivo `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. Código de cliente `acmeclient`
1. ID de actividad `1111`
1. Sal `experience`
1. Valor para hash `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, valor hash `-919077116`
1. Valor absoluto del hash `919077116`
1. Resto después de la división por 10000, `7116`
1. Valor después de que el resto se divida entre 10000, `0.7116`
1. Resultado después de multiplicar el valor por el número total de experiencias `3 * 0.7116 = 2.1348`
1. El índice de experiencia es `2`, lo que significa la tercera experiencia, ya que utilizamos la indexación basada en `0`.
