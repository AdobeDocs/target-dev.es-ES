---
title: Registro del lado del cliente para datos de A4T en Experience Platform Web SDK
description: Obtenga información sobre cómo habilitar el registro en el lado del cliente para Adobe Analytics for Target (A4T) mediante Experience Platform Web SDK.
seo-title: Client-side logging for A4T data in the Experience Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;registro;sdk web;experiencia;plataforma;
feature: Implementation
source-git-commit: 4d4ca7dcffdbaee5770084bd85c3109df0d6a8d4
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Registro en el lado del cliente de datos de A4T en [!DNL Experience Platform Web SDK]

[!DNL Adobe Experience Platform Web SDK] le permite recopilar [datos de Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) en el lado del cliente de la aplicación web.

El registro en el lado del cliente significa que se devuelven datos relevantes de [!DNL Target] en el lado del cliente, lo que le permite recopilar datos y compartirlos con [!DNL Analytics]. Esta opción debería habilitarse si desea enviar manualmente datos a Analytics mediante la [API de inserción de datos](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Actualmente se está desarrollando un método para realizar esto usando [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html), que estará disponible en un futuro próximo.

Este documento describe los pasos para configurar el registro de A4T en el lado del cliente para [!DNL Platform Web SDK] y proporciona ejemplos de implementación para casos de uso comunes.

## Requisitos previos   {#prerequisites}

En este tutorial se da por hecho que está familiarizado con los conceptos y procesos fundamentales relacionados con el uso de [!DNL Platform Web SDK] con fines de personalización. Revise la siguiente documentación si necesita una introducción:

* [Configuración de Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview)
* [Enviando eventos](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)
* [Procesando contenido personalizado](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Configurar el registro del lado del cliente [!DNL Analytics] {#set-up-client-side-logging}

Las siguientes subsecciones describen cómo habilitar el registro del lado del cliente de [!DNL Analytics] para la implementación de [!DNL Platform Web SDK].

### Habilitar el registro del lado del cliente [!DNL Analytics] {#enable-analytics-client-side-logging}

Para considerar el registro del lado del cliente [!DNL Analytics] habilitado para su implementación, debe deshabilitar la configuración de [!DNL Adobe Analytics] en su [secuencia de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview).

![Configuración del flujo de datos de Analytics deshabilitada](/help/dev/implement/a4t/assets/disable-analytics-datastream.png)

### Recuperar [!DNL A4T] datos de SDK y enviarlos a [!DNL Analytics] {#a4t-to-analytics}

Para que este método de generación de informes funcione correctamente, debe enviar los datos relacionados con [!DNL A4T] recuperados del comando [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview) en la visita de [!DNL Analytics].

Cuando [!DNL Target] Edge calcula una respuesta de propuestas, comprueba si el registro del lado del cliente de [!DNL Analytics] está habilitado (por ejemplo, si [!DNL Analytics] está deshabilitado en la secuencia de datos). Si el registro del lado del cliente está habilitado, el sistema agrega un token [!DNL Analytics] a cada propuesta en la respuesta.

El flujo tiene un aspecto similar al siguiente:

![Flujo de registro del lado del cliente](/help/dev/implement/a4t/assets/analytics-client-side-logging.png)

El siguiente es un ejemplo de una respuesta `interact` cuando el registro del lado del cliente [!DNL Analytics] está habilitado. Si la propuesta es para una actividad que tiene informes de [!DNL Analytics], tendrá una propiedad `scopeDetails.characteristics.analyticsToken`.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            }
          ]
        },
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Las propuestas de [!UICONTROL Form-based Experience Composer] actividades pueden contener contenido y elementos de métricas de clic en la misma propuesta. Por lo tanto, en lugar de tener un solo token de análisis para la visualización de contenido en la propiedad `scopeDetails.characteristics.analyticsToken`, pueden tener un token de análisis de clic y visualización especificado en las propiedades `scopeDetails.characteristics.analyticsDisplayToken` y `scopeDetails.characteristics.analyticsClickToken`, según corresponda.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            },
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Todos los valores de `scopeDetails.characteristics.analyticsToken`, así como `scopeDetails.characteristics.analyticsDisplayToken` (para el contenido mostrado) y `scopeDetails.characteristics.analyticsClickToken` (para las métricas de clics) son las cargas útiles de A4T que deben recopilarse e incluirse como etiqueta `tnta` en la llamada de la API de inserción de datos [Data Insertion](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

>[!IMPORTANT]
>
>Las propiedades `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` pueden contener varios tokens, concatenados como una sola cadena delimitada por comas.
>
>En los ejemplos de implementación proporcionados en la sección siguiente, se recopilan de forma iterativa varios tokens de [!DNL Analytics]. Para concatenar una matriz de [!DNL Analytics] tokens, utilice una función similar a la siguiente:
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Ejemplos de implementación {#implementation-examples}

Las siguientes subsecciones muestran cómo implementar el registro del lado del cliente [!DNL Analytics] para casos de uso comunes.

### [!UICONTROL Form-Based Experience Composer] actividades {#form-based-composer}

Puede usar [!DNL Platform Web SDK] para controlar la ejecución de propuestas desde [actividades del Compositor de experiencias basadas en formularios de Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

Cuando solicita propuestas para un ámbito de decisión específico, la propuesta devuelta contiene el token [!DNL Analytics] correspondiente. La práctica recomendada es encadenar el comando [!DNL Experience Platform Web SDK] `sendEvent` e iterar en las propuestas devueltas para ejecutarlas mientras se recopilan los tokens de [!DNL Analytics] al mismo tiempo.

Puede almacenar en déclencheur un comando `sendEvent` para un ámbito de actividad [!UICONTROL Form-Based Experience Composer] de esta manera:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

Desde aquí, debe implementar código para ejecutar las propuestas y construir una carga útil que finalmente se enviará a [!DNL Analytics]. Este es un ejemplo de lo que `results.propositions` podría contener:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Para extraer el token [!DNL Analytics] de una propuesta con elementos de contenido, puede implementar una función similar a la siguiente:

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Una propuesta puede tener diferentes tipos de elementos, tal como indica la propiedad `schema` del elemento en cuestión. Hay cuatro esquemas de elementos de propuesta compatibles con [!UICONTROL Form-Based Experience Composer] actividades:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` y `JSON_SCHEMA` son los esquemas que reflejan el tipo de oferta, mientras que `MEASUREMENT_SCHEMA` refleja las métricas que deben adjuntarse a un elemento DOM.

[!DNL Analytics] cargas para métricas de clics deben recopilarse y enviarse a [!DNL Analytics] por separado de los elementos de contenido, en el momento en que el visitante hace clic en el contenido mostrado anteriormente.

La siguiente función de ayuda para obtener la métrica de clics de cargas útiles de A4T resulta útil en este caso:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Resumen de implementación {#implementation-summary}

En resumen, se deben ejecutar los siguientes pasos al aplicar [!UICONTROL Form-Based Experience Composer] actividades con [!DNL Experience Platform Web SDK]:

1. Envíe un evento que obtenga [!UICONTROL Form-Based Experience Composer] ofertas de actividad;
1. Aplicar los cambios de contenido a la página;
1. Enviar el evento de notificación `decisioning.propositionDisplay`;
1. Recopilar los tokens de visualización de [!DNL Analytics] de la respuesta de SDK y construir una carga útil para la visita de [!DNL Analytics];
1. Enviar la carga a [!DNL Analytics] mediante la [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Si hay métricas de clics en las propuestas enviadas, los oyentes de clics deben configurarse para que cuando se realice un clic, envíe el evento de notificación `decisioning.propositionInteract`. El controlador `onBeforeEventSend` debe configurarse para que al interceptar `decisioning.propositionInteract` eventos, se produzcan las siguientes acciones:
   1. Recopilando los tokens de clic [!DNL Analytics] de `xdm._experience.decisioning.propositions`
   1. Enviando la visita de clic [!DNL Analytics] con la carga recopilada de [!DNL Analytics] a través de [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Actividades de [!UICONTROL Visual Experience Composer] (VEC) {#visual-experience-composer-acitivties}

El [!DNL Platform Web SDK] le permite administrar ofertas creadas con [Compositor de experiencias visuales (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>Los pasos para implementar este caso de uso son muy similares a los pasos para [actividades del Compositor de experiencias basadas en formularios](#form-based-composer). Consulte la sección anterior para obtener más información.

Cuando el procesamiento automático está habilitado, puede recopilar los [!DNL Analytics] tokens de las propuestas que se ejecutaron en la página. La práctica recomendada es encadenar el comando [!DNL Experience Platform Web SDK] `sendEvent` e iterar en las propuestas devueltas para filtrar las que Web SDK ha intentado procesar.

**Ejemplo**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  
  for (var i = 0; i < results.propositions.length; i++) {
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Usar `onBeforeEventSend` para controlar las métricas de página {#using-onbeforeeventsend}

Con actividades de [!DNL Adobe Target], puede configurar diferentes métricas en la página, ya sea adjuntadas manualmente al DOM o automáticamente adjuntas al DOM (actividades creadas por VEC). Ambos tipos son una interacción retrasada del usuario final en la página web.

Para tener en cuenta esto, la práctica recomendada es recopilar [!DNL Analytics] cargas útiles mediante el vínculo `onBeforeEventSend` [!DNL Adobe Experience Platform Web SDK]. El vínculo `onBeforeEventSend` debe configurarse con el comando `configure` y se refleja en todos los eventos que se envían a través de la secuencia de datos.

A continuación se muestra un ejemplo de cómo se puede configurar `onBeforeEventSent` para almacenar en déclencheur las visitas de [!DNL Analytics]:

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Pasos siguientes {#next-steps}

En esta guía se trató el registro del lado del cliente para datos de A4T en [!DNL Platform Web SDK]. Consulte la guía sobre [registro en el lado del servidor](/help/dev/implement/a4t/server-side-a4t.md) para obtener más información sobre cómo administrar los datos de A4T en Edge Network.