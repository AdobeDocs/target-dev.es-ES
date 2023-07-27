---
keywords: mbox global, target classic, usar mbox global desde target classic
description: Aprenda a utilizar un mbox global heredado para su [!DNL Adobe Target] actividades si ya ha creado un mbox global en sus páginas para las implementaciones heredadas.
title: ¿Puedo usar un mbox global desde una implementación heredada?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 36%

---

# Uso de un mbox global desde una implementación heredada

De forma predeterminada, [!DNL Target] crea un mbox global llamado target-global-mbox, que se utiliza para ejecutar actividades creadas en [!DNL Target]. Sin embargo, si ya ha creado un mbox global en sus páginas para implementaciones heredadas, puede usarlo para sus actividades de [!DNL Target].

>[!NOTE]
>
>Solo se permite tener un mbox global por cuenta.

Para usar un mbox global existente tanto para [!DNL Target] como para su implementación heredada, es necesario configurar algunos parámetros.

1. Ir a [!DNL Target], luego haga clic en **[!UICONTROL Administration]** > **[!UICONTROL Implementación]**.

   De forma predeterminada, **[!UICONTROL Carga de página habilitada (mBox global de Auto-Create)]** está habilitado y el nombre del mbox global personalizado es `target-global-mbox`.

1. Si desea utilizar un mbox existente, deshabilite **[!UICONTROL Carga de página habilitada (mBox global de Auto-Create)]** y especifique el nombre de un mbox global creado anteriormente en **[!UICONTROL Mbox global]** field.

   La lista desplegable Mbox global enumera todos los mboxes de la cuenta. Si desea utilizar un mbox que aún no existe, créelo.

1. Haga clic en **[!UICONTROL Guardar]**.

   Se actualiza la configuración de de la cuenta.

1. Descargue el nuevo archivo at.js y haga referencia a él en su sitio.

   Se actualizarán todas las actividades existentes para utilizar el mbox global especificado, incluidas las actividades que haya creado e implementado hasta ese momento.

## Solución de problemas de implementación de mbox global

Se pueden usar las siguientes preguntas frecuentes para solucionar los problemas de su implementación de mbox global:

### ¿Por qué no se está cargando el mbox global, o por qué hay una latencia en la carga del mbox global cuando se carga la página?

Asegúrese de que la referencia de at.js sea la primera llamada de JavaScript en la página. Para ver otras soluciones a este problema, consulte [Preguntas más frecuentes sobre mbox global](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
