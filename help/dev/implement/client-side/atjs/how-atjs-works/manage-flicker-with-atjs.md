---
keywords: parpadeo, at.js, implementación, asincrónico, asincrónico, sincrónico, sincrónico, $8
description: Descubra cómo at.js y  [!DNL Target] evitan el parpadeo (el contenido predeterminado se muestra momentáneamente antes de ser reemplazado por el contenido de la actividad) durante la carga de la página o la aplicación.
title: ¿Cómo administra at.js el parpadeo?
feature: at.js
exl-id: 8aacf254-ec3d-4831-89bb-db7f163b3869
TQID: https://experienceleague.adobe.com/r8uyzkf1gSHmppyDHPOcn5jrH86Hedb4ArMmtigq93w
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 717
ht-degree: 57%

---

# Cómo gestiona at.js el parpadeo

Información sobre cómo la biblioteca JavaScript de at.js de [!DNL Adobe Target] evita el parpadeo mientras se carga una página o una aplicación.

El parpadeo tiene lugar cuando se muestra momentáneamente el contenido predeterminado a los visitantes antes de que lo reemplace el contenido de la actividad. El parpadeo no es deseable porque confunde a los visitantes.

## Uso de un mbox global creado automáticamente

Si habilita la función [mbox global creado automáticamente](/help/dev/implement/client-side/atjs/global-mbox/customize-global-mbox.md) al configurar at.js, éste gestiona el parpadeo cambiando al configuración de opacidad mientras la página carga. Cuando se carga at.js, cambia la configuración de opacidad del elemento `<body>` a &quot;0&quot;, lo que hace que la página sea invisible inicialmente para los visitantes. Después de recibir una respuesta de [!DNL Target] (o si se detecta un error en la solicitud [!DNL Target]), at.js restablece la opacidad a &quot;1&quot;. Esto garantiza que el visitante solo vea la página después de haberse aplicado el contenido de sus actividades.

Si habilita el ajuste al configurar at.js, at.js establece la opacidad del estilo HTML BODY en 0. Después de recibir una respuesta de [!DNL Target], at.js restablece la opacidad de HTML BODY a 1.

La opacidad establecida en 0 mantiene el contenido de la página oculto para evitar el parpadeo, pero el navegador sigue procesando la página y carga todos los activos necesarios, como CSS, imágenes, etc.

Si `opacity: 0` no funciona en su implementación, también puede administrar el parpadeo personalizando `bodyHiddenStyle` y establecerlo en `body {visibility:hidden !important}`. Puede usar `body {opacity:0 !important}` o `body {visibility:hidden !important}`, el que funcione mejor para sus circunstancias específicas.

La siguiente ilustración muestra las llamadas a Ocultar cuerpo y Mostrar cuerpo en at.js 1.*x* y at.js 2.x.

**at.js 2.x**

(Haga clic en la imagen para ampliarla a ancho completo).

![Flujo de Target: solicitud de carga de página de at.js](/help/dev/implement/client-side/assets/atjs-20-flow-page-load-request.png "Flujo de Target: solicitud de carga de página de at.js"){zoomable="yes"}

**at.js 1.*x***

(Haga clic en la imagen para ampliarla a ancho completo).

![Flujo de Target: mbox global creado automáticamente](/help/dev/implement/client-side/atjs/how-atjs-works/assets/target-flow2.png "flujo de Target: mbox global creado automáticamente"){zoomable="yes"}

Para obtener más información sobre la anulación de `bodyHiddenStyle`, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Administración del parpadeo al cargar at.js de forma asíncrona

Cargar at.js de forma asíncrona es un modo excelente de evitar el bloqueo de presentación por parte del navegador; sin embargo, esta técnica puede producir parpadeos en la página web.

Puede evitar el parpadeo utilizando un fragmento de ocultamiento previo que será visible después de que Target personalice los elementos HTML relevantes.

at.js se puede cargar de forma asíncrona, ya sea directamente incrustado en la página o a través de un administrador de etiquetas (por ejemplo, Adobe Experience Platform Launch).

Si at.js está incrustado en la página, se debe añadir el fragmento antes de cargar at.js. Si carga at.js a través de un administrador de etiquetas, que también se carga asincrónicamente, debe añadir el fragmento antes de cargar el administrador de etiquetas. Si el administrador de etiquetas se carga sincrónicamente, el script se puede incluir en el administrador de etiquetas antes que at.js.

El fragmento de código de ocultamiento previo es como sigue:

```
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

De forma predeterminada, el fragmento oculta previamente el BODY de HTML completo. En algunos casos solo se pueden ocultar previamente determinados elementos HTML y no la página completa. Se puede conseguir personalizando el parámetro de estilo. Se puede reemplazar con algo que oculte previamente únicamente regiones particulares de la página.

Imagine que tiene dos regiones identificadas por los ID container-1 y container-2; el estilo se puede reemplazar de este modo:

```
#container-1, #container-2 {opacity: 0 !important}
```

En lugar del predeterminado:

```
body {opacity: 0 !important}
```

## Administración del parpadeo en at.js 2.x para triggerView()

Al utilizar `triggerView()` para mostrar contenido dirigido en su SPA, la administración de parpadeo se proporciona fuera del cuadro. Esto significa que no es necesario agregar manualmente la lógica de ocultamiento previo. En su lugar, at.js 2.x oculta previamente la ubicación donde debe mostrarse la vista antes de aplicar el contenido objetivo.

## Administración del parpadeo con getOffer() y applyOffer()

Dado que tanto `getOffer()` como `applyOffer()` son API de bajo nivel, no hay control integrado de parpadeo. Puede transferir un selector o un elemento HTML como opción para `applyOffer()`, en este caso `applyOffer()` añade el contenido de la actividad a este elemento concreto; sin embargo, debe asegurarse de que el elemento esté oculto previamente de forma correcta antes de invocar a `getOffer()` y `applyOffer()`.

```
document.documentElement.style.opacity = "0";
 
adobe.target.getOffer({
    mbox: 'target-global-mbox',
    success: function(offer) {
        adobe.target.applyOffer({
            mbox: 'target-global-mbox',
            offer: offer
        });
 
        document.documentElement.style.opacity = "1";
    },
    error: function() {
        document.documentElement.style.opacity = "1";        
    }
});
```

## Uso de un mbox regional con mboxCreate() en at.js 1.x (no admitido en at.js 2.x)

Si utiliza una implementación de mbox regional, puede usar `mboxCreate()` con su página aprovisionada similar al siguiente código de ejemplo:

```
<div class="mboxDefault">
Some default content
</div>
<script>
mboxCreate('some-mbox');
</script>
```

Si sus páginas están aprovisionadas correctamente, at.js administra el parpadeo cambiando la propiedad “visibilidad” del CSS del elemento por la clase mboxDefault.
