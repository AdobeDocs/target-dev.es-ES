---
title: Inicialice el SDK de Java mediante el método create
description: Aprenda a utilizar el método create para inicializar el SDK de Java y crear una instancia de [!UICONTROL TargetClient] para realizar llamadas a  [!DNL Adobe Target] para experimentos y experiencias personalizadas.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: 1d080b5e402e5d55039bf06611b44678cc6c36de
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 17%

---

# Inicialización del SDK de Java

## Descripción

Utilice el método `create` para inicializar el SDK de Java e instanciar [!UICONTROL Target Client] para realizar llamadas a [!DNL Adobe Target] con el fin de realizar experimentos y experiencias personalizadas.

## Método

[!UICONTROL TargetClient] se creó con `TargetClient.create`.

### crear

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig se creó con `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Parámetros

`ClientConfigBuilder` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- | --- | --- | --- | --- |
| cliente | Cadena | Sí | Ninguna | [!UICONTROL Target Client Id] |
| organizationId | Cadena | Sí | Ninguna | [!UICONTROL Experience Cloud Organization ID] |
| connectTimeout | Número | No | 10000 | Tiempo de espera de conexión para todas las solicitudes en milisegundos |
| socketTimeout | Número | No | 10000 | Tiempo de espera de socket para todas las solicitudes en milisegundos |
| maxConnectionsPerHost | Número | No | 100 | Número máximo de conexiones por host [!DNL Target] |
| maxConnectionsTotal | Número | No | 200 | Máximo de conexiones, incluidos todos los hosts de [!DNL Target] |
| connectionTtlMs | Número | No | -1 | Tiempo total de vida (TTL) define la duración máxima de las conexiones persistentes en milisegundos. De forma predeterminada, las conexiones se mantendrán activas indefinidamente |
| inactiveConnectionValidationMs | Número | No | 1000 | Período de inactividad en milisegundos tras el cual se vuelven a validar las conexiones persistentes antes de volver a utilizarse |
| evictIdleConnectionsAfterSecs | Número | No | 20 | Tiempo en segundos para expulsar las conexiones inactivas del grupo de conexiones |
| enableRetries | Booleano | No | true | Reintentos automáticos para tiempos de espera de socket (máximo 4) |
| logRequests | Booleano | No | false | Registrar [!DNL Target] solicitudes y respuestas en la depuración |
| logRequestStatus | Booleano | No | false | Registrar tiempo de respuesta, estado y dirección URL de [!DNL Target] |
| serverDomain | Cadena | No | `*client*.tt.omtrdc.net` | Anula el nombre de host predeterminado |
| secure | Booleano | No | true | No configurado para aplicar el esquema HTTP |
| requestInterceptor | HttpRequestInterceptor | No | Nulo | Añadir interceptor de solicitud personalizada |
| defaultPropertyToken | Cadena | No | Ninguna | Establece el token de propiedad predeterminado para cada llamada a `getOffers`. **Para la toma de decisiones en el dispositivo**, el SDK solo descargará el artefacto que contenga las actividades calificadas para el token de propiedad establecido en `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod enum | No | SERVER_SIDE | Debe establecerse a ON_DEVICE o HYBRID para habilitar la toma de decisiones en el dispositivo |
| telemetryEnabled | Booleano | No | true | Permite que los clientes excluyan la recopilación de datos adicionales durante las solicitudes a [!DNL Target] servidores |
| proxyConfig | ClientProxyConfig | No | Ninguna | Permite al cliente proporcionar sus propios detalles de proxy |
| exceptionHandler | TargetExceptionHandler | No | Ninguna | Se puede utilizar para implementar la administración de excepciones personalizada durante el procesamiento de reglas |
| httpClient | HttpClient | No | Ninguna | Permite a los usuarios reemplazar el cliente HTTP [!DNL Target] por un cliente HTTP personalizado |
| onDeviceEnvironment | Cadena | No | producción | Se puede utilizar para especificar un entorno diferente en el dispositivo, como el ensayo |
| onDeviceConfigHostname | Cadena | No | `assets.adobetarget.com` | Se puede utilizar para especificar un host diferente para utilizar y descargar el archivo del artefacto de toma de decisiones en el dispositivo |
| onDeviceDecisioningPollingIntSecs | int | No | 300 (5 minutos) | Número de segundos entre capturas del archivo de artefacto de toma de decisiones en el dispositivo |
| onDeviceArtifactPayload | byte[] | No | Ninguna | Proporciona toma de decisiones en el dispositivo con carga útil de artefacto anterior para permitir la ejecución inmediata |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | No | Ninguna | Registra llamadas de retorno para eventos de toma de decisiones en el dispositivo |
| onDeviceAllMatchingRulesMboxes | List\&lt;String\> | No | Ninguna | Permite a los usuarios especificar los mboxes para los que se devolverá todo el contenido de reglas coincidentes durante la toma de decisiones en el dispositivo |

## Ejemplo

### Java

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient.create(clientConfig);

// make calls to Adobe Target
```
