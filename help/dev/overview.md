---
keywords: guía para desarrolladores de target; información general; inicio
title: Guía para desarrolladores de Adobe Target
description: ¿Cómo implemento y administro [!DNL Adobe Target] y trabajo con sus API y SDK?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: dadc3804da4592dba4ad88b8c5c9f804c56e232b
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 5%

---

# Guía para desarrolladores de [!DNL Adobe Target]

**([Ver [!DNL Target] actualizaciones de la documentación](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html?lang=es){target=_blank})**

Esta guía para desarrolladores de *[!DNL Adobe Target]* proporciona recursos y guías para desarrolladores de [!DNL Target], incluida la documentación de API y SDK para implementar y administrar [!DNL Target].

>[!NOTE]
>
>Además de esta guía, también están disponibles las guías de [!DNL Adobe Target] siguientes:
>
>* [*[!DNL Adobe Target] Guía para profesionales de la empresa *](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=es){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=es){target=_blank}
>
>Para obtener información de la versión, consulte [Notas de la versión de Target (actual)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html?lang=es){target=_blank} en la *[!DNL Adobe Target]Guía para profesionales de la empresa*.

## Introducción a la implementación

**[Antes de implementar](/help/dev/before-implement/considerations-before-you-implement-target.md)**: Consideraciones que debe abordar antes de implementar [!DNL Adobe Target].

## Implementación del lado del cliente

[**SDK web de Adobe Experience Platform**](/help/dev/implement/client-side/aep-web-sdk.md): [!DNL Adobe Experience Platform Web SDK] le permite interactuar con los distintos servicios de [!DNL Experience Cloud] (incluido [!DNL Target]) mediante [!UICONTROL Adobe Experience Edge Network].

[**Biblioteca JavaScript at.js de Target**](/help/dev/implement/client-side/overview.md): La biblioteca JavaScript at.js mejora los tiempos de carga de página en implementaciones web, mejora la seguridad y proporciona mejores opciones de implementación en aplicaciones de una sola página.

## Implementación del lado del servidor

[**Información general del SDK de Target**](implement/server-side/server-side-overview.md): Introducción a los SDK de [!DNL Adobe Target], incluida la toma de decisiones en el dispositivo.

[**SDK de Node.js**](implement/server-side/node-js/overview.md): Cómo usar el SDK de Node.js [!DNL Target].

[**SDK de Java**](implement/server-side/java/overview.md): Cómo usar el SDK de Java de [!DNL Target].

SDK [**.NET**](implement/server-side/net/overview.md): Cómo usar el SDK .NET de [!DNL Target].

[**SDK de Python**](implement/server-side/python/overview.md): Cómo usar el SDK de Python [!DNL Target].

## Implementación híbrida

[**Implementación híbrida**](implement/hybrid/hybrid-overview.md): Implemente [!DNL Target] con una combinación de implementación del lado del cliente y del lado del servidor.

## Implementación de Recommendations

[**Implementación de Recommendations**](implement/recommendations/recommendations.md): Planifique e implemente [!DNL Adobe Target Recommendations].

## Implementación de aplicaciones móviles

[**Descripción general del SDK móvil de AEP**](implement/mobile/overview.md): Información general sobre cómo implementar [!DNL Adobe Target] con [!DNL Adobe Experience Platform] SDK móviles.

[**Referencia del SDK móvil de AEP**](https://developer.adobe.com/client-sdks/documentation/): Implementar [!DNL Adobe Target] con [!DNL Adobe Experience Platform] SDK móviles.

## Implementación de correo electrónico

[**Descripción general del correo electrónico**](implement/email/overview.md): Información general sobre cómo implementar [!DNL Adobe Target] en correos electrónicos.

## Guías de API

[**Introducción**](before-administer/target-api-overview.md): Información general sobre las API de [!DNL Adobe Target].

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md): utilice las API de entrega [!DNL Adobe Target] para ofrecer experiencias en canales web y móviles, así como dispositivos de IoT no basados en el explorador, como un televisor conectado, un quiosco o una pantalla digital en la tienda.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md): use la API de administración de [!DNL Adobe Target] para administrar propiedades, actividades, audiencias, ofertas, propiedades, informes, mboxes, hosts, entornos y mucho más.

[**[!DNL Target Profile API]**](/help/dev/administer/profile-api/profiles-api.md): recupere información del perfil de usuario [!DNL Adobe Target].

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports): Recupere datos de informe de actividad [!UICONTROL A/B Test] y [!UICONTROL Automated Personalization].

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/): Use la API [!DNL Target Recommendations].

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md): administre listas de bloqueados para definir las características utilizadas en [!DNL Target] modelos de aprendizaje automático.

[**API de Admin Console**](https://developer.adobe.com/umapi/): administre usuarios y autorizaciones de productos mediante las API de administración de usuarios y sincronización de usuarios de Adobe.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=es): Use la API [!DNL Adobe Experience Platform Edge Network Server] para una variedad de casos de uso de recopilación de datos, personalización, publicidad y marketing.

## Recursos

* [repositorio de código abierto de Adobe](https://github.com/adobe)
* [Source de SDK de JS de nodo de destino](https://github.com/adobe/target-nodejs-sdk)
* [Ejemplos del SDK de JS del nodo de destino Repositorio](https://github.com/adobe/target-nodejs-sdk-samples)
* [Source de SDK de Java de Target](https://github.com/adobe/target-java-sdk)
* [Repositorio de ejemplo del SDK de Java de Target](https://github.com/adobe/target-java-sdk-samples)
* [Implementación de Target](./before-implement/prepare-to-implement-target.md)
* [Administración de Target](./before-administer/target-api-overview.md)
* [Repositorio de GitHub de Adobe Target Dev Docs](https://github.com/AdobeDocs/target-developers)
* [Notas de la versión de Adobe Target](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html?lang=es)
* [Guía del usuario de Adobe Target para empresas](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=es)

