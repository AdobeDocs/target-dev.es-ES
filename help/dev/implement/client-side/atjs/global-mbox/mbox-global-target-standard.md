---
keywords: mbox global, target classic, usar mbox global desde target classic
description: Aprenda a utilizar un mbox global heredado para sus actividades  [!DNL Adobe Target] si ya ha creado un mbox global en sus páginas para sus implementaciones heredadas.
title: ¿Puedo usar un mbox global desde una implementación heredada?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
TQID: https://experienceleague.adobe.com/BCubNDwB8gxZ9bpuCNhxcnFnjB1xQK8ZRkLveinPj4w
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 304
ht-degree: 19%

---

# Uso de un mbox global desde una implementación heredada

De manera predeterminada, [!DNL Target] crea un mbox global llamado target-global-mbox, que se usa para ejecutar las actividades creadas en [!DNL Target]. Sin embargo, si ya ha creado un mbox global en sus páginas para las implementaciones heredadas, puede utilizarlo para las actividades de [!DNL Target].

>[!NOTE]
>
>Solo se permite tener un mbox global por cuenta.

Para usar un mbox global existente tanto para [!DNL Target] como para su implementación heredada, es necesario configurar algunos parámetros.

1. Vaya a [!DNL Target] y, a continuación, haga clic en **[!UICONTROL Administración]** > **[!UICONTROL Implementación]**.

   De manera predeterminada, **[!UICONTROL la carga de página está habilitada (mbox global de creación automática]** está habilitado y el mbox global personalizado se llama `target-global-mbox`.

1. Si desea usar un mbox existente, deshabilite **[!UICONTROL Page load enabled (Auto-create global mbox]**) y especifique el nombre de un mbox global creado anteriormente en el campo **[!UICONTROL Mbox global]**.

   La lista desplegable Mbox global enumera todos los mboxes de la cuenta. Si desea utilizar un mbox que aún no existe, créelo.

1. Haga clic en **[!UICONTROL Guardar]**.

   Se actualiza la configuración de la cuenta.

1. Descargue el nuevo archivo at.js y haga referencia a él en su sitio.

   Se actualizarán todas las actividades existentes para utilizar el mbox global especificado, incluidas las actividades que haya creado e implementado hasta ese momento.

## Solución de problemas de implementación de mbox global

Se pueden usar las siguientes preguntas frecuentes para solucionar los problemas de su implementación de mbox global:

### ¿Por qué no se carga el mbox global o por qué hay latencia en la carga del mbox global cuando se carga la página?

Asegúrese de que la referencia de at.js sea la primera llamada de JavaScript en la página. Para ver otras soluciones a este problema, consulte [Preguntas más frecuentes sobre mbox global](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
