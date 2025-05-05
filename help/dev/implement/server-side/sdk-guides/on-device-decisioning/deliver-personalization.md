---
title: Ofrezca personalización mediante los SDK para Adobe Target
description: Obtenga información sobre cómo entregar personalización mediante [!UICONTROL on-device decisioning].
feature: APIs/SDKs
exl-id: bac64c78-0d3a-40d7-ae2b-afa0f1b8dc4f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Entrega de personalización

## Resumen de los pasos

1. Habilitar [!UICONTROL on-device decisioning] para su organización
1. Crear una actividad [!UICONTROL Experience Targeting] (XT)
1. Definir experiencia personalizada por audiencia
1. Verificar experiencia personalizada por audiencia
1. Configuración de informes
1. Agregar métricas para KPI de seguimiento
1. Implementación de ofertas personalizadas en la aplicación
1. Implementación de código para hacer un seguimiento de eventos de conversión
1. Activar su actividad de personalización [!UICONTROL Experience Targeting] (XT)

Supongamos que es una empresa de turismo. Desea ofrecer una oferta personalizada del 25% de descuento en determinados paquetes de viaje. Para que la oferta resuene entre sus usuarios, decide mostrar un punto de referencia de la ciudad de destino. También debe asegurarse de que la entrega de sus ofertas personalizadas se ejecute con una latencia cercana a cero para que no afecte negativamente a las experiencias de los usuarios y distorsione los resultados.

## 1. Habilite [!UICONTROL on-device decisioning] para su organización

1. Al habilitar la toma de decisiones en el dispositivo, se garantiza que una actividad A/B se ejecute con una latencia cercana a cero. Para habilitar esta característica, vaya a **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** en [!DNL Adobe Target] y habilite la opción **[!UICONTROL On-Device Decisioning]**.

   ![imagen alt](assets/asset-odd-toggle.png)

   >[!NOTE]
   >
   >Debe tener el rol de administrador o aprobador [user](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=es) para habilitar o deshabilitar la opción [!UICONTROL On-Device Decisioning].

   Después de habilitar la opción **[!UICONTROL On-Device Decisioning]**, [!DNL Adobe Target] comienza a generar *artefactos de regla* para su cliente.

## 2. Crear una actividad [!UICONTROL Experience Targeting] (XT)

1. En [!DNL Adobe Target], vaya a la página **[!UICONTROL Activities]** y, a continuación, seleccione **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]**.

   ![imagen alt](assets/asset-xt.png)

1. En el modal **[!UICONTROL Create Experience Targeting Activity]**, deje seleccionada la opción predeterminada **[!UICONTROL Web]** (1), seleccione **[!UICONTROL Form]** como compositor de experiencias (2), seleccione un espacio de trabajo y una propiedad (3) y haga clic en **[!UICONTROL Next]** (4).

   ![imagen alt](assets/asset-xt-next.png)

## 3. Defina una experiencia personalizada por audiencia

1. En el paso **[!UICONTROL Experiences]** de creación de la actividad, haga clic en **[!UICONTROL Change Audience]** para crear una audiencia de los visitantes que deseen viajar a San Francisco, California.

   ![imagen alt](assets/asset-change-audience.png)

1. En el modal **[!UICONTROL Create Audience]**, defina una regla personalizada donde `destinationCity = San Francisco`. Define el grupo de usuarios que desea viajar a San Francisco.

   ![imagen alt](assets/asset-audience-sf.png)

1. En el paso **[!UICONTROL Experiences]**, escriba el nombre de la ubicación (1) dentro de su aplicación donde desea presentar una oferta especial con respecto a Golden Gate Bridge, pero solo para los que se dirigen a San Francisco. En el ejemplo que se muestra aquí, homepage es la ubicación seleccionada para la oferta de HTML (2), que se define en el área **[!UICONTROL Content]**.

   ![imagen alt](assets/asset-content-sf.png)

1. Agregue otra audiencia de segmentación haciendo clic en **[!UICONTROL Add Experience Targeting]**. En esta ocasión, defina una regla de audiencia donde `destinationCity = New York` sea el destino de una audiencia que desee viajar a Nueva York. Defina la ubicación dentro de su aplicación donde desea presentar una oferta especial con respecto al Empire State Building. En el ejemplo que se muestra aquí, `homepage` es la ubicación seleccionada para la oferta de HTML (2), que se define en el área **[!UICONTROL Content]**.

   ![imagen alt](assets/asset-content-ny.png)

## 4. Verificar la experiencia personalizada por audiencia

En el paso **[!UICONTROL Targeting]**, compruebe que ha configurado la experiencia personalizada que desea por audiencia.

![imagen alt](assets/asset-verify-sf-ny.png)

## 5. Configurar informes

En el paso **[!UICONTROL Goals & Settings]**, elija **[!UICONTROL Adobe Target]** como **[!UICONTROL Reporting Source]** para ver los resultados de la actividad en la interfaz de usuario de [!DNL Adobe Target] o elija **[!UICONTROL Adobe Analytics]** para verlos en la interfaz de usuario de Adobe Analytics.

![imagen alt](assets/asset-reporting-sf-ny.png)

## 6. Agregar métricas para el seguimiento de KPI

Elija un(a) **[!UICONTROL Goal Metric]** para medir el éxito de la actividad. En este ejemplo, una conversión correcta se basa en si el usuario hace clic en la oferta de destino personalizada.

## 7. Implementar las ofertas personalizadas en la aplicación

>[!BEGINTABS]

>[!TAB Nodo.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {      
    execute: {
      pageLoad: {
        parameters: {
          destinationCity: "San Francisco"
        }
      }
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## 8. Implementar código para rastrear eventos de conversión

>[!BEGINTABS]

>[!TAB Nodo.js]

```js {line-numbers="true"}
//... Code removed for brevity

//When a conversion happens
TargetClient.sendNotifications({
    targetCookie,
    "request" : {
      "notifications" : [
        {
          type: "click",
          timestamp : Date.now(),
          id: "conversion",
          mbox : {
            name : "destinationOffer"
          }
        }
      ]
    }
})
```

>[!TAB Java]

```java {line-numbers="true"
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);
NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();

Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.CLICK);
notification.setTimestamp(System.currentTimeMillis());
notification.setTokens(
    Collections.singletonList(
        "IbG2Jz2xmHaqX7Ml/YRxRGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="));

TargetDeliveryRequest targetDeliveryRequest =
    TargetDeliveryRequest.builder()
        .context(context)
        .execute(executeRequest)
        .notifications(Collections.singletonList(notification))
        .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
notificationDeliveryService.sendNotification(request);
```

>[!ENDTABS]

## 9. Active la actividad de segmentación de experiencias (XT)

![imagen alt](assets/asset-xt-activate.png)
