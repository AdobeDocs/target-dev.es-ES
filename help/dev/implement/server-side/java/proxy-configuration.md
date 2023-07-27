---
title: Implemente la configuración proxy en [!DNL Adobe Target] SDK de Java
description: Obtenga información sobre cómo configurar el proxy de TargetClient en la [!DNL Adobe Target] SDK de Java.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 1%

---

# Configuración de proxy (Java)

## Proxy básico

Si la aplicación que ejecuta el SDK requiere un proxy para acceder a Internet, la variable `TargetClient` deberá configurarse con una configuración proxy de la siguiente manera.

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

Si se requiere autenticación proxy, las credenciales se pueden pasar como parámetros a `ClientProxyConfig` , según el ejemplo siguiente. Tenga en cuenta que esto solo funciona para la autenticación proxy simple de nombre de usuario y contraseña.

### Autenticación proxy básica

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
