---
title: Use [!DNL Adobe Target] con [!DNL Web SDK] para la personalización.
description: Aprenda a procesar contenido personalizado con [!DNL Experience Platform Web SDK] using [!DNL Adobe Target].
feature: AEP Web SDK
source-git-commit: 1fe6adc25604612ed9fa090f1f68c18b9c0bdf63
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 5%

---

# Usar [!DNL Adobe Target] y [!DNL Web SDK] para personalización

[!DNL Adobe Experience Platform] [!DNL Web SDK] puede entregar y procesar experiencias personalizadas administradas en [!DNL Adobe Target] al canal web. Puede usar un editor de WYSIWYG, llamado [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es) (VEC), o una interfaz no visual, [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=es), para crear, activar y entregar sus actividades y experiencias de personalización.

>[!IMPORTANT]
>
>Aprenda a migrar su implementación de [!DNL Target] a [!DNL Experience Platform Web SDK] con el tutorial [Migrar Target de at.js 2.x a Experience Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=es).
>
>Aprenda a implementar [!DNL Target] por primera vez con el tutorial [Implementar Adobe Experience Cloud con Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es). Para obtener información específica sobre [!DNL Target], consulte la sección del tutorial titulada [Configurar Target con Experience Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=es).

Las siguientes características se han probado y actualmente son compatibles con [!DNL Target]:

* [Pruebas A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=es)
* [Informes de impresión y conversión de A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es)
* [Actividades de Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=es)
* [Actividades de segmentación de experiencias](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=es)
* [Pruebas multivariable (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=es)
* [Actividades de Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=es)
* [Informes de conversión e impresión de destino nativo](https://experienceleague.adobe.com/docs/target/using/reports/reports.html?lang=es)
* [Compatibilidad con VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es)

## Diagrama del sistema [!DNL Web SDK]

El diagrama siguiente le ayuda a comprender el flujo de trabajo de [!DNL Target] y [!DNL Web SDK] Edge Decisioning.

![Diagrama de Adobe Target edge Decisioning con Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/assets/target-platform-web-sdk-new.png)

| La llamada | Detalles |
| --- | --- |
| 1 | El dispositivo carga [!DNL Web SDK]. [!DNL Web SDK] envía una solicitud a Edge Network con datos XDM, el ID de entorno de flujos de datos, los parámetros pasados y el ID de cliente (opcional). La página (o los contenedores) está oculta previamente. |
| 2 | Edge Network envía la solicitud a los servicios Edge para enriquecerla con el ID de visitante, el consentimiento y otra información de contexto del visitante, como la geolocalización y los nombres descriptivos del dispositivo. |
| 3 | Edge Network envía la solicitud de personalización enriquecida al perímetro [!DNL Target] con el ID de visitante y los parámetros proporcionados. |
| 4 | Se ejecutan los scripts de perfil y se incluyen en el almacenamiento de perfiles [!DNL Target]. El almacenamiento de perfiles recupera segmentos de [!UICONTROL Audience Library] (por ejemplo, segmentos compartidos de [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | En función de los parámetros de solicitud de URL y los datos de perfil, [!DNL Target] determina qué actividades y experiencias se mostrarán al visitante en la vista de página actual y en futuras vistas previamente recuperadas. [!DNL Target] entonces envía esto de vuelta a Edge Network. |
| 6 | a. Edge Network devuelve la respuesta de personalización a la página, incluyendo, de forma opcional, los valores de perfil para una personalización adicional. El contenido personalizado de la página actual se muestra lo más rápido posible y sin parpadeo del contenido predeterminado.<br>b. El contenido personalizado para vistas que se muestran como resultado de acciones del usuario en una aplicación de una sola página (SPA) se almacena en caché para que se pueda aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas. <br>c. Edge Network envía el ID de visitante y otros valores en las cookies, como el consentimiento, el ID de sesión, la identidad, la comprobación de cookies y la personalización. |
| 7 | Web SDK envía la notificación desde el dispositivo a Edge Network. |
| 8 | Edge Network reenvía [!UICONTROL Analytics for Target] detalles (A4T) (metadatos de actividad, experiencia y conversión) al perímetro [!DNL Analytics]. |

## Habilitando [!DNL Adobe Target]

Para habilitar [!DNL Target], haga lo siguiente:

1. Habilite [!DNL Target] en su [secuencia de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/overview) con el código de cliente apropiado.
1. Agregue la opción `renderDecisions` a los eventos.

A continuación, de forma opcional, también puede añadir las siguientes opciones:

* **`decisionScopes`**: recupere actividades específicas (útiles para las actividades creadas con el compositor basado en formularios) agregando esta opción a los eventos.
* **[Fragmento preocultado](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/personalization/manage-flicker)**: oculta solo ciertas partes de la página.

## Usar el VEC [!UICONTROL Adobe Target]

Para usar el VEC con una implementación de [!DNL Web SDK], instale y active la extensión [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o la extensión [Chrome](https://experienceleague.adobe.com/es/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension) VEC Helper.

Para obtener más información, consulte la [extensión de ayuda del Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=es) en la *guía de Adobe Target*.

## Representación de contenido personalizado

Consulte [Procesamiento de contenido personalizado](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/personalization/rendering-personalization-content) para obtener más información.

## Audiencias en XDM

Al definir audiencias para las actividades [!DNL Target] que se entregan mediante [!DNL Web SDK], se debe definir y utilizar [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es). Después de definir esquemas XDM, clases y grupos de campos de esquema, puede crear una regla de audiencia [!DNL Target] definida por datos XDM para el direccionamiento. En [!DNL Target], los datos XDM se muestran en [!UICONTROL Audience Builder] como un parámetro personalizado. El XDM se serializa usando notación de puntos (por ejemplo, `web.webPageDetails.name`).

Si tiene [!DNL Target] actividades con audiencias predefinidas que utilizan parámetros personalizados o un perfil de usuario, no se entregan correctamente a través de SDK. En lugar de utilizar parámetros personalizados o el perfil de usuario, debe utilizar XDM. Sin embargo, hay campos de segmentación de audiencia predeterminados admitidos a través de [!DNL Web SDK] que no requieren XDM. Estos campos están disponibles en la interfaz de usuario de [!DNL Target] que no requieren XDM:

* Biblioteca de segmentos
* Geografía
* Red
* Sistema operativo
* Páginas del sitio
* Explorador
* Informe de
* Periodo de tiempo

Para obtener más información, consulte [Categorías para audiencias](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=es) en la *guía de Adobe Target*.

### Tokens de respuesta

Los tokens de respuesta se utilizan para enviar metadatos a terceros, como Google o Facebook. Se devuelven tokens de respuesta
en el campo `meta` dentro de `propositions` > `items`.

Este es un ejemplo:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Para recopilar los tokens de respuesta, debe suscribirse a la promesa `alloy.sendEvent`, iterar a través de `propositions` y extraer los detalles de `items` -> `meta`.

Cada `proposition` tiene un campo booleano `renderAttempted` que indica si `proposition` se representó o no. Consulte el siguiente ejemplo:

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Cuando se habilita la representación automática, la matriz de propuestas contiene:

#### Al cargar la página:

* Basado en el compositor basado en formularios `propositions` con el indicador `renderAttempted` establecido en `false`
* Propuestas basadas en el Compositor de experiencias visuales con el indicador `renderAttempted` establecido en `true`
* Propuestas basadas en el Compositor de experiencias visuales para una vista de aplicación de una sola página con el indicador `renderAttempted` establecido en `true`

#### Al ver - cambiar (para vistas en caché):

* Propuestas basadas en el Compositor de experiencias visuales para una vista de aplicación de una sola página con el indicador `renderAttempted` establecido en `true`

Cuando la representación automática está desactivada, la matriz de propuestas contiene:

#### Al cargar la página:

* [!DNL Form-based Composer] basado en `propositions` con el marcador `renderAttempted` establecido en `false`
* Propuestas basadas en [!DNL Visual Experience Composer] con el indicador `renderAttempted` establecido en `false`
* Propuestas basadas en [!DNL Visual Experience Composer] para una vista de aplicación de una sola página con el indicador `renderAttempted` establecido en `false`

#### Al ver - cambiar (para vistas en caché):

* Propuestas basadas en el Compositor de experiencias visuales para una vista de aplicación de una sola página con el indicador `renderAttempted` establecido en `false`

### Actualización de perfil único

El [!DNL Web SDK] le permite actualizar el perfil al perfil [!DNL Target] y al [!DNL Web SDK] como un evento de experiencia.

Para actualizar un perfil [!DNL Target], asegúrese de que los datos del perfil se pasen con lo siguiente:

* En `"data {"`
* En `"__adobe.target"`
* Prefijo `"profile."`

| Clave | Tipo | Descripción |
| --- | --- | --- |
| `renderDecisions` | Booleano | Indica al componente de personalización si debe interpretar las acciones del DOM |
| `decisionScopes` | Matriz `<String>` | Una lista de ámbitos para los que recuperar decisiones |
| `xdm` | Objeto | Datos con formato XDM que aterrizan en Web SDK como un evento de experiencia |
| `data` | Objeto | Pares arbitrarios de clave/valor enviados a [!DNL Target] soluciones bajo la clase de destino. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**Retraso al guardar los parámetros de perfil o entidad hasta que se muestre el contenido al usuario final**

Para retrasar el registro de atributos en el perfil hasta que se muestre el contenido, establezca `data.adobe.target._save=false` en su solicitud.

Por ejemplo: su sitio web contiene tres ámbitos de decisión que corresponden a tres vínculos de categoría en el sitio web (hombres, mujeres y niños) y desea rastrear la categoría que visitó finalmente el usuario. Envíe estas solicitudes con el indicador `__save` establecido en `false` para evitar que se mantenga la categoría en el momento en que se solicita el contenido. Una vez visualizado el contenido, envíe la carga útil adecuada (incluidos `eventToken` y `stateToken`) para que se registren los atributos correspondientes.

El ejemplo siguiente envía un mensaje de estilo trackEvent, ejecuta scripts de perfil, guarda atributos y registra inmediatamente el evento.

```js
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": { /* Experience Event XDM data */ },
    "data": {
        "__adobe": {
            "target": {
                " __save": true|false,
                //defaults to true if omitted
                "profile.gender": "female",
                "profile.age": 30,
                "entity.name": "T-shirt",
                "entity.id": "1234"
            }
        }
    }
})
```

>[!NOTE]
>
>Si se omite la directiva `__save`, se guardan los atributos de perfil y entidad inmediatamente. La directiva `__save` solo es relevante para los atributos de perfil y los detalles de entidad.

## Solicitar recomendaciones

La tabla siguiente enumera [!DNL Recommendations] atributos y si cada uno de ellos es compatible a través de [!DNL Web SDK]:

| Categoría | Atributo | Estado de soporte |
| --- | --- | --- |
| Recommendations: atributos de entidad predeterminados | entity.id | Admitido |
|  | entity.name | Admitido |
|  | entity.categoryId | Admitido |
|  | entity.pageUrl | Admitido |
|  | entity.thumbnailUrl | Admitido |
|  | entity.message | Admitido |
|  | entity.value | Admitido |
|  | entity.inventory | Admitido |
|  | entity.brand | Admitido |
|  | entity.margin | Admitido |
|  | entity.event.detailsOnly | Admitido |
| Recommendations: atributos de entidad personalizados | entity.yourCustomAttributeName | Admitido |
| Recommendations: parámetros reservados de mbox/página | Excludedids | Admitido |
|  | cartIds | Admitido |
|  | productPurchasedId | Admitido |
| Categoría de página o elemento para la afinidad de la categoría | user.categoryId | Admitido |

**Cómo enviar atributos de Recommendations a [!DNL Target]:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Mostrar métricas de conversión de mbox {#display-mbox-conversion-metrics}

El siguiente ejemplo muestra cómo se puede realizar un seguimiento de las conversiones de mbox de visualización y enviar parámetros de perfil a [!DNL Target], sin que sea necesario calificar para ningún contenido o actividad.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "conversion-step-1" //example scope name
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    }
});
```


| Propiedad | Descripción |
|---------|----------|
| `xdm._experience.decisioning.propositions[x].scope` | El ámbito al que se asocia la métrica de éxito (que la atribuirá a una actividad específica del lado de Target). |
| `xdm._experience.decisioning.propositions[x].eventType` | Cadena que describe el tipo de evento deseado. Establezca esto en `"decisioning.propositionDisplay"` para este caso de uso. |

## Depuración

mboxTrace y mboxDebug han quedado obsoletos. En su lugar, use un método de [depuración de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/use-cases/debugging).

## Terminología  

**Propuestas**: en [!DNL Target], las propuestas se correlacionan con la experiencia seleccionada de una actividad.

**Esquema**: El esquema de una decisión es el tipo de oferta de [!DNL Target].

**Ámbito**: Ámbito de la decisión. En [!DNL Target], el ámbito es el mbox. El mbox global es el ámbito `__view__`.

**XDM**: el XDM se serializa en notación de puntos y luego se coloca en [!DNL Target] como parámetros de mbox.
