---
title: Notificar al destinatario
description: Asegúrese de que todos los eventos de los que  [!DNL Target] debe realizar un seguimiento se envían mediante el método trackEvent.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: efccadab-d139-4423-8613-c2743d87b3a0
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# Notificar a [!DNL Target]

Al completar este paso, se asegura de que todos los eventos que deben enviarse a [!DNL Adobe Target] se envíen mediante el método `trackEvent`.

Cualquier evento que deba rastrearse en [!DNL Target] puede ser un evento de conversión principal o una métrica de éxito.

>[!TIP]
>
>Haga clic en las imágenes de este tema para expandirlas a pantalla completa.

## Notificar al diagrama [!DNL Target] {#diagram}

El número de paso de la siguiente ilustración corresponde a la sección siguiente.

![Notificar al diagrama de Target](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1: Activar la API de seguimiento [!DNL Adobe Target]

Este paso le ayuda a asegurarse de que todos los eventos que deben enviarse a [!DNL Target] se envíen mediante el método `trackEvent`.

+++Ver detalles

![Activar el diagrama de API de seguimiento de Adobe Target](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

Envía los atributos de conversión de pedidos como se indica en la sección *Requisitos previos* a continuación. El nombre del mbox no importa, pero la conversión es usar `orderConfirmPage`.

No es necesario incluir los atributos de conversión de pedidos en esta llamada. Idealmente, estas llamadas registran métricas de éxito que pueden considerarse como eventos de miniconversión antes de los eventos de conversión principales. `CardIds` debe incluirse en las recomendaciones basadas en el carro de compras en función del evento `Add to Cart`.

**Requisitos previos**

* Reúnase con su equipo empresarial para identificar todos los eventos que pueden considerarse como métricas de conversión o de éxito. También debe identificar el evento de conversión que genera ingresos para que esos detalles se puedan enviar a [!DNL Target] junto con los datos del evento.
* Asegúrese de que los siguientes atributos estén disponibles en la capa de datos para que pueda enviarlos con el evento de conversión. El evento de conversión genera ingresos, como una compra de producto o un evento de Agregar al carro de compras.

   * `productPurchaseId`: ID de producto comprados como parte del pedido. Separe varios productos con comas.
   * `orderTotal`: total del pedido de la compra.
   * `orderId`: ID de pedido de la compra.

  La siguiente ilustración muestra una regla [para [!DNL tags] in [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/tags.html?lang=es){target=_blank} que solo debería activarse en la página [!UICONTROL Confirmation].

  ![Página de configuración de la acción](/help/dev/patterns/recs-atjs/assets/action-configuration.png){width="400" zoomable="yes"}

* Si está realizando el seguimiento de un evento para agregar al carro de compras, envíe `cartIds` como parámetro. Se puede pasar una lista de identificadores de producto separados por comas para `cardIds`.

**Lecturas**

* [adobe.target.trackEvent(), método](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds para criterios basados en el carro de compras](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=es#cart-based){target=_blank}

**Acciones**

* Utilice el método `adobe.target-trackEvent()` para enviar todos los datos que deben enviarse a [!DNL Target].
