---
keywords: solución de problemas, preguntas más frecuentes, FAQ, global, mbox global
description: Lea las preguntas más frecuentes (FAQ) y las respuestas acerca de los mboxes globales de Adobe [!DNL Target] s.
title: ¿Cuáles son las preguntas más frecuentes sobre el mbox global?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
TQID: https://experienceleague.adobe.com/bxsjCqSQpp6M20StzZtMBrfxjJCKgPEPfS2OlBUP00A
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 309
ht-degree: 32%

---

# Preguntas más frecuentes sobre mbox global

Lista de las preguntas más frecuentes (FAQ) sobre los mboxes globales.

## ¿Puedo tener más de un mbox global si mi cuenta de [!DNL Target] está establecida en varios dominios?

Se admite un único mbox global en su cuenta.

Puede limitar dónde se ejecutan sus actividades añadiéndoles reglas de URL. Para obtener más información, vea [Incluir la misma experiencia en páginas similares](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html?lang=es).

También puede pasar un parámetro en la página usando [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) y, a continuación, seleccionar esos parámetros en la sección &quot;configurar URL&quot; del [!UICONTROL Visual Experience Composer] (VEC) o agregando los parámetros como &quot;refinamientos&quot; en el [!UICONTROL Form-Based Experience Composer].

## ¿Cómo paso los datos de ingresos en un mbox global de [!DNL Target]?

Para recopilar ingresos e información de pedidos en target-global-mbox, se deben enviar &quot;parámetros de mbox&quot; a [!DNL Target]. Estos parámetros son pares de nombre/valor utilizados para enviar más información a [!DNL Target]. [!DNL Target] busca automáticamente estos parámetros (nombres reservados) para rellenar los datos de ingresos.

Para `orderConfirmPage`, debe pasar `orderTotal`, `orderId` y `productPurchasedId`.

Estos parámetros deben enviarse a target-global-mbox mediante `targetPageParams()`. Para obtener más información, consulte [Transferencia de parámetros a un mbox global](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

También deseará agregar la segmentación al elemento de conversión para que [!DNL Target] solo cuente las conversiones en target-global-mbox cuando se haya visto la página de confirmación de pedido, como se muestra a continuación:

![imagen alt](assets/revenue1.png)

La sección Páginas del sitio arriba ilustrada contiene las siguientes selecciones: Página actual, URL, contiene, orderconfirm.

![imagen alt](assets/revenue2.png)

Las opciones en la imagen anterior incluyen los siguientes ajustes.

* **Qué se quiere medir con esta actividad:** ingresos
* **Vista predeterminada para informes:** ingresos por visitante (RPV)
* **¿Qué acción tomó la audiencia para indicar que se había alcanzado el objetivo?** Visualizó un mbox, target-global-mbox
