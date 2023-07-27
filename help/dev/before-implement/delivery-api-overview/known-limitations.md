---
title: Consideraciones de la API de envío de Adobe Target y limitaciones conocidas
description: ¿Qué consideraciones y limitaciones conocidas debo tener en cuenta al utilizar? [!UICONTROL API de envío de Adobe Target]?
keywords: api de envío
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# Consideraciones y limitaciones conocidas

* No hay autenticación para [!DNL Target] API de envío.
* Esta API no procesa cookies ni redirige llamadas.
* Compatibilidad con [!UICONTROL Automated Personalization] (AP) y [!UICONTROL Recommendations] actividades: Esta API tiene dos modos para recuperar contenido: modo de ejecución y modo de recuperación previa. El modo de recuperación previa solo se puede utilizar para [!UICONTROL Prueba AB] y [!UICONTROL Segmentación de experiencias] Actividades de (XT). No utilice el modo de recuperación previa para [!UICONTROL Automated Personalization] (AP), [!UICONTROL Asignación automática], [!UICONTROL Segmentación automática], o [!UICONTROL Recommendations] tipos de actividades.
* Los nombres de encabezado HTTP/1.1 y HTTP/2 no distinguen entre mayúsculas y minúsculas; sin embargo, HTTP/2 exige nombres de encabezado en minúsculas. Para obtener más información, consulte la [Documentación del Protocolo de transferencia de hipertexto versión 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Si utiliza un punto de conexión que dirija a los visitantes a través de su nueva infraestructura de equilibrador de carga, sus conexiones se actualizan automáticamente a HTTP/2. Este proceso de actualización convierte los encabezados de solicitud en encabezados en minúsculas para que no se consideren con un formato incorrecto.

  Este problema puede suponer un problema para los clientes si sus bibliotecas están configuradas para buscar encabezados de solicitud/respuesta que distingan entre mayúsculas y minúsculas (específicamente, no en minúsculas).
