---
keywords: control de calidad, vista previa, vínculo de vista previa, móvil, vista previa para móviles
description: Utilice los vínculos de vista previa para móviles para realizar un completo control de calidad de las actividades de aplicaciones móviles. Puede inscribirse en diferentes experiencias sin dispositivos de prueba especiales.
title: ¿Cómo utilizo el vínculo de vista previa para móviles en? [!DNL Target] ¿Móvil?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 97c96e63f9121793a83b445ad3dc33c5d094509a
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 51%

---

# [!DNL Target] vista previa para móviles

Use el vínculo de vista previa en móviles para realizar fácilmente un control de calidad exhaustivo de las actividades de aplicaciones móviles y registrarse en diversas experiencias directamente en el dispositivo sin tener que usar uno especial para pruebas.

## Información general

La funcionalidad de vista previa para móviles le permite probar completamente sus actividades de aplicación móvil antes del lanzamiento.

## Requisitos previos  

1. **Utilice una versión compatible del SDK:** La función de vista previa para móviles requiere que descargue e instale la versión adecuada del SDK de Adobe Mobile en sus aplicaciones correspondientes.

   Para obtener instrucciones para descargar el SDK adecuado, consulte [Versiones actuales del SDK](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} en el *[!DNL Adobe Experience Platform Mobile SDK]* documentación.

1. **Configure un esquema de direcciones URL:** el vínculo de vista previa utiliza un esquema de direcciones URL para abrir la aplicación. Debe especificar un esquema de URL único para la vista previa.

   Para obtener más información, consulte [Vista previa](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Adobe Target* en el *[!DNL Adobe Experience Platform Mobile SDK]* documentación.

   Los siguientes vínculos contienen más información:

   * **iOS**: para obtener más información sobre la configuración de esquemas de URL para iOS, consulte [Definición de un esquema de URL personalizado para la aplicación](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} en el sitio web de Apple Developer.
   * **Android**: Para obtener más información sobre la configuración de esquemas de URL para Android, consulte [Creación de vínculos profundos al contenido de la aplicación](https://developer.android.com/training/app-links/deep-linking){target=_blank} en el sitio web de desarrolladores de Android.

1. **Configuración de `collectLaunchInfo` API (solo i0S)**

   Para obtener más información, consulte [Vista previa](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Adobe Target* en el *[!DNL Adobe Experience Platform Mobile SDK]* documentación.

## Generación de un vínculo de vista previa

1. En el [!DNL Target] IU, haga clic en **[!UICONTROL Más opciones]** (los puntos suspensivos verticales), y seleccione **[!UICONTROL Crear vista previa para móviles]**.

   ![imagen alt](assets/mobile-preview-create.png)

1. Seleccione las actividades que desea previsualizar y haga clic en **[!UICONTROL Generar vínculo de vista previa para móviles]**.

   >[!NOTE]
   >
   >Solo se pueden seleccionar actividades AB y XT basadas en formularios.

   ![imagen alt](assets/mobile-preview-select-activities.png)

1. Especifique el esquema de URL de su aplicación.

   Debe ser el mismo que está presente en su aplicación iOS o Android. Si es necesario, repita este proceso de forma separada para iOS y Android.

   ![imagen alt](assets/mobile-preview-enter-url-scheme.png)

1. Haga clic en **[!UICONTROL Generar vínculo de vista previa para móviles]** y, a continuación, copie el vínculo.

   ![imagen alt](assets/mobile-preview-generate-and-copy.png)

## Vista previa en su dispositivo

Abra el vínculo en un navegador móvil en un dispositivo en el que tenga instalada la aplicación. Puede ser la aplicación de producción descargada desde la tienda App Store de Apple o la tienda Google Play. No es necesario que sea una compilación especial. Si tiene un vínculo de vista previa activo, podrá ver las experiencias en el dispositivo.

1. Abra el vínculo en su navegador móvil.

   Comparta el vínculo que ha copiado en el paso anterior desde el [!DNL Target] Conecte la interfaz de usuario a su dispositivo móvil de forma práctica, por ejemplo, mediante texto, correo electrónico o Slack.

   |![vista previa del vínculo profundo 1](assets/mobile-preview-open-deeplink.png)|![vista previa del vínculo profundo 2](assets/mobile-preview-open-app.png)|

   La aplicación se abre e inicia el [!DNL Target] Modo de vista previa para móviles.

1. Seleccione la combinación de experiencias que desee usar y, a continuación, haga clic en **[!UICONTROL Launch Experiences]**.

   |![vista previa para móvil 1](assets/mobile-preview-experience-selection-1.png)|![vista previa para móvil 2](assets/mobile-preview-experience-result-1-france.png)|![vista previa para móvil 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![vista previa para móvil 4](assets/mobile-preview-experience-selection-2.png)|![vista previa para móvil 5](assets/mobile-preview-experience-result-2-aus.png)|![vista previa para móvil 6](assets/mobile-preview-experience-result-2-10off.png)|

## Limitaciones  

* Debe volver a cargarse la vista para que el nuevo contenido se muestre después de hacer clic en el botón **[!UICONTROL Launch Experiences]**. El modo más sencillo es cambiar a una pantalla diferente y regresar a aquella en la que espera que se produzca el cambio.
* La vista previa para móviles no es compatible con las versiones de Android anteriores a API-19 (KitKat).
