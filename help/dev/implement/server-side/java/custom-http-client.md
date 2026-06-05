---
title: Obtenga información sobre cómo configurar el cliente HTTP personalizado
description: Obtenga información sobre cómo configurar TargetClient mediante ClientConfig.builder().httpClient().
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
TQID: https://experienceleague.adobe.com/SwijRIrhqSG4Mlij4sBH9Kx8tRB-6Bo7eyMoUZREOW8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 108
ht-degree: 0%

---

# Configuración personalizada de cliente HTTP (Java)

Si la aplicación que ejecuta SDK requiere un cliente HTTP personalizado para habilitar características como configurar SSL o agregar encabezados predeterminados a las solicitudes, `TargetClient` deberá configurarse con `ClientConfig.builder().httpClient()`:

## Configuración básica personalizada del cliente HTTP

SDK admite actualmente clientes HTTP que implementan la interfaz `org.apache.http.client.HttpClient`.

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

Este es un ejemplo de cómo configurar SSL en `TargetClient` personalizando `HttpClient` pasado a `ClientConfig`. El siguiente fragmento de código utiliza clases del paquete `org.apache.http.conn.ssl` para la configuración SSL.

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
