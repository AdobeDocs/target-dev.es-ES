---
title: Inicialice el SDK de Java  [!DNL Adobe Target] para registrar solicitudes
description: Obtenga información sobre cómo registrar solicitudes en el SDK de Java  [!DNL Adobe Target] Java.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 4%

---

# Registrador (Java)

## Descripción

Al [inicializar el SDK](initialize-sdk.md), existen varias opciones en el objeto `ClientConfig`, que se pueden configurar para registrar solicitudes.

| Opción | Descripción |
| --- | --- |
| `logRequests` | Registra todo el cuerpo de la solicitud, así como el cuerpo de la respuesta. |
| `logRequestStatus` | Registra la dirección URL de la solicitud, el estado junto con el tiempo de respuesta. |

[!DNL Target] El SDK de Java utiliza el registro `slf4j`. Debe proporcionar la implementación del registrador como `java.util.logging`, `logback` y `log4j`. Consulte [http://www.slf4j.org/manual.html](http://www.slf4j.org/manual.html) para obtener más información. Todos los registros se imprimirán en `debug`.

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
