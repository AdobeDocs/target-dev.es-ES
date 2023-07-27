---
title: Suscribirse a eventos en [!DNL Adobe Target] SDK DE .NET
description: Obtenga información sobre cómo suscribirse a varios eventos que se producen en .NET SDK mediante [!UICONTROL OnDeviceDecisioningHandler] objeto.
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# Eventos de SDK (.NET)

## Descripción

Cuándo [inicialización del SDK](initialize-sdk.md), un opcional `OnDeviceDecisioningReady` El delegado se puede proporcionar en `TargetClientConfig` , que se invocará cuando el SDK esté listo para las llamadas de método en el dispositivo. También hay un par de delegados más disponibles para gestionar el [!UICONTROL toma de decisiones en el dispositivo] descarga de artefactos.

## Solicitud

Los siguientes delegados se pueden configurar para determinados eventos:

| Nombre | Argumentos | Descripción |
| --- | --- | --- |
| OnDeviceDecisioningReady | Ninguna | Se llama solo una vez la primera vez que el cliente está listo para [!UICONTROL toma de decisiones en el dispositivo] |
| DescargaDeArtefactoCorrecta | contenido de cadena del archivo de artefactos | Se llama cada vez que un [!UICONTROL toma de decisiones en el dispositivo] el artefacto se ha descargado |
| ArtifactDownloadFailed | Excepción | Se llama cada vez que se produce un error al descargar un [!UICONTROL toma de decisiones en el dispositivo] artefacto |

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
