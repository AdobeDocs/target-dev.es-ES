---
title: Cómo utilizar solicitudes asincrónicas en [!DNL Adobe Target] SDK DE .NET
description: Descubra cómo [!DNL Target] El SDK de Java admite solicitudes asincrónicas, lo que puede reducir el tiempo de objetivo efectivo a cero.
feature: APIs/SDKs
exl-id: fd36cc7b-a884-4e57-93c2-8aff8256109a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 4%

---

# Solicitudes asincrónicas (.NET)

## Descripción

Una ventaja de la integración del lado del servidor es que se puede aprovechar el enorme ancho de banda y recursos informáticos disponibles en el lado del servidor mediante el paralelismo. [!DNL Target] .NET SDK admite solicitudes asincrónicas, lo que facilita la integración [!DNL Target] en el flujo de trabajo asincrónico existente de una aplicación.

## Métodos compatibles

### \.NET

```dotnet {line-numbers="true"}
Task<TargetDeliveryResponse> GetOffersAsync(TargetDeliveryRequest request);
Task<TargetDeliveryResponse> SendNotificationsAsync(TargetDeliveryRequest request);
Task<TargetAttributes> GetAttributesAsync(TargetDeliveryRequest request, params string[] mboxes);
```

## Ejemplo

Podría aparecer un ejemplo de uso de API de SDK asincrónico de la siguiente manera:

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

En este ejemplo se supone que tiene [se ha inicializado el SDK](initialize-sdk.md).
