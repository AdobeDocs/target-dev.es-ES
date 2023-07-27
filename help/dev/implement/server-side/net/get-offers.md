---
title: Uso de getOffers() en [!DNL Adobe Target] al utilizar .NET SDK
description: Aprenda a utilizar getOffers() para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 14%

---

# Obtener ofertas (.NET)

## Descripción

`GetOffers()` se utiliza para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].

## Método

`TargetClient.GetOffers` firma del método.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest` se crea mediante `TargetDeliveryRequest.Builder`.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## Parámetros

El `TargetDeliveryRequest.Builder` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| el contexto | Contexto | Sí | Especifica el contexto de la solicitud |
| sessionId | Cadena | No | Se utiliza para vincular varios [!DNL Target] solicitudes |
| thirdPartyId | Cadena | No | El identificador de su empresa del usuario que puede enviar con cada llamada |
| cookies |  (lista) | No | Lista de cookies devueltas en [!DNL Target] solicitud del mismo usuario. |
| customerIds | Mapa | No | ID de cliente en formato compatible con VisitorId |
| ejecutar | ExecuteRequest | No | Solicitud PageLoad o mboxes para ejecutar. Se evaluará inmediatamente en el servidor |
| recuperación previa | PrefetchRequest | No | Solicitud de vistas, carga de página o mboxes para recuperación previa. Devuelve con el token de notificación que se devolverá en la conversión. |
| notificaciones |  (lista) | No | Se utiliza para enviar notificaciones sobre el contenido recuperado previamente que se ha mostrado |
| requestId | Cadena | No | El ID de solicitud que se devolverá en la respuesta. Se genera automáticamente si no está presente. |
| impressionId | Cadena | No | Si están presentes, la segunda y las solicitudes posteriores con el mismo ID no incrementarán las impresiones en las actividades/métricas. Se genera automáticamente si no está presente. |
| environmentId | Largo | No | ID de entorno de cliente válido. Si no se especifica, el host se determinará en función del host proporcionado. |
| propiedad | Propiedad | No | Especifica la at_property a través del campo de token. Se puede utilizar para controlar el ámbito del envío. |
| trazar | Seguimiento | No | Habilita el seguimiento para la API de envío. |
| qaMode | QAMode | No | Utilice este objeto para activar el modo de control de calidad en la solicitud. |
| locationHint | Cadena | No | [!DNL Target] sugerencia de ubicación del clúster perimetral. Se utiliza para dirigirse al clúster de Edge especificado para esta solicitud. |
| visitante | API | No | Se utiliza para proporcionar un objeto de API de visitante personalizado. |
| id | VisitorId | No | Objeto que contiene los identificadores del visitante. P. ej. tntId, thirdPartyId, mcId, customerIds. |
| experienceCloud | Experience Cloud | No | Especifica integraciones con Audience Manager y Analytics. Se rellena automáticamente con cookies, si no se proporciona. |
| tntId | Cadena | No | Identificador principal en [!DNL Target] para un usuario. Se obtuvo de targetCookies. Se genera automáticamente si no se proporciona. |
| mcId | Cadena | No | Se utiliza para combinar y compartir datos entre distintas soluciones de Adobe (ECID). Se obtuvo de targetCookies. Se genera automáticamente si no se proporciona. |
| trackingServer | Cadena | No | El servidor de Adobe Analytics para [!DNL Adobe Target] y [!DNL Adobe Analytics] para unir correctamente los datos. |
| trackingServerSecure | Cadena | No | El [!UICONTROL Servidor seguro de Adobe Analytics] para que [!DNL Adobe Target] y [!DNL Adobe Analytics] para unir correctamente los datos. |
| decisioningMethod | DecisioningMethod | No | Se puede utilizar para establecer explícitamente el método de toma de decisiones ON_DEVICE o HYBRID para la toma de decisiones en el dispositivo |

Los valores de cada campo deben ajustarse a [API de envío de Target](/help/dev/implement/delivery-api/overview.md) especificación de solicitud.

## Respuesta

El `TargetDeliveryResponse` devuelto por `TargetClient.GetOffers()` tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| Solicitud | TargetDeliveryRequest&#x200B; | [API de envío de Target](/help/dev/implement/delivery-api/overview.md) solicitud |
| Respuesta | DeliveryResponse&#x200B; | [API de envío de Target](/help/dev/implement/delivery-api/overview.md)* respuesta |
| Estado | HttpStatusCode | Código de estado HTTP de respuesta |
| Mensaje | string | Mensaje de estado de respuesta o mensaje de error |
| Ubicaciones | Ubicaciones | [!DNL Target] nombres de ubicación, incluidos el nombre de mbox global y mboxes/vistas para los que solo está disponible la toma de decisiones remota |
| GetCookies | Diccionario | Devuelve un diccionario de metadatos de sesión para este usuario. Esto debe pasarse el siguiente [!DNL Target] para este usuario. |
| VisitorState | IDictionary | El estado del visitante se establecerá en el lado del cliente para la inicialización de la biblioteca JavaScript de la API del visitante |

El `TargetCookie` El objeto utilizado para guardar datos para la sesión de usuario tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| Nombre | string | Nombre de la cookie |
| Valor | string | Valor de cookie |
| MaxAge | int | El `MaxAge` es una opción práctica para configurar Caduca en relación con el tiempo actual en segundos |

No tiene que preocuparse por la caducidad de las cookies. [!DNL Target] tiradores `MaxAge` dentro del SDK.

## Ejemplo

## \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
    .Build();

var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```
