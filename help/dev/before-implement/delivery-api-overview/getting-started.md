---
title: Introducción a la API de entrega de Adobe Target
description: ¿Cómo se usa [!UICONTROL Adobe Target Delivery API]?
keywords: api de envío
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Introducción a [!UICONTROL Adobe Target Delivery API]

Una llamada de [!UICONTROL Target Delivery API] tiene este aspecto:

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

Se puede recuperar `clientCode` de la interfaz de usuario de [!DNL Target] navegando a **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

Antes de realizar una llamada de [!UICONTROL Target Delivery API], siga estos pasos para asegurarse de que una respuesta contenga la experiencia relevante para mostrar a los usuarios finales:

1. Cree una actividad [!DNL Target] (A/B, XT, AP o Recommendations) usando [Compositor basado en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=es) o [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es).
1. Utilice la API de envío para obtener una respuesta para los mboxes utilizados en la actividad [!DNL Target] creada en el paso 2.
1. Presente la experiencia al visitante.
