---
title: API de actualización de perfil en lote de Adobe Target
description: Aprenda a utilizar [!DNL Adobe Target] [!UICONTROL API de actualización de perfil en lote] para enviar datos de perfil de varios visitantes a [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 38a5e82d3170fa64220bd63f505f1470af43e8a3
workflow-type: tm+mt
source-wordcount: '824'
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
* [!DNL Adobe] no garantiza que el 100 % de los datos de perfil por lotes se incorporen y conserven en Target y que, por lo tanto, estén disponibles para su uso en la segmentación. En el diseño actual, existe la posibilidad de que un pequeño porcentaje de datos (hasta el 0,1 % de los lotes de producción grandes) no se incorpore o conserve.

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

Una respuesta predeterminada correcta cuando lo anterior `batchStatus` Al hacer clic en un vínculo URL, se muestra lo siguiente:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Los valores esperados para los campos de estado son:

| Estado | Detalles |
| --- | --- |
| [!UICONTROL complete] | La solicitud de actualización de lote de perfiles se completó correctamente. |
| [!UICONTROL incompleto] | La solicitud de actualización de lote de perfiles aún se está procesando y no se ha completado. |
| [!UICONTROL atascado] | La solicitud de actualización de lote de perfiles está atascada y no se pudo completar. |

### Respuesta URL de estado detallado del lote

Se puede obtener una respuesta más detallada pasando un parámetro `showDetails=true` a la `batchStatus` url anterior.

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
