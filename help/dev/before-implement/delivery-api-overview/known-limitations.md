---
title: Consideraciones de la API de envío de Adobe Target y limitaciones conocidas
description: ¿Qué consideraciones y limitaciones conocidas debo tener en cuenta al usar [!UICONTROL Adobe Target Delivery API]?
keywords: API de envío
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/LCgGZONQpYfw6JxNCNc2Iu13Mft8Zfx-3Uxvm2EeUVk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 154
ht-degree: 7%

---

# Consideraciones y limitaciones conocidas

La siguiente información enumera consideraciones y limitaciones conocidas con el uso de [!DNL Adobe Target] [!DNL Delivery API].

* No hay autenticación para las API de entrega de [!DNL Target].
* Esta API no procesa cookies ni redirige llamadas.
* Los nombres de encabezado HTTP/1.1 y HTTP/2 no distinguen entre mayúsculas y minúsculas; sin embargo, HTTP/2 exige nombres de encabezado en minúsculas. Para obtener más información, consulte la [Documentación del Protocolo de transferencia de hipertexto versión 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Si utiliza un punto de conexión que dirija a los visitantes a través de su nueva infraestructura de equilibrador de carga, sus conexiones se actualizan automáticamente a HTTP/2. Este proceso de actualización convierte los encabezados de solicitud en encabezados en minúsculas para que no se consideren con un formato incorrecto.

  Este problema puede suponer un problema para los clientes si sus bibliotecas están configuradas para buscar encabezados de solicitud/respuesta que distingan entre mayúsculas y minúsculas (específicamente, no en minúsculas).
