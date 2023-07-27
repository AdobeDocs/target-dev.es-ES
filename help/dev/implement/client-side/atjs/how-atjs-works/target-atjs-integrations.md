---
keywords: integración de at.js, integraciones compatibles, integraciones incompatibles, integraciones de terceros
description: Consulte las integraciones admitidas (y no admitidas) por [!DNL Adobe Target] at.js, que incluye [!UICONTROL Analytics for Target] (A4T), el [!UICONTROL Servicio de ID de Experience Cloud], y más.
title: ¿Qué integraciones admite at.js?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 64%

---

# Integraciones de at.js

Información sobre integraciones comunes con [!DNL Adobe Target] y su estado de compatibilidad con at.js.

Si tiene una necesidad imperiosa de una integración que no se admite ni se menciona aquí, póngase en contacto con su representante de cuentas o asesor.

## Integraciones compatibles

| Integración | Detalles |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | Consulte [Adobe Analytics como fuente de informes para Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html). |
| [!UICONTROL Perfiles y audiencias] (P&amp;A) | Consulte [Audiencias](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=es) en el *Guía del usuario de servicios principales*. |
| [!UICONTROL Servicio Experience Cloud ID] | Consulte la [documentación del servicio Adobe Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| [!UICONTROL Etiquetas en Adobe Experience Platform] | [!UICONTROL Etiquetas en Adobe Experience Platform] son las funciones de administración de etiquetas de próxima generación de [!DNL Adobe]. [!UICONTROL Las etiquetas ofrecen a los clientes una forma sencilla de implementar y administrar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. ] Consulte [Implementación [!DNL Target] uso de Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
| [!UICONTROL Adobe Experience Manager] AEM () Cloud Service | El [!UICONTROL AEM Cloud Service] permite crear contenido [!UICONTROL Prueba A/B] y [!UICONTROL Segmentación de experiencias] AEM actividades dentro del flujo de trabajo de la. Admite at.js con [!UICONTROL Adobe Experience Manager] 6.2 con FP-11577 (o posterior). Para obtener más información, consulte [Integración con  [!DNL Adobe Target] y seleccione su versión de AEM.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es) |
| [!UICONTROL Fragmentos de experiencia de AEM] | AEM Fragmentos de experiencias creados en el en [!DNL Target] AEM Las actividades de le permiten combinar la facilidad de uso y la potencia de las actividades de con las potentes capacidades de Inteligencia automatizada (AI) y Aprendizaje automático (ML) en [!DNL Target] para probar y personalizar experiencias a escala.  AEM aúna todos sus contenidos y recursos en una ubicación centralizada que potencia su estrategia de personalización. AEM le permite crear fácilmente contenido para equipos de escritorio, tabletas y dispositivos móviles en una misma ubicación y sin tener que escribir código. AEM No es necesario crear páginas para cada dispositivo: ajusta automáticamente todas las experiencias con el uso de su contenido.  Consulte [fragmentos de experiencia de AEM](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html). |

## Integraciones incompatibles

| Integración | Detalles |
|--- |--- |
| Heredado [!DNL Target] hasta [!DNL SiteCatalyst] Integración | Esta era la integración que enviaba identificadores de campaña y fórmula a [!DNL SiteCatalyst] mediante la llamada a página para que usted pudiera generar informes en la interfaz del usuario de [!DNL SiteCatalyst]. Esta funcionalidad se ha reemplazado por A4T. |
| Heredado [!DNL Target] hasta [!DNL SiteCatalyst] Integración | Esta era la integración que generó las llamadas de mbox denominadas `"SiteCatalyst: Event"` y `"SiteCatalyst: Purchase"` para que usted pudiera generar métricas de éxito y perfiles de usuarios basados en evars y props. Esta funcionalidad se ha reemplazado por A4T y P&amp;A. |
| Heredado [!DNL Audience Manager] AAM () a [!DNL Target] Integración | Esta era la integración que hacía una llamada a la API del front-end para recuperar segmentos AAM y luego enviarlos como parámetros de mbox en cada llamada de mbox en la página. |

## Integraciones de terceros

| Integración | Detalles |
|--- |--- |
| Otros administradores de etiquetas | at.js debería funcionar con plataformas de administración de etiquetas que no son de Adobe, pero tenga cuidado de usar características de integración personalizada que otros proveedores han desarrollado. Dichas integraciones podrían depender de funciones mbox.js internas que ya no existen en at.js. |
| Proveedores de datos externos (por ejemplo, las API de clima, Demandbase y BlueKai) | Muchos proveedores de datos de terceros utilizados para complementar el perfil de usuario de Target se pueden integrar utilizando la función [Proveedores de datos](../atjs-functions/targetglobalsettings.md#data-providers) de at.js. |
