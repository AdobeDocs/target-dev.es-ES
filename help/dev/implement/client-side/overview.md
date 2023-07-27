---
keywords: implementar, implementación, at.js, sdk web de adobe experience platform, sdk web de aep
description: Obtenga información sobre cómo implementar [!DNL Adobe Target] para la web del lado del cliente mediante [!DNL Adobe Experience Platform Web SDK] (SDK web de AEP) o la biblioteca JavaScript at.js.
title: ¿Cómo puedo implementar [!DNL Target] para la web del lado del cliente
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 30%

---

# Información general: implementación [!DNL Target] para la web del lado del cliente

En una implementación del lado del cliente de [!DNL Adobe Target], [!DNL Target] envía las experiencias asociadas a una actividad directamente al explorador del cliente. El explorador decide qué experiencia mostrar y lo hace. Con una implementación del lado del cliente, se puede utilizar un editor WYSIWYG, el [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) o una interfaz no visual, el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para crear experiencias de actividad y personalización.

Para implementar [!DNL Target] En el lado del cliente, debe utilizar una de las siguientes bibliotecas de JavaScript:

* [SDK web de Adobe Experience Platform](/help/dev/implement/client-side/aep-web-sdk.md)

  El [!UICONTROL SDK web de Adobe Experience Platform] le permite interactuar con los distintos servicios de [!DNL Adobe Experience Cloud] (incluido [!DNL Target]) a través de [!UICONTROL Adobe Experience Edge Network]. Si decide migrar al [!UICONTROL SDK web de Adobe Experience Platform], consulte [Qué es [!UICONTROL SDK web de Adobe Experience Platform]](/help/dev/implement/client-side/aep-web-sdk.md).

* [[!DNL Target] Biblioteca JavaScript de at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  La biblioteca JavaScript at.js mejora los tiempos de carga de página en implementaciones web, mejora la seguridad y proporciona mejores opciones de implementación en aplicaciones de una sola página. Si decide migrar a at.js, consulte [Cómo funciona at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) y [[!DNL Adobe Target] Generador de habilidades: Chat del desarrollador, migrar el mbox.js de Adobe Target a at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).
