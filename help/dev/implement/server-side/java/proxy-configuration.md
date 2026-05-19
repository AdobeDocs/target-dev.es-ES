---
title: Implementar la configuración proxy en  [!DNL Adobe Target] Java SDK
description: Aprenda a configurar la configuración proxy de TargetClient en  [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
TQID: https://experienceleague.adobe.com/Vo8KrM-3AGIvoO-E-iAQcAPqzXE24BM30LX7ji5E2Nk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 2%

---

# Configuración de proxy (Java)

## Proxy básico

Si la aplicación que ejecuta SDK requiere un proxy para acceder a Internet, `TargetClient` deberá configurarse con una configuración proxy de la siguiente manera.

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


