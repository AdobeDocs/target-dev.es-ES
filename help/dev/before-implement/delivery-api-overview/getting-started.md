---
title: Introducción a la API de entrega de Adobe Target
description: ¿Cómo uso la [!UICONTROL API de envío de Adobe Target]?
keywords: API de envío
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/DC-YVq6VfAaqMU1utmIMw73gzp4PIJgQjaS0a8FQEO4
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 132
ht-degree: 1%

---

# Introducción a la [!UICONTROL API de envío de Adobe Target]

Una llamada a la API [!UICONTROL Target Delivery] tiene este aspecto:

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

Se puede recuperar `clientCode` de la interfaz de usuario de [!DNL Target] navegando a **[!UICONTROL Administración]** > **[!UICONTROL Implementación]**.

Antes de realizar una llamada a la API [!UICONTROL Target Delivery], siga estos pasos para asegurarse de que una respuesta contenga la experiencia relevante para mostrar a los usuarios finales:

1. Cree una actividad [!DNL Target] (A/B, XT, AP o Recommendations) con [Compositor basado en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) o [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. Utilice la API de envío para obtener una respuesta para los mboxes utilizados en la actividad [!DNL Target] creada en el paso 2.
1. Presente la experiencia al visitante.
