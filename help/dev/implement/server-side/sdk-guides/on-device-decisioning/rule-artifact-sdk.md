---
title: Descargar, almacenar y actualizar automáticamente el artefacto de regla de toma de decisiones en el dispositivo
description: Aprenda a trabajar con el artefacto de la regla de toma de decisiones en el dispositivo al inicializar el SDK  [!DNL Adobe Target] .
feature: APIs/SDKs
exl-id: be41a723-616f-4aa3-9a38-8143438bd18a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Descarga, almacenamiento y actualización automática del artefacto de regla mediante el SDK [!DNL Adobe Target]

Este método es mejor si puede inicializar el SDK de [!DNL Adobe Target] al mismo tiempo que inicializa e inicia el servidor web. El SDK [!DNL Adobe Target] descargará el artefacto de regla y lo almacenará en la memoria caché antes de que la aplicación del servidor web comience a servir solicitudes. Una vez que la aplicación web esté en funcionamiento, todas las [!DNL Adobe Target] decisiones se ejecutarán mediante el artefacto de regla en memoria. El artefacto de regla en caché se actualizará en función de `pollingInterval` que especifique durante el paso de inicialización del SDK.

## Resumen de los pasos

1. Instalación del SDK
1. Inicialización del SDK
1. Almacenar y utilizar el artefacto de regla

## 1. Instalar el SDK

>[!BEGINTABS]

>[!TAB NPM]

```javascript {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB MVN]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0</version>
</dependency>
```

>[!ENDTABS]

## 2. Inicializar el SDK

1. En primer lugar, importe el SDK. Importe al mismo archivo desde el que puede controlar el inicio del servidor.

   **Nodo.js**

   ```javascript {line-numbers="true"}
   const TargetClient = require("@adobe/target-nodejs-sdk");
   ```

   **Java**

   ```javascript {line-numbers="true"}
   import com.adobe.target.edge.client.ClientConfig;
   import com.adobe.target.edge.client.TargetClient;
   ```

1. Para configurar el SDK, utilice el método create.

   **Nodo.js**

   ```javascript {line-numbers="true"}
   const CONFIG = {
       client: "<your target client code>",
       organizationId: "your EC org id",
       decisioningMethod: "on-device",
       pollingInterval : 300000,
       events: {
           clientReady: startWebServer
       }
   };
   
   const TargetClient = TargetClient.create(CONFIG);
   
   function startWebServer() {
       //Adobe Target SDK has now downloaded the JSON Artifacts and is available in the memory.
       //You can start your web server now to serve requests now.
   }
   ```

   **Java**

   ```javascript {line-numbers="true"}
   ClientConfig config = ClientConfig.builder()
       .client("<you target client code>")
       .organizationId("<your EC org id>")
       .build();
   TargetClient targetClient = TargetClient.create(config);
   ```

1. El cliente y el id. de organización se pueden recuperar de [!DNL Adobe Target] navegando a **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**, como se muestra aquí.

   &lt;!— Insert image-client-code.png —>
   ![Página de implementación bajo Administración en Target](assets/asset-rule-artifact-3.png)

## 3. Almacenar y utilizar el artefacto de regla

No es necesario que administre el artefacto de regla usted mismo. Llamar a los métodos SDK debería ser sencillo.

>[!BEGINTABS]

>[!TAB Nodo.js]

```javascript {line-numbers="true"}
//req is the request object from the server request listener method
const targetCookie = req.cookies[TargetClient.TargetCookieName];
const request = {
    context: {
        channel: "web"
    },
    execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner"
        }],
    },
};

TargetClient.getOffers({
    request,
    targetCookie
}).then(function(response) {
    //This Target response is coming from the In-memory Target artifact.
    console.log("Target response", response);
}).catch(function(err) {
    console.error("Target:", err);
})
```

>[!TAB Java]

```java {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("homepage").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

>[!NOTE]
>
>En el ejemplo de código anterior, el objeto `TargetClient` contiene una referencia al artefacto de regla en memoria. Cuando se utiliza este objeto para invocar métodos estándar del SDK, utiliza el artefacto de regla en memoria para la toma de decisiones. Si la aplicación está estructurada de modo que necesita llamar a los métodos SDK en archivos que no sean el que inicializa y escucha las solicitudes del cliente, y si esos archivos no tienen acceso al objeto TargetClient, puede descargar la carga útil JSON y almacenarla en un archivo JSON local para consumirla en otros archivos que necesiten inicializar el SDK. Esto se explica en la siguiente sección, con respecto a [la descarga del artefacto de regla mediante una carga útil JSON](rule-artifact-json.md).

Este es un ejemplo que inicia una aplicación web después de inicializar el SDK [!DNL Adobe Target].

>[!BEGINTABS]

>[!TAB Nodo.js]

```javascript {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
    client: "<your target client code>",
    organizationId: "your EC org id",
    decisioningMethod: "on-device",
    pollingInterval : 300000,
    events: {
        clientReady: startWebServer
    }
};

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());

function saveCookie(res, cookie) {
  if (!cookie) {
    return;
  }

  res.cookie(cookie.name, cookie.value, {maxAge: cookie.maxAge * 1000});
}

const getResponseHeaders = () => ({
  "Content-Type": "text/html",
  "Expires": new Date().toUTCString()
});

function sendSuccessResponse(res, response) {
  res.set(getResponseHeaders());
  saveCookie(res, response.targetCookie);
  res.status(200).send(response);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

function startWebServer() {
    app.get('/*', async (req, res) => {
    const targetCookie = req.cookies[TargetClient.TargetCookieName];
    const request = {
        execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner" // Ensure that you have a LIVE Activity running on this location
        }]
        }};

    try {
        const response = await targetClient.getOffers({ request, targetCookie });
        sendSuccessResponse(res, response);
    } catch (error) {
        console.error("Target:", error);
        sendErrorResponse(res, error);
    }
    });

    app.listen(3000, function () {
    console.log("Listening on port 3000 and watching!");
    });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

@Controller
public class TargetController {

  private TargetClient targetClient;

  TargetController() {
    // You should instantiate TargetClient in a Bean and inject the instance into this class 
    // but we show the code here for demonstration purpose.
    ClientConfig config = ClientConfig.builder()
        .client("<you target client code>")
        .organizationId("<your EC org id>")
        .build();
    targetClient = TargetClient.create(config);
  }

  @GetMapping("/")
  public String homePage() {
    MboxRequest mbox = new MboxRequest().name("homepage").index(0);
    TargetDeliveryRequest request = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
        .build();
    TargetDeliveryResponse response = targetClient.getOffers(request);
    // ...
  }
}
```

>[!ENDTABS]
