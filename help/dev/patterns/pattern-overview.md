---
title: Información general sobre patrones de implementación
description: Comprender cómo utilizar los patrones de implementación
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: c4b9dfed19e5e4a56bfeae26c4310b997a2d617e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Información general sobre patrones de implementación

[!DNL Adobe Target] Los patrones de implementación le ayudan a comprender y crear la siguiente arquitectura para su [!DNL Target] implementación.

Haga clic en la imagen para expandirla a pantalla completa.

![Diagrama de arquitectura de Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Tenga en cuenta que los números de la imagen no indican la secuencia de operaciones:

1. SDK del lado del cliente para [!DNL Adobe Target] y [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] llamada
1. Llamada de adquisición de ECID
1. API de actualización de perfiles en lote y [!DNL Customer Attributes] Servicio de (CA)
1. Ingesta de datos de perfil de las fuentes de datos del cliente a [!DNL Target] almacén de perfiles
1. Recopilación de datos de perfil/comportamiento y decisión de qué experiencia mostrar al usuario final
1. Las experiencias se procesan en la página
1. at.js procesa las experiencias de la página

Cada patrón consta de diferentes partes. Cada parte corresponde a un requisito de implementación crítico para su [!DNL Target] implementación.

Cada parte se explica en una página independiente en esta guía. Por ejemplo, la variable [!DNL Target] El patrón de implementación contiene las siguientes páginas:

* Inicializar SDK
* Enriquecimiento del perfil
* Experiencias de procesamiento
* Notificar [!DNL Target]
