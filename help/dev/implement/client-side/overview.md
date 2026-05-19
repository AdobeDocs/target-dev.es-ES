---
keywords: implementar, implementación, at.js, sdk web de adobe experience platform, sdk web de aep
description: Obtenga información sobre cómo implementar [!DNL Adobe Target] para la web del lado del cliente mediante [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) o la biblioteca JavaScript at.js.
title: ¿Cómo implemento [!DNL Target] para la web del lado del cliente?
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
TQID: https://experienceleague.adobe.com/KgJyhvTguS8EXbwELaApI1mcs5egnEKHKpnxVYGqT4I
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
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 929e1f10bc5dd0741f0fe28cd46435e680a4a308
workflow-type: tm+mt
source-wordcount: 233
ht-degree: 28%

---

# Información general: implementar [!DNL Target] para la web del lado del cliente

En una implementación del lado del cliente de [!DNL Adobe Target], [!DNL Target] envía las experiencias asociadas a una actividad directamente al explorador del cliente. El explorador decide qué experiencia mostrar y lo hace. Con una implementación del lado del cliente, se puede utilizar un editor WYSIWYG, el [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es) (VEC) o una interfaz no visual, el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=es), para crear experiencias de actividad y personalización.

Para implementar [!DNL Target] del lado del cliente, debe usar una de las bibliotecas de JavaScript siguientes:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  [!UICONTROL Adobe Experience Platform Web SDK] le permite interactuar con los distintos servicios de [!DNL Adobe Experience Cloud] (incluido [!DNL Target]) a través de [!UICONTROL Adobe Experience Edge Network]. Si decide migrar a [!UICONTROL Adobe Experience Platform Web SDK], vea [Qué es [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md).

* [[!DNL Target] biblioteca JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

  La biblioteca JavaScript de at.js mejora los tiempos de carga de página en implementaciones web, mejora la seguridad y proporciona mejores opciones de implementación en aplicaciones de una sola página. Si decide migrar a at.js, consulte [Funcionamiento de At.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) y [[!DNL Adobe Target] Generador de habilidades: Chat del desarrollador, migre el mbox.js de Adobe Target a at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Consulte [Comparación de la biblioteca at.js con Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) para conocer las diferencias entre los dos enfoques de implementación.
