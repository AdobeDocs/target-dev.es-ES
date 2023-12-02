---
title: Información general sobre las API de perfil Adobe Target
description: Aprenda a utilizar las API de perfil de Adobe Target para enviar datos sobre visitantes a [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 1a1c3d96cf6ef5c337a63fdec8c700da695ff5d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!DNL Adobe Target Profile APIs overview]

Un perfil de usuario contiene información demográfica y de comportamiento de un visitante de una página web, como la edad, el sexo, los productos comprados, la última hora de visita, etc. [!DNL Adobe Target] utiliza esta información para personalizar el contenido que sirve a cada visitante.

La información de perfil de cada visitante se almacena en cookies o en aplicaciones de terceros.

Si la página web implementa [!DNL Target] código ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) o el [SDK web de Adobe Experience Platform](/help/dev/implement/client-side/aep-web-sdk.md)), la información de perfil de las cookies se pasa a [!DNL Target] uso de parámetros de perfil. [!DNL Target] identifica a cada visitante de forma exclusiva mediante una `pcID` que genera en las cookies del visitante. Sin embargo, puede pasar parámetros de perfil desde una aplicación externa a través de llamadas de mbox mediante `mbox3rdPartyIds`.

Utilice el [!DNL Adobe Target] API de perfil de cuando tiene datos de perfil de los visitantes que enviar a [!DNL Target] que no puede enviar o no desea enviar como parte de su integración basada en páginas con [!DNL Target]. Pueden ser datos de un sistema de administración de la relación con los clientes (CRM) o de un punto de venta (POS) que no esté disponible en la página. O estos datos pueden ser más confidenciales y no tiene sentido que se transmitan en la página.

Existen dos formas de actualizar los perfiles mediante API:

* [API de actualización de perfil único](/help/dev/administer/profile-api/profile-single-api.md)
* [Actualización de perfil en lote mediante lote](/help/dev/administer/profile-api/profile-bulk-api.md)

La documentación heredada de la API de perfiles se puede encontrar aquí: [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}
