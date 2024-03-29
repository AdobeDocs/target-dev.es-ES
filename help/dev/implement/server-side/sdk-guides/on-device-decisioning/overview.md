---
keywords: servidor, lado del servidor, sdk, sdk, en el dispositivo, toma de decisiones, en el dispositivo, en el dispositivo, latencia cero, latencia, casi cero, node.js, lado del servidor3
description: Aprenda a utilizar [!UICONTROL [!UICONTROL on-device decisioning]] para almacenar en caché [!DNL Target] Actividades A/B y MVT en el servidor para realizar la toma de decisiones en memoria con una latencia cercana a cero.
title: ¿Qué es la toma de decisiones en el dispositivo?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: ff0becf3fe3a6fd6694e13243b6a93b910316434
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 9%

---

# Información general sobre la toma de decisiones en el dispositivo

La próxima generación [!DNL Adobe Target] Los SDK ahora ofrecen [!UICONTROL on-device decisioning], que permite almacenar en caché las campañas A/B y de Segmentación de experiencias (XT) en el servidor y tomar decisiones en memoria con una latencia cercana a cero, sin bloquear las solicitudes de red a [!DNL Adobe Target]de Edge Network.

[!DNL Adobe Target] también ofrece la flexibilidad de ofrecer la experiencia más relevante y actualizada de sus campañas de experimentación y personalización impulsadas por ML a través de una llamada al servidor en directo. En otras palabras, cuando el rendimiento es más importante, puede elegir utilizar [!UICONTROL on-device decisioning], pero cuando se necesita la experiencia más relevante y actualizada, se puede realizar una llamada al servidor. Consulte [cuándo usar la toma de decisiones en el dispositivo o en el perímetro](../../sdk-guides/on-device-decisioning/supported-features.md) para conocer los casos de uso que justifican el uso de uno sobre el otro.

>[!NOTE]
>
>La toma de decisiones en el dispositivo está disponible tanto para implementaciones del lado del cliente como del lado del servidor. Este artículo describe [!UICONTROL on-device decisioning] para del lado del servidor. Para obtener información sobre [!UICONTROL on-device decisioning] para obtener información sobre el lado del cliente, consulte la documentación de implementación del lado del cliente [aquí](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## ¿Cómo funciona?

Al instalar e inicializar un [!DNL Adobe Target] SDK con [!UICONTROL on-device decisioning] habilitado, a *artefacto de regla* se descarga y almacena en caché localmente en el servidor, desde la CDN de Akamai más cercana al servidor. Cuando una solicitud para recuperar un [!DNL Adobe Target] experiencia se realiza dentro de la aplicación del lado del servidor, la decisión con respecto a qué contenido se va a devolver se realiza en memoria, en función de los metadatos codificados en el artefacto de regla en caché, que define todos los [!UICONTROL on-device decisioning] Actividades A/B y XT.

El diagrama siguiente muestra la [!UICONTROL on-device decisioning] arquitectura. Haga clic en para expandir la imagen.

(Haga clic en la imagen para ampliarla a ancho completo).

![Diagrama de la arquitectura de decisiones en el dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Diagrama de la arquitectura de decisiones en el dispositivo"){zoomable=&quot;yes&quot;}

## ¿Cuáles son los beneficios?

* **Ofrezca decisiones de latencia cercanas a cero.** La agrupación y la toma de decisiones se realizan en la memoria y en el dispositivo para evitar el bloqueo de solicitudes de red.
* **Mejorar el rendimiento de la aplicación.** Ejecute experimentos y proporcione personalización a sus clientes y usuarios sin poner en riesgo las experiencias de los usuarios finales.
* **Mejore la puntuación de calidad del sitio Google.** Cuando las decisiones se toman en memoria y en el servidor, mejore la puntuación de calidad del sitio de Google de su negocio en línea para que los consumidores puedan descubrirlo mejor.
* **Aprenda de los análisis en tiempo real.** Obtenga información del rendimiento de su actividad en tiempo real mediante [!DNL Adobe Target] para la creación de informes de A4T, lo que le permite pivotar sobre su estrategia en momentos críticos.

## Funcionalidad admitida

### Actividades

La toma de decisiones en el dispositivo admite los siguientes tipos de actividades creadas por [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html):

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting] (XT)

### Método de asignación

La toma de decisiones en el dispositivo admite el siguiente método de asignación:

* Manual

### Segmentación de audiencia

La toma de decisiones en el dispositivo admite las siguientes reglas de audiencia:

| Regla de audiencia | Toma de decisiones en el dispositivo |
| --- | --- |
| [Ubicación geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Sí<P>Al utilizar la toma de decisiones en el dispositivo, se admiten los siguientes atributos geográficos:<ul><li>País/región</li><li>Ciudad</li><li>Latitud</li><li>Longitud</li></ul> |
| [Red](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | No |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | No |
| [Parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Sí |
| [Sistema operativo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Sí |
| [Páginas del sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Sí |
| [Explorador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Sí |
| [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | No |
| [Fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | No |
| [Lapso de tiempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Sí |
| [Audiencias de Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Audiencias de Adobe Audience Manager, Adobe Analytics y Adobe Experience Manager | No |

## ¿Cómo aprovisiono a mi cliente para que utilice [!UICONTROL on-device decisioning]?

La toma de decisiones en el dispositivo está disponible para todos los [!DNL Adobe Target] clientes que utilizan [!DNL Adobe Target] SDK del lado del servidor. Para habilitar esta función, vaya a **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** en el [!DNL Adobe Target] y habilite la variable **[!UICONTROL On-Device Decisioning]** alternar.

>[!NOTE]
>
>Debe tener el administrador o aprobador *función de usuario* para habilitar o deshabilitar [!UICONTROL On-Device Decisioning] alternar.

![imagen alt](assets/asset-odd-toggle.png)

Después de habilitar la opción Toma de decisiones en el dispositivo, [!DNL Adobe Target] empezará a generar y propagar *artefactos de regla* para su cliente.

>[!NOTE]
>
>Asegúrese de habilitar la opción antes de inicializar el [!DNL Adobe Target] SDK que utilizar [!UICONTROL on-device decisioning]. Los artefactos de regla primero deberán generarse y propagarse a las CDN de Akamai para [!UICONTROL on-device decisioning] para trabajar.

### Incluir todos los existentes [!UICONTROL on-device decisioning] actividades cualificadas en la opción artefactos

Alternar esto **el** cuando te gustaría toda la vida [!DNL Target] actividades que cumplen los requisitos para [!UICONTROL on-device decisioning] para que se incluya automáticamente en el artefacto.

Dejando esta opción **desactivado** significa que tendrá que volver a crear y activar cualquier [!UICONTROL on-device decisioning] actividades para que se incluyan en el artefacto de reglas generadas.

## ¿Cómo sé si una actividad es [!UICONTROL on-device decisioning] ¿capaz?

Después de crear una actividad de, aparece una etiqueta llamada **[!UICONTROL Decisioning Method]**, visible en la página de detalles de la actividad, indica si la actividad está [!UICONTROL on-device decisioning] capaz.

![imagen alt](assets/asset-odd9.png)

También puede ver todas las actividades que son [!UICONTROL on-device decisioning] capaz en la **[!UICONTROL Activities]** página añadiendo la columna **[!UICONTROL Decisioning Method]** a la lista de actividades.

![imagen alt](assets/asset-odd7.png)

>[!NOTE]
>
>Después de crear y activar una actividad que es [!UICONTROL on-device decisioning] capaz, pueden pasar 20 minutos antes de que se incluya en el artefacto de reglas que se genera y propaga a los puntos de interés de CDN de Akamai.

## ¿Cuál es el resumen de los pasos que debo seguir para garantizar mi [!UICONTROL on-device decisioning] Las actividades de se entregan correctamente mediante [!DNL Adobe Target]¿Cuál es el SDK del lado del servidor?

1. Acceda a la [!DNL Adobe Target] IU de y navegue hasta **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** para habilitar el **[!UICONTROL On-Device Decisioning]** alternar.
1. Habilite la **[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]** alternar.
1. Cree y active un tipo de actividad compatible con [!UICONTROL on-device decisioning]y compruebe que la variable **[!UICONTROL Decisioning Method]** es **[!UICONTROL On-Device Decisioning]** para esa actividad.
1. Instale e inicialice [Node.js](../../node-js/overview.md) o [Java](../../java/overview.md) SDK con `decisioningMethod = on-device`.
1. Implementación `getOffers()` o `getAttributes()` en el código para recuperar una experiencia en el dispositivo.
1. Implemente su código.

Para ver ejemplos que muestran la introducción a los pasos 1-3 anteriores, consulte la [Primeros pasos](../getting-started/getting-started.md) sección.


## Recursos adicionales

### Seminario web: personalice y pruebe con una latencia cero con decisiones en el dispositivo de [!DNL Adobe Target]

Más que nunca, a los especialistas en marketing, propietarios de productos y desarrolladores se les está asignando la tarea de optimizar la experiencia general del cliente en los sitios, las aplicaciones y en cualquier otro lugar donde se conecten con sus clientes. Varias herramientas con silos de datos e implementaciones complejas son inadecuadas.

En este seminario web grabado, [!DNL Adobe Target] los expertos en productos analizan cómo mover las decisiones de optimización de experiencias críticas en el dispositivo para ejecutarse localmente con latencia cercana a cero puede abrirles las puertas a nuevos casos de uso interesantes, a la vez que mejoran el rendimiento del sitio para sus clientes.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Tutorial: Toma de decisiones en el dispositivo

[!DNL Adobe Target] [!UICONTROL on-device decisioning] habilita la entrega de contenido con latencia cercana a cero.

Este vídeo de 7 minutos:

* Describe [!UICONTROL on-device decisioning], incluido cómo se compara con otros métodos de [!DNL Target] implementación
* Muestra cómo habilitar [!UICONTROL on-device decisioning] en Target
* Examina una actividad de compositor basada en formularios de ejemplo que se ha configurado con contenido JSON
* Muestra código SDK de Node.JS de ejemplo que contiene la configuración de clave necesaria para [!UICONTROL on-device decisioning]
* Muestra los resultados en un explorador

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Para ver más vídeos y tutoriales, consulte la [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=es).

### Adobe Tech Blog - Parte 1: Ejecutar [!DNL Adobe Target] SDK de NodeJS para la experimentación y personalización en plataformas Edge (empleados de Akamai Edge)

[Haga clic aquí para acceder a la publicación del blog](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog - Parte 2: Ejecución del SDK de NodeJS de [!DNL Adobe Target] para la experimentación y personalización en plataformas Edge (AWS Lambda@Edge)

[Haga clic aquí para acceder a la publicación del blog](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
