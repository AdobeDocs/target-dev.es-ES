---
title: Uso de getAttributes en [!DNL Adobe Target] con .NET SDK
description: Aprenda a utilizar getAttributes() para recuperar experimentación y experiencias personalizadas de [!DNL Target] y extraer valores de atributo.
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 10%

---

# Obtener atributos (.NET)

## Descripción

`GetAttributes()` se utiliza para recuperar experimentación y experiencias personalizadas de [!DNL Target] y extraer valores de atributo.

## Método

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## Parámetros

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | No | null | Lo mismo [!DNL Target] solicitud tal como se usa para [Obtener ofertas&#x200B;](get-offers.md) |
| mboxNames | cadena de parámetros[] | No | null | Matriz de parámetros de nombres de mbox |

## Resultado

A `TargetAttributes` el objeto se devuelve desde `TargetClient.GetAttributes()` que tiene las siguientes propiedades y métodos:

| Propiedad/Método | Tipo de devolución | Descripción |
| --- | --- | --- |
| Respuesta | TargetDeliveryResponse | Devuelve el objeto de respuesta normalmente devuelto por [Obtener ofertas](get-offers.md) |
| ToDictionary | IReadOnlyDictionary | Devuelve un diccionario de diccionarios con pares de valor clave agrupados por nombres de mbox |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | Devuelve un diccionario con pares de valor clave para el mbox proporcionado |
| GetBoolean(mboxName, key, defaultValue) | bool | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| GetString(mboxName, key, defaultValue) | string | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| GetInteger(mboxName, key, defaultValue) | int | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| GetDouble(mboxName, key, defaultValue) | doble | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |
| GetValue(mboxName, key, defaultValue) | T  | Devuelve el valor de un nombre de mbox y una clave de atributo especificados |

## Ejemplo

### \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .Build();

var offerAttributes = targetClient.GetAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
var searchProviderId = offerAttributes.GetString("demo-engineering-flags", "searchProviderId");

//returns a simple Dictionary representing the mbox offer
var engineeringFlags = offerAttributes.ToMboxDictionary("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

var assetUrl = $"http://{engineeringFlags["cdnHostname"]}/path/to/asset";
```
