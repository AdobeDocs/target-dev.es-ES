---
keywords: integración de at.js, integraciones compatibles, integraciones incompatibles, integraciones de terceros
description: Vea las integraciones admitidas (y no admitidas) por  [!DNL Adobe Target] at.js, entre ellas [!UICONTROL Analytics for Target] (A4T), [!UICONTROL Experience Cloud ID Service] y más.
title: ¿Qué integraciones admite at.js?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
TQID: https://experienceleague.adobe.com/RdcxcIGufo2O5aKPqIAJVINkCzZ1Brcv8EXiX1n4buc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e6ff21d3-dec6-4298-8590-7c749fffaf78
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 530
ht-degree: 54%

---

# Integraciones de at.js

Información sobre integraciones comunes con [!DNL Adobe Target] y su estado de compatibilidad con at.js.

Si tiene una necesidad imperiosa de una integración que no se admite ni se menciona aquí, póngase en contacto con su representante de cuentas o asesor.

## Integraciones compatibles

| Integración | Detalles |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | Consulte [Adobe Analytics como fuente de informes para Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es). |
| [!UICONTROL Perfiles y audiencias] (P&amp;A) | Consulte [Audiencias](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=es) en la *Guía del usuario de servicios principales*. |
| [!UICONTROL Servicio Experience Cloud ID] | Consulte la [documentación del servicio Adobe Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es). |
| [!UICONTROL Etiquetas en Adobe Experience Platform] | [!UICONTROL Las etiquetas en Adobe Experience Platform] son la próxima generación de funcionalidades de administración de etiquetas de [!DNL Adobe]. Las [!UICONTROL etiquetas] ofrecen a los clientes una alternativa sencilla para implementar y administrar las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. Ver [Implementar [!DNL Target] usando Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
| [!UICONTROL Adobe Experience Manager] (AEM) Cloud Service | [!UICONTROL AEM Cloud Service] permite la creación de [!UICONTROL pruebas A/B] y [!UICONTROL actividades de segmentación de experiencias] en el flujo de trabajo de AEM. Admite at.js con [!UICONTROL Adobe Experience Manager] 6.2 con FP-11577 (o posterior). Para obtener más información, consulta [Integración con [!DNL Adobe Target]](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es) y selecciona tu versión de AEM. |
| [!UICONTROL Fragmentos de experiencia de AEM] | Los fragmentos de experiencias creados en AEM en [!DNL Target] actividades le permiten combinar la facilidad de uso y la potencia de AEM con potentes capacidades de inteligencia automatizada (AI) y aprendizaje automático (ML) en [!DNL Target] para probar y personalizar experiencias a escala.  AEM aúna todos sus contenidos y recursos en una ubicación centralizada que potencia su estrategia de personalización. AEM le permite crear fácilmente contenido para equipos de escritorio, tabletas y dispositivos móviles en una misma ubicación y sin tener que escribir código. No es necesario crear páginas para cada dispositivo: AEM ajusta automáticamente cada experiencia con su contenido.  Consulte [fragmentos de experiencia de AEM](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=es). |

## Integraciones incompatibles

| Integración | Detalles |
|--- |--- |
| Integración heredada de [!DNL Target] a [!DNL SiteCatalyst] | Esta era la integración que envió los identificadores de campaña y fórmula a [!DNL SiteCatalyst] a través de la llamada a página para que usted pudiera generar informes en la interfaz de usuario de [!DNL SiteCatalyst]. Esta funcionalidad se ha reemplazado por A4T. |
| Integración heredada de [!DNL Target] a [!DNL SiteCatalyst] | Esta era la integración que generó las llamadas de mbox denominadas `"SiteCatalyst: Event"` y `"SiteCatalyst: Purchase"` para que usted pudiera generar métricas de éxito y perfiles de usuarios basados en evars y props. Esta funcionalidad se ha reemplazado por A4T y P&amp;A. |
| Integración heredada de [!DNL Audience Manager] (AAM) con [!DNL Target] | Esta era la integración que hacía una llamada a la API del front-end para recuperar segmentos AAM y luego enviarlos como parámetros de mbox en cada llamada de mbox en la página. |

## Integraciones de terceros

| Integración | Detalles |
|--- |--- |
| Otros administradores de etiquetas | at.js debería funcionar con plataformas de administración de etiquetas que no son de Adobe, pero tenga cuidado de usar características de integración personalizada que otros proveedores han desarrollado. Dichas integraciones podrían depender de funciones mbox.js internas que ya no existen en at.js. |
| Proveedores de datos externos (por ejemplo, las API de clima, Demandbase y BlueKai) | Muchos proveedores de datos de terceros utilizados para complementar el perfil de usuario de Target se pueden integrar utilizando la función [Proveedores de datos](../atjs-functions/targetglobalsettings.md#data-providers) de at.js. |
