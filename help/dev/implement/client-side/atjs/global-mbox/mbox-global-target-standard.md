---
keywords: mbox global, target classic, usar mbox global desde target classic
description: Aprenda a utilizar un mbox global heredado para sus actividades  [!DNL Adobe Target] si ya ha creado un mbox global en sus páginas para sus implementaciones heredadas.
title: ¿Puedo usar un mbox global desde una implementación heredada?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 20%

---

# Uso de un mbox global desde una implementación heredada

De manera predeterminada, [!DNL Target] crea un mbox global llamado target-global-mbox, que se usa para ejecutar las actividades creadas en [!DNL Target]. Sin embargo, si ya ha creado un mbox global en sus páginas para las implementaciones heredadas, puede utilizarlo para las actividades de [!DNL Target].

>[!NOTE]
>
>Solo se permite tener un mbox global por cuenta.

Para usar un mbox global existente tanto para [!DNL Target] como para su implementación heredada, es necesario configurar algunos parámetros.

1. Vaya a [!DNL Target] y luego haga clic en **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

   De manera predeterminada, **[!UICONTROL Page load enabled (Auto-create global mbox]** está habilitado y el mbox global personalizado se llama `target-global-mbox`.

1. Si desea usar un mbox existente, deshabilite **[!UICONTROL Page load enabled (Auto-create global mbox]** y especifique el nombre de un mbox global creado anteriormente en el campo **[!UICONTROL Global Mbox]**.

   La lista desplegable Mbox global enumera todos los mboxes de la cuenta. Si desea utilizar un mbox que aún no existe, créelo.

1. Haga clic en **[!UICONTROL Save]**.

   Se actualiza la configuración de la cuenta.

1. Descargue el nuevo archivo at.js y haga referencia a él en su sitio.

   Se actualizarán todas las actividades existentes para utilizar el mbox global especificado, incluidas las actividades que haya creado e implementado hasta ese momento.

## Solución de problemas de implementación de mbox global

Se pueden usar las siguientes preguntas frecuentes para solucionar los problemas de su implementación de mbox global:

### ¿Por qué no se carga el mbox global o por qué hay latencia en la carga del mbox global cuando se carga la página?

Asegúrese de que la referencia de at.js sea la primera llamada de JavaScript en la página. Para ver otras soluciones a este problema, consulte [Preguntas más frecuentes sobre mbox global](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
