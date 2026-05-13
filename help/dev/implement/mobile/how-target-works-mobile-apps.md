---
description: Aprenda a usar  [!DNL Adobe Mobile SDK]  para mostrar las experiencias óptimas a los visitantes de su aplicación móvil.
title: ¿Cómo funciona  [!DNL Target] en aplicaciones móviles?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
TQID: https://experienceleague.adobe.com/R3B-i9BFKaoTkbfzVLOU-j8VV2K-MpNrf0WTCkMceT8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 21%

---

# Cómo funciona [!DNL Target] en las aplicaciones móviles

[!DNL Adobe Mobile SDK] se pone en contacto con el servidor [!DNL Target] para obtener el contenido y otros puntos de datos con el fin de mostrar la experiencia adecuada al usuario.

>[!IMPORTANT]
>
>La compatibilidad con los SDK de [!DNL Adobe Mobile] versión 4.*x* finalizó el 31 de agosto de 2021 y ya no se recomienda para [!DNL Adobe Target] usuarios móviles.
>
>[Adobe Experience Platform SDK para aplicaciones móviles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} es la solución recomendada para impulsar [!DNL Adobe Experience Cloud] soluciones y servicios en sus aplicaciones móviles.

## [!DNL Target] ubicaciones y métricas de éxito

Las *ubicaciones de target* también se denominan mbox. Una ubicación identificada en la aplicación se habilita para realizar pruebas o personalizaciones (por ejemplo, el mensaje de bienvenida de la pantalla de inicio). Estas ubicaciones se identifican durante el proceso de creación de la prueba.

Una *[métrica de éxito](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)* es una acción realizada por el usuario que identifica si una actividad específica se realizó correctamente (como iniciar sesión, realizar una compra o reservar un ticket, entre otras).

![imagen alt](assets/mobile-target-location.png)

* **[!DNL Target]ubicación:** El contenido que se muestra debajo del botón de registro.

  Este usuario se beneficia de envío gratuito hasta las 18.00 h. Esta ubicación se puede reutilizar en varias actividades [!DNL Target] para ejecutar pruebas A/B y personalización.

* **Métrica de éxito:** Acción realizada por el usuario cuando este pulsa el botón de registro.

**Comprenda cómo funciona [!DNL Target] en SDK**

![imagen alt](assets/how-target-mobile-works.png)
