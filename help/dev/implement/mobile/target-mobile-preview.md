---
keywords: control de calidad, vista previa, vínculo de vista previa, móvil, vista previa para móviles
description: Utilice los vínculos de vista previa para móviles para realizar un completo control de calidad de las actividades de aplicaciones móviles. Puede inscribirse en diferentes experiencias sin dispositivos de prueba especiales.
title: ¿Cómo utilizo el vínculo de vista previa para móviles en? [!DNL Target] ¿Móvil?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 68%

---

# [!DNL Target] vista previa para móviles

Use el vínculo de vista previa en móviles para realizar fácilmente un control de calidad exhaustivo de las actividades de aplicaciones móviles y registrarse en diversas experiencias directamente en el dispositivo sin tener que usar uno especial para pruebas.

>[!NOTE]
>
>La función de vista previa para móviles requiere que descargue e instale la versión apropiada (4.14 o posterior) del SDK de Adobe Mobile.

## Información general

La funcionalidad de vista previa para móviles le permite probar completamente sus actividades de aplicación móvil antes del lanzamiento.

## Requisitos previos  

1. **Utilice una versión compatible del SDK:** la función de vista previa para móviles requiere que descargue e instale la versión apropiada (4.14 o posterior) del SDK de Adobe Mobile en las aplicaciones correspondientes.

   Para obtener instrucciones sobre la descarga del SDK apropiado, consulte:

   * **iOS:** [Antes de comenzar](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/requirements.html) en el *Ayuda de Mobile Services para iOS*.
   * **Android:** [Antes de comenzar](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html) en el *Ayuda de Mobile Services para Android*.

1. **Configure un esquema de direcciones URL:** el vínculo de vista previa utiliza un esquema de direcciones URL para abrir la aplicación. Debe especificar un esquema de URL único para la vista previa.

   La siguiente ilustración muestra un ejemplo en iOS:

   ![imagen alt](assets/mobile-preview-url-scheme-ios.png)

   La siguiente ilustración muestra un ejemplo en Android:

   ![imagen alt](assets/Android_Deeplink.png)

1. **Seguimiento de Adobe DeepLink**

   **iOS:** en el delegado de la aplicación, realice una llamada a `[ADBMobile trackAdobeDeepLink:url` cuando se le pida al delegado que abra el recurso con el esquema de la URL especificado en el paso anterior.

   El siguiente fragmento de código es un ejemplo:

   ```javascript {line-numbers="true"}
   - (BOOL) application:(UIApplication *)app openURL:(NSURL *)url 
                options:(NSDictionary<NSString *,id> *)options { 
   
       if ([[url scheme] isEqualToString:@"com.adobe.targetmobile"]) { 
           [ADBMobile trackAdobeDeepLink:url]; 
           return YES; 
       } 
       return NO; 
   } 
   ```

   **Android:** en la aplicación, realice una llamada a `Config.trackAdobeDeepLink(URL);` cuando se pida a la persona que llama que abra el recurso con el esquema de la URL especificado en el paso anterior.

   ```javascript {line-numbers="true"}
    private Boolean shouldOpenDeeplinkUrl() { 
        Intent appLinkIntent = getIntent(); 
        String appLinkAction = appLinkIntent.getAction(); 
        Uri appLinkData = appLinkIntent.getData; 
        if (appLinkData.toString().startsWith("com.adobe.targetmobile")) { 
            Config.trackAdobeDeepLink(appLinkData); 
            return true; 
        } 
        return false; 
     }
   ```

   Para que la vista previa para móviles funcione en Android, también debe añadir el siguiente fragmento de código en AndroidManifest.xml si utiliza la versión 5 del SDK de Adobe Mobile:

   ```javascript {line-numbers="true"}
   <activity android:name="com.adobe.marketing.mobile.FullscreenMessageActivity" />
   ```

   Si utiliza la versión 4 del SDK de Adobe Mobile, utilice el siguiente fragmento de código:

   ```javascript {line-numbers="true"}
   <activity android:name="com.adobe.mobile.MessageFullScreenActivity" />
   ```

## Generación de un vínculo de vista previa

1. En el [!DNL Target] IU, haga clic en **[!UICONTROL Más opciones]** (tres elipses verticales) y, a continuación, seleccione **[!UICONTROL Crear vista previa para móviles]**.

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
