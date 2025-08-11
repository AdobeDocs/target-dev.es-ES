---
title: Registro del lado del servidor para datos de A4T en Experience Platform Web SDK
description: Obtenga información sobre cómo habilitar el registro en el lado del servidor para Adobe Analytics for Target (A4T) mediante Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;registro;
feature: Implementation
source-git-commit: b1b0424bfe61fb8b4e88723e6bb2c565d75f8351
workflow-type: tm+mt
source-wordcount: '144'
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