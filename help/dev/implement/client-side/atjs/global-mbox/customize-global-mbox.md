---
keywords: mbox global, personalizar mbox global, editar at.js, at.js, implementar at.js
description: Aprenda a personalizar un mbox global para at.js en la página [!UICONTROL Administration]-[!UICONTROL Implementation] de  [!DNL Adobe Target].
title: ¿Cómo puedo personalizar un mbox global?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
TQID: https://experienceleague.adobe.com/MtbjwpKrZ-WmBnE5tBY74oJgQVB-zPLrCuFDrFshkGo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 209
ht-degree: 17%

---

# Personalización de un mbox global

Información para personalizar un mbox global de [!DNL Adobe Target] para at.js.

1. Haga clic en **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

1. Deshabilite **[!UICONTROL Page load enabled (Auto create global mbox)]** y luego agregue el nombre del mbox global personalizado que desea usar para publicar actividades de [!DNL Target].

>[!WARNING]
>
>El cambio se guarda automáticamente al seleccionar un mbox global diferente.

Este mbox global personalizado también se usa para el rastreo de clics.

![mbox-global-personalizado](../../assets/custom-global-mbox.png)

1. Implemente la biblioteca at.js en su sitio.

   Consulte [Cómo implementar at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) para obtener más información.

1. Programe la transición según su versión.

   Cuando esté listo para que [!DNL Target] empiece a usar el mbox global en todas las actividades futuras, proceda con este paso.

   Actualice el nombre del mbox global personalizado para que coincida con el nombre usado en el paso 2 anterior.


>[!WARNING]
>
>Todas las actividades de su cuenta se sincronizan con este mbox. Asegúrese de que el mbox global esté presente en el sitio para que las actividades de sigan funcionando. Asegúrese de editar y volver a guardar las actividades afectadas que se crearon con el [!UICONTROL Visual Experience Composer] (VEC) que se sincronizan con este mbox. No es necesario volver a guardar las actividades creadas en [!UICONTROL Form-Based Experience Composer] o mediante API.
