---
keywords: aplicación móvil,sdk de aep,aplicación nativa,vistas web,nativa;swift,sdk móvil de adobe experience platform,sdk móvil,código nativo
description: Aprenda a implementar [!DNL Adobe Target] con [!DNL AEP Mobile SDK] en una aplicación nativa con vistas web.
title: Implementar [!DNL Adobe Target] en una aplicación móvil que usa código nativo con vistas web
feature: Implement Mobile
role: Developer
exl-id: 3dd2e1d7-c744-4ba8-aaa4-6c2fe64d01fa
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Implementar [!DNL Target] con [!DNL AEP Mobile SDK] en una aplicación nativa con vistas web

Este artículo comparte prácticas recomendadas para implementar [!DNL Adobe Target] en una aplicación móvil que usa código nativo con vistas web mediante [!DNL Adobe Experience Platform Mobile SDK].

Este artículo usa una aplicación iOS de ejemplo que usa la integración [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} y [!DNL Target] escrita en [Swift desde el repositorio de GitHub](https://github.com/adobe/aep-sdk-app/){target=_blank}.

En el mundo real, es probable que la aplicación empresarial utilice vistas web en la aplicación móvil. Una vista web es un contenedor que carga una página web mediante una dirección URL. El contenedor es similar a una ventana de explorador sin controles. En iOS, el contenedor de vista web funciona como un explorador Safari al procesar páginas web.

## Requisitos previos  

Para comenzar con [!DNL Adobe Experience Platform Mobile SDK], debe realizar algunas tareas previas.

Para obtener más información, consulte [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} en la documentación de [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank}.

## Sincronizar código nativo con vistas web

El desafío que se presenta al implementar [!DNL Target] en una aplicación nativa con vistas web es que [!DNL Adobe Experience Platform Mobile SDK] ya ha generado todos los identificadores necesarios para que las soluciones de [!DNL Adobe] funcionen sin problemas. Sin embargo, los identificadores aún no son visibles para las vistas web porque no están en el entorno de plataforma nativo. Por lo tanto, debe crear un puente para pasar algunos identificadores SDK a las vistas web para que la identidad del visitante persista en el entorno web. Si no lo hace correctamente, se duplican las visitas, lo que afecta a los informes.

Afortunadamente, [!DNL Adobe Experience Platform Mobile SDK] proporciona un método conveniente para generar [!DNL Adobe] parámetros necesarios para que las vistas web se consuman y persistan para el mismo visitante, como se muestra en el siguiente código de ejemplo:

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

Para obtener más información acerca del método `Identity.appendTo` y ver un ejemplo de cómo utilizarlo, vea [Swift > Example](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} en la *documentación del SDK móvil*.

Con `Identity.appendTo`, esta dirección URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

se transforma en:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Como puede ver, hay un parámetro `adobe_mc` anexado a la dirección URL. Este parámetro contiene valores codificados para:

* TS=1660667205: La marca de tiempo actual. Esta marca de tiempo garantiza que la vista web no reciba valores caducados.
* MCMID=69624092487065093697422606480535692677: [!UICONTROL Experience Cloud ID] (ECID). También conocido como MID o [!UICONTROL Marketing Cloud ID], requerido para la identificación de visitantes entre soluciones [!DNL Adobe].
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: El [!UICONTROL Adobe Organization ID].

El `Identity.getUrlVariables` es un método [!DNL Adobe Experience Platform Mobile SDK] alternativo que devuelve una cadena formada correctamente que contiene las variables de dirección URL [!DNL Experience Cloud Identity Service]. Para obtener más información, consulte [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} en la *referencia de API de identidad*.

## Pasar el ID de sesión [!DNL Target] para la experiencia en la misma sesión

Se necesita un paso adicional para que el recorrido del usuario [!DNL Target] funcione sin problemas en las vistas nativa y web. Este paso incluye la extracción y el paso del ID de sesión [!DNL Target] de [!DNL Adobe Experience Platform Mobile SDK] a las vistas web de la aplicación móvil.

El `Target.getSessionId` extrae el ID de sesión que se puede pasar a la URL de vista web como parámetro de `mboxSession`:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Realizar pruebas en las vistas web

Los vínculos de vista previa web se generan en la página [!UICONTROL Activity detail] al hacer clic en el vínculo [[!UICONTROL Adobe QA] ](/help/dev/implement/mobile/target-mobile-preview.md) para mostrar una ventana emergente con el fin de copiar cada vínculo de vista previa de experiencia, de forma similar a la siguiente:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Los vínculos de vista previa web contienen `at_preview_index` y `at_preview_listed_activities_only` parámetros adicionales. Copie estos parámetros para construir vínculos de vista previa compatibles con dispositivos móviles con parámetros de vínculo web.

Por ejemplo:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Después de abrir el vínculo en un explorador iOS Safari, la aplicación captura la dirección URL en la clase `AppDelegate` de forma similar al siguiente ejemplo:

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
