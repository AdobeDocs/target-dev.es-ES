---
title: Patrón de implementación de Recommendations mediante at.js
description: Descubra cómo utilizar el patrón de implementación para Recommendations con at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
TQID: https://experienceleague.adobe.com/uYNa5mL-8ffPS-ddjnQzILnPFMbjNJqKZDmQT8qFeGA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 152
ht-degree: 0%

---

# Resumen del patrón de implementación de [!DNL Recommendations] mediante at.js

Este patrón de implementación le ayuda a comprender y crear su implementación de [!DNL Adobe Target Recommendations] al usar la [biblioteca JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md).

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
