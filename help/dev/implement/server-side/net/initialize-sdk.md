---
title: Inicialice .NET SDK con el método create
description: Aprenda a utilizar el método create para inicializar el SDK de Java y crear una instancia de [!UICONTROL TargetClient] para realizar llamadas a  [!DNL Adobe Target] para experimentos y experiencias personalizadas.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 16%

---

# Inicializar .NET SDK

## Descripción

Utilice el método `Create` para inicializar .NET SDK e instanciar [!UICONTROL Target Client] para realizar llamadas a [!DNL Adobe Target] con el fin de realizar experimentos y experiencias personalizadas.

Cuando utilice la inyección de dependencia de .NET, simplemente agregue el SDK en el paso de configuración del servicio llamando a `services.AddTargetLibrary()`;, y después inserte `ITargetClient targetClient` en el constructor de la aplicación.

Después de esto, use el método `Initialize` del SDK para configurar el SDK y así completar el paso de inicialización.

## Método

`TargetClient` se creó con `TargetClient.Create`.

## C\#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig` se ha creado mediante ClientConfig.Builder.

## C\#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## Parámetros

`TargetClientConfig.Builder` tiene la siguiente estructura:

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
| --- | --- | --- | --- | --- |
| Cliente | string | Sí | Ninguna | [!UICONTROL Target Client Id] |
| OrganizationId | string | Sí | Ninguna | [!UICONTROL Experience Cloud Organization ID] |
| Tiempo de espera | int | No | 10000 | Tiempo de espera para todas las solicitudes en milisegundos |
| Proxy |  | WebProxy | No | null | Proxy para todas las [!DNL Target] solicitudes |
| RetryPolicy | Política | No | null | Directiva de reintento para todas las [!DNL Target] solicitudes |
| AsyncRetryPolicy | AsyncPolicy | No | null | Directiva de reintentos asincrónicos para todas las [!DNL Target] solicitudes |
| Logger | ILogger | No | null | Se usa para el registro de depuración de [!DNL Target] solicitudes y respuestas |
| ServerDomain | string | No | `client.tt.omtrdc.net` | Anula el nombre de host predeterminado |
| Secure | bool | No | true | No configurado para aplicar el esquema HTTP |
| DefaultPropertyToken | string | No | null | Establece el token de propiedad predeterminado para cada llamada a `getOffers` |
| TelemetryEnabled | bool | No | true | Envío de datos de telemetría para mejorar la experiencia de uso del SDK |
| DecisioningMethod | DecisioningMethod enum | No | ServerSide | Debe establecerse en OnDevice o Hybrid para habilitar la toma de decisiones en el dispositivo |
| OnDeviceDecisioningReady | Acción | No | null | Delegar para el evento Listo para la toma de decisiones en el dispositivo (llamado una vez cuando la toma de decisiones en el dispositivo está lista) |
| DescargaDeArtefactoCorrecta | Acción | No | null | Delegar para el éxito de la descarga de artefactos de toma de decisiones en el dispositivo (llamado cada vez que se descarga correctamente el artefacto) |
| ArtifactDownloadFailed | Acción | No | null | Error de descarga de artefacto de Delegado para la toma de decisiones en el dispositivo (invocado en cada descarga de artefacto fallida) |
| OnDeviceEnvironment | string | No | producción | Se puede utilizar para especificar un entorno diferente en el dispositivo, como el ensayo |
| OnDeviceConfigHostname | string | No | `assets.adobetarget.com` | Se puede utilizar para especificar un host diferente para utilizar y descargar el archivo del artefacto de toma de decisiones en el dispositivo |
| OnDeviceDecisioningPollingIntSecs | int | No | 300 (5 min.) | Número de segundos entre capturas del archivo de artefacto de toma de decisiones en el dispositivo |
| OnDeviceArtifactPayload | string | No | null | Proporciona una carga útil de artefacto local para la toma de decisiones en el dispositivo y permitir la ejecución inmediata |

## Ejemplo

## C\#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
