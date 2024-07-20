---
title: Implementar la configuración proxy en el SDK de Java  [!DNL Adobe Target] Java
description: Obtenga información sobre cómo configurar la configuración proxy de TargetClient en el SDK de Java  [!DNL Adobe Target] TargetClient.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: 59ab3f53e2efcbb9f7b1b2073060bbd6a173e380
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Configuración de proxy (Java)

## Proxy básico

Si la aplicación que ejecuta el SDK requiere un proxy para acceder a Internet, `TargetClient` deberá configurarse con un proxy de la siguiente manera.

### Configuración proxy básica

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Autenticación

Si se requiere autenticación proxy, las credenciales se pueden pasar como parámetros al constructor `ClientProxyConfig`, según el ejemplo siguiente. Tenga en cuenta que esto solo funciona para la autenticación proxy simple de nombre de usuario y contraseña.

### Autenticación proxy básica

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Toma de decisiones en el dispositivo

Para que las solicitudes recuperen el artefacto de reglas, el proxy debe configurarse para no almacenar la respuesta en caché. Sin embargo, si no es posible configurar el mecanismo de almacenamiento en caché del proxy para esa solicitud, utilice una opción de configuración como solución alternativa para omitir la caché de nivel proxy. Esta solución alternativa agrega el encabezado `Authorization` con un valor de cadena vacío a la solicitud de reglas, lo que debería indicar al proxy que la respuesta no se debe almacenar en caché.

Para habilitar esta solución, configure lo siguiente:

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


