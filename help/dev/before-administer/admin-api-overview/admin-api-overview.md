---
title: Información general de API de administración de Adobe Target
description: Descripción general de [!DNL Adobe Target Admin API]
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 3%

---

# Información general de API de administración de Target

Este artículo proporciona información general sobre la información básica necesaria para comprender y utilizar [!DNL Adobe Target Admin API]s correctamente. El siguiente contenido supone que comprende cómo [configurar autenticación](../configure-authentication.md) para [!DNL Adobe Target Admin API]s.

>[!NOTE]
>
>Si desea administrar el [!DNL Target] a través de la interfaz de usuario de, consulte la [sección de administración de *Guía para profesionales de Adobe Target Business*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).
>
>Las API de administrador y las API de perfil suelen denominarse de forma colectiva (&quot;API de administrador y de perfil&quot;), pero también pueden denominarse por separado (&quot;API de administrador&quot; y &quot;API de perfil&quot;). La API de Recommendations es una implementación específica de un [!DNL Target] API de administración.

## Antes de empezar  

En todos los ejemplos de código proporcionados para [API de administrador](../../administer/admin-api/admin-api-overview-new.md), reemplazar {tenant} con su valor de inquilino, `your-bearer-token` con el token de acceso que genera con su JWT y `your-api-key` con su clave de API de la [Consola de Adobe Developer](https://developer.adobe.com/console/home). Para obtener más información sobre los inquilinos y JWT, consulte el artículo sobre cómo [configurar autenticación](../configure-authentication.md) para Adobe [!DNL Target] API de administrador.

## Versiones

Todas las API tienen una versión asociada. Es importante proporcionar la versión correcta de la API que desee utilizar.

Si la solicitud contiene una carga útil (POST o PUT), el `Content-Type` encabezado de la solicitud se utiliza para especificar la versión.

Si la solicitud no contiene una carga útil (GET, DELETE o OPTIONS), el `Accept` se utiliza para especificar la versión.

Si no se proporciona una versión, la llamada predeterminada será V1 (application/vnd.adobe.target.v1+json).

>[!NOTE]
>
>Si no se especifica la versión correcta, por ejemplo, si utiliza una carga útil V2 pero no especifica el encabezado Content-Type, la API responderá con un error no admitido si la API no es compatible con versiones anteriores.

Mensaje de error para funciones no admitidas

```
{
    "httpStatus": 406,
    "requestId": "8752b736-cf71-4d81-86c3-94be2b5ae648",
    "requestTime": "2018-02-02T21:39:06.405Z",
    "errors": [
        {
            "errorCode": "Unsupported.Feature",
            "message": "Unsupported features detected"
        }
    ]
}
```

Colección de Admin Postman

Postman es una aplicación que facilita la activación de llamadas de API. Esta [Recopilación de Postman de la API de administración de Target](https://developers.adobetarget.com/api/#admin-postman-collection) contiene todas las llamadas a la API de administración de Target que requieren autenticación mediante actividades, audiencias, ofertas, informes, mboxes y entornos

## Códigos de respuesta

Estos son los códigos de respuesta comunes para las API de administrador de Target.

| Estado | Significado | Descripción |
| --- | --- | --- |
| 200 | [Aceptar](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) | OK |  |
| 400 | [Solicitud incorrecta](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | Solicitud incorrecta. Lo más probable es que los datos proporcionados en la solicitud no sean válidos. |  |
| 401 | [No autorizado](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | El usuario no tiene permiso para realizar esta operación. |  |
| 403 | [Prohibido](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | El acceso a este recurso está prohibido. |  |
| 404 | [No encontrado](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | No se ha encontrado el recurso al que se hace referencia. |  |

## Actividades

Una actividad de le permite probar o personalizar el contenido para los usuarios. Las actividades pueden ser de uno de los siguientes tipos:

* [Campaña A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Segmentación de experiencias (XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html)
* [Recommendations](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html)
* [Personalización automatizada](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Prueba multivariada (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)

## Actualizaciones por lotes

Se pueden ejecutar varias API de administrador como una sola solicitud por lotes.

### Ejecutar llamadas en lote

`POST /{tenant}/target/batch`

Apilar varias llamadas de API y ejecutarlas en un solo lote.

El agrupamiento permite pasar instrucciones para varias operaciones en una única solicitud HTTP. También puede especificar dependencias entre operaciones relacionadas (descritas en una sección a continuación). TNT procesará cada una de sus operaciones independientes (posiblemente en paralelo) y procesará sus operaciones dependientes secuencialmente. Una vez completadas todas las operaciones, se devolverá una respuesta consolidada y se cerrará la conexión HTTP.

La API por lotes admite una matriz de solicitudes HTTP lógicas representadas como matrices JSON: cada solicitud tiene un método (correspondiente al método HTTP GET/PUT/POST/DELETE, etc.), relativeUrl (la parte de la URL después de admin/rest/), una matriz de encabezados opcional (correspondiente a los encabezados HTTP) y un cuerpo opcional (para las solicitudes de POST y PUT). La API por lotes devuelve una matriz de respuestas HTTP lógicas representadas como matrices JSON . Cada respuesta tiene un código de estado, una matriz de encabezados opcional y un cuerpo opcional (que es una cadena codificada en JSON). Para realizar solicitudes por lotes, cree un objeto JSON que describa cada operación individual que se va a realizar. El número máximo de operaciones permitidas es de 256 (de 0 a 255).

Especificación de dependencias entre operaciones en la solicitud De forma predeterminada, las operaciones especificadas en la solicitud de API por lotes son independientes: se pueden ejecutar en orden arbitrario en el servidor y un error en una operación no afecta a la ejecución de otras operaciones.

A menudo, las operaciones de la solicitud dependen, por ejemplo, la salida de una operación se puede utilizar en la entrada de la siguiente operación. Por ejemplo, la oferta creada en operationId=0 debe utilizarse en la creación de campañas operationId=1.

Para vincular dos operaciones por lotes, especifique en la operación dependiente el ID de la operación requerida, por ejemplo: &quot;dependsOnOperationId&quot; : 5. Además, los ID de los recursos creados mediante solicitudes de POST de operaciones por lotes se pueden utilizar en operaciones dependientes tanto en &quot;relativeUrl&quot; como en &quot;body&quot;.

#### Permisos y limitación

Para ejecutar acciones de API por lotes, el usuario subyacente debe tener al menos derechos de &quot;editor&quot; (para cada operación individual en caso de que se requieran derechos adicionales que el usuario, la operación individual fallará). Las estrategias de regulación habituales se aplican en acciones de API por lotes como si cada operación se hubiera realizado individualmente.

El procesamiento por lotes finaliza cuando se han completado todas las operaciones, una operación podría ser correcta (código de estado 2xx), fallida (código de estado 4xx, 5xx) o se omitirá porque una operación de dependencia ha fallado o se ha omitido.

#### Parámetros de objeto de solicitud

| Atributo | Descripción | Límites | Valor predeterminado |
| --- | --- | --- | --- |
| body | cuerpo para la operación por lotes HTTP. se ignorarán para todas las acciones excepto POST y PUT. Puede hacer referencia a ID de acciones por lotes anteriores, por ejemplo: &quot;offerId&quot;: &quot;{operationIdResponse:0}&quot;, &quot;segmentId&quot;: &quot;{operationIdResponse:1}&quot; | debe ser un JSON válido; en caso de hacer referencia a un operationIdResponse, la respuesta de operationId debe ser un ID válido y el método de esa acción debe ser un POST | objeto vacío {} |  |
| dependsOnOperationIds | Lista de ID de restricción que garantiza que la operación actual se ejecutará sólo si las operaciones especificadas se han completado correctamente. Se puede utilizar para lograr encadenar operaciones. | se permiten un máximo de 255 operaciones; solo se permiten valores únicos; debe señalar a un operationId válido en la matriz; no se permiten dependencias cíclicas |  |  |
| encabezados | matriz de encabezados clave-valor que se enviarán con una operación determinada. Si la autenticación para la API por lotes se ha realizado mediante el encabezado Autorización, también se copiará para operaciones individuales. | el número máximo de encabezados permitidos en la matriz es 50 | Content-Type: application/json |  |
| headers->name | nombre del encabezado | debe ser único entre otros nombres de encabezado. rfc no distingue entre mayúsculas y minúsculas en los encabezados; de lo contrario, los valores se anularán entre sí. |  |  |
| headers->value | valor de encabezado | N/A | cadena vacía |  |
| method | Método HTTP para utilizar. Opciones disponibles: GET, POST, PUT, PATCH DELETE | solo se permiten los métodos GET, POST, PUT, PATCH y DELETE |  |  |
| operationId | ID de operación utilizado para identificar una operación, entre otras operaciones, para obtener respuestas y resultados de referencia. | único entre otras operaciones; valores entre 0 y 255 |  |  |
| operaciones | lista de operaciones para realizar en un lote. El orden no es relevante. | se permiten un máximo de 256 operaciones |  |  |
| relativeUrl | URL relativa para la API de rest de administrador, la parte después de &quot;/admin/rest/&quot;. Puede contener parámetros de cadena de consulta como: &quot;/v2/campaigns?limit=10&amp;offset=10&quot;. Puede hacer referencia a direcciones URL con ID de contenedores de acciones por lotes anteriores, por ejemplo: &quot;/v1/offers/{operationIdResponse:0}&quot;. En caso de que se envíen parámetros de consulta, deben codificarse con la dirección URL. | debe comenzar por / (ser relativo); solo se admiten nuevas API de JSON válidas; en caso de una URL relativa no válida, se devolverá una respuesta 404 para una operación en particular; en caso de hacer referencia a un operationIdResponse, la respuesta de operationId referida debe ser un ID válido y el método en esa acción debe ser POST |  |  |

#### Objeto de solicitud de ejemplo

```
{
  "operations": [
    {
      "operationId": 1,
      "dependsOnOperationIds~": [0],
      "method": "POST",
      "relativeUrl": "/v1/offers",
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ],
      "body~": {
        "key": "value"
      }
    }
  ]
}
```

#### Parámetros de objeto de respuesta

| Parámetro | Descripción |
| --- | --- |
| operationId | ID de operación utilizado para identificar una operación, entre otras operaciones, el mismo ID con el que se envió en la solicitud del POST. |  |
| omitido | indicador booleano para marcar si la operación se ha ejecutado o omitido. Será verdadero en caso de que la operación actual dependa de una operación que ha fallado (devuelto un valor statusCode diferente a 2xx). |  |
| statusCode | Si se devuelven, todas las operaciones dependientes se omitirán (no se ejecutarán). |  |
| encabezados | matriz de encabezados clave-valor que se enviarán como respuesta a una operación concreta. |  |
| headers->name | nombre del encabezado |  |
| headers->value | valor de encabezado |  |
| body | cuerpo de la operación de respuesta por lotes HTTP |  |

#### Objeto de respuesta de ejemplo

```
{
  "results": [
    {
      "operationId": 1,
      "skipped~": false,
      "statusCode~": 200,
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json; charset=UTF-8"
        }
      ],
      "body~": {
        "id": 5
      }
    }
  ]
}
```
