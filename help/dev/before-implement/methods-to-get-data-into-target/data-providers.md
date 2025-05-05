---
keywords: implementación, implementación, configuración, configuración, proveedores de datos
description: Obtener datos en  [!DNL Target] mediante proveedores de datos.
title: ¿Cómo puedo obtener datos en  [!DNL Target] usando proveedores de datos?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 55%

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

* [Uso de Proveedores de datos en Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html?lang=es)
* [Implementación de Proveedores de datos en Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html?lang=es)
