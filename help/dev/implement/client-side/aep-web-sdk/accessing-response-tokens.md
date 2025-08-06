---
title: Acceso a los tokens de respuesta mediante Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo tener acceso a los tokens de respuesta con  [!DNL Adobe Experience Platform Web SDK].
keywords: personalización;target;adobe target;renderDecisions;sendEvent;decisionScopes;result.decisions,token de respuesta;
feature: AEP Web SDK
source-git-commit: f010ca54aac3c2a644a77fb2f88aff1996f6ddfe
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Acceso a tokens de respuesta

El contenido de Personalization devuelto desde [!DNL Adobe Target] incluye [tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que son detalles sobre la actividad, oferta, experiencia, perfil de usuario, información geográfica y más. Estos detalles se pueden compartir con herramientas de terceros o utilizar para la depuración. Los tokens de respuesta se pueden configurar en la interfaz de usuario [!DNL Target].

Para acceder a cualquier contenido de personalización, proporcione una función de llamada de retorno al enviar un evento. Se llama a esta devolución de llamada después de que SDK reciba una respuesta correcta del servidor. Se ha proporcionado una llamada de retorno con un objeto `result`, que podría contener una propiedad `propositions` con el contenido de personalización devuelto. A continuación se muestra un ejemplo de cómo proporcionar una función de llamada de retorno.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

En este ejemplo, `result.propositions`, si existe, es una matriz que contiene propuestas de personalización relacionadas con el evento. Consulte [Procesamiento de contenido personalizado](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content) para obtener más información sobre el contenido de `result.propositions.`

Supongamos que desea recopilar todos los nombres de las actividades de todas las propuestas que Web SDK procesó automáticamente e insertarlos en una sola matriz. A continuación, puede enviar la matriz única a un tercero. En este caso:

1. Extraer propuestas del objeto `result`.
1. Recorra en bucle cada propuesta.
1. Determine si SDK procesó la propuesta.
1. Si es así, realice un bucle en cada elemento de la propuesta.
1. Recupere el nombre de la actividad de la propiedad `meta`, que es un objeto que contiene tokens de respuesta.
1. Inserte el nombre de la actividad en una matriz.
1. Envíe los nombres de las actividades a un tercero.

El código tendría el siguiente aspecto:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
