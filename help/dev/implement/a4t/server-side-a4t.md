---
title: Registro del lado del servidor para datos de A4T en Experience Platform Web SDK
description: Obtenga información sobre cómo habilitar el registro en el lado del servidor para Adobe Analytics for Target (A4T) mediante Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;registro;
feature: Implementation
exl-id: 716f7343-69a6-44d7-baec-a0a0df1b6e1f
TQID: https://experienceleague.adobe.com/I7-G2VO2AN3qFsgkk4JX2Pg6WJfZq0HZkcGL4XQNoWg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 161
ht-degree: 0%

---

# Registro del lado del servidor para datos de A4T en [!DNL Experience Platform Web SDK]

[!DNL Adobe Experience Platform Web SDK] le permite implementar la funcionalidad [!UICONTROL Adobe Analytics for Target] (A4T) en [!UICONTROL Experience Platform Edge Network]. Cuando el registro en el lado del servidor está habilitado, todas las [!DNL Analytics] visitas enviadas a través de Edge Network se aumentan con [!DNL Target] detalles en el lado del servidor, sin tener que pasar por el proceso de vinculación de visitas.

El registro del lado del servidor para [!DNL Analytics] está habilitado cuando [!DNL Analytics] está habilitado en la configuración de la secuencia de datos:

![Configuración de secuencia de datos de Analytics habilitada](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

El diagrama siguiente muestra cómo fluyen los datos a través del sistema cuando el registro de [!DNL Analytics] en el lado del servidor está habilitado:

![Flujo de registro del lado del servidor](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## Pasos siguientes

En esta guía se describe el registro en el lado del servidor para datos de A4T en Web SDK. Consulte la guía de [registro en el lado del cliente](/help/dev/implement/a4t/client-side-logging.md) para obtener más información sobre cómo administrar los datos de A4T en el lado del cliente.
