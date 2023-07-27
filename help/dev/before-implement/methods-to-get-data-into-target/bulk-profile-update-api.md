---
keywords: implementación, implementación, configuración, configuración, actualización de perfiles en lote
description: Introducción de datos en [!DNL Target] uso de la API de actualización de perfiles en lote.
title: ¿Cómo puedo obtener datos en? [!DNL Target] ¿Utiliza la API de actualización de perfiles en lote?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 62%

---

# API de actualización de perfiles en lote

Mediante API, envíe un archivo .csv a [!DNL Adobe Target] con actualizaciones del perfil del visitante para muchos visitantes. Cada perfil de visitante se puede actualizar con varios atributos de perfil en página con una llamada.

Esta opción es similar a los Atributos del cliente con algunas diferencias:

* Los atributos del cliente utilizan una carga FTP mientras que la variable [!UICONTROL API de actualización de perfil en lote de Target] utiliza una API de POST HTTP.
* Los datos de atributos del cliente se pueden compartir con [!DNL Analytics]. [!UICONTROL La actualización de perfiles en lote solo se puede usar en Target.]
* Los Atributos del cliente admiten la creación de un perfil para un usuario [!DNL Target] aún no ha visto. La API de actualización de perfiles en lote actualiza las existentes [!DNL Target] solo perfiles.
* Los atributos del cliente requieren el uso del ID de Experience Cloud (ECID) y el uso de un ID de origen, como el ID de CRM o el ID de fidelidad.
* La API de actualización de perfiles en lote requiere el ID de TNT o el `mbox3rdPartyId`.
* No se pueden enviar los siguientes caracteres en `mbox3rdPartyID`: signo más (+) y barra diagonal (/).

## Formato

El archivo .csv debe hacer referencia a cada visitante a través de su [!DNL Target] PCID o `mbox3rdPartyId`. El Experience Cloud ID (ECID) no se admite. Todos los atributos o valores del perfil se crean y actualizan a través de la API. En la documentación de la API encontrará detalles sobre el formato.

## Casos de uso de ejemplo

Su CRM u otro sistema interno almacena datos valiosos sobre sus visitantes que le interesa actualizar sistemáticamente en Target sin exponer los datos de perfil en la implementación de su página.

## Ventajas del método

No hay ningún límite en la cantidad de atributos del perfil.

Los atributos de perfil enviados a través del sitio se pueden actualizar a través de la API y viceversa.

## Advertencias

El tamaño del archivo en lote debe ser inferior a 50 MB. Además, el número total de filas no puede superar las 500 000 filas por carga.

No hay ningún límite en el número de filas que puede cargar en lotes consecutivos en un período de 24 horas. Sin embargo, el proceso de ingestión puede acelerarse durante el horario laboral para garantizar que otros procesos se ejecuten de forma eficaz.

Las [actualizaciones de llamadas en lote V2](https://developers.adobetarget.com/api/#updating-profiles) consecutivas   sin llamadas mbox intermedias para los mismos ID de terceros ignoran las propiedades actualizadas en la primera actualización de la llamada en lote.

## Ejemplos de código

Consulte [Actualización de perfiles](https://developers.adobetarget.com/api/#updating-profiles).

### Vínculos a información relevante

[Actualización de perfiles](https://developers.adobetarget.com/api/#updating-profiles)
