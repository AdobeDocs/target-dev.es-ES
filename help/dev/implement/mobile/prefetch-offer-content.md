---
keywords: oferta, recuperación previa, iOS, android, sdk, móvil, sdk móvil, 8 dólares
description: Utilice la función de recuperación previa  [!DNL Adobe Target] en los SDK de iOS y Android Mobile para recuperar contenido de ofertas el menor número posible de veces almacenando en caché las respuestas del servidor.
title: ¿Puedo recuperar previamente contenido de ofertas para aplicaciones móviles?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 43%

---

# Recuperación previa de contenido de ofertas

La función de recuperación previa de [!DNL Target] usa los SDK para móviles de iOS y Android a fin de recuperar contenido de ofertas el menor número posible de veces almacenando en caché las respuestas del servidor.

>[!IMPORTANT]
>
>Compatibilidad con [!DNL Adobe Mobile] versión 4.Los SDK de *x* finalizaron el 31 de agosto de 2021 y ya no se recomiendan para [!DNL Adobe Target] usuarios móviles.
>
>El SDK de [Adobe Experience Platform para aplicaciones móviles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} es la solución recomendada para impulsar [!DNL Adobe Experience Cloud] soluciones y servicios en sus aplicaciones móviles.

Este proceso reduce el tiempo de carga, evita múltiples llamadas de red y permite que se notifique a [!DNL Target] sobre qué mbox visitó el usuario de una aplicación móvil. Todo el contenido se recupera y almacena en caché durante la llamada de recuperación previa, y se recupera de la memoria caché para todas las llamadas futuras que incluyan este contenido para el nombre de mbox especificado.

Tenga en cuenta las siguientes limitaciones al utilizar el método de recuperación previa con los SDK para móviles de iOS y Android:

* El contenido de recuperación previa no persiste de un inicio a otro. El contenido de recuperación previa se guarda en caché mientras la aplicación esté activa o hasta que se realice una llamada al método `clearPrefetchCache()`.
* No se admite la funcionalidad de recuperación previa para los métodos de asignación de tráfico [!UICONTROL Auto-Allocate] y [!UICONTROL Auto-Target], para los tipos de actividad [!UICONTROL Automated Personalization] o [!UICONTROL Recommendations], o para las [ofertas de recomendaciones dentro de una actividad A/B o XT](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html?lang=es).

Para obtener más información, incluidos los métodos de recuperación previa, las clases públicas y ejemplos de código, consulte:

* **iOS:** [Recuperar previamente contenido de ofertas en iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html?lang=es) en la ayuda del SDK para iOS de *Mobile Services*.
* **Android:** [Recuperar previamente contenido de ofertas en Android](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=es) en la ayuda del SDK para Android de *Mobile Services*.
