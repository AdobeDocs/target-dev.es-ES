---
title: Uso de getOffers() en [!DNL Adobe Target] al utilizar el SDK de Java
description: Aprenda a utilizar getOffers() para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 13%

---

# Obtener ofertas (Java)

## Descripción

`getOffers()` se utiliza para ejecutar una decisión y recuperar una experiencia de [!DNL Adobe Target].

## Método

### getOffers

El `TargetClient.getOffers` la firma del método se muestra de la siguiente manera.

**Solicitud**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

TargetDeliveryRequest se crea mediante `TargetDeliveryRequest.builder`.

**Respuesta**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## Parámetros

El `[!UICONTROL TargetDeliveryRequestBuilder]` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| el contexto | Contexto | Sí | Especifica el contexto de la solicitud |
| sessionId |  | Cadena | No | Se utiliza para vincular varios [!DNL Target] solicitudes |
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
| mcId | Cadena | No | Se utiliza para combinar y compartir datos entre diferentes [!DNL Adobe] soluciones de (ECID). Se obtuvo de targetCookies. Se genera automáticamente si no se proporciona. |
| trackingServer | Cadena | No | El servidor de Adobe Analytics para [!DNL Adobe Target] y [!DNL Adobe Analytics] para unir correctamente los datos. |
| trackingServerSecure | Cadena | No | El [!UICONTROL Servidor seguro de Adobe Analytics] para que [!DNL Adobe Target] y [!DNL Adobe Analytics] para unir correctamente los datos. |
| decisioningMethod | DecisioningMethod | No | Se puede utilizar para establecer explícitamente el método de toma de decisiones ON_DEVICE o HYBRID para la toma de decisiones en el dispositivo |

Los valores de cada campo deben ajustarse a *[!UICONTROL API de envío de vista de Target]* especificación de solicitud. Para obtener más información sobre *[!UICONTROL API de envío de vista de Target]*, consulte [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)


## Respuesta

El `TargetDeliveryResponse` devuelto por `TargetClient.getOffers(`) tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| de eventos | TargetDeliveryRequest&#x200B; | *[!DNL Target]* de eventos |
| respuesta | DeliveryResponse | *[!DNL Target]* respuesta |
| cookies |  (lista) | Lista de metadatos de sesión para este usuario. Se debe pasar en la siguiente solicitud de destino para este usuario. |
| visitorState | Mapa | El estado del visitante se establecerá en el lado del cliente para que lo utilice la API de visitante |
| responseStatus | ResponseStatus | Un objeto que representa el estado de la respuesta |

El `ResponseStatus` en la respuesta contiene los siguientes campos:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| status | int | Estado HTTP devuelto desde [!DNL Target] |
| message | Cadena | Mensaje de estado en caso de que el estado HTTP no sea 200 |
| remoteMboxes | Lista de cadenas | Se utiliza para la toma de decisiones en el dispositivo. Contiene una lista de mboxes que tienen actividades remotas que no se pueden decidir completamente en el dispositivo. |
| remoteViews | Lista de cadenas | Se utiliza para la toma de decisiones en el dispositivo. Contiene una lista de vistas que tienen actividades remotas que no se pueden decidir completamente en el dispositivo. |

El `TargetCookie` El objeto utilizado para guardar datos para la sesión de usuario tiene la siguiente estructura:

| Nombre | Tipo | Descripción |
| --- | --- | --- |
| name | Cadena | Nombre de la cookie |
| value | Cadena | Valor de la cookie, el valor se convertirá en cadena |
| maxAge | Número | La opción maxAge es una comodidad para configurar las caducidades en relación con el tiempo actual en segundos |

No tiene que preocuparse por la caducidad de las cookies. Target administra maxAge dentro del SDK.

## Ejemplo

**Solicitud**

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().setMboxes(mboxRequests))
        .build();
```

**Respuesta**

```javascript {line-numbers="true"}
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```
