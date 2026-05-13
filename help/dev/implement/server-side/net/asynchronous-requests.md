---
title: Utilizar solicitudes asincrónicas en  [!DNL Adobe Target] .NET SDK
description: Descubra cómo  [!DNL Target] Java SDK admite solicitudes asincrónicas, lo que puede reducir el tiempo de destino efectivo a cero.
feature: APIs/SDKs
exl-id: fd36cc7b-a884-4e57-93c2-8aff8256109a
TQID: https://experienceleague.adobe.com/E9rNmPdXe7HYg7XlIffpC4opGM9X6fFoHK-u0oLI-XE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 91
ht-degree: 4%

---

# Solicitudes asincrónicas (.NET)

## Descripción

Una ventaja de la integración del lado del servidor es que se puede aprovechar el enorme ancho de banda y recursos informáticos disponibles en el lado del servidor mediante el paralelismo. [!DNL Target] .NET SDK admite solicitudes asincrónicas, lo que facilita la integración de [!DNL Target] en el flujo de trabajo asincrónico existente de una aplicación.

## Métodos compatibles

### \.NET

```dotnet {line-numbers="true"}
Task<TargetDeliveryResponse> GetOffersAsync(TargetDeliveryRequest request);
Task<TargetDeliveryResponse> SendNotificationsAsync(TargetDeliveryRequest request);
Task<TargetAttributes> GetAttributesAsync(TargetDeliveryRequest request, params string[] mboxes);
```

## Ejemplo

Un ejemplo de uso asincrónico de la API de SDK podría aparecer de la siguiente manera:

### \.NET

```dotnet {line-numbers="true"}
var deliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { new MboxRequest(index: 1, name: "a1-serverside-ab") }))
    .Build();

var response = await this.targetClient.GetOffersAsync(deliveryRequest);

var notificationRequest = new TargetDeliveryRequest.Builder()
    .SetSessionId(response.Request.SessionId)
    .SetTntId(response.Response?.Id?.TntId)
    .SetNotifications(new List<Notification>
        {
            new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
                mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
                tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
        })
    .Build();

var notificationResponse = await this.targetClient.SendNotificationsAsync(notificationRequest);
```

Este ejemplo supone que ha [inicializado SDK](initialize-sdk.md).
