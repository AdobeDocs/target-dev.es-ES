---
title: Administración de despliegues para pruebas de funciones
description: Obtenga información sobre cómo administrar despliegues para pruebas de características usando [!UICONTROL toma de decisiones en el dispositivo].
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
TQID: https://experienceleague.adobe.com/soG8leVV3R4Y4FSns5oIJ43oziIhtOb2zJ5bkFYxeo0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 596
ht-degree: 1%

---

# Administración de despliegues para pruebas de funciones

## Resumen de los pasos

1. Habilitar [!UICONTROL toma de decisiones en el dispositivo] para su organización
1. Crear una actividad [!UICONTROL Prueba A/B]
1. Definición de la configuración de funciones y despliegue
1. Implementar y procesar la función en la aplicación
1. Implementar el seguimiento de eventos en la aplicación
1. Activación de la actividad A/B
1. Ajuste el despliegue y la asignación de tráfico según sea necesario

## &#x200B;1. Habilitar [!UICONTROL toma de decisiones en el dispositivo] para su organización

Al habilitar la toma de decisiones en el dispositivo, se garantiza que una actividad A/B se ejecute con una latencia cercana a cero. Para habilitar esta característica, vaya a **[!UICONTROL Administración]** > **[!UICONTROL Implementación]** > **[!UICONTROL Detalles de la cuenta]** en [!DNL Adobe Target] y habilite la opción **[!UICONTROL Toma de decisiones en el dispositivo]**.

![imagen alt](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Debe tener el rol de administrador o aprobador [user](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=es) para habilitar o deshabilitar la opción [!UICONTROL On-Device Decisioning].

Después de habilitar la opción [!UICONTROL Toma de decisiones en el dispositivo], [!DNL Adobe Target] comienza a generar *artefactos de regla* para su cliente.

## &#x200B;2. Crear una actividad [!UICONTROL Prueba A/B]

1. En [!DNL Adobe Target], vaya a la página **[!UICONTROL Actividades]** y, a continuación, seleccione **[!UICONTROL Crear actividad]** > **[!UICONTROL Prueba A/B]**.

   ![imagen alt](assets/asset-ab.png)

1. En el modal **[!UICONTROL Crear actividad de prueba A/B]**, deje seleccionada la opción predeterminada **[!UICONTROL Web]** (1), seleccione **[!UICONTROL Formulario]** como compositor de experiencias (2), seleccione **[!UICONTROL Workspace predeterminado]** con **[!UICONTROL Sin restricciones de propiedad]** (3) y haga clic en **[!UICONTROL Siguiente]** (4).

   ![imagen alt](assets/asset-form.png)

## &#x200B;3. Definición de la configuración de funciones y despliegue

En el paso de creación de la actividad **[!UICONTROL Experiencias]**, indique un nombre para su actividad (1). Introduzca el nombre de la ubicación (2) dentro de la aplicación donde desea administrar los despliegues de la función. Por ejemplo, `ondevice-rollout` o `homepage-addtocart-rollout` son nombres de ubicación que indican los destinos para administrar los despliegues de características. En el siguiente ejemplo, `ondevice-rollout` es la ubicación definida para la Experiencia A. Si lo desea, puede añadir refinamientos de audiencia (4) para restringir la calificación a la actividad.

![imagen alt](assets/asset-location-rollout.png)

1. En la sección **[!UICONTROL Contenido]** de la misma página, seleccione **[!UICONTROL Crear oferta JSON]** en la lista desplegable (1) como se muestra.

   ![imagen alt](assets/asset-offer.png)

1. En el cuadro de texto **[!UICONTROL Datos JSON]** que aparece, escriba la variable de indicador de característica para la característica que desea implementar con esta actividad en la Experiencia A (1), usando un objeto JSON válido (2).

   ![imagen alt](assets/asset-json-a-rollout.png)

1. Haga clic en **[!UICONTROL Siguiente]** (1) para avanzar al paso **[!UICONTROL Segmentación]** de creación de actividad.

   ![imagen alt](assets/asset-next-2-t-rollout.png)

1. En el paso **[!UICONTROL Segmentación]**, mantenga la audiencia de **[!UICONTROL Todos los visitantes]** (1) para simplificar. Sin embargo, ajuste la asignación de tráfico (2) al 10 %. Esto restringirá la función a solo el 10 % de los visitantes del sitio. Haga clic en Siguiente (3) para avanzar al paso **[!UICONTROL Objetivos y configuración]**.

   ![imagen alt](assets/asset-next-2-g-rollout.png)

1. En el paso **[!UICONTROL Objetivos y configuración]**, elige **[!UICONTROL Adobe Target]** (1) como **[!UICONTROL Source de informes]** para ver los resultados de tu actividad en la interfaz de usuario de [!DNL Adobe Target].

1. Elija una **[!UICONTROL Métrica de objetivo]** para medir la actividad. En este ejemplo, una conversión correcta se basa en si el usuario compra un artículo, tal como indica si el usuario llegó a la ubicación orderConfirm (2).

1. Haga clic en **[!UICONTROL Guardar y cerrar]** (3) para guardar la actividad.

   ![imagen alt](assets/asset-conv-rollout.png)

## &#x200B;4. Implementar y procesar la función en la aplicación

>[!BEGINTABS]

>[!TAB Nodo.js]

```js {line-numbers="true"}
targetClient.getAttributes(["ondevice-rollout"]).then(function(attributes) {
      const featureFlags = attributes.asObject("ondevice-rollout");

      // Your flag variables are now available in the featureFlags object variable.
      //If you failed to qualify for the Activity, you will have an empty object.
      console.log(featureFlags);
    });
```

>[!TAB Java]

```java {line-numbers="true"}
    Attributes attrs = targetJavaClient.getAttributes(targetDeliveryRequest, "ondevice-rollout");
    Map<String, Object> featureFlags = attrs.toMboxMap("ondevice-rollout");
​
    // Your flag variables are now available in the featureFlags object variable.
    //If you failed to qualify for the Activity, you will have an empty object.
    System.out.println(featureFlags);
```

>[!ENDTABS]

## &#x200B;5. Implementar el seguimiento de eventos en la aplicación

Después de hacer que la variable de indicador de funcionalidad esté disponible en la aplicación, puede utilizarla para habilitar cualquier función que ya forme parte de la aplicación. Si un visitante no cumple los requisitos para la actividad, significa que no se incluyó como parte del bloque del 10 % definido como audiencia.

>[!BEGINTABS]

>[!TAB Nodo.js]

```js {line-numbers="true"}
//... Code removed for brevity

if(featureFlags.enable == "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}

// alternatively, the getValue method could be used on the Attributes object.

if(attributes.getValue("ondevice-rollout", "enable") === "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}
```

>[!TAB Java]

```java {line-numbers="true"}
//... Code removed for brevity
​
if("yes".equals(String.valueOf(featureFlags.get("enable")))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
​
// alternatively, the getString method could be used on the Attributes object.
​
if("yes".equals(attrs.getString("ondevice-rollout", "enable"))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
```

>[!ENDTABS]

## &#x200B;6. Activación de la actividad de despliegue

![imagen alt](assets/asset-activate-rollout.png)

## &#x200B;7. Ajuste el despliegue y la asignación de tráfico según sea necesario

Una vez que haya activado la actividad, edítela en cualquier momento para aumentar o disminuir la asignación de tráfico según sea necesario.

Aumento de la asignación del tráfico del 10 % al 50 % debido al éxito del despliegue inicial.

![imagen alt](assets/asset-adjust-rollout.png)
