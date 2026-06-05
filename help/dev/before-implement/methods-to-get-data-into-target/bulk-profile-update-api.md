---
keywords: implementación, implementación, configuración, configuración, actualización de perfiles en lote api
description: Obtenga datos en  [!DNL Target] mediante la API de actualización de perfil en lotes [!UICONTROL Bulk Profile Update].
title: ¿Cómo puedo obtener datos en  [!DNL Target] usando la API de actualización de perfiles en lotes [!UICONTROL 2&rbrace;?]
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
TQID: https://experienceleague.adobe.com/vBcIsBR6wwYr7MbRh7UJvt71ULDEq6iXVZ5spZlif-0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 284
ht-degree: 5%

---

# API de actualización de perfil en lote

La [!DNL Adobe Target] [!UICONTROL API de actualización de perfiles en lote] le permite actualizar los perfiles de usuario de varios visitantes de un sitio web en lote mediante un archivo por lotes.

Con la [!UICONTROL API de actualización de perfiles en lotes], puede enviar convenientemente datos detallados del perfil del visitante en forma de parámetros de perfil para muchos usuarios a [!DNL Target] desde cualquier fuente externa. Las fuentes externas pueden incluir sistemas de administración de la relación con los clientes (CRM) o puntos de venta (POS), que normalmente no están disponibles en una página web.

Comparar la [!UICONTROL API de actualización de perfiles en lotes] con la [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Atributos del cliente] frente a la [!UICONTROL API de actualización de perfiles en lotes]

Esta opción es similar a [[!UICONTROL atributos del cliente]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) con algunas diferencias:

* [!UICONTROL Los atributos del cliente] utilizan una carga de FTP. La [!UICONTROL API de actualización de perfiles en lote de Target] usa una API de HTTP POST.
* Los datos del [!UICONTROL atributo del cliente] se pueden compartir con [!DNL Analytics]. La [!UICONTROL actualización de perfil en lotes] solo se puede usar en [!DNL Target].
* [!UICONTROL Los atributos del cliente] admiten la creación de un perfil para un usuario [!DNL Target] que aún no ha visto.
   * [!UICONTROL API de actualización de perfiles en lote] v2: no es necesario especificar todos los valores de parámetro para cada `pcId`. Los perfiles se crean para cualquier `pcId` o `mbox3rdPartyId` que no se encuentre en [!DNL Target].
   * [!UICONTROL API de actualización de perfiles en lote] v1: la [!UICONTROL API de actualización de perfiles en lote] actualiza únicamente los perfiles existentes de [!DNL Target]. Si usa la versión 1, los perfiles no se crean para los elementos que faltan `pcIds` o `mbox3rdPartyIds`.
* [!UICONTROL Los atributos del cliente] requieren el uso de [!UICONTROL Experience Cloud ID] (ECID) y el uso de un ID de origen, como el ID de CRM o el ID de fidelidad.
* La [!UICONTROL API de actualización de perfiles en lote] requiere el identificador de TNT o `mbox3rdPartyId`.
* No se pueden enviar los siguientes caracteres en `mbox3rdPartyID`: signo más (+) y barra diagonal (/).

## Recursos

Para obtener más información, consulte:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)