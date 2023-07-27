---
keywords: mbox global, personalizar mbox global, editar at.js, at.js, implementar at.js
description: Aprenda a personalizar un mbox global para at.js en [!UICONTROL Administration]-[!UICONTROL Implementación] página en [!DNL Adobe Target].
title: ¿Cómo puedo personalizar un mbox global?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 17%

---

# Personalización de un mbox global

Información para personalizar un [!DNL Adobe Target] mbox global para at.js.

1. Haga clic en **[!UICONTROL Administración]** > **[!UICONTROL Implementación]**.

1. Deshabilitar **[!UICONTROL Carga de página habilitada (Creación automática de mbox global)]** A continuación, añada el nombre del mbox global personalizado que desea utilizar para publicar actividades desde [!DNL Target].

>[!WARNING]
>
>El cambio se guarda automáticamente al seleccionar un mbox global diferente.

Este mbox global personalizado también se usa para el rastreo de clics.

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. Implemente la biblioteca at.js en su sitio.

   Consulte [Cómo implementar at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) para obtener más información.

1. Programe la transición según su versión.

   Cuando esté listo para [!DNL Target] para empezar a usar el mbox global en todas las actividades futuras, siga este paso.

   Actualice el nombre del mbox global personalizado para que coincida con el nombre usado en el paso 2 anterior.


>[!WARNING]
>
>Todas las actividades de su cuenta se sincronizan con este mbox. Asegúrese de que el mbox global esté presente en el sitio para que las actividades de sigan funcionando. Asegúrese de editar y volver a guardar las actividades afectadas que se crearon con [!UICONTROL Compositor de experiencias visuales] (VEC) que se sincronizan con este mbox. No es necesario volver a guardar las actividades creadas en [!UICONTROL Compositor de experiencias basadas en formularios] o mediante API.
