---
title: Patrón de implementación de Recommendations con at.js
description: Descubra cómo utilizar el patrón de implementación para Recommendations con at.js
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 752c52c0db5173f49fd828c297fa7afd7c53c6ce
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# [!DNL Recommendations] información general sobre el patrón de implementación de at.js

Este patrón de implementación le ayuda a comprender y crear sus [!DNL Adobe Target Recommendations] implementación al utilizar el [Biblioteca JavaScript de at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

Haga clic en la imagen para expandirla a pantalla completa.

![Diagrama de arquitectura de Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Tenga en cuenta que los números de la imagen no indican la secuencia de operaciones:

1. SDK del lado del cliente para [!DNL Adobe Target] y [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] llamada
1. [!UICONTROL ID de Experience Cloud] Llamada de adquisición de (ECID)
1. API de actualización de perfiles en lote y [!DNL Customer Attributes] Servicio de (CA)
1. Ingesta de datos de perfil de las fuentes de datos del cliente a [!DNL Target] almacén de perfiles
1. Recopilación de datos de perfil y comportamiento y decisión de qué experiencia mostrar al visitante
1. Las experiencias se procesan en la página
1. at.js procesa las experiencias de la página

Cada patrón consta de diferentes partes, y cada parte corresponde a un requisito de implementación crítico para su [!DNL Target] implementación.

Cada parte se explica en un artículo independiente en esta guía:

* [Inicializar SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Configuración de la recopilación de datos](/help/dev/patterns/recs-atjs/data-collection.md)
* [Procesar experiencias](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Notificar al destinatario](/help/dev/patterns/recs-atjs/notify-target.md)

