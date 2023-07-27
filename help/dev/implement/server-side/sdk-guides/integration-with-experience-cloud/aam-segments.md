---
title: Integración con segmentos de de Experience Cloud AAM
description: Integración con Experience Cloud, integración con Audience Manager
keywords: api de entrega, lado del servidor, lado del servidor, integración, audience manager, aam
exl-id: c21e0200-23ba-4a0b-adf4-38e03c087f00
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 4%

---

# Segmentos de AAM

[!DNL Adobe Audience Manager] Los segmentos de se pueden aprovechar mediante [!DNL Adobe Target] SDK. AAM Para aprovechar los segmentos de, se deben proporcionar los siguientes campos:

>[!NOTE]
>
>AAM Los segmentos de la lista de distribución no son compatibles con las actividades de toma de decisiones en el dispositivo.

| Nombre del campo | Requerido | Descripción |
| --- | --- | --- |
| `locationHint` | Sí | AAM Sugerencia de ubicación DCS se utiliza para determinar qué extremo de DCS de DCS de DCS se visita para recuperar el perfil. Debe ser >= 1. |
| `marketingCloudVisitorId` | Sí | ID de visitante de Marketing Cloud |
| `blob` | Sí | AAM AAM Se utiliza un blob de para enviar datos adicionales a los usuarios de la aplicación de correo electrónico No debe estar en blanco y tener un tamaño &lt;= 1024. |

El SDK rellenará automáticamente estos campos cuando realice una `getOffers` llamada al método, pero deberá asegurarse de que se proporciona una cookie de visitante válida. Para obtener esta cookie, debe implementar VisitorAPI.js en el explorador.

## Guía de implementación

### Uso de cookies

Las cookies se utilizan para establecer una correlación [!DNL Adobe Audience Manager] solicitudes con [!DNL Adobe Target] solicitudes. Estas son las cookies utilizadas en esta implementación.

| Cookie | Nombre | Descripción |
| --- | --- | --- |
| cookie de visitante | `AMCVS_XXXXXXXXXXXXXXXXXXXXXXXX%40AdobeOrg` | Esta cookie la establece `VisitorAPI.js` cuando se inicializa con `visitorState` desde el destinatario `getOffers` respuesta. |
| cookie de target | `mbox` | Su servidor web debe configurar esta cookie con el nombre y el valor de `targetCookie` desde el destinatario `getOffers` respuesta. |

### Información general sobre los pasos

Supongamos que un usuario introduce una URL en un explorador que envía una solicitud al servidor web. Al cumplir esa solicitud:

1. El servidor lee las cookies de visitante y destinatario de la solicitud.
1. El servidor realiza una llamada al `getOffers` método del [!DNL Target] SDK, donde se especifican las cookies de visitante y destino si están disponibles.
1. Si la variable `getOffers` La llamada de se ha completado, los valores de `targetCookie` y `visitorState` de la respuesta se utilizan.
   1. Se establece una cookie en la respuesta con valores tomados de `targetCookie`. Esto se realiza utilizando `Set-Cookie` encabezado de respuesta, que indica al explorador que mantenga la cookie de target.
   1. Se prepara una respuesta del HTML que inicializa `VisitorAPI.js` y pasa `visitorState` de la respuesta de destinatario.
1. La respuesta del HTML se carga en el explorador...
   1. `VisitorAPI.js` se incluye en el encabezado del documento.
   1. La API de visitante se inicializa con `visitorState` desde el `getOffers` Respuesta del SDK. Esto hará que la cookie del visitante se establezca en el explorador para que se envíe al servidor en solicitudes posteriores.

### Código de ejemplo

El siguiente ejemplo de código implementa cada uno de los pasos descritos anteriormente. Cada paso aparece en el código como un comentario en línea junto a su implementación.

#### Node.js

Este ejemplo se basa en [express, un marco web de Node.js](https://expressjs.com/).

>[!BEGINTABS]

>[!TAB server.js]

```js {line-numbers="true"}
const fs = require("fs");
const express = require("express");
const cookieParser = require("cookie-parser");
const Handlebars = require("handlebars");
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  timeout: 10000,
  logger: console,
};
const targetClient = TargetClient.create(CONFIG);
const TEMPLATE = fs.readFileSync(`${__dirname}/index.handlebars`).toString();
const handlebarsTemplate = Handlebars.compile(TEMPLATE);

Handlebars.registerHelper("toJSON", function (object) {
  return new Handlebars.SafeString(JSON.stringify(object, null, 4));
});

const app = express();
app.use(cookieParser());
app.use(express.static(__dirname + "/public"));

app.get("/", async (req, res) => {
  // The server reads the visitor and target cookies from the request.
  const visitorCookie =
    req.cookies[
      encodeURIComponent(
        TargetClient.getVisitorCookieName(CONFIG.organizationId)
      )
    ];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const address = { url: req.headers.host + req.originalUrl };

  const targetRequest = {
    execute: {
      mboxes: [
        { name: "homepage", index: 1, address },
        { name: "SummerShoesOffer", index: 2, address },
        { name: "SummerDressOffer", index: 3, address }
      ],
    },
  };

  res.set({
    "Content-Type": "text/html",
    Expires: new Date().toUTCString(),
  });

  try {
    // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
    const targetResponse = await targetClient.getOffers({
      request: targetRequest,
      visitorCookie,
      targetCookie,
    });

    // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
    // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
    res.cookie(
      targetResponse.targetCookie.name,
      targetResponse.targetCookie.value,
      { maxAge: targetResponse.targetCookie.maxAge * 1000 }
    );

    // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
    const html = handlebarsTemplate({
      organizationId: CONFIG.organizationId,
      targetResponse,
    });

    res.status(200).send(html);
  } catch (error) {
    console.error("Target:", error);
    res.status(500).send(error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB index.handlebars]

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>

  <!-- VisitorAPI.js is included in the document header. -->
  <script src="VisitorAPI.js"></script>
  <script>
    // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
    Visitor.getInstance("{{organizationId}}", {serverState: {{toJSON targetResponse.visitorState}} });
  </script>
</head>
<body>
  <h1>response</h1>
  <pre>{{toJSON targetResponse}}</pre>
</body>
</html>
```

>[!ENDTABS]

#### Java

Este ejemplo utiliza [spring, un marco web de Java](https://spring.io/).

>[!BEGINTABS]

>[!TAB ClientSampleApplication.java]

```java {line-numbers="true"}
@SpringBootApplication
public class ClientSampleApplication {

    public static void main(String[] args) {
        System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
        SpringApplication.run(ClientSampleApplication.class, args);
    }

    @Bean
    TargetClient marketingCloudClient() {
        ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .defaultDecisioningMethod(DecisioningMethod.SERVER_SIDE)
                .build();

        return TargetClient.create(clientConfig);
    }
}
```

>[!TAB TargetController.java]

```java {line-numbers="true"}
@Controller
@RequestMapping("/")
public class TargetController {

    @Autowired
    private TargetClientService targetClientService;

    @GetMapping
    public String index(Model model, HttpServletRequest request, HttpServletResponse response) {
        // The server reads the visitor and target cookies from the request.
        List<TargetCookie> targetCookies = getTargetCookies(request.getCookies());

        Address address = getAddress(request);

        List<MboxRequest> mboxRequests = new ArrayList<>();
        mboxRequests.add((MboxRequest) new MboxRequest().name("homepage").index(1).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerShoesOffer").index(2).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerDressOffer").index(3).address(address));

        TargetDeliveryResponse targetDeliveryResponse = targetClientService.getOffers(mboxRequests, targetCookies, request,
                response);

        // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
        model.addAttribute("visitorState", targetDeliveryResponse.getVisitorState());
        model.addAttribute("targetResponse", targetDeliveryResponse);
        model.addAttribute("organizationId", "1234567890@AdobeOrg");

        return "index";
    }
}
```

>[!TAB TargetClientService.java]

```java {line-numbers="true"}
@Service
public class TargetClientService {

    private final TargetClient targetJavaClient;

    public TargetClientService(TargetClient targetJavaClient) {
        this.targetJavaClient = targetJavaClient;
    }

    public TargetDeliveryResponse getOffers(List<MboxRequest> executeMboxes, List<TargetCookie> cookies, HttpServletRequest request, HttpServletResponse response) {

        Context context = getContext(request);
        ExecuteRequest executeRequest = new ExecuteRequest();
        executeRequest.setMboxes(executeMboxes);

        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .execute(executeRequest)
                .cookies(cookies)
                .build();

        // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);

        // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
        // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
        setCookies(targetResponse.getCookies(), response);
        return targetResponse;
    }
}
```

>[!TAB TargetRequestUtils.java]

```java {line-numbers="true"}
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Target Only : GetOffer</title>

    <!-- VisitorAPI.js is included in the document header. -->
    <script src="../../js/VisitorAPI.js"></script>
    <script th:inline="javascript">
        // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
        Visitor.getInstance(/*[[${organizationId}]]*/ "", {serverState: /*[[${visitorState}]]*/ {}});
    </script>
</head>
<body>
    <h1>response</h1>
    <pre>[[${targetResponse}]]</pre>
</body>
</html>
```

>[!ENDTABS]

Para obtener más información sobre TargetRequestUtils.java, consulte [Métodos de utilidad (Java)](https://experienceleague.corp.adobe.com/docs/target-dev/developer/server-side/java/utility-methods.html){target=_blank}
