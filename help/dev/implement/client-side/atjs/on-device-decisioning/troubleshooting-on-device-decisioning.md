---
keywords: implementación, biblioteca javascript, js, atjs, toma de decisiones en el dispositivo, toma de decisiones en el dispositivo, at.js, en el dispositivo, en el dispositivo, solución de problemas, solución de problemas, implementación2
description: Obtenga información sobre cómo solucionar problemas de [!UICONTROL toma de decisiones en el dispositivo] con la biblioteca at.js.
title: ¿Cómo puedo solucionar problemas de la toma de decisiones en el dispositivo con la biblioteca JavaScript at.js?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
TQID: https://experienceleague.adobe.com/Ji3jAHC0Ek7FrVnabEEMm-KCtxJLJ5rSz4uyi6sWpiE
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
source-git-commit: 235baadf4059d2c363368408012630d6619aef99
workflow-type: tm+mt
source-wordcount: 281
ht-degree: 0%

---

# Solucionar problemas de [!UICONTROL toma de decisiones en el dispositivo] para at.js

Complete los siguientes pasos para solucionar problemas de la [!UICONTROL toma de decisiones en el dispositivo] en [!UICONTROL Adobe Target] con la biblioteca JavaScript at.js:

## Paso 1: Habilitar el registro de consola para at.js

Anexar el parámetro de URL `mboxDebug=1` permite que at.js imprima mensajes en la consola del explorador.

Todos los mensajes contienen el prefijo &quot;AT:&quot; para obtener una descripción general más práctica. Para asegurarse de que un artefacto se haya cargado correctamente, el registro de la consola debe contener mensajes similares a los siguientes:

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

La siguiente ilustración muestra estos mensajes en el registro de la consola:

(Haga clic en la imagen para ampliarla a ancho completo).

![Registro de consola con mensajes de artefactos](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "Registro de consola con mensajes de artefactos"){zoomable="yes"}

## Paso 2: Compruebe la descarga del artefacto de regla en la pestaña Red del explorador

Abra la pestaña Red del explorador.

Por ejemplo, para abrir DevTools en Google Chrome:

1. Presione Control+Mayús+J (Windows) o Comando+Opción+J (Mac).
1. Vaya a la pestaña Red.
1. Filtre las llamadas por la palabra clave &quot;rules.json&quot; para asegurarse de que solo se muestre el archivo de reglas de artefactos.

   Además, puede filtrar por &quot;/delivery|rules.json/&quot; para mostrar todas las llamadas de Target y el artefacto rules.json.

   ![Ficha Red en Google Chrome](assets/rule-json.png)

## Paso 3: Verificar la descarga de artefactos de regla mediante eventos personalizados de at.js

La biblioteca at.js distribuye dos nuevos eventos personalizados para admitir [!UICONTROL la toma de decisiones en el dispositivo].

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

Puede suscribirse para escuchar estos eventos personalizados en su aplicación y actuar cuando la descarga del archivo de reglas de artefactos se realice correctamente o no.

El siguiente ejemplo muestra un ejemplo de código que escucha eventos de éxito y error de descarga de artefactos:

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```



