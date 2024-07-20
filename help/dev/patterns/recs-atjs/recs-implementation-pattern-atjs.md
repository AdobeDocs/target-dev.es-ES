---
title: Patrón de implementación de Recommendations con at.js
description: Descubra cómo utilizar el patrón de implementación para Recommendations con at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Resumen del patrón de implementación de [!DNL Recommendations] mediante at.js

Este patrón de implementación le ayuda a comprender y crear su implementación de [!DNL Adobe Target Recommendations] al usar la [biblioteca JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

Haga clic en la imagen para expandirla a pantalla completa.

![diagrama de arquitectura de Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Tenga en cuenta que los números de la imagen no indican la secuencia de operaciones:

1. SDK del lado del cliente para [!DNL Adobe Target] y [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] llamada
1. [!UICONTROL Experience Cloud ID] (ECID) llamada de adquisición
1. API de actualización de perfiles en lote y servicio [!DNL Customer Attributes] (CA)
1. Ingesta de datos de perfil de las fuentes de datos del cliente al almacén de perfiles [!DNL Target]
1. Recopilación de datos de perfil y comportamiento y decisión de qué experiencia mostrar al visitante
1. Las experiencias se procesan en la página
1. at.js procesa las experiencias de la página

Cada patrón consta de diferentes partes, y cada parte corresponde a un requisito de implementación crítico para la implementación de [!DNL Target].

Cada parte se explica en un artículo independiente en esta guía:

* [Inicializar SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Configuración de la recopilación de datos](/help/dev/patterns/recs-atjs/data-collection.md)
* [Procesar experiencias](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Notificar al destinatario](/help/dev/patterns/recs-atjs/notify-target.md)
