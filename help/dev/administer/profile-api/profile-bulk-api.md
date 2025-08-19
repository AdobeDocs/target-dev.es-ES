---
title: API de actualización de perfil en lote de Adobe Target
description: Aprenda a usar [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] para enviar datos de perfil de varios visitantes a [!DNL Target] para usarlos en la segmentación.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: dae198fd8ef3fc8473ad31807c146802339b1832
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 7%

---

# [!DNL Adobe Target Bulk Profile Update API]

[!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] le permite actualizar los perfiles de usuario de varios visitantes de un sitio web de forma masiva mediante un archivo por lotes.

Con [!UICONTROL Bulk Profile Update API], puede enviar convenientemente datos detallados del perfil del visitante en forma de parámetros de perfil para muchos usuarios a [!DNL Target] desde cualquier origen externo. Las fuentes externas pueden incluir sistemas de administración de la relación con los clientes (CRM) o puntos de venta (POS), que normalmente no están disponibles en una página web.

| Versión  | Ejemplo de URL | Funciones |
| --- | --- | --- |
| Versión 1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | Solo es compatible con la actualización de perfiles en lote. |
| Versión 2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Crear perfil si no se encuentra.</li><li>Actualización del estado por fila.</li></ul> |

>[!NOTE]
>
>Versión 2 (v2) de [!DNL Bulk Profile Update API] es la versión actual. Sin embargo, [!DNL Target] sigue siendo compatible con la versión 1 (v1).
>
>* Si su implementación de [!DNL Target] usa [!DNL Experience Cloud ID] (ECID) como uno de los identificadores de perfil para visitantes anónimos, no use `pcId` como clave en un archivo por lotes de la versión 2 (v2). El uso de `pcId` con la versión 2 de [!DNL Bulk Profile Update API] está pensado solamente para implementaciones [!DNL Target] independientes que no dependen de ECID.
>
>* Si su implementación utiliza ECID para la identificación del perfil y desea utilizar `pcId` como clave en el archivo por lotes, utilice la versión 1 (v1) de la API.
>
>* Si su implementación usa `thirdPartyId` para la identificación del perfil, use la versión 2 (v2) de la API con `thirdPartyId` como clave.

## Ventajas de [!UICONTROL Bulk Profile Update API]

* No hay ningún límite en la cantidad de atributos del perfil.
* Los atributos de perfil enviados a través del sitio se pueden actualizar mediante la API y viceversa.

## Advertencias

* El tamaño del archivo en lote debe ser inferior a 50 MB. Además, el número total de filas no puede superar las 500 000 filas por carga.
* Las actualizaciones suelen producirse en menos de una hora, pero pueden tardar hasta 24 horas en reflejarse.
* No hay límite en el número o las filas que puede cargar durante un periodo de 24 horas en lotes posteriores. Sin embargo, el proceso de ingestión puede acelerarse durante el horario laboral para garantizar que otros procesos se ejecuten de forma eficaz.
* Las llamadas de actualización por lotes v2 consecutivas sin llamadas de mbox intermedias para los mismos ID de terceros anulan las propiedades actualizadas en la primera llamada de actualización por lotes.
* [!DNL Adobe] no garantiza que el 100% de los datos de perfil por lotes se incorporarán y conservarán en Target y, por lo tanto, estarán disponibles para su uso en la segmentación. En el diseño actual, existe la posibilidad de que un pequeño porcentaje de datos (hasta el 0,1 % de los lotes de producción grandes) no se incorpore o conserve.

## Archivo por lotes

Para actualizar los datos de perfil de forma masiva, cree un archivo por lotes. El archivo por lotes es un archivo de texto con valores separados por comas similar al siguiente archivo de muestra.

``` ```
batch=pcId,param1,param2,param3,param4
123,value1
124,value1,,,value4
125,,value2
126,value1,value2,value3,value4
``` ```

>[!NOTE]
>
>El parámetro `batch=` es obligatorio y debe especificarse al principio del archivo.

Hace referencia a este archivo en la llamada de POST a [!DNL Target] servidores para procesar el archivo. Al crear el archivo por lotes, tenga en cuenta lo siguiente:

* La primera fila del archivo debe especificar encabezados de columna.
* El primer encabezado debe ser un `pcId` o `thirdPartyId`. No se admite [!UICONTROL Marketing Cloud visitor ID]. [!UICONTROL pcId] es un visitorID generado por [!DNL Target]. `thirdPartyId` es un identificador especificado por la aplicación cliente, que se pasa a [!DNL Target] a través de una llamada de mbox como `mbox3rdPartyId`. Se debe hacer referencia a él aquí como `thirdPartyId`.
* Los parámetros y valores especificados en el archivo por lotes deben estar codificados en URL mediante UTF-8 por motivos de seguridad. Los parámetros y valores se pueden reenviar a otros nodos perimetrales para su procesamiento mediante solicitudes HTTP.
* Los parámetros sólo deben tener el formato `paramName`. Los parámetros se muestran en [!DNL Target] como `profile.paramName`.
* Si usa [!UICONTROL Bulk Profile Update API] v2, no es necesario especificar todos los valores de parámetro para cada `pcId`. Los perfiles se crean para cualquier `pcId` o `mbox3rdPartyId` que no se encuentre en [!DNL Target]. Si utiliza la versión 1, los perfiles no se crean para los pcIds o mbox3rdPartyIds que faltan.
* El tamaño del archivo en lote debe ser inferior a 50 MB. Además, el número total de filas no debe superar los 500 000. Este límite garantiza que los servidores no se inunden con demasiadas solicitudes.
* Puede enviar varios archivos. Sin embargo, la suma total de las filas de todos los archivos que envía en un día no debe superar un millón para cada cliente.
* No hay restricciones en el número de atributos que se pueden cargar. Sin embargo, el tamaño total de los datos de perfil externos, que incluyen los atributos del cliente, la API del perfil, los parámetros de perfil In-Mbox y la salida del script de perfil, no debe superar los 64 KB.
* Los parámetros y valores distinguen entre mayúsculas y minúsculas.

## petición HTTP POST

Realice una petición HTTP POST a [!DNL Target] servidores Edge para procesar el archivo. Este es un ejemplo de una petición HTTP POST para el archivo batch.txt mediante el comando curl:

``` ```
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``` ```

Donde:

BATCH.TXT es el nombre de archivo. CLIENTCODE es el código de cliente [!DNL Target].

Si no conoce su código de cliente, en la interfaz de usuario de [!DNL Target], haga clic en **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. El código de cliente se muestra en la sección [!UICONTROL Account Details].

### Inspeccione la respuesta

La API de perfiles devuelve el estado de envío del lote para su procesamiento junto con un vínculo en &quot;batchStatus&quot; a una dirección URL diferente que muestra el estado general del trabajo por lotes en particular.

### Ejemplo de respuesta de API

El siguiente código recortado es un ejemplo de respuesta de API de perfiles:

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

Si hay un error, la respuesta contiene `success=false` y un mensaje detallado del error.

### Respuesta de estado de lote predeterminada

Una respuesta predeterminada correcta cuando se hace clic en el vínculo de URL `batchStatus` anterior tiene el siguiente aspecto:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Los valores esperados para los campos de estado son:

| Estado | Detalles |
| --- | --- |
| [!UICONTROL complete] | La solicitud de actualización de lote de perfiles se completó correctamente. |
| [!UICONTROL incomplete] | La solicitud de actualización de lote de perfiles aún se está procesando y no se ha completado. |
| [!UICONTROL stuck] | La solicitud de actualización de lote de perfiles está atascada y no se pudo completar. |

### Respuesta URL de estado detallado del lote

Se puede obtener una respuesta más detallada pasando un parámetro `showDetails=true` a la dirección URL `batchStatus` anterior.

Por ejemplo:

```
http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383&showDetails=true
```

#### Respuesta detallada

```
<response>
    <batchId>demo4-1701473848678-13029383</batchId>
    <status>complete</status>
    <batchSize>1</batchSize>
    <consumedCount>1</consumedCount>
    <successfulUpdates>1</successfulUpdates>
    <profilesNotFound>0</profilesNotFound>
    <failedUpdates>0</failedUpdates>
</response>
```
