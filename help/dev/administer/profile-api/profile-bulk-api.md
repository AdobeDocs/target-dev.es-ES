---
title: API de actualización de perfil en lote de Adobe Target
description: Aprenda a utilizar [!DNL Adobe Target] [!UICONTROL API de actualización de perfil en lote] para enviar datos de perfil de varios visitantes a [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 8bc819823462fae71335ac3b6c871140158638fe
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 8%

---

# [!DNL Adobe Target Bulk Profile Update API]

El [!DNL Adobe Target] [!UICONTROL API de actualización de perfil en lote] permite actualizar de forma masiva los perfiles de usuario de varios visitantes de un sitio web mediante un archivo por lotes.

Uso del [!UICONTROL API de actualización de perfil en lote], puede enviar cómodamente datos detallados del perfil del visitante en forma de parámetros de perfil para que muchos usuarios de [!DNL Target] de cualquier fuente externa. Las fuentes externas pueden incluir sistemas de administración de la relación con los clientes (CRM) o puntos de venta (POS), que normalmente no están disponibles en una página web.

| Versión  | Ejemplo de URL | Funciones |
| --- | --- | --- |
| Versión 1 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate` | Solo es compatible con la actualización de perfiles en lote. |
| Versión 2 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Crear perfil si no se encuentra.</li><li>Actualización del estado por fila.</li></ul> |

>[!NOTE]
>
>Versión 2 (v2) de [!UICONTROL API de actualización de perfil en lote] es la versión actual. Sin embargo, [!DNL Target] sigue siendo compatible con la versión 1 (v1).

## Ventajas de la API de actualización de perfiles en lote

* No hay ningún límite en la cantidad de atributos del perfil.
* Los atributos de perfil enviados a través del sitio se pueden actualizar mediante la API y viceversa.

## Advertencias

* El tamaño del archivo en lote debe ser inferior a 50 MB. Además, el número total de filas no puede superar las 500 000 filas por carga.
* No hay límite en el número o las filas que puede cargar durante un periodo de 24 horas en lotes posteriores. Sin embargo, el proceso de ingestión puede acelerarse durante el horario laboral para garantizar que otros procesos se ejecuten de forma eficaz.
* Las llamadas de actualización por lotes v2 consecutivas sin llamadas de mbox intermedias para los mismos ID de terceros anulan las propiedades actualizadas en la primera llamada de actualización por lotes.

## Archivo por lotes

Para actualizar los datos de perfil de forma masiva, cree un archivo por lotes. El archivo por lotes es un archivo de texto con valores separados por comas similar al siguiente archivo de muestra.

``````
batch=pcId, param1, param2, param3, param4 123, value1 124, value1,,, value4 125,, value2 126, value1, value2, value3, value4
``````

Hace referencia a este archivo en la llamada del POST a [!DNL Target] para procesar el archivo. Al crear el archivo por lotes, tenga en cuenta lo siguiente:

* La primera fila del archivo debe especificar encabezados de columna.
* El primer encabezado debe ser un `pcId` o `thirdPartyId`. El [!UICONTROL ID de visitante de Marketing Cloud] no es compatible. [!UICONTROL pcId] es un [!DNL Target]ID de visitante no generado. `thirdPartyId` es un ID especificado por la aplicación cliente, que se pasa a [!DNL Target] mediante una llamada de mbox como `mbox3rdPartyId`. Debe ser referido aquí como `thirdPartyId`.
* Los parámetros y valores especificados en el archivo por lotes deben estar codificados en URL mediante UTF-8 por motivos de seguridad. Los parámetros y valores se pueden reenviar a otros nodos perimetrales para su procesamiento mediante solicitudes HTTP.
* Los parámetros deben tener el formato `paramName` solo. Los parámetros se muestran en [!DNL Target] as `profile.paramName`.
* Si está utilizando [!UICONTROL API de actualización de perfil en lote] v2, no es necesario especificar todos los valores de parámetro para cada `pcId`. Los perfiles se crean para cualquier `pcId` o `mbox3rdPartyId` que no se encuentra en [!DNL Target]. Si utiliza la versión 1, los perfiles no se crean para los pcIds o mbox3rdPartyIds que faltan.
* El tamaño del archivo en lote debe ser inferior a 50 MB. Además, el número total de filas no debe superar los 500 000. Este límite garantiza que los servidores no se inunden con demasiadas solicitudes.
* Puede enviar varios archivos. Sin embargo, la suma total de las filas de todos los archivos que envía en un día no debe superar un millón para cada cliente.
* No hay límite en el número de atributos que se cargan. Sin embargo, el tamaño total de un perfil, incluidos los datos del sistema, no debe superar los 2000 KB. [!DNL Adobe] recomienda utilizar menos de 1000 KB de almacenamiento para los atributos de perfil.
* Los parámetros y valores distinguen entre mayúsculas y minúsculas.

## Solicitud de POST HTTP

Realizar una solicitud de POST HTTP a [!DNL Target] servidores Edge para procesar el archivo. Este es un ejemplo de solicitud de POST HTTP para el archivo batch.txt mediante el comando curl:

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

Donde:

BATCH.TXT es el nombre de archivo. CLIENTCODE es el [!DNL Target] código de cliente.

Si no conoce su código de cliente, en la [!DNL Target] clic en interfaz de usuario **[!UICONTROL Administration]** > **[!UICONTROL Implementación]**. El código de cliente se muestra en la [!UICONTROL Detalles de cuenta] sección.

### Inspect la respuesta

v2 devuelve un estado de perfil a perfil y v1 solo devuelve el estado general. La respuesta incluye un vínculo a una dirección URL diferente que tiene el mensaje de éxito perfil a perfil.

### Respuesta de ejemplo

```
true http://mboxedge19.tt.omtrdc.net/m2/demo/v2/profile/batchStatus?batchId=demo-1845664501&m2Node=00 Batch submitted for processing
```

Si hay un error, la respuesta contiene `success=false` y un mensaje detallado del error.

Una respuesta correcta tiene el siguiente aspecto:

``````
demo-1845664501 1436187396849-250353.03_03 success 2403081156529-351655.03_03 success 2403081156529-351656.03_03 success 1436187396849-250351.01_00 success 
``````

Los valores esperados para los campos de estado son:

**success**: se ha actualizado el perfil. Si no se ha encontrado el perfil, se ha creado uno con los valores del lote.
**error**: el perfil no se ha actualizado ni creado debido a un error, una excepción o una pérdida de mensaje.
**pendiente**: el perfil aún no se ha actualizado ni creado.



