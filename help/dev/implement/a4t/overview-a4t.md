---
title: Registro de Adobe Analytics for Target (A4T) en Experience Platform Web SDK
description: Obtenga información sobre cómo controlar la recopilación de datos de Adobe Analytics for Target (A4T) mediante Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;registro;analytics;sdk;sdk web;
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Registro de [!DNL Adobe Analytics for Target] (A4T) en [!DNL Experience Platform Web SDK]

Al utilizar [!DNL Adobe Target] para la personalización, puede elegir qué sistema desea utilizar para la medición de rendimiento. Cada [actividad de destino](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=es) le permite seleccionar entre [!DNL Target] informes y [!DNL Analytics] informes de Adobe.

Si está usando un informe de [!DNL Analytics], [!DNL Target] tiene que comunicar lo siguiente a [!DNL Analytics]:

* Qué actividad [!DNL Target] han ingresado sus visitantes
* Qué experiencia han visto
* Qué conversión se ha alcanzado

El [!DNL Adobe Experience Platform Web SDK] admite dos tipos de registro de [!DNL Analytics] para casos de uso de [!UICONTROL Analytics for Target] (A4T):

| Método de registro | Descripción |
| --- | --- |
| Registro [!DNL Analytics] del lado del servidor | Todas las [!DNL Analytics] visitas enviadas a través de Edge Network se aumentan con [!DNL Target] detalles en el servidor, sin tener que pasar por el proceso de vinculación de visitas. |
| Registro [!DNL Analytics] del lado del cliente | Se devuelven datos de [!DNL Target] en el lado del cliente, lo que le permite aumentar y enviar datos manualmente a [!DNL Analytics] mediante la [API de inserción de datos](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=es). |

El método de registro viene determinado por si tiene [!DNL Adobe Analytics] habilitado en su [secuencia de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/overview) configurada:

![Flujo de decisión del método de registro](/help/dev/implement/a4t/assets/analytics-logging.png)

## Pasos siguientes

Este documento proporciona una breve introducción a los diferentes métodos de registro para datos de A4T en Web SDK. Para obtener información más detallada sobre cada uno de estos métodos, consulte la siguiente documentación:

* [Registro del lado del servidor para datos de A4T en Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Registro del lado del cliente para datos de A4T en Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
