---
title: Información general sobre patrones de implementación
description: Comprender cómo utilizar los patrones de implementación
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e15513f5c52240536ccf41f16ba7f4dc6dbf9a04
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Información general sobre patrones de implementación

[!DNL Adobe Target] Los patrones de implementación le ayudan a comprender y crear la siguiente arquitectura para su [!DNL Target] implementación.

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

Cada parte se explica en un tema independiente en esta guía. Por ejemplo, la variable [[!DNL Recommendations] patrón de implementación con at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) contiene los siguientes temas:

* Inicializar SDK
* Configuración de la recopilación de datos
* Experiencias de procesamiento
* Notificar [!DNL Target]

