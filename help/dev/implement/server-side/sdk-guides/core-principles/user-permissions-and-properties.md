---
title: Permisos de usuario y propiedades
description: Los SDK  [!DNL Target] incluyen compatibilidad con permisos y propiedades de usuario.
exl-id: 612faf1a-e8f9-4321-b831-90fba69ead3a
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Permisos de usuario y propiedades

Los SDK de [!DNL Target] incluyen compatibilidad con permisos y propiedades de usuario. Si no conoce cómo [!DNL Adobe Target] administra los permisos de empresa a través de espacios de trabajo y propiedades, puede obtener más información al respecto en [Permisos de usuario de empresa](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=es).

El cliente puede utilizar un token de propiedad de una de las dos maneras siguientes.

## Token de propiedad global

>[!BEGINTABS]

>[!TAB Nodo.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    propertyToken: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({...})
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("emeaprod4")
    .organizationId("0DD934B85278256B0A490D44@AdobeOrg")
    .defaultPropertyToken("8c4630b1-16db-e2fc-3391-8b3d81436cfb")
    .build();

TargetClient targetClient = TargetClient.create(clientConfig);
```

>[!ENDTABS]

## Token de propiedad incidental en la llamada de getOffers

También se puede especificar un token de propiedad en una llamada individual a `getOffers`. Para ello, añada un objeto de propiedad a la solicitud. Un token de propiedad especificado de esta manera tiene prioridad sobre un conjunto de la configuración.

>[!BEGINTABS]

>[!TAB Nodo.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
    request: {
        execute: {
            pageLoad: {}
        },
        property: {
            token: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
        }           
    }
})
```

>[!TAB Java]

```java {line-numbers="true"}
ExecuteRequest executeRequest = new ExecuteRequest()
    .mboxes(getMboxRequests(mbox));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
    .context(getContext(request))
    .execute(executeRequest)
    .cookies(getTargetCookies(request.getCookies()))
    .property(new Property().token("8c4630b1-16db-e2fc-3391-8b3d81436cfb"))
    .build();

TargetDeliveryResponse targetResponse = targetClient.getOffers(targetDeliveryRequest);
```

>[!ENDTABS]
