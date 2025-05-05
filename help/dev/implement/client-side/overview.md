---
keywords: implementar, implementación, at.js, sdk web de adobe experience platform, sdk web de aep
description: Obtenga información sobre cómo implementar [!DNL Adobe Target] para la web del lado del cliente mediante [!DNL Adobe Experience Platform Web SDK] (SDK web de AEP) o la biblioteca JavaScript at.js.
title: ¿Cómo implemento [!DNL Target] para la web del lado del cliente?
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 2d2a593df661c7e6c6e6384af6042e8aa4575fdb
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 28%

---

# Información general: implementar [!DNL Target] para la web del lado del cliente

En una implementación del lado del cliente de [!DNL Adobe Target], [!DNL Target] envía las experiencias asociadas a una actividad directamente al explorador del cliente. El explorador decide qué experiencia mostrar y lo hace. Con una implementación del lado del cliente, se puede utilizar un editor WYSIWYG, el [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es) (VEC) o una interfaz no visual, el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=es), para crear experiencias de actividad y personalización.

Para implementar [!DNL Target] del lado del cliente, debe usar una de las bibliotecas de JavaScript siguientes:

* [SDK web de Adobe Experience Platform](/help/dev/implement/client-side/aep-web-sdk.md)

  [!UICONTROL Adobe Experience Platform Web SDK] le permite interactuar con los distintos servicios de [!DNL Adobe Experience Cloud] (incluido [!DNL Target]) a través de [!UICONTROL Adobe Experience Edge Network]. Si decide migrar a [!UICONTROL Adobe Experience Platform Web SDK], vea [Qué es [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk.md).

* [[!DNL Target] biblioteca JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  La biblioteca JavaScript de at.js mejora los tiempos de carga de página en implementaciones web, mejora la seguridad y proporciona mejores opciones de implementación en aplicaciones de una sola página. Si decide migrar a at.js, consulte [Funcionamiento de At.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) y [[!DNL Adobe Target] Generador de habilidades: Chat del desarrollador, migre el mbox.js de Adobe Target a at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Consulte [Comparación de la biblioteca at.js con el SDK web](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} para conocer las diferencias entre los dos enfoques de implementación.