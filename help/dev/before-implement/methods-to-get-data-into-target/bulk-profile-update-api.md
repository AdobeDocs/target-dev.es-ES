---
keywords: implementación, implementación, configuración, configuración, actualización de perfiles en lote api
description: Obtener datos en  [!DNL Target] usando [!UICONTROL Bulk Profile Update API].
title: ¿Cómo puedo obtener datos en  [!DNL Target] usando [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 7%

---

# API de actualización de perfil en lote

[!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] le permite actualizar los perfiles de usuario de varios visitantes de un sitio web de forma masiva mediante un archivo por lotes.

Con [!UICONTROL Bulk Profile Update API], puede enviar convenientemente datos detallados del perfil del visitante en forma de parámetros de perfil para muchos usuarios a [!DNL Target] desde cualquier origen externo. Las fuentes externas pueden incluir sistemas de administración de la relación con los clientes (CRM) o puntos de venta (POS), que normalmente no están disponibles en una página web.

Comparar [!UICONTROL Bulk Profile Update API] con [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] frente a [!UICONTROL Bulk Profile Update API]

Esta opción es similar a [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) con algunas diferencias:

* [!UICONTROL Customer attributes] usa una carga FTP. [!UICONTROL Target Bulk Profile Update API] utiliza una API de POST HTTP.
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