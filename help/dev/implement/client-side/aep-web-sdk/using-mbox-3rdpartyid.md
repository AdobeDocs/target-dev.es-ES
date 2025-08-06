---
title: Sincronización de perfiles en tiempo real para mbox3rdPartyId
description: Aprenda a utilizar mbox3rdPartyId con  [!DNL Adobe Experience Platform Web SDK].
keywords: personalización;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
source-git-commit: b694698b0957db499172af34ff3a61c10d22b0d1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 16%

---

# Usar mbox3rdPartyId

El `mbox3rdPartyId` en [!DNL Adobe Target] es el ID de visitante de su compañía, como el ID de pertenencia para el programa de fidelidad de su empresa.

Cuando un visitante inicia sesión en el sitio de una empresa, esta generalmente crea un ID vinculado a la cuenta del visitante, la tarjeta de fidelidad, el número de pertenencia u otros identificadores aplicables para esa empresa. [Más información](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)

## Cómo usar `mbox3rdPartyId` con [!DNL Platform Web SDK]

### Paso 1: Configurar `Target Third Party ID Namespace`

Configure `Target Third Party ID Namespace` en su [secuencia de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) con el área de nombres de ID que desea usar como ID de terceros de mbox. [Más información sobre áreas de nombres de ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![IU de Experience Platform que muestra el campo de área de nombres de ID de terceros de Target.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### Paso 2: Enviar `mbox3rdpartyId` a [!DNL Target]

Envíe `mbox3rdpartyId` a [!DNL Target] en el comando `sendEvent`, utilizando el área de nombres de ID que configuró en el paso 1.
[Más información sobre el envío de identificadores](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
