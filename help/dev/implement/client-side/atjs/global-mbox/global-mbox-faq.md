---
keywords: solución de problemas, preguntas más frecuentes, FAQ, global, mbox global
description: Lea las preguntas más frecuentes (FAQ) y las respuestas acerca del Adobe [!DNL Target] mboxes globales.
title: ¿Cuáles son las preguntas más frecuentes sobre el mbox global?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 63%

---

# Preguntas más frecuentes sobre mbox global

Lista de las preguntas más frecuentes (FAQ) sobre los mboxes globales.

## ¿Puedo tener más de un mbox global si mi [!DNL Target] ¿La cuenta de se ha establecido en varios dominios?

Se admite un único mbox global en su cuenta.

Puede limitar dónde se ejecutan sus actividades añadiéndoles reglas de URL. Para obtener más información, consulte [Incluir la misma experiencia en páginas similares](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

También puede transferir un parámetro en la página utilizando [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) y, a continuación, seleccionar esos parámetros en la sección “configurar URL” del [!UICONTROL Compositor de experiencias visuales][!UICONTROL  (VEC) o añadiendo los parámetros como “refinamientos” en el Compositor de experiencias basadas en formularios].

## ¿Cómo paso los datos de ingresos en un [!DNL Target] mbox global?

Para recopilar ingresos e información de pedidos en target-global-mbox, se deben enviar &quot;parámetros de mbox&quot; a [!DNL Target]. Estos parámetros son pares de nombre/valor que se utilizan para enviar más información a [!DNL Target]. [!DNL Target] busca automáticamente estos parámetros (son nombres reservados) para rellenar los datos de ingresos.

Para `orderConfirmPage`, debe transferir `orderTotal`, `orderId` y `productPurchasedId`.

Estos parámetros deben enviarse a target-global-mbox mediante `targetPageParams()`. Para obtener más información, consulte [Transferencia de parámetros a un mbox global](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

También deseará añadir la segmentación al fragmento de conversión para que [!DNL Target] solo cuenta las conversiones en target-global-mbox cuando se ha visto la página de confirmación de pedido, como se muestra a continuación:

![imagen alt](assets/revenue1.png)

La sección Páginas del sitio arriba ilustrada contiene las siguientes selecciones: Página actual, URL, contiene, orderconfirm.

![imagen alt](assets/revenue2.png)

Las opciones en la imagen anterior incluyen los siguientes ajustes.

* **Qué se quiere medir con esta actividad:** ingresos
* **Vista predeterminada para informes:** ingresos por visitante (RPV)
* **¿Qué acción realizó su audiencia para indicar que se ha alcanzado su objetivo?** Visualizó un mbox, target-global-mbox
