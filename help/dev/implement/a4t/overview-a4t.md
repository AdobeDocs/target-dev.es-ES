---
title: Registro de Adobe Analytics for Target (A4T) en Experience Platform Web SDK
description: Obtenga información sobre cómo controlar la recopilación de datos de Adobe Analytics for Target (A4T) mediante Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;registro;analytics;sdk;sdk web;
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
TQID: https://experienceleague.adobe.com/cShqvj3wSialxA-ajnROnIpzjuz66pNg3CLM6l2xPLg
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 262
ht-degree: 0%

---

# Registro de [!DNL Adobe Analytics for Target] (A4T) en [!DNL Experience Platform Web SDK]

Al utilizar [!DNL Adobe Target] para la personalización, puede elegir qué sistema desea utilizar para la medición de rendimiento. Cada [actividad de destino](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) le permite seleccionar entre [!DNL Target] informes y [!DNL Analytics] informes de Adobe.

Si está usando un informe de [!DNL Analytics], [!DNL Target] tiene que comunicar lo siguiente a [!DNL Analytics]:

* Qué actividad [!DNL Target] han ingresado sus visitantes
* Qué experiencia han visto
* Qué conversión se ha alcanzado

El [!DNL Adobe Experience Platform Web SDK] admite dos tipos de registro de [!DNL Analytics] para casos de uso de [!UICONTROL Analytics for Target] (A4T):

| Método de registro | Descripción |
| --- | --- |
| Registro [!DNL Analytics] del lado del servidor | Todas las [!DNL Analytics] visitas enviadas a través de Edge Network se aumentan con [!DNL Target] detalles en el servidor, sin tener que pasar por el proceso de vinculación de visitas. |
| Registro [!DNL Analytics] del lado del cliente | Se devuelven datos de [!DNL Target] en el lado del cliente, lo que le permite aumentar y enviar datos manualmente a [!DNL Analytics] mediante la [API de inserción de datos](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

El método de registro viene determinado por si tiene [!DNL Adobe Analytics] habilitado en su [secuencia de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) configurada:

![Flujo de decisión del método de registro](/help/dev/implement/a4t/assets/analytics-logging.png)

## Pasos siguientes

Este documento proporciona una breve introducción a los diferentes métodos de registro para datos de A4T en Web SDK. Para obtener información más detallada sobre cada uno de estos métodos, consulte la siguiente documentación:

* [Registro del lado del servidor para datos de A4T en Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Registro del lado del cliente para datos de A4T en Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
