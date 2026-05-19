---
keywords: implementación, implementación, configuración, configuración, actualización de perfiles en lote api
description: Obtener datos en  [!DNL Target] usando [!UICONTROL Bulk Profile Update API].
title: ¿Cómo puedo obtener datos en  [!DNL Target] usando [!UICONTROL Bulk Profile Update API]?
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
source-wordcount: 221
ht-degree: 7%

---

# API de actualización de perfil en lote

[!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] le permite actualizar los perfiles de usuario de varios visitantes de un sitio web de forma masiva mediante un archivo por lotes.

Con [!UICONTROL Bulk Profile Update API], puede enviar convenientemente datos detallados del perfil del visitante en forma de parámetros de perfil para muchos usuarios a [!DNL Target] desde cualquier origen externo. Las fuentes externas pueden incluir sistemas de administración de la relación con los clientes (CRM) o puntos de venta (POS), que normalmente no están disponibles en una página web.

Comparar [!UICONTROL Bulk Profile Update API] con [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] frente a [!UICONTROL Bulk Profile Update API]

Esta opción es similar a [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) con algunas diferencias:

* [!UICONTROL Customer attributes] usa una carga FTP. [!UICONTROL Target Bulk Profile Update API] utiliza una API HTTP POST.
* [!UICONTROL Customer attribute] datos se pueden compartir con [!DNL Analytics]. [!UICONTROL Bulk Profile Update] solo se puede usar en [!DNL Target].
* Compatibilidad con [!UICONTROL Customer attributes] al crear un perfil para un usuario [!DNL Target] que aún no ha visto.
   * [!UICONTROL Bulk Profile Update API] v2: no es necesario especificar todos los valores de parámetro para cada `pcId`. Los perfiles se crean para cualquier `pcId` o `mbox3rdPartyId` que no se encuentre en [!DNL Target].
   * [!UICONTROL Bulk Profile Update API] v1: [!UICONTROL Bulk Profile Update API] actualiza solo los perfiles existentes de [!DNL Target]. Si usa la versión 1, los perfiles no se crean para los elementos que faltan `pcIds` o `mbox3rdPartyIds`.
* [!UICONTROL Customer attributes] requiere el uso de [!UICONTROL Experience Cloud ID] (ECID) y el uso de un ID de origen, como el ID de CRM o el ID de fidelidad.
* [!UICONTROL Bulk Profile Update API] requiere el identificador de TNT o `mbox3rdPartyId`.
* No se pueden enviar los siguientes caracteres en `mbox3rdPartyID`: signo más (+) y barra diagonal (/).

## Recursos

Para obtener más información, consulte:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)