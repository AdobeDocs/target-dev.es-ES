---
keywords: implementación, implementación, configuración, configuración, actualización de perfiles en lote api
description: Introducción de datos en [!DNL Target] uso del [!UICONTROL API de actualización de perfil en lote].
title: ¿Cómo puedo obtener datos en? [!DNL Target] Uso del [!UICONTROL API de actualización de perfil en lote]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 24%

---

# API de actualización de perfil en lote

Mediante API, envíe un archivo .csv a [!DNL Adobe Target] con actualizaciones del perfil del visitante para muchos visitantes. Cada perfil de visitante se puede actualizar con varios atributos de perfil en página con una llamada.

Esta opción es similar a [!UICONTROL atributos del cliente] con algunas diferencias:

* [!UICONTROL Atributos del cliente] utilice una carga por FTP. El [!UICONTROL API de actualización de perfil en lote de Target] utiliza una API de POST HTTP.
* [!UICONTROL Atributo del cliente] Los datos de se pueden compartir con [!DNL Analytics]. La actualización de perfiles en lote solo se puede usar en [!DNL Target].
* [!UICONTROL Atributos del cliente] compatibilidad con la creación de un perfil para un usuario [!DNL Target] aún no ha visto.
   * [!UICONTROL API de actualización de perfil en lote] v2: No es necesario especificar todos los valores de parámetro para cada `pcId`. Los perfiles se crean para cualquier `pcId` o `mbox3rdPartyId` que no se encuentra en [!DNL Target].
   * [!UICONTROL API de actualización de perfil en lote] v1: La [!UICONTROL API de actualización de perfil en lote] actualizaciones existentes [!DNL Target] solo perfiles. Si utiliza la versión 1, los perfiles no se crean para los que faltan `pcIds` o `mbox3rdPartyIds`.
* [!UICONTROL Atributos del cliente] requerir el uso de la variable [!UICONTROL ID de Experience Cloud] (ECID) y el uso de un ID de origen, como el ID de CRM o el ID de fidelidad.
* El [!UICONTROL API de actualización de perfil en lote] requiere el ID de TNT o el `mbox3rdPartyId`.
* No se pueden enviar los siguientes caracteres en `mbox3rdPartyID`: signo más (+) y barra diagonal (/).

## Formato

El archivo .csv debe hacer referencia a cada visitante a través de su [!DNL Target] PCID o `mbox3rdPartyId`. El [!UICONTROL ID de Experience Cloud] (ECID) no es compatible. Todos los atributos o valores del perfil se crean y actualizan a través de la API. En la documentación de la API encontrará detalles sobre el formato.

## Casos de uso de ejemplo

Su CRM u otro sistema interno almacena datos valiosos sobre sus visitantes que desea actualizar de manera consistente en [!DNL Target], sin exponer los datos de perfil en la implementación de la página.

## Ventajas del método

* No hay ningún límite en la cantidad de atributos del perfil.
* Los atributos de perfil enviados a través del sitio se pueden actualizar mediante la API y viceversa.

## Advertencias

* El tamaño del archivo en lote debe ser inferior a 50 MB. Además, el número total de filas no puede superar las 500 000 filas por carga.
* Las actualizaciones suelen producirse en menos de una hora, pero pueden tardar hasta 24 horas en reflejarse.
* No hay límite en el número o las filas que puede cargar durante un periodo de 24 horas en lotes posteriores. Sin embargo, el proceso de ingestión puede acelerarse durante el horario laboral para garantizar que otros procesos se ejecuten de forma eficaz.
* Llamadas de actualización en lote V2 consecutivas sin llamadas de mbox intermedias para lo mismo `thirdPartyIds` anule las propiedades actualizadas en la primera llamada de actualización por lotes.

## Recursos

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)