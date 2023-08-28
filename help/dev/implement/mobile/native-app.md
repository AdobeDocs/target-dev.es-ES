---
keywords: aplicación móvil,sdk de aep,aplicación nativa,vistas web,nativa;swift,sdk móvil de adobe experience platform,sdk móvil,código nativo
description: Obtenga información sobre cómo implementar [!DNL Adobe Target] con el [!DNL AEP Mobile SDK] en una aplicación nativa con vistas web.
title: Implementación [!DNL Adobe Target] en una aplicación móvil que utiliza código nativo con vistas web
feature: Implement Mobile
role: Developer
source-git-commit: c0fda36cb5472d71438c47b8b484716003da4214
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# Implementación [!DNL Target] con el [!DNL AEP Mobile SDK] en una aplicación nativa con vistas web

Este artículo incluye prácticas recomendadas para la implementación de [!DNL Adobe Target] en una aplicación móvil que utiliza código nativo con vistas web mediante [!DNL Adobe Experience Platform Mobile SDK].

Este artículo utiliza una aplicación de iOS de ejemplo con [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} and a [!DNL Target] integration written in [Swift from the GitHub repository](https://github.com/adobe/aep-sdk-app/){target=_blank}.

En el mundo real, es probable que la aplicación empresarial utilice vistas web en la aplicación móvil. Una vista web es un contenedor que carga una página web mediante una dirección URL. El contenedor es similar a una ventana de explorador sin controles. En iOS, el contenedor de vista web funciona como un explorador Safari al procesar páginas web.

## Requisitos previos  

Para empezar a usar la [!DNL Adobe Experience Platform Mobile SDK], debe realizar algunas tareas previas necesarias.

Para obtener más información, consulte [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} documentación.

## Sincronizar código nativo con vistas web

El desafío al implementar [!DNL Target] en una aplicación nativa con vistas web es que la variable [!DNL Adobe Experience Platform Mobile SDK] ya ha generado todos los identificadores necesarios para [!DNL Adobe] soluciones para trabajar sin problemas. Sin embargo, los identificadores aún no son visibles para las vistas web porque no están en el entorno de plataforma nativo. Por lo tanto, debe crear un puente para pasar algunos identificadores SDK a las vistas web para que la identidad del visitante persista en el entorno web. Si no lo hace correctamente, se duplican las visitas, lo que afecta a los informes.

Afortunadamente, la [!DNL Adobe Experience Platform Mobile SDK] proporciona un método cómodo para generar [!DNL Adobe] parámetros necesarios para que las vistas web consuman y persistan para el mismo visitante, como se muestra en el siguiente código de ejemplo:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  print("appendedURL \(String(describing: appendedURL))")
  // load the url with ECID on the main thread
  DispatchQueue.main.async {
    let request = NSMutableURLRequest(url: appendedURL!)
    self.webView.load(request as URLRequest)
  }
});
```

Para obtener más información sobre `Identity.appendTo` y para ver un ejemplo de cómo utilizar el método, consulte [Swift > Ejemplo](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} en el *Documentación del SDK móvil*.

Uso de `Identity.appendTo`, esta URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

se transforma en:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Como puede ver, hay `adobe_mc` parámetro añadido a la dirección URL. Este parámetro contiene valores codificados para:

* TS=1660667205: La marca de tiempo actual. Esta marca de tiempo garantiza que la vista web no reciba valores caducados.
* MCMID=69624092487065093697422606480535692677: La variable [!UICONTROL ID de Experience Cloud] (ECID). También conocido como MID o [!UICONTROL ID de Marketing Cloud] requerido para [!DNL Adobe] identificación de visitantes entre soluciones.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: El [!UICONTROL ID de organización de Adobe].

El `Identity.getUrlVariables` es una alternativa [!DNL Adobe Experience Platform Mobile SDK] método que devuelve una cadena formada correctamente que contiene la variable [!DNL Experience Cloud Identity Service] Variables de URL. Para obtener más información, consulte [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} en el *Referencia de API de identidad*.

## Pase el [!DNL Target] ID de sesión para la experiencia en la misma sesión

Se necesita un paso adicional para realizar la [!DNL Target] el recorrido del usuario funciona sin problemas en las vistas nativa y web. Este paso incluye la extracción y el paso de [!DNL Target] ID de sesión de [!DNL Adobe Experience Platform Mobile SDK] a las vistas web de la aplicación móvil.

El `Target.getSessionId` extrae el ID de sesión que se puede pasar a la URL del visor web como un `mboxSession` parámetro:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Realizar pruebas en las vistas web

Los vínculos de vista previa web se generan en la [!UICONTROL Detalles de actividad] haciendo clic en el botón [[!UICONTROL ADOBE QA] vincular](/help/dev/implement/mobile/target-mobile-preview.md) para mostrar una ventana emergente para copiar cada vínculo de vista previa de experiencia, similar a la siguiente:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Los vínculos de vista previa web contienen `at_preview_index` y `at_preview_listed_activities_only` parámetros. Copie estos parámetros para construir vínculos de vista previa compatibles con dispositivos móviles con parámetros de vínculo web.

Por ejemplo:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Después de abrir el vínculo en un explorador iOS Safari, la aplicación captura la dirección URL en el `AppDelegate` clase similar al siguiente ejemplo:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

Ahora que ha capturado todos los parámetros necesarios en la aplicación, puede pasarlos a la web cuando sea necesario:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

El resultado final del vínculo de vista web puede tener este aspecto:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
