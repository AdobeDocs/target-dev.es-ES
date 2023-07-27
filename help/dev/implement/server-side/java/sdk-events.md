---
title: Suscribirse a eventos en [!DNL Adobe Target] SDK de Java
description: Obtenga información sobre cómo suscribirse a varios eventos que se producen dentro del SDK de Java mediante [!UICONTROL OnDeviceDecisioningHandler] objeto.
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 4%

---

# Eventos de SDK (Java)

## Descripción

Cuándo [inicialización del SDK](initialize-sdk.md), un opcional `OnDeviceDecisioningHandler` se puede proporcionar en el `ClientConfig` objeto. Se puede utilizar para suscribirse a varios eventos que se producen dentro del SDK. Por ejemplo, la variable `onDeviceDecisioningReady` se puede utilizar con una función de llamada de retorno que se invocará cuando el SDK esté listo para las llamadas de método.

## Solicitud

El `OnDeviceDecisioningHandler` contiene las siguientes llamadas de retorno, a las que se llama para determinados eventos:

| Nombre | Argumentos | Descripción |
| --- | --- | --- |
| onDeviceDecisioningReady | Ninguna | Se llama solo una vez la primera vez que el cliente está listo para [!UICONTROL toma de decisiones en el dispositivo] |
| artifactDownloadSucceeded | byte[] contenido del archivo de artefactos | Se llama cada vez que [!UICONTROL toma de decisiones en el dispositivo] el artefacto se ha descargado |
| artifactDownloadFailed | Excepción | Se llama cada vez que se produce un error al descargar un [!UICONTROL toma de decisiones en el dispositivo] artefacto |

## Ejemplo

### Eventos de SDK

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .defaultDecisioningMethod(DecisioningMethod.ON_DEVICE)
        .onDeviceDecisioningHandler(new OnDeviceDecisioningHandler() {
            @Override
            public void onDeviceDecisioningReady() {
                // make getOffers requests
                makeTargetRequests();
            }

            @Override
            public void artifactDownloadSucceeded(byte[] artifactData) {
                System.out.println("The artifact was successfully downloaded.");
            }

            @Override
            public void artifactDownloadFailed(TargetClientException e) {
                System.out.println("The artifact failed to download.");
            }
        }).build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);


void makeTargetRequests() {
    List<MboxRequest> mboxRequests = new ArrayList<>();
    mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
            .context(new Context().channel(ChannelType.WEB))
            .execute(new ExecuteRequest().setMboxes(mboxRequests))
            .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
}
```
