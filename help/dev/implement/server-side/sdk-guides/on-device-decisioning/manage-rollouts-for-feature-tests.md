---
title: Administración de despliegues para pruebas de funciones
description: Obtenga información sobre cómo administrar despliegues para pruebas de características usando [!UICONTROL on-device decisioning].
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Administración de despliegues para pruebas de funciones

## Resumen de los pasos

1. Habilitar [!UICONTROL on-device decisioning] para su organización
1. Crear una actividad [!UICONTROL A/B Test]
1. Definición de la configuración de funciones y despliegue
1. Implementar y procesar la función en la aplicación
1. Implementar el seguimiento de eventos en la aplicación
1. Activación de la actividad A/B
1. Ajuste el despliegue y la asignación de tráfico según sea necesario

## 1. Habilite [!UICONTROL on-device decisioning] para su organización

Al habilitar la toma de decisiones en el dispositivo, se garantiza que una actividad A/B se ejecute con una latencia cercana a cero. Para habilitar esta característica, vaya a **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** en [!DNL Adobe Target] y habilite la opción **[!UICONTROL On-Device Decisioning]**.

![imagen alt](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Debe tener el rol de administrador o aprobador [user](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) para habilitar o deshabilitar la opción [!UICONTROL On-Device Decisioning].

Después de habilitar la opción [!UICONTROL On-Device Decisioning], [!DNL Adobe Target] comienza a generar *artefactos de regla* para su cliente.

## 2. Crear una actividad [!UICONTROL A/B Test]

1. En [!DNL Adobe Target], vaya a la página **[!UICONTROL Activities]** y, a continuación, seleccione **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**.

   ![imagen alt](assets/asset-ab.png)

1. En el modal **[!UICONTROL Create A/B Test Activity]**, deje seleccionada la opción predeterminada **[!UICONTROL Web]** (1), seleccione **[!UICONTROL Form]** como compositor de experiencias (2), seleccione **[!UICONTROL Default Workspace]** con **[!UICONTROL No Property Restrictions]** (3) y haga clic en **[!UICONTROL Next]** (4).

   ![imagen alt](assets/asset-form.png)

## 3. Defina la función y la configuración de despliegue

En el paso **[!UICONTROL Experiences]** de creación de la actividad, indique un nombre para la actividad (1). Introduzca el nombre de la ubicación (2) dentro de la aplicación donde desea administrar los despliegues de la función. Por ejemplo, `ondevice-rollout` o `homepage-addtocart-rollout` son nombres de ubicación que indican los destinos para administrar los despliegues de características. En el siguiente ejemplo, `ondevice-rollout` es la ubicación definida para la Experiencia A. Si lo desea, puede añadir refinamientos de audiencia (4) para restringir la calificación a la actividad.

![imagen alt](assets/asset-location-rollout.png)

1. En la sección **[!UICONTROL Content]** de la misma página, seleccione **[!UICONTROL Create JSON Offer]** en la lista desplegable (1) como se muestra.

   ![imagen alt](assets/asset-offer.png)

1. En el cuadro de texto **[!UICONTROL JSON Data]** que aparece, escriba la variable de indicador de característica para la característica que desea implementar con esta actividad en la Experiencia A (1), usando un objeto JSON válido (2).

   ![imagen alt](assets/asset-json-a-rollout.png)

1. Haga clic en **[!UICONTROL Next]** (1) para avanzar al paso **[!UICONTROL Targeting]** de creación de la actividad.

   ![imagen alt](assets/asset-next-2-t-rollout.png)

1. En el paso **[!UICONTROL Targeting]**, mantenga la audiencia **[!UICONTROL All Visitors]** (1) para simplificar. Sin embargo, ajuste la asignación de tráfico (2) al 10 %. Esto restringirá la función a solo el 10 % de los visitantes del sitio. Haga clic en Siguiente (3) para avanzar al paso **[!UICONTROL Goals & Settings]**.

   ![imagen alt](assets/asset-next-2-g-rollout.png)

1. En el paso **[!UICONTROL Goals & Settings]**, elija **[!UICONTROL Adobe Target]** (1) como **[!UICONTROL Reporting Source]** para ver los resultados de su actividad en la interfaz de usuario de [!DNL Adobe Target].

1. Elija un(a) **[!UICONTROL Goal Metric]** para medir la actividad. En este ejemplo, una conversión correcta se basa en si el usuario compra un artículo, tal como indica si el usuario llegó a la ubicación orderConfirm (2).

1. Haga clic en **[!UICONTROL Save & Close]** (3) para guardar la actividad.

   ![imagen alt](assets/asset-conv-rollout.png)

## 4. Implementar y procesar la función en la aplicación

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

## 5. Implemente el seguimiento de eventos en la aplicación

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

## 6. Active la actividad de despliegue

![imagen alt](assets/asset-activate-rollout.png)

## 7. Ajuste el despliegue y la asignación de tráfico según sea necesario

Una vez que haya activado la actividad, edítela en cualquier momento para aumentar o disminuir la asignación de tráfico según sea necesario.

Aumento de la asignación del tráfico del 10 % al 50 % debido al éxito del despliegue inicial.

![imagen alt](assets/asset-adjust-rollout.png)
