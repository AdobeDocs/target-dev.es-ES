---
title: Entrega por lotes o única de la API de envío de Adobe Target
description: ¿Cómo se usa [!UICONTROL API de envío de Adobe Target] ¿Llamadas de envío únicas o por lotes?
keywords: api de envío
exl-id: 525cd1f2-616a-486c-8f49-8117615500bb
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# Entrega única o por lotes

El [!UICONTROL API de envío de Adobe Target] admite una sola llamada de envío o una llamada de envío por lotes. Se puede realizar una solicitud de servidor para el contenido de uno o varios mboxes.

Valore los costes de rendimiento al decidir realizar una sola llamada en lugar de una llamada por lotes. Si conoce todo el contenido que debe mostrarse para un usuario, la práctica recomendada es recuperar contenido para todos los mboxes con una sola llamada de envío por lotes para evitar hacer varias llamadas de envío.

## Llamada de envío única

Puede recuperar una experiencia para mostrarla al usuario de un mbox mediante el [!UICONTROL API de envío de Adobe Target]. Tenga en cuenta que si realiza una sola llamada de envío, debe iniciar otra llamada al servidor para recuperar contenido adicional para un mbox de un usuario. Esto puede resultar muy costoso con el tiempo, por lo que asegúrese de evaluar su enfoque al utilizar la llamada de API de entrega única.

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
  "id": {
    "tntId": "abcdefghijkl00023.1_1"
  },
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
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

En el ejemplo de llamada de entrega única anterior, la experiencia se recupera para mostrarla al usuario con `tntId`: `abcdefghijkl00023.1_1` para un `mbox`:`SummerOffer` en el canal web. Esta sola llamada de envío genera la siguiente respuesta:

```
{
  "status": 200,
  "requestId": "25e0cc42-3d7b-456a-8b49-af60c1fb23d9",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.1_1"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
    }
}
```

En la respuesta, observe lo siguiente `content` contiene el HTML que describe la experiencia que se mostrará al usuario en la web que corresponde al mbox Oferta de verano.

### Ejecutar carga de página

Si hay experiencias que se deben mostrar cuando se produce una carga de página en el canal Web, como la prueba A/B de las fuentes ubicadas en el pie de página o el encabezado, puede especificar `pageLoad` en el `execute` para recuperar todas las modificaciones que se deben aplicar.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "window": {
      "width": 1819,
      "height": 842
    },
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "execute": {
    "pageLoad": {}
  }
}'
```

La llamada de ejemplo anterior recupera cualquier experiencia para mostrar a un usuario cuándo se abre la página `https://target.enablementadobe.com/react/demo/#/` carga.

```
{
      "status": 200,
      "requestId": "355ebc47-edb6-481f-aeae-ae55d71afaca",
      "client": "demo",
      "id": {
          "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
      },
      "edgeHost": "mboxedge28.tt.omtrdc.net",
      "execute": {
          "pageLoad": {
              "options": [
                  {
                      "content": [
                          {
                              "type": "setHtml",
                              "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV.nav:eq(0) > DIV.container:eq(0) > DIV.nav-right:eq(0) > A.nav-item:eq(0)",
                              "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > A:nth-of-type(1)",
                              "content": "Modified Home"
                          }
                      ],
                      "type": "actions"
                  }
              ],
              "metrics": [
                  {
                      "type": "click",
                      "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV.form-group:eq(0) > BUTTON.btn:eq(0)",
                      "eventToken": "QPaLjCeI9qKCBUylkRQKBg=="
                  }
              ]
          }
      }
  }
```

En el `content` , se puede recuperar la modificación que debe aplicarse al cargar una página. En el ejemplo anterior, tenga en cuenta que es necesario nombrar un vínculo en el encabezado *Inicio modificado*.

## Llamada de envío por lotes

En lugar de realizar varias llamadas de envío con un solo mbox en cada llamada, realizar una llamada de envío con un lote de mboxes puede reducir las llamadas innecesarias al servidor. La invocación de una llamada al servidor debe minimizarse en la medida de lo posible para obtener un alto rendimiento.

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
  "id": {
    "tntId": "abcdefghijkl00023.1_1"
  },
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
        "name" : "SummerOffer",
        "index" : 1
      },
      {
        "name" : "SummerShoesOffer",
        "index" : 2
      },
      {
        "name" : "SummerDressOffer",
        "index" : 3
      }      
    ]
  }
}'
```

En el ejemplo de llamada de entrega por lotes anterior, las experiencias se recuperan para mostrarlas para el usuario con `tntId`: `abcdefghijkl00023.1_1` para varios `mbox`:`SummerOffer`, `SummerShoesOffer`, y `SummerDressOffer`. Como sabemos que necesitamos mostrar una experiencia para varios mboxes para este usuario, podemos procesar estas solicitudes por lotes y hacer una llamada al servidor en lugar de tres llamadas de envío individuales.

```
{
  "status": 200,
  "requestId": "fe15286f-effb-434f-85d8-c3db804075ce",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_120"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",

                  }
              ]
          },
          {
              "index": 2,
              "name": "SummerShoesOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>",
                      "type": "html",
                  }
              ]
          },
          {
              "index": 3,
              "name": "SummerDressOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
  }
}
```

En la respuesta anterior, puede ver que dentro de la variable `content` de cada mbox, se puede recuperar la representación del HTML de la experiencia que se mostrará al usuario para cada mbox.
