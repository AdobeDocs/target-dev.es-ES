---
title: Notificar al destinatario
description: Asegúrese de que rastrea todos los eventos que necesita [!DNL Target] se envían utilizando el método trackEvent.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 6cd78f8e3cbdd97a09b0cb6ca3af55994e85f819
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# Notificar [!DNL Target]

Completar este paso garantiza que todos los eventos que deben enviarse a [!DNL Adobe Target] se envían utilizando `trackEvent` método.

Cualquier evento que deba rastrearse en [!DNL Target] puede ser un evento de conversión principal o una métrica de éxito.

>[!TIP]
>
>Haga clic en las imágenes de este tema para expandirlas a pantalla completa.

## Notificar [!DNL Target] diagrama {#diagram}

El número de paso de la siguiente ilustración corresponde a la sección siguiente.

![Diagrama de Notificar a Target](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## Fire [!DNL Adobe Target] API de seguimiento

Este paso le ayuda a asegurarse de que todos los eventos de se deben enviar a [!DNL Target] se envían utilizando `trackEvent` método.

+++Ver detalles

![Activar el diagrama API de seguimiento de Adobe Target](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram.png){width="400" zoomable="yes"}

Los atributos de conversión de pedidos se envían tal como se indica en la *Requisitos previos* más abajo. El nombre del mbox no importa, pero la conversión es usar `orderConfirmPage`.

No es necesario incluir los atributos de conversión de pedidos en esta llamada. Idealmente, estas llamadas registran métricas de éxito que pueden considerarse como eventos de miniconversión antes de los eventos de conversión principales. `CardIds` debe incluirse en las recomendaciones basadas en el carro de compras en función de `Add to Cart` evento.

**Requisitos previos**

* Reúnase con su equipo empresarial para identificar todos los eventos que pueden considerarse como métricas de conversión o de éxito. También debe identificar el evento de conversión que genera ingresos para que esos detalles se puedan enviar a [!DNL Target] junto con los datos de evento.
* Asegúrese de que los siguientes atributos estén disponibles en la capa de datos para que pueda enviarlos con el evento de conversión. El evento de conversión genera ingresos, como una compra de producto o un evento de Agregar al carro de compras.

   * `productPurchaseId`: ID de productos que se compraron como parte del pedido. Separe varios productos con comas.
   * `orderTotal`: Total del pedido de la compra.
   * `orderId`: ID de pedido de la compra.

* Si está realizando el seguimiento de un evento para agregar al carro de compras, envíe `cartIds` como parámetro. Se puede pasar una lista de ID de producto separados por comas para `cardIds`.

**Lecturas**

* [adobe.target.trackEvent(), método](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds para criterios basados en el carro de compras](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Acciones**

* Uso `adobe.target-trackEvent()` para enviar todos los datos que deben enviarse a [!DNL Target].







