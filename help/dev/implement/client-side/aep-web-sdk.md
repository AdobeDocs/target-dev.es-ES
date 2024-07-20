---
keywords: SDK web de Adobe Experience Platform, sdk web de aep, sdk web, sdk, adobe experience cloud, platform edge network, adobe experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: Aprenda a utilizar [!UICONTROL Adobe Experience Platform Web SDK] para interactuar con los distintos servicios de [!UICONTROL Adobe Experience Cloud] a través de [!UICONTROL AEP Edge Network].
title: ¿Cómo puedo implementar con [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 8%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (SDK web de AEP) es una biblioteca JavaScript del lado del cliente que permite a los clientes de [!UICONTROL Adobe Experience Cloud] interactuar con los distintos servicios de [!DNL Adobe Experience Cloud] (incluido [!DNL Target]) a través de [!UICONTROL Adobe Experience Platform Edge Network]. Además de la biblioteca JavaScript, existe una extensión [!UICONTROL Adobe Experience Platform] que le ayudará con las configuraciones del SDK web.

Para obtener más información, vea los siguientes vínculos en la ayuda de *[!UICONTROL Adobe Experience Platform Web SDK]*:

* Para obtener información completa: [Qué es [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* Para obtener información específica de [!DNL Target]: [[!DNL Target] Información general](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=es)

## Tutoriales

Los siguientes tutoriales le ayudan con la implementación:

### Implementar [!DNL Adobe Experience Cloud] con [!DNL Platform Web SDK]

Aprenda a implementar aplicaciones de [!DNL Experience Cloud] mediante [!DNL Adobe Experience Platform Web SDK] con [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es). Para obtener información específica de [!DNL Target], consulte la sección del tutorial titulada [Configurar [!DNL Target] con el SDK web de Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrar [!DNL Target] desde at.js 2.*x* a [!DNL Platform Web SDK]

Descubra cómo migrar su implementación de [!DNL Target] desde at.js 2.*x* a [!DNL Adobe Experience Platform Web SDK] con [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=es).

## Documentación recomendada

Además de la documentación de [!UICONTROL Platform Web SDK] mencionada anteriormente, los temas de esta guía también contienen información específica de [!UICONTROL Platform Web SDK] en relación con las características y la funcionalidad de [!DNL Target].

| Función | Descripción/Vínculo |
| --- | --- |
| [Control de calidad de la actividad](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Use direcciones URL de control de calidad en [!DNL Target] para realizar sencillos controles de calidad de las actividades de extremo a extremo con vínculos de vista previa invariables, segmentar audiencias de manera opcional y crear informes de control de calidad que permanecen segmentados a partir de datos de actividades activas. El control de calidad de la actividad le permite probar por completo sus actividades [!DNL Target] antes de lanzarlas.<p>Ver [Compatibilidad con modo de control de calidad de la biblioteca JavaScript de Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) y [URL de vista previa](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics for Target] (A4T) es una integración de soluciones cruzadas que le permite crear actividades basadas en las métricas de conversión y los segmentos de audiencia de [!DNL Analytics] La integración con A4T le permite utilizar informes de Analytics para examinar sus resultados.<p>Consulte [Tipos de actividades compatibles](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) y [Pasos de implementación para una implementación del SDK web de Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Las audiencias de [!DNL Target] determinan quién ve el contenido y las experiencias en una actividad segmentada.<p>Ver [Usar la lista de audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) y [Combinar varias audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Creación de audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=es) | Usar audiencias creadas en [!DNL Adobe Experience Platform] proporciona datos de clientes más completos que conducen a una personalización más impactante.<p>Ver [Usar audiencias de Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep). |
| [Decisiones de oferta](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Agregue decisiones de oferta creadas en [!DNL Adobe Journey Optimizer] a [!DNL Target] actividades (prueba A/B manual o segmentación de experiencias) para determinar y entregar la siguiente mejor oferta para sus visitantes en la web y dispositivos móviles. |
| [Ofertas de redireccionamiento: preguntas más frecuentes sobre A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | Las ofertas de redireccionamiento hacen que los navegadores de los visitantes redirijan a una página nueva.<p>Ver [¿Admite [!UICONTROL Adobe Experience Platform Web SDK] ofertas de redireccionamiento para A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Los tokens de respuesta le permiten enviar datos de [!DNL Target] a Google Analytics y otras integraciones de terceros.<p>Consulte [Envío de datos a Google Analytics mediante el SDK web de Platform](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) para ver una muestra de código de cómo realizar esta tarea. |
| [Implementación de aplicación de una sola página](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) en la guía de información general de *[!UICONTROL Platform Web SDK]*. | SPA [!UICONTROL Adobe Experience Platform Web SDK] proporciona funciones enriquecidas que equipan su empresa para ejecutar personalizaciones en tecnologías de próxima generación del lado del cliente, como aplicaciones de una sola página (). |
| [Cambios en el cifrado de TLS (Seguridad de capa de transporte)](../../before-implement/tls-transport-layer-security-encryption.md) | TLS (Transport Layer Security) le ayuda a mantener los estándares de seguridad más altos y a promover la seguridad de los datos de los clientes. |
