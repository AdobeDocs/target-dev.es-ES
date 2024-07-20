---
title: Prácticas recomendadas al utilizar la toma de decisiones en el dispositivo
description: Conozca las prácticas recomendadas al usar [!UICONTROL on-device decisioning] en  [!DNL Adobe Target]
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Prácticas recomendadas

[!DNL Adobe] recomienda las siguientes prácticas recomendadas al usar [!UICONTROL on-device decisioning]:

## Prácticas recomendadas cuando el método de toma de decisiones es &quot;en el dispositivo&quot;

Cuando se utiliza &quot;en el dispositivo&quot; como método de toma de decisiones, el artefacto se descarga cuando el visitante carga la página web por primera vez. Cualquier calificación de actividad que deba producirse en la primera carga de página (sin caché) solo se produce después de que el artefacto se haya descargado completamente. Hay ciertas prácticas recomendadas que puede seguir para asegurarse de que las clasificaciones de actividad se produzcan rápidamente para un visitante nuevo anónimo.

* Desactive las actividades compatibles con el dispositivo que no estén pensadas para estar en el artefacto.
* Si tiene Target Premium, puede usar [properties/workspaces](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=es) para crear archivos de artefactos diferentes para espacios de trabajo diferentes.
* Si los archivos de artefactos se vuelven muy grandes debido a razones legítimas, puede utilizar el método de toma de decisiones &quot;híbrido&quot;. Este método le permite descargar el artefacto en paralelo y todas las llamadas a la API de Target se transfieren hasta que el artefacto se ha descargado. Lea la sección de prácticas recomendadas sobre el modo de toma de decisiones &quot;híbrido&quot; a continuación para obtener más información sobre este enfoque.
* SPA Si tiene una aplicación de una sola página (), [!DNL Adobe] recomienda cargar e inicializar at.js antes de cargar el archivo JavaScript principal de la aplicación durante la primera carga de página. Este método inicia la descarga del artefacto mucho antes, lo que proporciona una representación de la experiencia más rápida.

## Prácticas recomendadas cuando el método de toma de decisiones es &quot;híbrido&quot;

Cuando se utiliza &quot;híbrido&quot; como método de toma de decisiones, el artefacto se descarga en paralelo. Hasta que se descargue el artefacto, cualquier llamada a la API [!DNL Target] se realizará por cable aunque las &quot;ubicaciones&quot; sean compatibles con el dispositivo. Este comportamiento es el predeterminado para todas las llamadas de `getOffers()` y proporciona el mejor rendimiento en la mayoría de las situaciones. Si cambia el comportamiento predeterminado de `getOffers()` al establecer `decisioningMethod` en `on-device`, siga estas prácticas recomendadas para evitar errores y garantizar el mejor rendimiento.

* Si decide llamar a `getOffers()` con `decisioningMethod` como `on-device` cuando la página se carga por primera vez, debe hacerlo dentro del controlador de eventos at.js &quot;ARTIFACT_DOWNLOAD_SUCCEEDED&quot; para evitar errores. Si el artefacto es muy grande, cualquier &quot;ubicación&quot; que utilice este método se procesará solo después de que el artefacto se haya descargado completamente, lo que puede retrasar el procesamiento de la experiencia. [!DNL Adobe] recomienda que este método se utilice con muy poca frecuencia. Siga las prácticas recomendadas para reducir el tamaño del artefacto en la sección de prácticas recomendadas &quot;En el dispositivo&quot; anterior cuando use este método.
