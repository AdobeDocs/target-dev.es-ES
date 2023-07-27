---
keywords: aplicación móvil, ubicación de aplicación móvil, segmentar por aplicación móvil, ubicaciones de segmentación por móvil, métricas de éxito de aplicaciones móviles
description: Vea un código de ejemplo para aprender a crear ubicaciones y métricas de éxito en aplicaciones de iOS para que pueda usar [!DNL Adobe Target] para personalizar y optimizar su aplicación.
title: ¿Cómo puedo crear? [!DNL Target] Ubicaciones y métricas de éxito en una aplicación de iOS
feature: Implement Mobile
exl-id: 755c8b26-5c60-48fc-9e7e-5e97a25edb78
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 67%

---

# iOS: crear un [!DNL Target] ubicación y métrica de éxito

Para usar [!DNL Target] en la aplicación móvil, cree una ubicación y una métrica de éxito.

>[!IMPORTANT]
>
>Compatibilidad con el [!DNL Adobe Mobile] versión 4.*x* SDK finalizó el 31 de agosto de 2021 y ya no se recomienda para [!DNL Adobe Target] usuarios móviles.
>
>El [SDK de Adobe Experience Platform para aplicaciones móviles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} es la solución recomendada para alimentar [!DNL Adobe Experience Cloud] soluciones y servicios en sus aplicaciones móviles.

Esta sección incluye código de ejemplo que se puede usar como plantilla en la aplicación. Los ejemplos de esta sección contienen código para iOS. Los mismos patrones sirven para Android. La sintaxis de Android se encuentra en la guía [](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/target-main.html)SDK para Android 4.x para soluciones de Experience Cloud.

>[!NOTE]
>
>Consulte la [Documentación móvil](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-target-methods.html) para obtener una lista de todos los [!DNL Target] métodos.

Para crear un [!DNL Target] En la ubicación de en la aplicación y realice una solicitud, hay dos métodos principales:

* `targetCreateRequestWithName`
* `targetLoadRequest`

1. Crear un [!DNL Target] ubicación.

   Esta es un ejemplo de llamada para crear una solicitud:

   ```
   // make your request 
   ADBTargetLocationRequest *myRequest = [ADBMobile targetCreateRequestWithName:@"heroBanner" 
                                                    defaultContent:@"default.png" 
                                                    parameters:nil];
   ```

   | Parámetro | Descripción |
   |---|---|
   | `ADBTargetLocationRequest *myRequest` | Sustituya `myRequest` por el nombre de su `targetLocation` en la aplicación. |
   | `targetCreateRequestWithName:@"heroBanner"` | Sustituya `heroBanner` por el nombre de su `targetLocation` en Target. Es igual que el nombre del mbox. Este banner a pantalla completa aparece en la interfaz de Target. |
   | `defaultContent:@"default.png"` | Sustituya `default.png` por el valor que usa la aplicación cuando Target no responde. |
   | `parameters:nil` | Indique los parámetros de perfil o mbox. Encontrará más información en la sección “Pasar datos personalizados”. |

   Esta es un ejemplo de llamada para cargar una solicitud:

   ```
   // load your request 
   [ADBMobile targetLoadRequest:myRequest callback:^(NSString *content) { 
                                        // do something with content 
                                        heroImage.image = [UIImage imageNamed:content]; 
   }];
   ```

   | Parámetro | Descripción |
   |---|---|
   | `targetLoadRequest:myRequest` | Sustituya `myRequest` por el nombre de su `targetLocation` en la aplicación. |
   | `NSString *content` | Sustituya “content” por el contenido que regresa de Adobe. La cadena puede ser XML, JSON o texto sin formato. Use esta sección del código para definir variables, establecer rutas de imágenes, ver flujos de controladores, puntos de transacción o cualquier otra cosa que quiera hacer. Target devolverá el contenido introducido en la interfaz de usuario en el mismo formato. |
   | `heroImage.image = [UIImage imageNamed:content];` | Por ejemplo, tome el contenido y fije una ruta para una imagen a pantalla completa. |

1. Cree una métrica de éxito.

   Se puede usar el método `targetCreateOrderConfirmRequestWithName` para rastrear una métrica de conversión/éxito en la aplicación.

   ```
   ADBTargetLocationRequest *req = [ADBMobile targetCreateOrderConfirmRequestWithName: "orderConfirm" 
                                              orderId: orderId 
                                              orderTotal: @"39.95" 
                                              productPurchasedId: _galleryItem.title 
                                              parameters: nil]; 
   [ADBMobile targetLoadRequest: req callback: nil];
   ```

   | Parámetro | Descripción |
   |---|---|
   | `orderId` | Sustitúyalo por una variable dinámica que represente un ID de pedido único. |
   | `@"39.95"` | Sustitúyalo por una variable dinámica que represente un total de pedido único. |
   | `_galleryItem.title` | Sustitúyala por una variable dinámica que represente una lista de productos comprados separados por comas. |
   | `parameters: nil` | Diccionario opcional de parámetros adicionales. |

1. Compile la aplicación.

   Resultado del paso: cuando haya creado una ubicación de Target y haya etiquetado una métrica de éxito, cree una prueba A/B. La actividad se puede crear con el compositor de experiencias basadas en formulario.
