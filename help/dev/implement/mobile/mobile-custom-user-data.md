---
keywords: aplicación móvil, enviar datos de aplicación móvil, aplicación móvil de target, datos de usuario personalizados móviles, datos personalizados de aplicación móvil
description: Aprenda a enviar información adicional sobre la ubicación del usuario a [!DNL Adobe Target] como pares de nombre-valor para ayudarle a crear audiencias personalizadas.
title: ¿Cómo envío datos de usuario personalizados en una aplicación de iOS?
feature: Implement Mobile
exl-id: 9cf8e8fd-1898-43b1-b339-d7a21cb35d57
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: d051910f-2bda-47ea-a969-6ade9fcd71f1
    internal-label: Implement mobile
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 55%
---
# iOS: enviar datos de usuario personalizados

Puede enviar información adicional sobre la ubicación o el usuario a [!DNL Target] como pares nombre-valor.

>[!IMPORTANT]
>
>La compatibilidad con los SDK de [!DNL Adobe Mobile] versión 4.*x* finalizó el 31 de agosto de 2021 y ya no se recomienda para [!DNL Adobe Target] usuarios móviles.
>
>[Adobe Experience Platform SDK para aplicaciones móviles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} es la solución recomendada para impulsar [!DNL Adobe Experience Cloud] soluciones y servicios en sus aplicaciones móviles.

Esta información se puede usar para compilar audiencias personalizadas (por ejemplo, de usuarios que estén a más de 25 000 millas) y en la creación de informes.

Existen dos tipos de parámetros que puede enviar con una llamada a [!DNL Target]:

* **parámetros de mbox**: Los parámetros de mbox no son persistentes entre sesiones.
* **Parámetros de perfil**: los parámetros de perfil se almacenan en el almacén de perfiles del visitante y son persistentes en todas las sesiones. Los parámetros de mbox no persisten. Aunque algunas claves se reservan, tanto los parámetros de perfil como los de mbox pueden ser pares personalizados de clave-valor.

Aunque hay algunas claves reservadas, tanto los parámetros de perfil como los de mbox pueden contener pares personalizados de clave-valor.

1. Cree un diccionario.

   Primero, cree un diccionario con los valores que envía para pasarlos a [!DNL Target]. Para mayor comodidad, añádalo dentro del método `welcomeMessageCampaign` para no tener que preocuparse del ámbito.

   A continuación, le mostramos un diccionario de ejemplo. Puede copiarlo y pegarlo en `(void)welcomeMessageCampaign`. En este ejemplo, los valores de claves como `userLevel` y `userMiles` están insertados en el código. En general, se pasan las variables correspondientes.

   ```
   NSDictionary *targetParams = [[NSDictionary alloc] initWithObjectsAndKeys: 
                                 @"platinum",@"userLevel", 
                                 @26500,@"userMiles", 
                                 @"1067007",@"entity.id", 
                                 @"dealsapp.qa", @"host", 
                                 @"fashion",@"entity.categoryId", 
                                 @"millenial", @"profile.persona", 
                                 @"cohort_5", @"profile.cohort", 
                                 nil];
   ```

   * Las claves que tienen el prefijo “profile” (por ejemplo, `profile.persona`) se almacenan en el perfil del usuario.

     Estos atributos de perfil se pueden usar en una variedad de actividades y canales.

   * Las claves que no tienen prefijo (por ejemplo, `userMiles`) son parámetros de mbox.

     Estos parámetros solo están disponibles durante la sesión.

   * Las claves que tienen el prefijo “entity” (por ejemplo, `entity.category.id`) se usan en las recomendaciones de productos.

1. Compruebe los datos.
   1. En la aplicación `didFinishLaunchingWithOptions`, quite la marca de comentario o añada `[ADBMobile setDebugLogging:YES];`.

      De este modo, se imprimen registros de depuración detallados.
   1. Compile la aplicación.
   1. Compruebe que los parámetros se pasen en la llamada de Target.

      Busque el nombre de la ubicación de Target en la consola de depuración. Verá una llamada a `YOUR-CLIENT-CODE.tt.omtrdc.net` con todos los parámetros que acaba de pasar.

      (Haga clic en la imagen para ampliarla a ancho completo).

      ![Ubicación de destino en la consola de depuración](/help/dev/implement/mobile/assets/mobile-debug.png "Ubicación de destino en la consola de depuración"){zoomable="yes"}

   Puede generar audiencias y restringir o segmentar la visualización de contenido mediante estos parámetros en [!DNL Target].
