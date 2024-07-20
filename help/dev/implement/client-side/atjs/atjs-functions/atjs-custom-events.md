---
keywords: eventos personalizados, at.js, solicitud fallida, solicitud correcta, error de representación de contenido, representación de contenido correcta, biblioteca cargada, solicitar inicio, inicio de representación de contenido, representación de contenido sin ofertas, redireccionamiento de representación de contenido, eventos personalizados2
description: Utilice eventos personalizados para que se notifique a la biblioteca JavaScript  [!DNL Adobe Target] at.js cuando una solicitud o una oferta de mbox se realice correctamente o no se realice correctamente.
title: ¿Cómo utilizo los eventos personalizados de at.js?
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 71%

---

# Eventos personalizados de at.js

Información sobre `at.js custom events`, le avisa cuando una oferta o una solicitud de mbox se procesa correcta o incorrectamente.

Históricamente, mbox.js (ahora obsoleto) impedía que otros códigos de JavaScript que se ejecutaban en la página supieran lo que pasaba entre bastidores. Con el adelanto de at.js, tuvimos una oportunidad única de arreglar este problema.

Nuestros clientes nos han contado que les gustaría recibir notificación sobre varias situaciones, entre otras:

* Cuando una solicitud de mbox falla porque se ha superado el tiempo de espera, porque el código de estado es erróneo, por un error de análisis de JSON, etc.
* Cuando una solicitud de mbox se efectúa correctamente.
* Cuando la representación de ofertas falla porque falta un elemento mbox envolvente, porque no se encuentra el selector, etc.
* Cuando la representación se efectúa correctamente. Los cambios del DOM se han aplicado.

Los eventos predefinidos tienen una estructura que permite extraer los datos necesarios según el tipo de evento.

Para asegurarse de que los eventos se puedan usar en distintos casos, los eventos personalizados tienen un objeto de carga útil que se asigna a la propiedad de detalle del objeto del evento (que se pasa al controlador). Además, para evitar pasar cadenas como nombres de eventos, los eventos se exponen como constantes usando el espacio de nombres de `adobe.target.event`.

## Estructura

| Clave | Tipo | Descripción |
|--- |--- |--- |
| type | Cadena | Hay varios escenarios en los que le gustaría recibir notificaciones para ayudarlo a rastrear, depurar y personalizar la interacción con at.js.<p>Cada evento personalizado enumerado a continuación tiene dos formatos: una &quot;constante&quot; y un &quot;valor de cadena&quot;.<ul><li>**Constantes**: antepuesto con `adobe.target.event.`, presentado todo en mayúsculas y contiene caracteres subrayados. Para suscribirse a eventos personalizados *después* de cargas at.js pero *antes* de que se haya recibido la respuesta de mbox, use la constante.</li><li>**Valores de cadena**: en minúsculas y contiene guiones. Para suscribirse a eventos personalizados *antes* de cargas at.js, use el valor de cadena.</li></ul>**Solicitud fallida**<p>Constante: `adobe.target.event.REQUEST_FAILED`<p>Valor de cadena: `at-request-failed`<p>Descripción: Cuando una solicitud de mbox falla porque se ha superado el tiempo de espera, porque el código de estado es erróneo, por un error de análisis de JSON, etc.<p>**Solicitud satisfactoria**<p>Constante: `adobe.target.event.REQUEST_SUCCEEDED`<p>Valor de cadena: `at-request-succeeded`<p>Descripción: una solicitud de mbox ha sido satisfactoria.<p>**Error en la representación del contenido**<p>Constante: `adobe.target.event.CONTENT_RENDERING_FAILED`<p>Valor de cadena: `at-content-rendering-failed`<p>Descripción: Cuando la representación de ofertas falla porque falta un elemento mbox envolvente, porque no se encuentra el selector, etc.<p>**Representación del contenido satisfactoria**<p>Constante: `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>Valor de cadena: `at-content-rendering-succeeded`<p>Descripción: la prestación de oferta ha sido satisfactoria. Los cambios del DOM se han aplicado.<p>**Librería cargada**<p>Constante: `adobe.target.event.LIBRARY_LOADED`<p>Valor de cadena: `at-library-loaded`<p>Descripción: Este evento es ideal para realizar un seguimiento cuando at.js se ha cargado por completo. Puede usar este evento para personalizar la ejecución global de mbox. También puede usar este evento para deshabilitar el mbox global y luego escuchar este evento para lanzar el mbox global más tarde.<p>**Inicio de solicitud**<p>Constante: `adobe.target.event.REQUEST_START`<p>Valor de cadena: `at-request-start`<p>Descripción: Este evento se activa antes de que se ejecute una solicitud HTTP. Puede usar este evento para las mediciones de rendimiento usando API Resource Timing.<p>**Inicio de la representación del contenido**<p>Constante: `adobe.target.event.CONTENT_RENDERING_START`<p>Valor de cadena: `at-content-rendering-start`<p>Descripción: Este evento se activa antes de que se inicie el sondeo selector y el contenido se represente en la página. Puede usar este evento para seguir el progreso del procesamiento de contenido.<p>**Presentación de contenido sin ofertas**<p>Constante: `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>Valor de cadena: `at-content-rendering-no-offers`<p>Descripción: Este evento se lanza cuando no hay ofertas devueltas.<p>**Redireccionar la representación de contenido**<p>Constante: `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>Valor de cadena: `at-content-rendering-redirect`<p>Descripción: Este evento se activa cuando una oferta es redireccionada y [!DNL Target] se redireccionará a una dirección URL diferente. |
| mbox | Cadena | nombre de mbox |
| message | Cadena | Contiene una descripción legible por humanos, como lo que sucedió, el mensaje de error, etc. |
| seguimiento | Objeto | Contiene el `sessionId` y `deviceId`. En algunos casos, el `deviceId` podría no estar porque [!DNL Target] no lo pudo recuperar del servidor Edge. |
| type | Cadena | **Artefacto de toma de decisiones en el dispositivo correcto**<p>Constante:<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>Valor de cadena: `artifactDownloadSucceeded`<p>Descripción: se llama cuando el artefacto de toma de decisiones en el dispositivo se descarga correctamente.<p>**Error del artefacto de toma de decisiones en el dispositivo**<p>Constante: `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>Valor de cadena: `artifactDownloadFailed`<p>Descripción: se llama cuando no se pudo descargar el artefacto de toma de decisiones en el dispositivo. |

## Uso

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## Vídeo de formación: Tokens de respuesta y eventos personalizados de at.js ![Distintivo de tutorial](../../../assets/tutorial.png)

Vea el siguiente vídeo para aprender a utilizar los tokens de respuesta y los eventos personalizados de at.js con el fin de compartir información de perfil de [!DNL Target] con sistemas de terceros.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)
