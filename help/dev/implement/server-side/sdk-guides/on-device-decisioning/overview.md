---
keywords: servidor, lado del servidor, sdk, sdk, en el dispositivo, toma de decisiones, en el dispositivo, en el dispositivo, latencia cero, latencia, casi cero, node.js, lado del servidor3
description: Aprenda a utilizar [!UICONTROL [!UICONTROL on-device decisioning]] para almacenar en caché sus actividades A/B y MVT de  [!DNL Target] en su servidor para realizar la toma de decisiones en memoria con una latencia cercana a cero.
title: ¿Qué es la toma de decisiones en el dispositivo?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: ff0becf3fe3a6fd6694e13243b6a93b910316434
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 9%

---

# Información general sobre la toma de decisiones en el dispositivo

Los SDK de [!DNL Adobe Target] de próxima generación ahora ofrecen [!UICONTROL on-device decisioning], que permite almacenar en caché las campañas A/B y de segmentación de experiencias (XT) en el servidor y tomar decisiones en memoria con una latencia cercana a cero, sin bloquear las solicitudes de red al Edge Network de [!DNL Adobe Target].

[!DNL Adobe Target] también ofrece la flexibilidad de ofrecer la experiencia más relevante y actualizada de sus campañas de experimentación y personalización impulsadas por ML a través de una llamada al servidor en vivo. En otras palabras, cuando el rendimiento es más importante, puede elegir utilizar [!UICONTROL on-device decisioning], pero cuando se necesita la experiencia más relevante y actualizada, se puede realizar una llamada al servidor en su lugar. Consulte [cuándo usar la toma de decisiones en el dispositivo o en el perímetro](../../sdk-guides/on-device-decisioning/supported-features.md) para obtener más información sobre los casos de uso que justifican el uso de uno sobre el otro.

>[!NOTE]
>
>La toma de decisiones en el dispositivo está disponible tanto para implementaciones del lado del cliente como del lado del servidor. Este artículo describe [!UICONTROL on-device decisioning] para el lado del servidor. Para obtener información acerca de [!UICONTROL on-device decisioning] para el lado del cliente, consulte la documentación de implementación del lado del cliente [aquí](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## ¿Cómo funciona?

Al instalar e inicializar un SDK de [!DNL Adobe Target] con [!UICONTROL on-device decisioning] habilitado, se descarga un *artefacto de regla* y se almacena en caché localmente en el servidor, desde la red de distribución de contenido (CDN) de Akamai más cercana al servidor. Cuando se realiza una solicitud para recuperar una experiencia [!DNL Adobe Target] en la aplicación del lado del servidor, la decisión con respecto a qué contenido se va a devolver se realiza en memoria, según los metadatos codificados en el artefacto de reglas en caché, que define todas sus actividades A/B y XT de [!UICONTROL on-device decisioning].

El diagrama siguiente muestra la arquitectura de [!UICONTROL on-device decisioning]. Haga clic en para expandir la imagen.

(Haga clic en la imagen para ampliarla a ancho completo).

![Diagrama de arquitectura de toma de decisiones en el dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Diagrama de arquitectura de toma de decisiones en el dispositivo"){zoomable="yes"}

## ¿Cuáles son los beneficios?

* **Enviar decisiones de latencia cercanas a cero.**: la agrupación y la toma de decisiones se realizan en la memoria y en el dispositivo para evitar el bloqueo de solicitudes de red.
* **Mejorar el rendimiento de la aplicación.** Ejecute experimentos y proporcione personalización a sus clientes y usuarios sin poner en riesgo las experiencias de los usuarios finales.
* **Mejorar la puntuación de calidad del sitio de Google.** Con las decisiones que se toman en memoria y en el lado del servidor, mejore la puntuación de calidad del sitio de Google de su negocio en línea para que los consumidores puedan descubrirlo mejor.
* **Aprenda de los análisis en tiempo real.**: obtiene información del rendimiento de su actividad en tiempo real mediante la creación de informes de [!DNL Adobe Target] o A4T, lo que le permite pivotar sobre su estrategia en momentos críticos.

## Funcionalidad admitida

### Actividades

La toma de decisiones en el dispositivo admite los siguientes tipos de actividades creadas por el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=es):

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting] (XT)

### Método de asignación

La toma de decisiones en el dispositivo admite el siguiente método de asignación:

* Manual

### Segmentación de audiencia

La toma de decisiones en el dispositivo admite las siguientes reglas de audiencia:

| Regla de audiencia | Toma de decisiones en el dispositivo |
| --- | --- |
| [Ubicación geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=es) | Sí<P>Al utilizar la toma de decisiones en el dispositivo, se admiten los siguientes atributos geográficos:<ul><li>País/región</li><li>Ciudad</li><li>Latitud</li><li>Longitud</li></ul> |
| [Red](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=es) | No |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=es) | No |
| [Parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=es) | Sí |
| [Sistema operativo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=es) | Sí |
| [Páginas del sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=es) | Sí |
| [Explorador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=es) | Sí |
| [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=es) | No |
| [Fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=es) | No |
| [Lapso de tiempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=es) | Sí |
| [Audiencias de Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=es) (Audiencias de Adobe Audience Manager, Adobe Analytics y Adobe Experience Manager | No |

## ¿Cómo aprovisiono a mi cliente para que use [!UICONTROL on-device decisioning]?

La toma de decisiones en el dispositivo está disponible para todos los clientes de [!DNL Adobe Target] que utilizan [!DNL Adobe Target] SDK del lado del servidor. Para habilitar esta característica, vaya a **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** en la interfaz de usuario de [!DNL Adobe Target] y habilite la opción **[!UICONTROL On-Device Decisioning]**.

>[!NOTE]
>
>Debe tener el rol de administrador o aprobador *user* para habilitar o deshabilitar la opción [!UICONTROL On-Device Decisioning].

![imagen alt](assets/asset-odd-toggle.png)

Después de habilitar la opción Toma de decisiones en el dispositivo, [!DNL Adobe Target] empezará a generar y propagar *artefactos de regla* para su cliente.

>[!NOTE]
>
>Asegúrese de habilitar la opción antes de inicializar el SDK [!DNL Adobe Target] para usar [!UICONTROL on-device decisioning]. Los artefactos de regla primero deberán generarse y propagarse a las CDN de Akamai para que [!UICONTROL on-device decisioning] funcione.

### Incluir todas las actividades calificadas de [!UICONTROL on-device decisioning] existentes en la opción de artefactos

Cambie este(a) **on** cuando desee que todas sus actividades activas de [!DNL Target] que califican para [!UICONTROL on-device decisioning] se incluyan automáticamente en el artefacto.

Si deja esta opción **desactivada**, tendrá que volver a crear y activar las actividades [!UICONTROL on-device decisioning] para que se incluyan en el artefacto de reglas generadas.

## ¿Cómo sé si una actividad es compatible con [!UICONTROL on-device decisioning]?

Después de crear una actividad, una etiqueta denominada **[!UICONTROL Decisioning Method]**, visible en la página de detalles de la actividad, indica si la actividad es compatible con [!UICONTROL on-device decisioning].

![imagen alt](assets/asset-odd9.png)

También puede ver todas las actividades que son compatibles con [!UICONTROL on-device decisioning] en la página **[!UICONTROL Activities]** agregando la columna **[!UICONTROL Decisioning Method]** a la lista de actividades.

![imagen alt](assets/asset-odd7.png)

>[!NOTE]
>
>Después de crear y activar una actividad con capacidad para [!UICONTROL on-device decisioning], pueden pasar 20 minutos antes de que se incluya en el artefacto de reglas que se genera y propaga a los puntos de interés de CDN de Akamai.

## ¿Cuál es el resumen de los pasos que debo seguir para asegurarme de que mis actividades de [!UICONTROL on-device decisioning] se entreguen correctamente a través del SDK del lado del servidor de [!DNL Adobe Target]?

1. Acceda a la interfaz de usuario de [!DNL Adobe Target] y vaya a **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** para habilitar la opción **[!UICONTROL On-Device Decisioning]**.
1. Habilite la opción **[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]**.
1. Cree y active un tipo de actividad compatible con [!UICONTROL on-device decisioning] y compruebe que **[!UICONTROL Decisioning Method]** es **[!UICONTROL On-Device Decisioning]** para esa actividad.
1. Instale e inicialice el SDK [Node.js](../../node-js/overview.md) o [Java](../../java/overview.md) con `decisioningMethod = on-device`.
1. Implemente `getOffers()` o `getAttributes()` en su código para recuperar una experiencia en el dispositivo.
1. Implemente su código.

Para ver ejemplos que muestran cómo empezar con los pasos del 1 al 3 anteriores, consulte la sección [Introducción](../getting-started/getting-started.md).


## Recursos adicionales

### Seminario web: personalice y pruebe con una latencia cero con decisiones en el dispositivo de [!DNL Adobe Target]

Más que nunca, a los especialistas en marketing, propietarios de productos y desarrolladores se les está asignando la tarea de optimizar la experiencia general del cliente en los sitios, las aplicaciones y en cualquier otro lugar donde se conecten con sus clientes. Varias herramientas con silos de datos e implementaciones complejas son inadecuadas.

En este seminario web grabado, [!DNL Adobe Target] expertos en productos analizan cómo mover las decisiones de optimización de experiencias críticas en el dispositivo para ejecutarse localmente con latencia cercana a cero puede abrirles las puertas a nuevos casos de uso interesantes, a la vez que mejoran el rendimiento del sitio para sus clientes.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Tutorial: Toma de decisiones en el dispositivo

[!DNL Adobe Target] [!UICONTROL on-device decisioning] habilita la entrega de contenido de latencia cercana a cero.

Este vídeo de 7 minutos:

* Describe [!UICONTROL on-device decisioning], incluyendo cómo se compara con otros métodos de implementación de [!DNL Target]
* Muestra cómo habilitar [!UICONTROL on-device decisioning] en Target
* Examina una actividad de compositor basada en formularios de ejemplo que se ha configurado con contenido JSON
* Muestra código de SDK de Node.JS de muestra que contiene la configuración de clave necesaria para [!UICONTROL on-device decisioning]
* Muestra los resultados en un explorador

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Para ver más vídeos y tutoriales, consulta [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=es).

### Adobe Tech Blog - Parte 1: Ejecución del SDK de NodeJS de [!DNL Adobe Target] para la experimentación y personalización en plataformas Edge (empleados de Edge de Akamai)

[Haga clic aquí para obtener acceso a la publicación de blog](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog - Parte 2: Ejecución del SDK de NodeJS de [!DNL Adobe Target] para la experimentación y personalización en plataformas Edge (AWS Lambda@Edge)

[Haga clic aquí para obtener acceso a la publicación de blog](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
