---
keywords: implementación, implementación, configuración, configuración, actualización de perfiles en lote api
description: Introducción de datos en [!DNL Target] uso del [!UICONTROL API de actualización de perfil en lote].
title: ¿Cómo puedo obtener datos en? [!DNL Target] Uso del [!UICONTROL API de actualización de perfil en lote]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 5%

---

# API de actualización de perfil en lote

El [!DNL Adobe Target] [!UICONTROL API de actualización de perfil en lote] permite actualizar de forma masiva los perfiles de usuario de varios visitantes de un sitio web mediante un archivo por lotes.

Uso del [!UICONTROL API de actualización de perfil en lote], puede enviar cómodamente datos detallados del perfil del visitante en forma de parámetros de perfil para que muchos usuarios de [!DNL Target] de cualquier fuente externa. Las fuentes externas pueden incluir sistemas de administración de la relación con los clientes (CRM) o puntos de venta (POS), que normalmente no están disponibles en una página web.

Contrastar con [!UICONTROL API de actualización de perfil en lote] con el [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Atributos del cliente] frente a [!UICONTROL API de actualización de perfil en lote]

Esta opción es similar a [[!UICONTROL atributos del cliente]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) con algunas diferencias:

* [!UICONTROL Atributos del cliente] utilice una carga por FTP. El [!UICONTROL API de actualización de perfil en lote de Target] utiliza una API de POST HTTP.
* [!UICONTROL Atributo del cliente] Los datos de se pueden compartir con [!DNL Analytics]. El [!UICONTROL Actualización de perfil en lote] solo se puede utilizar en [!DNL Target].
* [!UICONTROL Atributos del cliente] compatibilidad con la creación de un perfil para un usuario [!DNL Target] aún no ha visto.
   * [!UICONTROL API de actualización de perfil en lote] v2: No es necesario especificar todos los valores de parámetro para cada `pcId`. Los perfiles se crean para cualquier `pcId` o `mbox3rdPartyId` que no se encuentra en [!DNL Target].
   * [!UICONTROL API de actualización de perfil en lote] v1: La [!UICONTROL API de actualización de perfil en lote] actualizaciones existentes [!DNL Target] solo perfiles. Si utiliza la versión 1, los perfiles no se crean para los que faltan `pcIds` o `mbox3rdPartyIds`.
* [!UICONTROL Atributos del cliente] requerir el uso de la variable [!UICONTROL ID de Experience Cloud] (ECID) y el uso de un ID de origen, como el ID de CRM o el ID de fidelidad.
* El [!UICONTROL API de actualización de perfil en lote] requiere el ID de TNT o el `mbox3rdPartyId`.
* No se pueden enviar los siguientes caracteres en `mbox3rdPartyID`: signo más (+) y barra diagonal (/).

## Recursos

Para obtener más información, consulte:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)