---
description: Aprenda a usar  [!DNL Adobe Mobile SDK]  para mostrar las experiencias óptimas a los visitantes de su aplicación móvil.
title: ¿Cómo funciona  [!DNL Target] en aplicaciones móviles?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 22%

---

# Cómo funciona [!DNL Target] en las aplicaciones móviles

[!DNL Adobe Mobile SDK] se pone en contacto con el servidor [!DNL Target] para obtener el contenido y otros puntos de datos con el fin de mostrar la experiencia adecuada al usuario.

>[!IMPORTANT]
>
>Compatibilidad con [!DNL Adobe Mobile] versión 4.Los SDK de *x* finalizaron el 31 de agosto de 2021 y ya no se recomiendan para [!DNL Adobe Target] usuarios móviles.
>
>El SDK de [Adobe Experience Platform para aplicaciones móviles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} es la solución recomendada para impulsar [!DNL Adobe Experience Cloud] soluciones y servicios en sus aplicaciones móviles.

## [!DNL Target] ubicaciones y métricas de éxito

Las *ubicaciones de target* también se denominan mbox. Una ubicación identificada en la aplicación se habilita para realizar pruebas o personalizaciones (por ejemplo, el mensaje de bienvenida de la pantalla de inicio). Estas ubicaciones se identifican durante el proceso de creación de la prueba.

Una *[métrica de éxito](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=es)* es una acción realizada por el usuario que identifica si una actividad específica se realizó correctamente (como iniciar sesión, realizar una compra o reservar un ticket, entre otras).

![imagen alt](assets/mobile-target-location.png)

* **[!DNL Target]ubicación:** El contenido que se muestra debajo del botón de registro.

  Este usuario se beneficia de envío gratuito hasta las 18.00 h. Esta ubicación se puede reutilizar en varias actividades [!DNL Target] para ejecutar pruebas A/B y personalización.

* **Métrica de éxito:** Acción realizada por el usuario cuando este pulsa el botón de registro.

**Comprenda cómo funciona [!DNL Target] en el SDK**

![imagen alt](assets/how-target-mobile-works.png)
