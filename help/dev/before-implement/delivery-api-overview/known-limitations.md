---
title: Consideraciones de la API de envío de Adobe Target y limitaciones conocidas
description: ¿Qué consideraciones y limitaciones conocidas debo tener en cuenta al usar [!UICONTROL Adobe Target Delivery API]?
keywords: api de envío
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 49acf92bbe06dbcee36fef2b7394acd7ce37baad
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 6%

---

# Consideraciones y limitaciones conocidas

* No hay autenticación para las API de entrega de [!DNL Target].
* Esta API no procesa cookies ni redirige llamadas.
* Los nombres de encabezado HTTP/1.1 y HTTP/2 no distinguen entre mayúsculas y minúsculas; sin embargo, HTTP/2 exige nombres de encabezado en minúsculas. Para obtener más información, consulte la [Documentación del Protocolo de transferencia de hipertexto versión 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Si utiliza un punto de conexión que dirija a los visitantes a través de su nueva infraestructura de equilibrador de carga, sus conexiones se actualizan automáticamente a HTTP/2. Este proceso de actualización convierte los encabezados de solicitud en encabezados en minúsculas para que no se consideren con un formato incorrecto.

  Este problema puede suponer un problema para los clientes si sus bibliotecas están configuradas para buscar encabezados de solicitud/respuesta que distingan entre mayúsculas y minúsculas (específicamente, no en minúsculas).
