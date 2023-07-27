---
title: Inicialice el SDK de Java mediante el método create
description: Aprenda a utilizar el método create para inicializar el SDK de Java e instanciar el [!UICONTROL TargetClient] para realizar llamadas a [!DNL Adobe Target] para experimentos y experiencias personalizadas.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 18%

---

# Inicialización del SDK de Java

## Descripción

Utilice el `create` para inicializar el SDK de Java y crear una instancia del [!UICONTROL Cliente de destino] para realizar llamadas a [!DNL Adobe Target] para experimentos y experiencias personalizadas.

## Método

[!UICONTROL TargetClient] se crea mediante `TargetClient.create`.

### crear

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig se crea mediante `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Parámetros

`ClientConfigBuilder` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- | --- | --- | --- | --- |
| cliente | Cadena | Sí | Ninguna | [!UICONTROL ID de cliente de Target] |
| organizationId | Cadena | Sí | Ninguna | [!UICONTROL ID de organización de Experience Cloud] |
| connectTimeout | Número | No | 10000 | Tiempo de espera de conexión para todas las solicitudes en milisegundos |
| socketTimeout | Número | No | 10000 | Tiempo de espera de socket para todas las solicitudes en milisegundos |
| maxConnectionsPerHost | Número | No | 100 | Máximo de conexiones por [!DNL Target] host |
| maxConnectionsTotal | Número | No | 200 | Conexiones máximas, incluidas todas [!DNL Target] hosts |
| enableRetries | Booleano | No | true | Reintentos automáticos para tiempos de espera de socket (máximo 4) |
| logRequests | Booleano | No | false | Registro [!DNL Target] solicitudes y respuestas en depuración |
| logRequestStatus | Booleano | No | false | Registro [!DNL Target] tiempo de respuesta, estado y dirección URL |
| serverDomain | Cadena | No | `*client*.tt.omtrdc.net` | Anula el nombre de host predeterminado |
| secure | Booleano | No | true | No configurado para aplicar el esquema HTTP |
| requestInterceptor | HttpRequestInterceptor | No | Nulo | Añadir interceptor de solicitud personalizada |
| defaultPropertyToken | Cadena | No | Ninguna | Establece el token de propiedad predeterminado para cada `getOffers` llamada. **Para la toma de decisiones en el dispositivo**, el SDK solo descargará el artefacto que contiene las actividades calificadas para el token de propiedad establecido en `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod enum | No | SERVER_SIDE | Debe establecerse a ON_DEVICE o HYBRID para habilitar la toma de decisiones en el dispositivo |
| telemetryEnabled | Booleano | No | true | Permite a los clientes excluir la recopilación de datos adicionales durante las solicitudes a [!DNL Target] servidores |
| proxyConfig | ClientProxyConfig | No | Ninguna | Permite al cliente proporcionar sus propios detalles de proxy |
| exceptionHandler | TargetExceptionHandler | No | Ninguna | Se puede utilizar para implementar la administración de excepciones personalizada durante el procesamiento de reglas |
| httpClient | HttpClient | No | Ninguna | Permite a los usuarios reemplazar el [!DNL Target] Cliente HTTP con un cliente HTTP personalizado |
| onDeviceEnvironment | Cadena | No | producción | Se puede utilizar para especificar un entorno diferente en el dispositivo, como el ensayo |
| onDeviceConfigHostname | Cadena | No | `assets.adobetarget.com` | Se puede utilizar para especificar un host diferente para utilizar y descargar el archivo del artefacto de toma de decisiones en el dispositivo |
| onDeviceDecisioningPollingIntSecs | int | No | 300 (5 minutos) | Número de segundos entre capturas del archivo de artefacto de toma de decisiones en el dispositivo |
| onDeviceArtifactPayload | byte[] | No | Ninguna | Proporciona toma de decisiones en el dispositivo con carga útil de artefacto anterior para permitir la ejecución inmediata |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | No | Ninguna | Registra llamadas de retorno para eventos de toma de decisiones en el dispositivo |
| onDeviceAllMatchingRulesMboxes | Lista\&lt;string> | No | Ninguna | Permite a los usuarios especificar los mboxes para los que se devolverá todo el contenido de reglas coincidentes durante la toma de decisiones en el dispositivo |

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
