---
keywords: SDK web de Adobe Experience Platform, sdk web de aep, sdk web, sdk, adobe experience cloud, platform edge network, adobe experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: Aprenda a utilizar el [!UICONTROL SDK web de Adobe Experience Platform] para interactuar con los distintos servicios de [!UICONTROL Adobe Experience Cloud] a través de [!UICONTROL Red perimetral de AEP].
title: ¿Cómo puedo implementar con? [!UICONTROL SDK web de Experience Platform]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 13%

---

# [!UICONTROL SDK web de Adobe Experience Platform]

[!UICONTROL SDK web de Adobe Experience Platform] (SDK web de AEP) es una biblioteca JavaScript del lado del cliente que permite a los clientes de [!UICONTROL Adobe Experience Cloud] para interactuar con los distintos servicios de [!DNL Adobe Experience Cloud] (incluido [!DNL Target]) a través de [!UICONTROL Adobe Experience Platform Edge Network]. Además de la biblioteca JavaScript de, hay una [!UICONTROL Adobe Experience Platform] para ayudarle con las configuraciones del SDK web.

Para obtener más información, consulte los siguientes vínculos en la *[!UICONTROL SDK web de Adobe Experience Platform]* ayuda:

* Para obtener información completa: [Qué es [!UICONTROL SDK web de Adobe Experience Platform]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* Para obtener información específica sobre [!DNL Target]: [[!DNL Target] Información general](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=es)

## Tutoriales

Los siguientes tutoriales le ayudan con la implementación:

### Implementación [!DNL Adobe Experience Cloud] con [!DNL Platform Web SDK]

Obtenga información sobre cómo implementar [!DNL Experience Cloud] aplicaciones que utilizan [!DNL Adobe Experience Platform Web SDK] con [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es). Para obtener información específica sobre [!DNL Target], consulte la sección del tutorial titulada [Configuración de [!DNL Target] con el SDK web de Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrar [!DNL Target] de at.js 2.*x* hasta [!DNL Platform Web SDK]

Obtenga información sobre cómo migrar su [!DNL Target] implementación desde at.js 2.*x* a la [!DNL Adobe Experience Platform Web SDK] con [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=es).

## Documentación recomendada

Además de las [!UICONTROL SDK web de Platform] documentación mencionada anteriormente, los temas de esta guía también contienen información específica de la [!UICONTROL SDK web de Platform] en lo que respecta a [!DNL Target] funciones y funcionalidad.

| Función | Descripción/Vínculo |
| --- | --- |
| [Control de calidad de la actividad](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Uso de URL de QA en [!DNL Target] para realizar sencillos controles de calidad de las actividades de extremo a extremo con vínculos de vista previa invariables, segmentar audiencias de manera opcional y crear informes de control de calidad que permanecen segmentados a partir de datos de actividades activas. El control de calidad de la actividad le permite probar [!DNL Target] antes de lanzarlas en directo.<p>Consulte [Compatibilidad con la biblioteca JavaScript Modo QA de Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) y [Previsualizar direcciones URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics para Target] (A4T) es una integración de soluciones cruzadas que le permite crear actividades basadas en [!DNL Analytics] métricas de conversión y segmentos de audiencia de. Esta integración de A4T le permite utilizar informes de Analytics para examinar sus resultados.<p>Consulte [Tipos de actividades compatibles](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) y [Pasos de implementación de un SDK web de Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Audiencias en [!DNL Target] determine quién ve el contenido y las experiencias en una actividad segmentada.<p>Consulte [Usar la lista Audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) y [Combinación de varias audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Creación de audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=es) | Usar audiencias creadas en [!DNL Adobe Experience Platform] proporciona datos de clientes más completos que conducen a una personalización más impactante.<p>Consulte [Usar audiencias de Adobe Experience Platform](https://experienceleague.adobe.com/docs/?lang=estarget/using/audiences/create-audiences/audiences.html#aep). |
| [Decisiones de oferta](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Añadir decisiones de oferta creadas en [!DNL Adobe Journey Optimizer] hasta [!DNL Target] actividades (prueba A/B manual o segmentación de experiencias) para determinar y ofrecer la siguiente mejor oferta para sus visitantes en la web y dispositivos móviles. |
| [Ofertas de redireccionamiento: preguntas más frecuentes sobre A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | Las ofertas de redireccionamiento hacen que los navegadores de los visitantes redirijan a una página nueva.<p>Consulte [¿El [!UICONTROL SDK web de Adobe Experience Platform] ¿admite ofertas de redireccionamiento para A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Los tokens de respuesta le permiten enviar [!DNL Target] datos a Google Analytics y otras integraciones de terceros.<p>Consulte [Envío de datos a los Google Analytics mediante el SDK web de Platform](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) para ver un ejemplo de código de cómo realizar esta tarea. |
| [Implementación de aplicación de una sola página](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) en el *[!UICONTROL SDK web de Platform] descripción general* guía. | [!UICONTROL SDK web de Adobe Experience Platform] SPA proporciona funciones enriquecidas que equipan su empresa para ejecutar personalizaciones en tecnologías de próxima generación del lado del cliente, como aplicaciones de una sola página (). |
| [Cambios en el cifrado de TLS (Seguridad de capa de transporte)](../../before-implement/tls-transport-layer-security-encryption.md) | TLS (Transport Layer Security) le ayuda a mantener los estándares de seguridad más altos y a promover la seguridad de los datos de los clientes. |
