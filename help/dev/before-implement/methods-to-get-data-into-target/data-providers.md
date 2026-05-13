---
keywords: implementación, implementación, configuración, configuración, proveedores de datos
description: Obtener datos en  [!DNL Target] mediante proveedores de datos.
title: ¿Cómo puedo obtener datos en  [!DNL Target] usando proveedores de datos?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
TQID: https://experienceleague.adobe.com/e8uMaGcACjHiaIT4WSlbKry82mhLHUDTSKmCuuhoWgw
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 314
ht-degree: 50%

---

# Proveedores de datos

Los proveedores de datos son una funcionalidad que le permite pasar fácilmente datos de terceros a [!DNL Adobe Target].

>[!NOTE]
>
>Los proveedores de datos requieren at.js 1.3 o posterior.

## Formato

La configuración `window.targetGlobalSettings.dataProviders` es una matriz de proveedores de datos.

Para obtener más información sobre la estructura de cada proveedor de datos, consulte [Proveedores de datos](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Casos de uso de ejemplo

Recabar datos de terceros, por ejemplo, un servicio meteorológico, un DMP o incluso su propio servicio web. Puede usar estos datos para crear audiencias, dirigir contenido y enriquecer el perfil del visitante.

## Ventajas del método

Esta configuración permite a los clientes recopilar datos de proveedores de datos de terceros, como Demandbase, BlueKai y servicios personalizados, así como pasar los datos a [!DNL Target] como parámetros de mbox en la solicitud de mbox global.

Admite la recopilación de datos de múltiples proveedores a través de solicitudes de desincronización y sincronización.

El uso de este enfoque facilita la administración del parpadeo del contenido predeterminado de la página, al tiempo que incluye tiempos de espera independientes para cada proveedor para limitar el impacto en el rendimiento de la página.

## Advertencias

Si los proveedores de datos agregados a `window.targetGlobalSettings.dataProviders` son asincrónicos, se ejecutan en paralelo. La solicitud de API del visitante se ejecuta en paralelo con las funciones agregadas a `window.targetGlobalSettings.dataProviders` para permitir un tiempo de espera mínimo.

at.js no intenta almacenar en caché los datos. Si el proveedor de datos obtiene datos solo una vez, el proveedor de datos debe asegurarse de que los datos estén en caché y, cuando se invoque la función del proveedor, sirva los datos de caché para la segunda invocación.

## Ejemplos de código

Se pueden encontrar varios ejemplos en [Proveedores de datos](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Vínculos a información relevante

Documentación: [Proveedores de datos](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## Vídeos de formación:

* [Uso de Proveedores de datos en Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Implementación de Proveedores de datos en Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
