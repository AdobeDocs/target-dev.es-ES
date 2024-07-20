---
title: Usar getAttributes en  [!DNL Adobe Target] con el SDK de Java
description: Aprenda a utilizar getAttributes() para recuperar experimentación y experiencias personalizadas de  [!DNL Target] y extraer valores de atributos.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 13%

---

# Obtener atributos (Java)

## Descripción

`getAttributes()` se usa para recuperar experimentación y experiencias personalizadas de [!DNL Target] y extraer valores de atributos.

## Método

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## Parámetros

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Sí | Ninguna | Se usó la misma solicitud de destino para [Obtener ofertas&#x200B;](get-offers.md) |
| mboxNames | matriz var-args | No | Ninguna | Matriz var-args de nombres de mbox |


## Resultado

Se devuelve un objeto `Attributes` de `TargetClient.getAttributes()` que tiene los siguientes métodos:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| getBoolean(mboxName, key) | Booleano | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| getString(mboxName, key) | Cadena | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| getInteger(mboxName, key) | Número entero | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| getDouble(mboxName, key) | Doble | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| toMboxMap(mboxName) | Mapa | Devuelve un mapa simple con pares de valor clave |
| getResponse() | TargetDeliveryResponse | Devuelve el objeto response normalmente devuelto por getOffers |

## Ejemplo

### Java

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .build();

Attributes offerAttributes = targetJavaClient.getAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
String searchProviderId = offerAttributes.getString("demo-engineering-flags", "searchProviderId");

//returns a simple Map representing the mbox offer
Map<String, Object> engineeringFlags = offerAttributes.toMboxMap("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

String assetUrl = "http://" + engineeringFlags.cdnHostname + "/path/to/asset";
```
