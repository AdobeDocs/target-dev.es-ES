---
title: Obtenga información sobre cómo configurar el cliente HTTP personalizado
description: Obtenga información sobre cómo configurar TargetClient mediante ClientConfig.builder().httpClient().
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Configuración personalizada de cliente HTTP (Java)

Si la aplicación que ejecuta el SDK requiere un cliente HTTP personalizado para habilitar funciones como configurar SSL o agregar encabezados predeterminados a las solicitudes, la variable `TargetClient` tendrá que configurarse con `ClientConfig.builder().httpClient()`:

## Configuración básica personalizada del cliente HTTP

Ahora mismo, el SDK admite clientes HTTP que implementan el `org.apache.http.client.HttpClient` interfaz.

### Implementación básica

```java {line-numbers="true"}
CloseableHttpClient httpClient = HttpClients.custom().build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Configuración personalizada de cliente HTTP con configuración SSL

Este es un ejemplo de cómo configurar SSL en la variable `TargetClient` al personalizar el `HttpClient` pasado a la `ClientConfig`. El siguiente fragmento de código utiliza clases del `org.apache.http.conn.ssl` para la configuración SSL.

### Implementación SSL

```java {line-numbers="true"}
SSLContext context = SSLContextBuilder.create().build();
SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(context);
CloseableHttpClient httpClient = HttpClients.custom().setSSLSocketFactory(sslSocketFactory).build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
