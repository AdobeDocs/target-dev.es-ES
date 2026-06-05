---
title: Ejecución de pruebas de funciones con atributos
description: Ejecución de pruebas de funciones con atributos
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
TQID: https://experienceleague.adobe.com/y2Mwmnn2k91-LKBy1UmZ5a1s6dZeb5VMyHdyJc2lc34
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 960
ht-degree: 1%

---

# Ejecución de pruebas de funciones con atributos

## Resumen de los pasos

1. Habilitar [!UICONTROL toma de decisiones en el dispositivo] para su organización
1. Crear una actividad [!UICONTROL Prueba A/B]
1. Defina su A y B
1. Añadir una audiencia
1. Establecer asignación de tráfico
1. Establecer la distribución del tráfico en variaciones
1. Configuración de informes
1. Agregar métricas para KPI de seguimiento
1. Implementar código para ejecutar pruebas de características con atributos
1. Implementación de código para hacer un seguimiento de eventos de conversión
1. Activación de las pruebas de funciones con atributos

>[!NOTE]
>
>Supongamos que es una empresa minorista de comercio electrónico. Desea aumentar la tasa de conversión cuando los clientes examinan y clasifican su catálogo de productos. Tiene la hipótesis de que ciertos algoritmos de ordenación y estrategias de paginación arrojan mejores resultados que otros. Para probar esta teoría, decida ejecutar una prueba de características que implique el rediseño del widget de ordenación utilizando diferentes opciones de ordenación para los usuarios finales. Debe asegurarse de que esta prueba de características se ejecute con una latencia cercana a cero para que no afecte negativamente a las experiencias de los usuarios ni distorsione los resultados.

## &#x200B;1. Habilitar [!UICONTROL toma de decisiones en el dispositivo] para su organización

Al habilitar la toma de decisiones en el dispositivo, se garantiza que una actividad A/B se ejecute con una latencia cercana a cero. Para habilitar esta característica, vaya a **[!UICONTROL Administración]** > **[!UICONTROL Implementación]** > **[!UICONTROL Detalles de la cuenta]** en [!DNL Adobe Target] y habilite la opción **[!UICONTROL Toma de decisiones en el dispositivo]**.

![imagen alt](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Debe tener el rol de administrador o aprobador [user](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=es) para habilitar o deshabilitar la opción **[!UICONTROL On-Device Decisioning]**.

Después de habilitar la opción **[!UICONTROL Toma de decisiones en el dispositivo]**, [!DNL Adobe Target] comienza a generar *artefactos de regla* para su cliente.

## &#x200B;2. Crear una actividad [!UICONTROL Prueba A/B]

1. En [!DNL Adobe Target], vaya a la página **[!UICONTROL Actividades]** y, a continuación, seleccione **[!UICONTROL Crear actividad]** > **[!UICONTROL Prueba A/B]**.

   ![imagen alt](assets/asset-ab.png)

1. En el modal **[!UICONTROL Crear actividad de prueba A/B]**, deje seleccionada la opción predeterminada **[!UICONTROL Web]** (1), seleccione **[!UICONTROL Formulario]** como compositor de experiencias (2), seleccione **[!UICONTROL Workspace predeterminado]** con **[!UICONTROL Sin restricciones de propiedad]** (3) y haga clic en **[!UICONTROL Siguiente]** (4).

   ![imagen alt](assets/asset-form.png)

## &#x200B;3. Defina su A y B

1. En el paso de creación de la actividad **[!UICONTROL Experiencias]**, indique un nombre para su actividad (1) y agregue una segunda experiencia, Experiencia B, haciendo clic en el botón **[!UICONTROL Agregar experiencia]** (2). Introduzca el nombre de la ubicación (3) dentro de la aplicación en la que desea ejecutar la prueba de funciones con atributos. En el siguiente ejemplo, `product-results-page` es la ubicación definida para la Experiencia A. (También es la ubicación definida para la Experiencia B).

   ![imagen alt](assets/asset-location.png)

   **[!UICONTROL La experiencia A]** contendrá el JSON que indica a su lógica empresarial que debe hacer lo siguiente:

   * Iniciar la característica de algoritmo de ordenación mediante el indicador de característica `test_sorting`
   * Ejecutar el algoritmo de ordenación recomendado definido en `sorting_algorithm _**_attribute`
   * Devolver 50 productos por página según la estrategia de paginación definida en `pagination_limit`

1. En la Experiencia A, haga clic para cambiar el contenido de **[!UICONTROL Contenido predeterminado]** al JSON seleccionando **[!UICONTROL Crear oferta JSON]** como se muestra a continuación (1).

   ![imagen alt](assets/asset-offer.png)

1. Defina el JSON con los indicadores y atributos `test_sorting`, `sorting_algorithm` y `pagination_limit` que se utilizarán para iniciar el algoritmo de ordenación recomendado con un límite de paginación de 50 productos.

   >[!NOTE]
   >
   >Cuando [!DNL Adobe Target] agrupa a un usuario para ver la Experiencia A, se devuelve el JSON con los atributos definidos en el ejemplo. En su código, deberá comprobar el valor del indicador de característica `test_sorting` para ver si la característica de ordenación debe estar activada. Si es así, utilizará el valor recomendado del atributo `sorting_algorithm` para mostrar los productos recomendados en la vista de lista de productos. El límite de productos que se mostrarán para la aplicación será 50, ya que ese es el valor del atributo `pagination_limit`.

   ![imagen alt](assets/asset-sorting.png)

   **[!UICONTROL La experiencia B]** definirá el JSON que indica a su lógica empresarial que debe hacer lo siguiente:

   * Iniciar la función de algoritmo de clasificación mediante el indicador de función test_sorting
   * Ejecutar el algoritmo de ordenación `best_sellers` definido en `sorting_algorithm _**_attribute`
   * Devolver 50 productos por página según la estrategia de paginación definida en `pagination_limit`

   >[!NOTE]
   >
   >Cuando [!DNL Adobe Target] agrupa a un usuario para ver la Experiencia B, se devuelve el JSON con los atributos definidos en el ejemplo. En su código, deberá comprobar el valor del indicador de característica `test_sorting` para ver si la característica de ordenación debe estar activada. Si es así, utilizará el valor `best_sellers` del atributo `sorting_algorithm` para mostrar los productos más vendidos en la vista de lista de productos. El límite de productos que se mostrarán para la aplicación será 50, ya que ese es el valor del atributo `pagination_limit`.

   ![imagen alt](assets/asset-sorting-b.png)

## &#x200B;4. Añadir una audiencia

En el paso **[!UICONTROL Segmentación]**, mantenga la audiencia de **[!UICONTROL Todos los visitantes]**. Esto le permitirá comprender el impacto de la función de clasificación, así como qué algoritmo y número de elementos influyen mejor en los resultados.

![imagen alt](assets/asset-audience-b.png)

## &#x200B;5. Establecer asignación de tráfico

Defina el porcentaje de visitantes con el que desea probar los algoritmos de ordenación y la estrategia de paginación. En otras palabras, ¿a qué porcentaje de los usuarios desea desplegar esta prueba? En este ejemplo, para implementar esta prueba para todos los usuarios que iniciaron sesión, mantenga la asignación de tráfico al 100%.

![imagen alt](assets/asset-allocation-100.png)

## &#x200B;6. Establecer la distribución del tráfico en variaciones

Defina el porcentaje de visitantes que verán el algoritmo de clasificación recomendado frente al algoritmo de clasificación de los más vendidos, con un límite de 50 productos por página. En este ejemplo, mantenga la distribución del tráfico como una división 50/50 entre las experiencias A y B.

![imagen alt](assets/asset-variations-50.png)

## &#x200B;7. Configuración de informes

En el paso **[!UICONTROL Objetivos y configuración]**, elige **[!UICONTROL Adobe Target]** como **[!UICONTROL Source de informes]** para ver los resultados de tu prueba A/B en la interfaz de usuario de [!DNL Adobe Target], o elige **[!UICONTROL Adobe Analytics]** para verlos en la interfaz de usuario de Adobe Analytics.

![imagen alt](assets/asset-reporting-b.png)

## &#x200B;8. Agregar métricas para KPI de seguimiento

Elija una **[!UICONTROL Métrica de objetivo]** para medir la prueba de características con atributos. En este ejemplo, el éxito se basa en si el usuario compra un producto, según el algoritmo de ordenación y la estrategia de paginación que se hayan mostrado.

## &#x200B;9. Implementar pruebas de características con atributos en la aplicación

>[!BEGINTABS]

>[!TAB Nodo.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const options = {
  client: "testClient",
  organizationId: "ABCDEF012345677890ABCDEF0@AdobeOrg",
  decisioningMethod: "on-device",
  events: {
    clientReady: targetClientReady
  }
};
const targetClient = TargetClient.create(options);

function targetClientReady() {
  return targetClient.getAttributes(["product-results-page"]).then(function(attributes) {
    const test_sorting = attributes.getValue("product-results-page", "test-sorting");
    const sorting_algorithm = attributes.getValue("product-results-page", "sorting_algorithm");
    const pagination_limit = attributes.getValue("product-results-page", "pagination_limit");
  });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

ClientConfig config = ClientConfig.builder()
    .client("testClient")
    .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
    .build();
TargetClient targetClient = TargetClient.create(config);
MboxRequest mbox = new MboxRequest().name("product-results-page").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## &#x200B;10. Implementación de código para hacer un seguimiento de eventos de conversión

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
            name : "product-results-page"
          }
        }
      ]
    }
})
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

Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## &#x200B;11. Activación de las pruebas de funciones con atributos

![imagen alt](assets/asset-activate.png)
