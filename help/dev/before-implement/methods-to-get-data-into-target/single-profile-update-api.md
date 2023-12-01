---
keywords: implementación, implementación, configuración, configuración, actualización de perfil único
description: Introducción de datos en [!DNL Target] uso de la API de actualización de perfil único.
title: ¿Cómo puedo obtener datos en? [!DNL Target] Uso del [!UICONTROL API de actualización de perfil único]?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# [!UICONTROL API de actualización de perfil único]

El [!DNL Adobe Target] [!UICONTROL API de actualización de perfil único] permite enviar una actualización de perfil para un solo usuario. El [!UICONTROL API de actualización de perfil único] es casi idéntico al de [!UICONTROL API de actualización de perfil en lote], pero se actualiza un perfil de visitante a la vez, en línea con la llamada de API en lugar de con un archivo .cvs.

El [!UICONTROL API de actualización de perfil único] y se utiliza generalmente cuando debe producirse una actualización en relación con una transacción que se produce en un canal que no se ha implementado [!DNL Target]. Por ejemplo, desea actualizar el perfil de un único visitante que realiza alguna acción sin conexión. Las acciones pueden incluir llegar a un centro de llamadas, financiar un préstamo, usar una tarjeta de fidelidad en una tienda, acceder a un quiosco, etc.

Contrastar con [!UICONTROL API de actualización de perfil único] con el [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## Recursos

Para obtener más información, consulte:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
