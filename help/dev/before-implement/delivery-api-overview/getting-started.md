---
title: Introducción a la API de entrega de Adobe Target
description: ¿Cómo se usa el [!UICONTROL API de envío de Adobe Target]?
keywords: api de envío
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Introducción a la [!UICONTROL API de envío de Adobe Target]

A [!UICONTROL API de envío de Target] la llamada tiene este aspecto:

```
curl -X POST \
  'https://`clientCode`.tt.omtrdc.net/rest/v1/delivery?client=`clientCode`&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

El `clientCode` se puede recuperar desde el [!DNL Target] IU navegando a **[!UICONTROL Administration]** > **[!UICONTROL Implementación]**.

Antes de realizar una [!UICONTROL API de envío de Target] Para realizar una llamada a, siga estos pasos para asegurarse de que una respuesta contenga la experiencia relevante para mostrar a los usuarios finales:

1. Crear un [!DNL Target] actividad (A/B, XT, AP o Recommendations) utilizando [Compositor basado en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) o el [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. Utilice la API de envío para obtener una respuesta para los mboxes utilizados en [!DNL Target] actividad creada en el paso 2.
1. Presente la experiencia al visitante.
