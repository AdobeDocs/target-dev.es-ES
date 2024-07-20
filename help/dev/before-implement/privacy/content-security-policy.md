---
keywords: política de seguridad de contenido, csp, at.js, lista de direcciones permitidas, lista de permitidos, parpadeo, ocultar previamente, ocultamiento previo, ocultamiento previo, política de seguridad de contenido, iFrame, iframe
description: Obtenga información acerca de las directivas de la directiva de seguridad de contenido (CSP) que debe agregar al usar  [!DNL Adobe Target].
title: ¿Cómo administra  [!DNL Target]  las políticas de seguridad de contenido (CSP)?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 28%

---

# Directivas de la política de seguridad de contenido (CSP)

Si está usando la [Política de seguridad de contenido](https://en.wikipedia.org/wiki/Content_Security_Policy) (CSP) para su implementación de [!DNL Adobe Target], debe agregar las siguientes directivas CSP al usar [at.js 2.1 o posterior](../../implement/client-side/atjs/target-atjs-versions.md):

* `connect-src` con `*.tt.omtrdc.net` incluido en la lista de permitidos. Necesario para permitir la solicitud de red al perímetro de [!DNL Target].
* `style-src unsafe-inline`. Necesaria para el control de parpadeo y preocultación.
* `script-src unsafe-inline`. Necesario para permitir la ejecución de JavaScript que pueda formar parte de una oferta de HTML.

## Preguntas más frecuentes

Consulte las siguientes preguntas frecuentes sobre las políticas de seguridad:

### ¿Las políticas de Flash entre dominios y uso compartido de recursos de origen cruzado (CORS) presentan problemas de seguridad?

La forma recomendada de implementar la política CORS es permitir el acceso solo a orígenes de confianza que la requieran a través de una lista de dominios permitidos de confianza. Lo mismo puede decirse de la política entre dominios de Flash. A algunos clientes de [!DNL Target] les preocupa el uso de caracteres comodín para los dominios en Target. El problema es que si un usuario ha iniciado sesión en una aplicación y visita un dominio permitido por la directiva, cualquier contenido malicioso que se ejecute en ese dominio puede recuperar contenido confidencial de la aplicación y llevar a cabo acciones dentro del contexto de seguridad del usuario que ha iniciado sesión. Esta situación se conoce comúnmente como Falsificación de solicitudes entre sitios (CSRF).

Sin embargo, en una implementación de [!DNL Target], estas directivas no deben representar un problema de seguridad.

“adobe.tt.omtrdc.net” es un dominio propiedad del Adobe. [!DNL Adobe Target] es una herramienta de prueba y personalización y se espera que [!DNL Target] pueda recibir y procesar solicitudes desde cualquier lugar sin requerir ninguna autenticación. Estas solicitudes contienen pares de clave/valor que se utilizan para pruebas A/B, recomendaciones o personalización de contenido.

El Adobe no almacena información de identificación personal (PII) u otra información confidencial en [!DNL Adobe Target] servidores Edge de a los que señala &quot;adobe.tt.omtrdc.net&quot;.

Se espera que se pueda acceder a [!DNL Target] desde cualquier dominio a través de llamadas de JavaScript. La única manera de permitir este acceso es aplicando &quot;Access-Control-Allow-Origin&quot; con un comodín.

### ¿Cómo puedo permitir o evitar que mi sitio se incruste como un iFrame en dominios extranjeros?

Para permitir que [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC) incruste el sitio web en un iFrame, se debe cambiar el CSP (si está configurado) en la configuración del servidor web. Los dominios de [!DNL Adobe] deben estar en la lista blanca y configurados.

Por motivos de seguridad, es posible que desee evitar que el sitio se incruste como un iFrame en dominios externos.

En las siguientes secciones se explica cómo permitir o evitar que el VEC incruste el sitio en un iFrame.

#### Permitir que el VEC incruste el sitio en un iFrame

La solución más sencilla para permitir que el VEC incruste su sitio web en un iFrame es permitir `*.adobe.com`, que es el comodín más amplio.

Por ejemplo:

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

Como en la siguiente ilustración (haga clic para ampliar):


![CSP con el comodín más amplio](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

Es posible que solo desee permitir el servicio real [!DNL Adobe]. Este escenario se puede lograr usando `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`.

Por ejemplo:

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

Como en la siguiente ilustración (haga clic para ampliar):

![CSP con ámbito de Experience Cloud](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

El acceso más restrictivo a la cuenta de una compañía se puede lograr usando `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`, donde `<Client Code>` representa su código de cliente específico.

Por ejemplo:

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

Como en la siguiente ilustración (haga clic para ampliar):

![CSP con ámbito clientcode](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Si tiene [Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) implementado, también debe estar desbloqueado.
>
>Por ejemplo:
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Evitar que el VEC incruste el sitio en un iFrame

Para evitar que el VEC incruste el sitio en un iFrame, puede restringirlo solo a &quot;uno mismo&quot;.

Por ejemplo:

`Content-Security-Policy: frame-ancestors 'self'`

Como se muestra en la siguiente ilustración (haga clic para ampliarla):

![Error de CSP](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

Se muestra el siguiente mensaje de error:

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

