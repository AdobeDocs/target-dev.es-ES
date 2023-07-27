---
title: Ejecución de pruebas de funciones con atributos
description: Ejecución de pruebas de funciones con atributos
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Ejecución de pruebas de funciones con atributos

## Resumen de los pasos

1. Activar [!UICONTROL toma de decisiones en el dispositivo] para su organización
1. Crear un [!UICONTROL Prueba A/B] actividad
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

## 1. Habilitar [!UICONTROL toma de decisiones en el dispositivo] para su organización

Al habilitar la toma de decisiones en el dispositivo, se garantiza que una actividad A/B se ejecute con una latencia cercana a cero. Para habilitar esta función, vaya a **[!UICONTROL Administration]** > **[!UICONTROL Implementación]** > **[!UICONTROL Detalles de la cuenta]** in [!DNL Adobe Target]y habilite la opción **[!UICONTROL Toma de decisiones en el dispositivo]** alternar.

![imagen alt](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Debe tener el administrador o aprobador [función de usuario](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) para habilitar o deshabilitar **[!UICONTROL Toma de decisiones en el dispositivo]** alternar.

Después de activar el **[!UICONTROL Toma de decisiones en el dispositivo]** alternar, [!DNL Adobe Target] comienza a generar *artefactos de regla* para su cliente.

## 2. Crear un [!UICONTROL Prueba A/B] actividad

1. Entrada [!DNL Adobe Target], vaya al **[!UICONTROL Actividades]** página, luego seleccione **[!UICONTROL Crear actividad]** > **[!UICONTROL Prueba A/B]**.

   ![imagen alt](assets/asset-ab.png)

1. En el **[!UICONTROL Crear actividad de prueba A/B]** modal, mantenga el valor predeterminado **[!UICONTROL Web]** opción seleccionada (1), seleccionar **[!UICONTROL Form]** como compositor de experiencias (2), seleccione **[!UICONTROL Workspace predeterminado]** con **[!UICONTROL Sin restricciones de propiedad]** (3) y haga clic en **[!UICONTROL Siguiente]** (4).

   ![imagen alt](assets/asset-form.png)

## 3. Defina su A y B

1. En el **[!UICONTROL Experiencias]** Paso de creación de la actividad, asigne un nombre a su actividad (1) y añada una segunda experiencia, Experiencia B, haciendo clic en **[!UICONTROL Añadir experiencia]** Botón (2). Introduzca el nombre de la ubicación (3) dentro de la aplicación en la que desea ejecutar la prueba de funciones con atributos. En el ejemplo que se muestra a continuación, `product-results-page` es la ubicación definida para la Experiencia A. (También es la ubicación definida para la Experiencia B).

   ![imagen alt](assets/asset-location.png)

   **[!UICONTROL Experiencia A]** contendrá el JSON que indica a la lógica empresarial que debe hacer lo siguiente:

   * Inicie la función de algoritmo de clasificación mediante el `test_sorting` indicador de funcionalidad
   * Ejecute el algoritmo de ordenación recomendado definido en la variable `sorting_algorithm _**_attribute`
   * Devolver 50 productos por página según la estrategia de paginación definida en la `pagination_limit`

1. En la Experiencia A, haga clic en para cambiar el contenido de **[!UICONTROL Contenido predeterminado]** al archivo JSON seleccionando **[!UICONTROL Crear oferta JSON]** como se muestra a continuación (1).

   ![imagen alt](assets/asset-offer.png)

1. Defina el JSON con `test_sorting`, `sorting_algorithm`, y `pagination_limit` indicadores y atributos que se utilizarán para iniciar el algoritmo de ordenación recomendado con un límite de paginación de 50 productos.

   >[!NOTE]
   >
   >Cuándo [!DNL Adobe Target] agrupa a un usuario para ver la Experiencia A; se devolverá el JSON con los atributos definidos en el ejemplo. En el código, deberá comprobar el valor del indicador de funcionalidad `test_sorting` para ver si la función de ordenación debe estar activada. Si es así, utilizará el valor recomendado de `sorting_algorithm` para mostrar los productos recomendados en la vista de lista de productos. El límite de productos que se mostrarán para la aplicación será 50, ya que ese es el valor de `pagination_limit` atributo.

   ![imagen alt](assets/asset-sorting.png)

   **[!UICONTROL Experiencia B]** definirá el JSON que indica a su lógica empresarial que debe hacer lo siguiente:

   * Iniciar la función de algoritmo de clasificación mediante el indicador de función test_sorting
   * Ejecute el `best_sellers` algoritmo de ordenación definido en `sorting_algorithm _**_attribute`
   * Devolver 50 productos por página según la estrategia de paginación definida en la `pagination_limit`

   >[!NOTE]
   >
   >Cuándo [!DNL Adobe Target] agrupa a un usuario para ver la Experiencia B, se devuelve el JSON con los atributos definidos en el ejemplo. En el código, deberá comprobar el valor del indicador de funcionalidad `test_sorting` para ver si la función de ordenación debe estar activada. Si es así, utilice la variable `best_sellers` valor del `sorting_algorithm` para mostrar los productos más vendidos en la vista de lista de productos. El límite de productos que se mostrarán para la aplicación será 50, ya que ese es el valor de `pagination_limit` atributo.

   ![imagen alt](assets/asset-sorting-b.png)

## 4. Añada una audiencia

En el **[!UICONTROL Segmentación]** paso, conserve el **[!UICONTROL Todos los visitantes]** audiencia. Esto le permitirá comprender el impacto de la función de clasificación, así como qué algoritmo y número de elementos influyen mejor en los resultados.

![imagen alt](assets/asset-audience-b.png)

## 5. Establecer la asignación del tráfico

Defina el porcentaje de visitantes con el que desea probar los algoritmos de ordenación y la estrategia de paginación. En otras palabras, ¿a qué porcentaje de los usuarios desea desplegar esta prueba? En este ejemplo, para implementar esta prueba para todos los usuarios que iniciaron sesión, mantenga la asignación de tráfico al 100%.

![imagen alt](assets/asset-allocation-100.png)

## 6. Establecer la distribución del tráfico en variaciones

Defina el porcentaje de visitantes que verán el algoritmo de clasificación recomendado frente al algoritmo de clasificación de los más vendidos, con un límite de 50 productos por página. En este ejemplo, mantenga la distribución del tráfico como una división 50/50 entre las experiencias A y B.

![imagen alt](assets/asset-variations-50.png)

## 7. Configurar informes

En el **[!UICONTROL Objetivos y configuración]** paso, elija **[!UICONTROL Adobe Target]** como el **[!UICONTROL Fuente de informes]** para ver los resultados de las pruebas A/B en la [!DNL Adobe Target] IU o elija **[!UICONTROL Adobe Analytics]** para verlos en la interfaz de usuario de Adobe Analytics.

![imagen alt](assets/asset-reporting-b.png)

## 8. Agregar métricas para el seguimiento de KPI

Elija una **[!UICONTROL Métrica de objetivo]** para medir la prueba de características con atributos. En este ejemplo, el éxito se basa en si el usuario compra un producto, según el algoritmo de ordenación y la estrategia de paginación que se hayan mostrado.

## 9. Implemente pruebas de funciones con atributos en la aplicación

>[!BEGINTABS]

>[!TAB Node.js]

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

## 10. Implementar código para rastrear eventos de conversión

>[!BEGINTABS]

>[!TAB Node.js]

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

## 11. Active las pruebas de funciones con atributos

![imagen alt](assets/asset-activate.png)
