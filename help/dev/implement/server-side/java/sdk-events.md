---
title: Suscribirse a eventos en el  [!DNL Adobe Target] SDK de Java
description: Obtenga información sobre cómo suscribirse a varios eventos que se producen dentro del SDK de Java mediante el objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# Eventos de SDK (Java)

## Descripción

Al [inicializar el SDK](initialize-sdk.md), se puede proporcionar un objeto `OnDeviceDecisioningHandler` opcional en el objeto `ClientConfig`. Se puede utilizar para suscribirse a varios eventos que se producen dentro del SDK. Por ejemplo, el evento `onDeviceDecisioningReady` se puede usar con una función de llamada de retorno que se invocará cuando el SDK esté listo para las llamadas de método.

## Solicitud

El objeto `OnDeviceDecisioningHandler` contiene las siguientes llamadas de retorno, a las que se llama para determinados eventos:

| Nombre | Argumentos | Descripción |
| --- | --- | --- |
| onDeviceDecisioningReady | Ninguna | Solo se llamó una vez la primera vez que el cliente está listo para [!UICONTROL on-device decisioning] |
| artifactDownloadSucceeded | contenido de byte[] del archivo de artefactos | Se llama cada vez que se descarga un artefacto [!UICONTROL on-device decisioning] |
| artifactDownloadFailed | Excepción | Se llama cada vez que se produce un error al descargar un artefacto [!UICONTROL on-device decisioning] |

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
