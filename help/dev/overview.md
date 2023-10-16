---
keywords: guía para desarrolladores de target; información general
title: Guía para desarrolladores de Adobe Target
description: ¿Cómo implemento y administro  [!DNL Adobe Target]  y trabajo con sus API y SDK?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: 063d0574ee380bf76130fb0f17db89cd09efdb7d
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 14%

---

# Guía para desarrolladores de [!DNL Adobe Target]

**([Ver [!DNL Target] actualizaciones de documentación](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank})**

Esta *[!DNL Adobe Target]Guía para desarrolladores* proporciona recursos y guías para [!DNL Target] desarrolladores de, incluida la documentación de API y SDK para implementar y administrar [!DNL Target].

>[!NOTE]
>
>Además de esta guía, también están disponibles las guías de [!DNL Adobe Target] siguientes:
>
>* [*[!DNL Adobe Target] Guía para profesionales de negocios *](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=es){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=es){target=_blank}
>
>Para obtener más información, consulte [Notas de la versión de Target (actual)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank} en el *[!DNL Adobe Target]Guía para profesionales de negocios*.

## Introducción a la implementación

**[](/help/dev/before-implement/considerations-before-you-implement-target.md)** Antes de la implementación: consideraciones que debe abordar antes de implementar [!DNL Adobe Target].

## Implementación del lado del cliente

[**SDK web de Adobe Experience Platform**](/help/dev/implement/client-side/aep-web-sdk.md): La [!DNL Adobe Experience Platform Web SDK] le permite interactuar con los distintos servicios de [!DNL Experience Cloud] (incluido [!DNL Target]) a través de [!UICONTROL Adobe Experience Edge Network].

[**Biblioteca JavaScript at.js de Target**](/help/dev/implement/client-side/overview.md): la biblioteca JavaScript at.js mejora los tiempos de carga de página en implementaciones web, mejora la seguridad y proporciona mejores opciones de implementación en aplicaciones de una sola página.

## Implementación del lado del servidor

[**Información general del SDK de Target**](implement/server-side/server-side-overview.md): Introducción a [!DNL Adobe Target] SDK, incluida la toma de decisiones en el dispositivo.

[**SDK de Node.js**](implement/server-side/node-js/overview.md): Cómo utilizar el [!DNL Target] SDK de Node.js.

[**SDK de Java**](implement/server-side/java/overview.md): Cómo utilizar el [!DNL Target] SDK de Java.

[**SDK DE .NET**](implement/server-side/net/overview.md): Cómo utilizar el [!DNL Target] SDK DE .NET.

[**Python SDK**](implement/server-side/python/overview.md): Cómo utilizar el [!DNL Target] SDK de Python.

## Implementación híbrida

[**Implementación híbrida**](implement/hybrid/hybrid-overview.md): Implementar [!DNL Target] mediante una combinación de implementación del lado del cliente y del lado del servidor.

## Implementación de Recommendations

[**Implementación de Recommendations**](implement/recommendations/recommendations.md): Planificar e implementar [!DNL Adobe Target Recommendations].

## Implementación de aplicaciones móviles

[**Información general del SDK móvil de AEP**](implement/mobile/overview.md): Información general sobre la implementación [!DNL Adobe Target] con [!DNL Adobe Experience Platform] SDK para móviles.

[**Referencia del SDK móvil de AEP**](https://developer.adobe.com/client-sdks/documentation/): Implementar [!DNL Adobe Target] con [!DNL Adobe Experience Platform] SDK para móviles.

## Implementación de correo electrónico

[**Resumen de correo electrónico**](implement/email/overview.md): Información general sobre la implementación [!DNL Adobe Target] en correos electrónicos.

## Guías de API

[**Introducción**](before-administer/target-api-overview.md): Información general de [!DNL Adobe Target] API.

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md): utilice el [!DNL Adobe Target] Las API de envío ofrecen experiencias en canales web y móviles, así como dispositivos IoT no basados en explorador, como un televisor conectado, un quiosco o una pantalla digital en la tienda.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md): utilice el [!DNL Adobe Target] API de administración para administrar propiedades, actividades, audiencias, ofertas, propiedades, informes, mboxes, hosts, entornos y mucho más.

[**[!DNL Target Profile API]**](https://developers.adobetarget.com/api/#profiles): Recuperar [!DNL Adobe Target] información del perfil de usuario.

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports): Recuperar [!UICONTROL Prueba A/B] y [!UICONTROL Automated Personalization] datos del informe de actividad.

[**[!DNL Target Recommendations API]**](http://developers.adobetarget.com/api/recommendations/): utilice el [!DNL Target Recommendations] API.

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md): administre listas de bloqueados para definir las funciones utilizadas en [!DNL Target] modelos de aprendizaje automático.

[**API de Admin Console**](https://developer.adobe.com/umapi/): administre los usuarios y las autorizaciones del producto a través de las API de administración de usuarios y sincronización de usuarios de Adobe.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html): utilice el [!DNL Adobe Experience Platform Edge Network Server] API para una variedad de casos de uso de recopilación de datos, personalización, publicidad y marketing.

## Recursos

* [repositorio de código abierto de Adobe](https://github.com/adobe)
* [Origen del SDK de JS del nodo de destino](https://github.com/adobe/target-nodejs-sdk)
* [Repositorio de ejemplos del SDK de JS del nodo de Target](https://github.com/adobe/target-nodejs-sdk-samples)
* [Origen del SDK de Java de Target](https://github.com/adobe/target-java-sdk)
* [Repositorio de ejemplo del SDK de Java de Target](https://github.com/adobe/target-java-sdk-samples)
* [Implementación de Target](./before-implement/prepare-to-implement-target.md)
* [Administración de Target](./before-administer/target-api-overview.md)
* [Repositorio de GitHub de Adobe Target Dev Docs](https://github.com/AdobeDocs/target-developers)
* [Notas de la versión de Adobe Target](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Guía del usuario de Adobe Target Business](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=es)

