---
title: Suscribirse a eventos en el SDK de  [!DNL Adobe Target] .NET
description: Obtenga información sobre cómo suscribirse a varios eventos que se producen en .NET SDK mediante el objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Eventos de SDK (.NET)

## Descripción

Al [inicializar el SDK](initialize-sdk.md), se puede proporcionar un delegado `OnDeviceDecisioningReady` opcional en el objeto `TargetClientConfig`, que se invocará cuando el SDK esté listo para las llamadas de método en el dispositivo. También hay un par de delegados más disponibles para administrar la descarga de artefactos de [!UICONTROL on-device decisioning].

## Solicitud

Los siguientes delegados se pueden configurar para determinados eventos:

| Nombre | Argumentos | Descripción |
| --- | --- | --- |
| OnDeviceDecisioningReady | Ninguna | Solo se llamó una vez la primera vez que el cliente está listo para [!UICONTROL on-device decisioning] |
| DescargaDeArtefactoCorrecta | contenido de cadena del archivo de artefactos | Se llama cada vez que se descarga un artefacto [!UICONTROL on-device decisioning] |
| ArtifactDownloadFailed | Excepción | Se llama cada vez que se produce un error al descargar un artefacto [!UICONTROL on-device decisioning] |

## Ejemplo

### \.NET

```dotnet {line-numbers="true"}
var clientConfig = new TargetClientConfig.Builder("acmeclient", "1234567890@AdobeOrg")
    .SetDecisioningMethod(DecisioningMethod.OnDevice)
    .SetOnDeviceDecisioningReady(DecisioningReady)
    .SetArtifactDownloadSucceeded(artifact => Console.WriteLine("The artifact was successfully downloaded. Contents: " + artifact))
    .SetArtifactDownloadFailed(exception => Console.WriteLine("The artifact failed to download. Exception: " + exception.Message))
    .Build();

var targetClient = TargetClient.Create(clientConfig);

// ...

static void DecisioningReady()
{
    var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

    var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
        .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
        .Build();

    var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
}
```
