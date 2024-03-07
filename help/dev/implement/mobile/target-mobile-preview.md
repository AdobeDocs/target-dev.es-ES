---
keywords: control de calidad, vista previa, vínculo de vista previa, móvil, vista previa para móviles
description: Utilice los vínculos de vista previa para móviles para realizar un completo control de calidad de las actividades de aplicaciones móviles.
title: ¿Cómo utilizo los vínculos de vista previa para móviles en? [!DNL Adobe Target] ¿Móvil?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 15e42d0fb049f9243ff5468ff5f22a8e79c55c79
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 23%

---

# [!DNL Target] vista previa para móviles

Use los vínculos de vista previa en móviles para realizar fácilmente un control de calidad exhaustivo de las actividades de aplicaciones móviles y registrarse en diferentes experiencias con el dispositivo sin tener que usar ningún dispositivo de prueba especial.

La funcionalidad de vista previa para móviles le permite probar completamente sus actividades de aplicación móvil antes del lanzamiento.

## Requisitos previos  

1. **Utilice una versión compatible del SDK:** La función de vista previa para móviles requiere que descargue e instale la versión adecuada de [!DNL Adobe Mobile SDK] en sus aplicaciones correspondientes.

   Para obtener instrucciones para descargar el SDK adecuado, consulte [Versiones actuales del SDK](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} en el *[!DNL Adobe Experience Platform Mobile SDK]* documentación.

1. **Configure un esquema de direcciones URL:** el vínculo de vista previa utiliza un esquema de direcciones URL para abrir la aplicación. Especifique un esquema URL único para la vista previa.

   Para obtener más información, consulte [Vista previa](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Configurar la extensión de Target en la interfaz de usuario de la conexión de datos* en el *[!DNL Mobile SDK]* documentación.

   Los siguientes vínculos contienen más información:

   * **iOS**: para obtener más información sobre la configuración de esquemas de URL para iOS, consulte [Definición de un esquema de URL personalizado para la aplicación](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} en el *Apple Developer* sitio web.
   * **Android**: Para obtener más información sobre la configuración de esquemas de URL para Android, consulte [Creación de vínculos profundos al contenido de la aplicación](https://developer.android.com/training/app-links/deep-linking){target=_blank} en el *Desarrolladores de Android* sitio web.

1. **Configure las variables `collectLaunchInfo` API (solo i0S)**

   Para obtener más información, consulte [Vista previa](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Configurar la extensión de Target en la interfaz de usuario de la conexión de datos* en el *[!DNL Mobile SDK]* documentación.

## Generación de un vínculo de vista previa

1. En el [!DNL Target] IU, haga clic en **[!UICONTROL More Options]** (los puntos suspensivos verticales), y seleccione **[!UICONTROL Create Mobile Preview Link]**.

   ![imagen alt](assets/mobile-preview-create.png)

1. Seleccione las actividades que desea previsualizar y haga clic en **[!UICONTROL Generate Mobile Preview Link]**.

   >[!NOTE]
   >
   >Solo puede seleccionar Basado en formularios [!UICONTROL A/B Test] y [!UICONTROL Experience Targeting] Actividades de (XT).

   ![imagen alt](assets/mobile-preview-select-activities.png)

1. Especifique el esquema de URL de su aplicación.

   El esquema de URL debe ser el mismo que el presente en la aplicación de iOS o Android. Repita este proceso por separado para iOS y Android, si es necesario.

   ![imagen alt](assets/mobile-preview-enter-url-scheme.png)

1. Clic **[!UICONTROL Generate Mobile Preview Link]** y, a continuación, copie el vínculo.

   ![imagen alt](assets/mobile-preview-generate-and-copy.png)

## Vista previa en su dispositivo

Abra el vínculo en un navegador móvil en un dispositivo en el que tenga instalada la aplicación. Esta aplicación puede ser la aplicación de producción que descargó del [!DNL Apple App Store] o el [!DNL Google Play Store]. No es necesario que la aplicación sea una compilación especial. Si tiene un vínculo de vista previa activo, puede ver las experiencias en el dispositivo.

1. Abra el vínculo en su navegador móvil.

   Comparta el vínculo que copió en la sección anterior desde el [!DNL Target] Conecte la interfaz de usuario a su dispositivo móvil de forma práctica, por ejemplo, mediante texto, correo electrónico o [!DNL Slack].

   |![vista previa del vínculo profundo 1](assets/mobile-preview-open-deeplink.png)|![vista previa del vínculo profundo 2](assets/mobile-preview-open-app.png)|

   La aplicación se abre e inicia el [!DNL Target] [!UICONTROL Mobile Preview Mode].

1. Seleccione la combinación de experiencias que desee ver y haga clic en **[!UICONTROL Launch Experiences]**.

   |![vista previa para móvil 1](assets/mobile-preview-experience-selection-1.png)|![vista previa para móvil 2](assets/mobile-preview-experience-result-1-france.png)|![vista previa para móvil 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![vista previa para móvil 4](assets/mobile-preview-experience-selection-2.png)|![vista previa para móvil 5](assets/mobile-preview-experience-result-2-aus.png)|![vista previa para móvil 6](assets/mobile-preview-experience-result-2-10off.png)|

## Limitaciones  

* La vista debe cargarse de nuevo para que el nuevo contenido se muestre después de **[!UICONTROL Launch Experiences]** Haga clic en el botón. El modo más sencillo es cambiar a una pantalla diferente y regresar a aquella en la que espera que se produzca el cambio.
* La vista previa para móviles no es compatible con las versiones de Android anteriores a API-19 (KitKat).
