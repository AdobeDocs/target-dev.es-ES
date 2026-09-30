---
title: Suscribirse a eventos en el SDK Java [!DNL Adobe Target]
description: Obtenga información sobre cómo suscribirse a varios eventos que ocurren en Java SDK mediante el objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
TQID: 'https://experienceleague.adobe.com/x3aig-jM-GXzmLNcUNclZUK9Y49tuSF9-sdkxzJFtiM'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%
---
# Eventos de SDK (Java)

## Descripción

Al [inicializar SDK](initialize-sdk.md), se puede proporcionar un objeto `OnDeviceDecisioningHandler` opcional en el objeto `ClientConfig`. Se puede utilizar para suscribirse a varios eventos que se producen dentro de SDK. Por ejemplo, el evento `onDeviceDecisioningReady` se puede utilizar con una función de devolución de llamada que se invocará cuando SDK esté listo para las llamadas de método.

## Solicitud

El objeto `OnDeviceDecisioningHandler` contiene las siguientes llamadas de retorno, a las que se llama para determinados eventos:

| Nombre | Argumentos | Descripción |
| --- | --- | --- |
| onDeviceDecisioningReady | Ninguna | Se llama solo una vez la primera vez que el cliente está listo para [!UICONTROL la toma de decisiones en el dispositivo] |
| artifactDownloadSucceeded | contenido de byte[] del archivo de artefactos | Se llama cada vez que se descarga un artefacto de [!UICONTROL toma de decisiones en el dispositivo] |
| artifactDownloadFailed | Excepción | Se llama cada vez que se produce un error al descargar un artefacto de [!UICONTROL toma de decisiones en el dispositivo] |

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
