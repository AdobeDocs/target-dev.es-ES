---
title: Permisos de usuario de API de envío de Adobe Target
description: Permisos de usuario de API de envío de Adobe Target
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium newtab=true" tooltip="Consulte qué se incluye en Target Premium."
keywords: api de envío
exl-id: 332f90bd-4079-4653-aa38-b35837631c94
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Permisos de usuario (Premium)

[!DNL Adobe] permite a los clientes administrar permisos para sus usuarios cuando utilizan Adobe Target. Con el fin de lograr un [!UICONTROL API de envío de Adobe Target] Llamada de, se debe pasar un token con los permisos adecuados dentro de la llamada de API. Para obtener más información sobre los permisos de usuario y cómo recuperar la visita del token [esta documentación](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
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
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
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

Una vez que tenga el token correspondiente, páselo a `property` -> `token` para cada llamada de API que se realice. Si la variable `property` -> `token` no se pasa dentro de cada llamada de API, no recibirá ninguna `content` volver de Adobe Target.

```
{
    "status": 200,
    "requestId": "07ce783d-58b9-461c-9f4c-6873aeb00c01",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage"
            }
        ]
    }
}
```

Como puede ver más arriba, sin pasar el `property` -> `token`, no recibirá ningún contenido de vuelta. Si espera contenido de su llamada de API pero no recupera nada de la respuesta, lo más probable es que se deba a que:  `property` -> `token` no se proporciona o se está pasando sin los permisos correctos.
