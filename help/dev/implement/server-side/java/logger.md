---
title: Inicialice  [!DNL Adobe Target] Java SDK para registrar solicitudes
description: Obtenga información sobre cómo registrar solicitudes en  [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
TQID: https://experienceleague.adobe.com/xvduuV6cjVJu-yIoaxCvbPE-ZttfEViuM8B7sVczAC0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 4%

---

# Registrador (Java)

## Descripción

Al [inicializar SDK](initialize-sdk.md), existen varias opciones en el objeto `ClientConfig`, que se pueden configurar para registrar solicitudes.

| Opción | Descripción |
| --- | --- |
| `logRequests` | Registra todo el cuerpo de la solicitud, así como el cuerpo de la respuesta. |
| `logRequestStatus` | Registra la dirección URL de la solicitud, el estado junto con el tiempo de respuesta. |

[!DNL Target] Java SDK usa el registro `slf4j`. Debe proporcionar la implementación del registrador como `java.util.logging`, `logback` y `log4j`. Consulte [https://www.slf4j.org/manual.html](https://www.slf4j.org/manual.html) para obtener más información. Todos los registros se imprimirán en `debug`.

## Ejemplo

Agregar la dependencia `slf4j`.

>[!BEGINTABS]

>[!TAB Gradle]

### Gradle

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

Habilite los registros de `DEBUG` en función de su implementación y marque los indicadores de registro de solicitudes.

### Depuración

```javascript {line-numbers="true"}
System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
ClientConfig config = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .logRequests(true)
        .logRequestStatus(true)
        .build();

TargetClient targetClient = TargetClient.create(config);
```

Debería ver las solicitudes, respuestas y tiempos de respuesta que se imprimen en la consola.
