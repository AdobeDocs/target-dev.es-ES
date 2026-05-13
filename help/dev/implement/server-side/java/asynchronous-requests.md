---
title: Cómo usar solicitudes asincrónicas en  [!DNL Adobe Target] Java SDK
description: Descubra cómo  [!DNL Target] Java SDK admite solicitudes asincrónicas, lo que puede reducir el tiempo de destino efectivo a cero.
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
TQID: https://experienceleague.adobe.com/Y9oTl8aU4-4HpMajdmy5KfvAwEFOpV0y9vUg7BdBRk8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 130
ht-degree: 3%

---

# Solicitudes asincrónicas (Java)

## Descripción

Una ventaja de la integración del lado del servidor es que puede aprovechar el enorme ancho de banda y recursos informáticos disponibles en el lado del servidor mediante el paralelismo. [!DNL Target] Java SDK admite solicitudes asincrónicas, lo que puede reducir el tiempo de destino efectivo a cero.

## Métodos compatibles

### Métodos

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## Ejemplo

Un controlador de aplicación `Spring` de ejemplo podría tener este aspecto:

### Controlador de muestra

```javascript {line-numbers="true"}
@RestController
public class TargetRestController {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/mboxTargetOnlyAsync")
        public TargetDeliveryResponse mboxTargetOnlyAsync(
                @RequestParam(name = "mbox", defaultValue = "server-side-mbox") String mbox,
                HttpServletRequest request, HttpServletResponse response) {
            ExecuteRequest executeRequest = new ExecuteRequest()
                    .mboxes(getMboxRequests(mbox));

            TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                    .context(getContext(request))
                    .execute(executeRequest)
                    .cookies(getTargetCookies(request.getCookies()))
                    .build();
            CompletableFuture<TargetDeliveryResponse> targetResponseAsync =
                    targetJavaClient.getOffersAsync(targetDeliveryRequest);
            targetResponseAsync.thenAccept(tr -> setCookies(tr.getCookies(), response));
            simulateIO();
            TargetDeliveryResponse targetResponse = targetResponseAsync.join();
            return targetResponse;
        }

    /**
     * Function for simulating network calls like other microservices and database calls
     */
    private void simulateIO() {
        try {
            Thread.sleep(200L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

En este ejemplo se supone que ha [inicializado SDK](initialize-sdk.md) como un bean de primavera y que tiene [métodos de utilidad](utility-methods.md) disponibles.

La solicitud [!DNL Target] se activa antes de `simulateIO` y, para el momento en que se ejecute, el resultado de destino también debe estar listo. Incluso si no lo es, usted tendrá ahorros significativos en la mayoría de los casos.
