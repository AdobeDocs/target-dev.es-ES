---
title: Actualización de perfiles
description: Aprenda a utilizar las API de perfil de Adobe Target para enviar datos sobre visitantes a  [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 3b0bc0b67800ed4b1da6ba2bfa05c677147a78ba
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# Actualización de perfiles

Un perfil de usuario contiene información demográfica y de comportamiento de un visitante de una página web, como la edad, el sexo, los productos comprados, la última hora de visita, etc. [!DNL Adobe Target] utiliza esta información para personalizar el contenido que sirve a cada visitante.

La información de perfil de cada visitante se almacena en cookies o en aplicaciones de terceros.

Si su página web implementa el código [!DNL Target] ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md) o [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)), la información de perfil de las cookies se pasa a [!DNL Target] mediante parámetros de perfil. [!DNL Target] identifica a cada visitante de manera única a través de un `pcID` que genera en las cookies del visitante. Sin embargo, puede pasar parámetros de perfil desde una aplicación externa a través de llamadas de mbox usando `mbox3rdPartyIds`.

Use las API de perfil [!DNL Adobe Target] cuando tenga datos de perfil sobre los visitantes que va a enviar a [!DNL Target] y que no pueda o no desee enviar como parte de su integración basada en páginas con [!DNL Target]. Pueden ser datos de un sistema de administración de la relación con los clientes (CRM) o de un punto de venta (POS) que no esté disponible en la página. O estos datos pueden ser más confidenciales y no tiene sentido que se transmitan en la página.

Existen dos formas de actualizar los perfiles mediante API:

* [API de actualización de perfil único](/help/dev/administer/profile-api/profile-single-api.md)
* [Actualización de perfil en lote mediante lote](/help/dev/administer/profile-api/profile-bulk-api.md)
