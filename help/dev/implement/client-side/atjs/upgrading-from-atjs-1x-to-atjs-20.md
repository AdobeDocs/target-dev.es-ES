---
keywords: versiones de at.js, versiones de at.js, aplicación de una sola página, spa, dominio cruzado, entre dominios
description: Obtenga información sobre cómo actualizar desde [!DNL Adobe Target] de at.js 1.x a at.js 2.x. Examine los diagramas de flujo del sistema, obtenga información sobre las funciones nuevas y obsoletas, y mucho más.
title: ¿Cómo puedo actualizar de at.js versión 1.x a la versión 2.x?
feature: at.js
exl-id: fbfa5743-0fa5-44c6-89b3-fdee9b50e126
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2925'
ht-degree: 73%

---

# Actualización de at.js 1.*x* a at.js 2.*x*

La versión más reciente de at.js en [!DNL Adobe Target] proporciona conjuntos de funciones enriquecidas que equipan su empresa para ejecutar la personalización en tecnologías de próxima generación de lado del cliente. Esta nueva versión se centra en actualizar at.js para tener interacciones armoniosas con aplicaciones de una sola página (SPA).

Estos son algunos de los beneficios de utilizar at.js 2.*x* con las que no están disponibles en versiones anteriores:

* La capacidad de almacenar en caché todas las ofertas al cargar la página para reducir el número de llamadas al servidor a una sola llamada.
* Importante mejora de las experiencias de los usuarios finales en su sitio porque las ofertas se muestran inmediatamente a través de la caché sin ningún tiempo de retraso que introducen las llamadas tradicionales al servidor.
* Una sencilla línea de código y configuración de desarrollador único para permitir que sus especialistas en marketing creen y ejecuten [!UICONTROL Prueba A/B] y [!UICONTROL Segmentación de experiencias] SPA (XT) actividades a través del VEC en su.

## at.js 2.*x*  Diagramas del sistema

Los siguientes diagramas le ayudan a comprender el flujo de trabajo de at.js 2.*x* con Vistas y cómo esto mejora la integración de SPA. Para obtener una mejor introducción a los conceptos utilizados en at.js 2.*x*, consulte [Implementación de Aplicación de una sola página (SPA)](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Haga clic en la imagen para ampliarla a ancho completo).

![Flujo de Target con at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "Flujo de Target con at.js 2.x"){zoomable=&quot;yes&quot;}

| La llamada | Detalles |
| --- | --- |
| 1 | La llamada devuelve el [!UICONTROL ID de Experience Cloud] si el usuario está autenticado; otra llamada sincroniza el ID de cliente. |
| 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento.<P>at.js  también se puede cargar de manera asíncrona con una opción de fragmento de ocultamiento previo implementado en la página. |
| 3 | Se solicita una carga de página que incluye todos los parámetros configurados (MCID, SDID y el ID del cliente). |
| 4 | Se ejecutan los scripts de perfiles y se incluyen en el Almacenamiento de perfiles. El Almacenamiento solicita audiencias de la Biblioteca de audiencias que cumplan los requisitos (por ejemplo, audiencias compartidas de [!DNL Adobe Analytics], [!DNL Audience Manager], etc.).<P>Se envían los atributos del cliente al Almacenamiento de perfiles en un procesamiento de lotes. |
| 5 | Según los parámetros de la solicitud de la URL y los datos de perfil, [!DNL Target] decide qué actividades y experiencias vuelven al visitante para la página actual y las vistas futuras. |
| 6 | El contenido dirigido se devuelve a la página, incluyendo, de manera opcional, los valores de perfil para una personalización adicional.<P>El contenido dirigido se muestra en la página actual lo más rápido posible y sin parpadeo del contenido predeterminado.<P>Contenido dirigido para vistas que se muestran como resultado de acciones del usuario en una SPA almacenada en caché en el explorador, de modo que se pueda aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas `triggerView()`. |
| 7 | [!UICONTROL Se envían los datos de Analytics a los servidores de recopilación de datos.] |
| 8 | Los datos de destino coinciden con [!UICONTROL Analytics] datos a través del SDID y se procesan en el [!UICONTROL Analytics] almacenamiento de informes.<P>Por lo tanto, los datos de [!UICONTROL Analytics] se pueden visualizar tanto en [!UICONTROL Analytics] como en [!DNL Target] mediante los informes de [!UICONTROL Analytics for Target] (A4T). |

Ahora, independientemente de que se implemente `triggerView()` en la SPA, las vistas y acciones se recuperan de la caché y se muestran al usuario sin una llamada al servidor. `triggerView()` también realiza una solicitud de notificaciones al back-end [!DNL Target] para aumentar y registrar los recuentos de impresión.

(Haga clic en la imagen para ampliarla a ancho completo).

![Flujo de Target at.js 2.*x* triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Flujo de Target at.js 2.*x* triggerView"){zoomable=&quot;yes&quot;}

| La llamada | Detalles |
| --- | --- |
| 1 | En la SPA, se llama a `triggerView()` para procesar la vista y aplicar acciones para modificar los elementos visuales. |
| 2 | El contenido dirigido para la vista se lee desde la caché. |
| 3 | El contenido dirigido se muestra lo más rápido posible y sin parpadeo del contenido predeterminado. |
| 4 | La solicitud de notificación se envía al Almacenamiento de perfiles de [!DNL Target] para contar al visitante en la actividad e incrementar las métricas. |
| 5 | [!UICONTROL Los datos de Analytics se envían a los servidores de recopilación de datos.] |
| 6 | [!DNL Target]Se comparan los datos de con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics.  [!UICONTROL Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en mediante los informes de A4T.][!DNL Target] |

## Implementación de at.js 2.*x*  

Implementación de at.js 2.*x* mediante etiquetas en [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) extensión.

>[!NOTE]
>
>Implementación de at.js mediante etiquetas en [!DNL Adobe Experience Platform] es el método preferido.
>
>O
>
>Descargar manualmente at.js 2.*x* uso del [!DNL Target] IU e implementarla mediante el [método de su elección](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md).

## Funciones obsoletas de at.js

Existen varias funciones que se han quedado obsoletas en at.js 2.*x*.

>[!WARNING]
>
>Si se siguen utilizando estas funciones obsoletas en el sitio cuando se implemente at.js 2.*x*, se mostrarán advertencias de la consola. Al realizar la actualización se recomienda probar la implementación de at.js 2.*x* en un entorno de ensayo, asegurarse de avanzar por cada advertencia que se haya registrado en la consola y traducir las funciones obsoletas por aquellas nuevas introducidas en at.js 2.*x*.

Puede encontrar las funciones obsoletas y sus equivalentes a continuación. Para ver una lista completa de las funciones, consulte [Funciones de at.js](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).

>[!NOTE]
>
>at.js 2.*x*  ya no oculta automáticamente los elementos marcados `mboxDefault`. Por lo tanto, los clientes tendrán que ajustar manualmente la lógica de ocultación previa en el sitio o a través de un administrador de etiquetas.

### mboxCreate(mbox,params)

**Descripción**:

Ejecuta una solicitud y aplica la oferta al DIV más cercano con el nombre de clase `mboxDefault`.

**Ejemplo:**

```html {line-numbers="true"}
<div class="mboxDefault">
  default content to replace by offer
</div>
<script>
  mboxCreate('mboxName','param1=value1','param2=value2');
</script>
```

**at.js 2.*x* equivalente**

`getOffer()` y `applyOffer()` son una alternativa a `mboxCreate(mbox, params)`.

**Ejemplo:**

```html {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  var el = document.currentScript.previousElementSibling;
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2"
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: el,
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      el.style.visibility = "visible";
    }
  });
</script> 
```

### mboxDefine() y mboxUpdate()

**Descripción**:

Crea una asignación interna entre un elemento y un nombre de mbox, pero no ejecuta la solicitud. Se utiliza junto con `mboxUpdate()`, que ejecuta la solicitud y aplica la oferta al elemento identificado por ID de nodo en `mboxDefine()`. También se puede usar para actualizar un mbox iniciado por `mboxCreate`.

**Ejemplo:**

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"></div>
<script>
 mboxDefine('someId','mboxName','param1=value1','param2=value2');
 mboxUpdate('mboxName','param3=value3','param4=value4');
</script>
```

**at.js 2.*x* equivalente**:

Una alternativa a `mboxDefine()` y `mboxUpdate` es `getOffer()` y `applyOffer()`, con la opción de selector utilizada en `applyOffer()`. Este método permite asignar la oferta a un elemento mediante cualquier selector de CSS, no solo a uno con un ID.

**Ejemplo:**

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2",
      param3: "value3",
      param4: "value4" 
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: "#someId",
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      var el = document.getElementById("someId");
      el.style.visibility = "visible";
    }
  });
</script>
```

### adobe.target.registerExtension()

**Descripción**:

Ofrece una forma estándar de registrar una extensión determinada.

Esto ya no se admite y no debe usarse.

## Resumen de las funciones de at.js obsoletas, nuevas y admitidas en 2.*x*  

| Método | Compatible? | nueva? | Obsoleto?<P>(Se muestra el contenido predeterminado) |
| --- | --- | --- | --- |
| `getOffer()` | Sí |  |  |
| `getOffers()` |  | Sí |  |
| `applyOffer()` | Sí |  |  |
| `applyOffers()` |  | Sí |  |
| `triggerView()` |  | Sí |  |
| `trackEvent()` | Sí |  |  |
| `mboxCreate()` |  |  | Sí |
| `mboxDefine()`<P>`mboxUpdate()` |  |  | Sí |
| `targetGlobalSettings()` | Sí |  |  |
| `Data Providers` | Sí |  |  |
| `targetPageParams()` | Sí |  |  |
| `targetPageParamsAll()` | Sí |  |  |
| `registerExtension()` |  |  | Sí |
| `At.js Custom Events` | Sí |  |  |

## Limitaciones y llamadas

Tenga en cuenta las siguientes limitaciones y llamadas:

### Seguimiento de conversiones

Los clientes que utilizan `mboxCreate()` para el seguimiento de conversiones deben utilizar `trackEvent()` o `getOffer()`.

### Entrega de ofertas

Los clientes que no reemplacen `mboxCreate()` por `getOffer()` o `applyOffer()` se arriesgan a que no se entreguen las ofertas.

### Puede usarse at.js 2.*x* en algunas páginas mientras que at.js 1.*x* está en otras páginas?

Sí, el perfil del visitante se conserva en todas las páginas que utilizan distintas versiones y bibliotecas. El formato de la cookie es el mismo.

### Nuevo uso de API en at.js 2.*x*

at.js 2.*x*  usa una nueva API que llamamos API de envío. Para depurar si at.js llama a la variable [!DNL Target] Edge Server correctamente, puede filtrar la pestaña Red de las herramientas para desarrolladores del explorador a &quot;entrega&quot;, &quot;`tt.omtrdc.net`,&quot; o su código de cliente. También notará que [!DNL Target] envía una carga útil JSON en lugar de pares clave-valor.

### [!DNL Target]Mbox Global de ya no se utiliza.

En at.js 2.*x*, ya no verá &quot;`target-global-mbox`&quot; visiblemente en las llamadas de red. En su lugar, hemos sustituido el &quot;`target-global-mbox`&quot; sintaxis para &quot;`execute > pageLoad`&quot; en la carga útil JSON enviado a [!DNL Target] servidores, como se ve a continuación:

```json {line-numbers="true"}
{
  "id": {
    // ...
  },
  "context": {
    "channel": "web",
    // ...
  },
  "execute": {
    "pageLoad": {}
  }
}
```

fundamentalmente, el concepto de mbox global se introdujo para hacer saber a [!DNL Target] si se recuperarán las ofertas y el contenido durante la carga de página. Esto lo hemos hecho más explícito en la versión más reciente.

### ¿Sigue siendo relevante el nombre de mbox global en at.js?

Los clientes pueden especificar un nombre de mbox global mediante **[!UICONTROL Target]** > **[!UICONTROL Administration]** > **[!UICONTROL Implementación]** > **[!UICONTROL Editar configuración de at.js]**. Este ajuste lo utilizan los servidores [!DNL Target] Edge para traducir Ejecutar > pageLoad al nombre de mbox global que aparece en la interfaz de usuario [!DNL Target]. Esto permite a los clientes seguir utilizando API del lado del servidor, el compositor basado en formularios, los comandos de perfil y crear audiencias utilizando el nombre de mbox global. Le recomendamos encarecidamente que se asegure de que se ha configurado el mismo nombre de mbox global en la **[!UICONTROL Administration]** > **[!UICONTROL Compositor de experiencias visuales]** , en caso de que tenga páginas con at.js 1.*x*, como se muestra en las ilustraciones siguientes.

![Modificación del diálogo at.js](../assets/modify-atjs.png)

y

![mbox global personalizado](../assets/custom-global-mbox.png)

### ¿Es necesario activar la configuración de creación automática de mbox global para at.js 2.*x*?

En la mayoría de los casos, sí. Esta configuración le indica a at.js 2.*x* que active una solicitud a los servidores Edge [!DNL Target] al cargar la página. Este ajuste debería estar activado ya que mbox global se traduce para Ejecutar > pageLoad, y si desea activar una solicitud al cargar la página.

### ¿Seguirán funcionando las actividades existentes de VEC aunque el nombre de mbox global de Target no se especifique desde at.js 2.*x*?

Sí, porque Ejecutar > pageLoad se trata en el backend [!DNL Target] como `target-global-mbox`.

### Si mis actividades basadas en formularios están dirigidas a `target-global-mbox`, ¿seguirán funcionando esas actividades?

Sí, porque Ejecutar > pageLoad se trata en los servidores [!DNL Target] Edge como `target-global-mbox`.

### Configuración compatible y no compatible en at.js 2.*x*

| Configuración | Compatible? |
| --- | --- |
| Dominio x | No |
| Creación automática de mbox global | Sí |
| Nombre de mbox global | Sí |

### Compatibilidad de seguimiento entre dominios en at.js 2.x

El seguimiento entre dominios permite unir visitantes de dominios distintos. Dado que se debe crear una nueva cookie para cada dominio, es difícil rastrear a los visitantes cuando navegan de un dominio a otro. Para realizar el seguimiento entre dominios, [!DNL Target] utiliza una cookie de terceros para rastrear visitantes entre dominios. Esto le permite crear un [!DNL Target] actividad que abarca `siteA.com` y `siteB.com` y los visitantes permanecen en la misma experiencia cuando navegan por dominios únicos. Esta funcionalidad se vincula a [!DNL Target]Comportamiento de cookies de terceros y de origen de.

>[!NOTE]
>
>El seguimiento entre dominios es compatible a partir de at.js 2.10, pero no lo es de serie en at.js 2.*x* anterior a 2.10. at.js 2 permite el seguimiento entre dominios.*x* a través de la biblioteca Experience Cloud ID (ECID) en la versión 4.3.0+.

Entrada [!DNL Target], la cookie de terceros se almacena en `<CLIENTCODE>.tt.omtrdc.net`. La cookie de origen se almacena en `clientdomain.com`. La primera solicitud devuelve encabezados de respuesta HTTP que intentan establecer cookies de terceros denominadas `mboxSession` y `mboxPC`, mientras se devuelve una solicitud de redirección con un parámetro adicional (`mboxXDomainCheck=true`). Si el navegador acepta cookies de terceros, la solicitud de redirección incluye dichas cookies y la experiencia se devuelve. Este flujo de trabajo es posible porque utilizamos el método HTTP GET.

Sin embargo, en at.js 2.*x*, no se utiliza la GET HTTP. En su lugar, se utiliza el POST HTTP a través de at.js 2.*x*[!DNL Target] para enviar cargas JSON a servidores de Edge. El uso del POST HTTP significa que se interrumpirá la solicitud de redirección para comprobar si un explorador admite cookies de terceros. Esto se debe a que las solicitudes HTTP GET son transacciones idempotentes, mientras que HTTP POST no es idempotente y no se debe repetir arbitrariamente. Por lo tanto, en el seguimiento entre dominios en at.js 2.*x* (anterior a 2.10) no es compatible de serie. Solo at.js 1.*x* es compatible de serie para el seguimiento entre dominios.

Para utilizar el seguimiento entre dominios para at.js v2.10 o posterior, puede realizar una de las siguientes acciones:

1. Instale el [Biblioteca ECID 4.3.0+](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=es) en conjunto con at.js 2.*x*. La biblioteca ECID sirve para administrar los ID persistentes que se utilizan para identificar a un visitante, incluso entre dominios. Después de instalar la biblioteca ECID 4.3.0+ y at.js 2.,*x*, podrá crear actividades que abarquen dominios únicos y rastrear usuarios. Es importante tener en cuenta que esta funcionalidad solo funciona después de que caduque la sesión.

1. En lugar de instalar la biblioteca ECID, si tiene at.js v2.10 o posterior, puede habilitar la configuración Dominio cruzado en [!DNL Target] IU en **[!UICONTROL Administration]** > **[!UICONTROL Implementación]**. (Como alternativa, puede configurar la variable _crossDomain_ opción para _activado_ en el código at.js).

Para utilizar el seguimiento entre dominios para las versiones de at.js v2.*x* antes de 2.10, puede implementar la opción #1 anteriormente (instalar la biblioteca ECID).

### Se admite Crear automáticamente un mbox global

Esta configuración indica a at.js 2.*x* que envíe una solicitud a los servidores Edge de [!DNL Target] mientras se carga la página. Dado que el mbox global se traduce en ejecutar > pageLoad, y este es interpretado por los servidores Edge de [!DNL Target], los clientes deben habilitarlo si desean activar una solicitud durante la carga de página.

### Se admite el nombre de mbox global

Los clientes pueden especificar un nombre de mbox global mediante **[!UICONTROL Target]** > **[!UICONTROL Administration]** > **[!UICONTROL Implementación]** > **[!UICONTROL Editar]**. Este ajuste lo utilizan los servidores Edge [!DNL Target] para representar ejecutar > pageLoad en el nombre de mbox global introducido. Esto permite a los clientes seguir utilizando las API del servidor, el compositor basado en formularios, scripts de perfil y crear audiencias dirigidas al mbox global.

### ¿Los eventos personalizados de at.js se aplican a `triggerView()`, o es solo para `applyOffer()` o `applyOffers()`?

* `adobe.target.event.CONTENT_RENDERING_FAILED`
* `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`
* `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`
* `adobe.target.event.CONTENT_RENDERING_REDIRECT`

Sí, los eventos personalizados de at.js también son aplicables en `triggerView()`.

### Dice cuando llamo. `triggerView()` con &amp;lazo;`"page" : "true"`&amp;brace;, enviará una notificación al [!DNL Target] back-end y aumentar la impresión. ¿También provoca que se ejecuten los scripts de perfil?

Cuando se realiza una llamada de recuperación previa al back-end de [!DNL Target], se ejecutan los scripts de perfil. A partir de ahí, los datos de perfil afectados se cifran y se devuelven al cliente. Después de la invocación de `triggerView()` con `{"page": "true"}`, se envía una notificación junto con los datos de perfil cifrados. Es entonces cuando el back-end de [!DNL Target] descifra los datos de perfil y los almacena en las bases de datos.

### ¿Es necesario agregar el código de ocultamiento previo antes de llamar a `triggerView()` para administrar el parpadeo?

No, no es necesario agregar el código de ocultamiento previo antes de llamar a `triggerView()`. at.js 2.*x*  administra la lógica de ocultamiento previo y el parpadeo antes de que se muestre y se aplique la vista.

### Qué at.js 1.*x* los parámetros para crear audiencias no son compatibles en at.js 2.*x*?

Los siguientes parámetros de at.js 1.x son *NO* actualmente se admite para la creación de audiencias al utilizar at.js 2.*x*:

* browserHeight
* browserWidth
* browserTimeOffset
* screenHeight
* screenWidth
* screenOrientation
* colorDepth
* devicePixelRatio
* vst.* parámetros (ver más abajo)

### at.js 2.*x*  no admite la creación de audiencias con vst.* parámetros

Clientes en at.js 1.*x* pudieron utilizar vst.* Parámetros de mbox para crear audiencias. Este fue un efecto secundario no intencionado de cómo at.js 1.*x* parámetros de mbox enviados a [!DNL Target] back-end. Después de migrar a at.js 2.*x*, ya no puede crear audiencias con estos parámetros porque at.js 2.*x* envía parámetros de mbox de forma diferente.

## Compatibilidad de at.js

Las tablas siguientes explican la 2.*x* compatibilidad con diferentes tipos de actividades, integraciones, funciones y funciones de at.js.

### Tipos de actividades

| Tipo | Compatible? |
| --- | --- |
| [!UICONTROL Prueba A/B] | Sí |
| [!UICONTROL Asignación automática] | Sí |
| [!UICONTROL Segmentación automática] | Sí |
| [!UICONTROL Segmentación de experiencias] | Sí |
| [!UICONTROL Prueba multivariable] | Sí |
| [!UICONTROL Personalización automatizada] | Sí |
| [!DNL Recommendations] | Sí |

>[!NOTE]
>
>[!UICONTROL Segmentación automática] Las actividades de son compatibles a través de at.js 2.*x* y el VEC cuando se apliquen todas las modificaciones al `Page Load Event`. Cuando se añaden modificaciones a vistas específicas, [!UICONTROL Prueba A/B], [!UICONTROL Asignación automática], y [!UICONTROL Segmentación de experiencias] Solo son compatibles las actividades de (XT).

### Integraciones

| Tipo | Compatible? |
| --- | --- |
| [!UICONTROL Analytics for Target] (A4T) | Sí |
| Audiencias | Sí |
| Atributos del cliente | Sí |
| Fragmentos de experiencia de AEM | Sí |
| [Extensión de Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) | Sí |
| Depurador | Sí |
| Auditor | Todavía no se han actualizado las reglas para at.js 2.*x* |
| Compatibilidad con Opt-In para [RGPD](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) | Esto es compatible con [Versión 2.1.0 de at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md#atjs-version-210-june-3-2019) o más tarde. |
| AEM Personalización mejorada con tecnología [!DNL Adobe Target] | No |

### Funciones

| Función | Compatible? |
| --- | --- |
| Dominio x | No |
| Propiedades/Espacios de trabajo | Sí |
| Vínculos de control de calidad | Sí |
| Compositor de experiencias basadas en formularios | Sí |
| Compositor de experiencias visuales (VEC) | Sí |
| Código personalizado | Sí |
| [Tokens de respuesta](#response-tokens) | Sí |
| Seguimiento de clics | Sí |
| Entrega de varias actividades | Sí |
| targetGlobalSettings | Sí (pero no x-dominio) |
| Métodos de at.js | Se admiten todas las opciones excepto<P>`mboxCreate()`<P>`mboxUpdate()`<P>`mboxDefine()`<P>que mostrará el contenido predeterminado. |

### Parámetros de cadena de consulta

| Parámetro | Compatible? |
| --- | --- |
| `?mboxDisable` | Sí |
| `?mboxDisable` | Sí |
| `?mboxTrace` | Sí |
| `?mboxSession` | No |
| `?mboxOverride.browserIp` | Sí |

## Tokens de respuesta

at.js 2.*x*, igual que at.js 1.*x*, utiliza el evento personalizado `at-request-succeeded` para los tokens de respuesta. Para obtener ejemplos de código utilizando el evento personalizado `at-request-succeeded`, consulte [Tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html).

## at.js 1.*x*  parámetros para at.js 2.*x* sobre la asignación de carga útil

Esta sección describe las asignaciones entre at.js 1.*x* y at.js 2.*x*.

Antes de profundizar en la asignación de parámetros, los puntos finales que utilizan estas versiones de la biblioteca han cambiado:

* at.js 1.*x* - `http://<client code>.tt.omtrdc.net/m2/<client code>/mbox/json`
* at.js 2.*x*  - `http://<client code>.tt.omtrdc.net/rest/v1/delivery`

Otra diferencia importante es que:

* at.js 1.*x* - El código de cliente forma parte de la ruta
* at.js 2.*x*  - El código de cliente se envía como parámetro de cadena de consulta, como:
  `http://<client code>.tt.omtrdc.net/rest/v1/delivery?client=democlient`

Las siguientes secciones enumeran cada at.js 1.*x* parámetro, su descripción y los 2 correspondientes.*x* Carga útil JSON (si corresponde):

### at_property

(at.js 1.*x* parámetro)

Se utiliza para [Permisos de usuario de Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=es).

```json {line-numbers="true"}
{
  ....
  "property": {
    "token": "1213213123122313121"
  }
  ....
}
```

### mboxHost

(at.js 1.*x* parámetro)

El dominio de la página donde [!DNL Target] La biblioteca se ejecuta.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "host": "test.com"
    }
  }
}
```

### webGLRenderer

(at.js 1.*x* parámetro)

Las capacidades del procesador WEB GL del explorador. El mecanismo de detección de dispositivos lo utiliza para determinar si el dispositivo del visitante es de escritorio, un iPhone, un dispositivo Android, etc.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "webGLRenderer": "AMD Radeon Pro 560X OpenGL Engine"
    }
  }
}
```

### mboxURL

(at.js 1.*x* parámetro)

La dirección URL de la página.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "url": "http://test.com"
    }
  }
}
```

### mboxReferrer

(at.js 1.*x* parámetro)

El referente de la página.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "referringUrl": "http://google.com"
    }
  }
}
```

### mbox (el nombre) es igual al mbox global

(at.js 1.*x* parámetro)

La API de envío ya no tiene un concepto de mbox global. En la carga útil JSON debe utilizar `execute > pageLoad`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "execute": {
    "pageLoad": {
       "parameters": ....
       "profileParameters": ...
       .....
    }
  }
}
```

### mbox (el nombre) *no* es igual al mbox global

(at.js 1.*x* parámetro)

Para utilizar un nombre de mbox, páselo a `execute > mboxes`. Un mbox requiere un índice y un nombre.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "execute": {
    "mboxes": [{
       "index": 0,
       "name": "some-mbox",
       "parameters": ....
       "profileParameters": ...
       .....
    }]
  }
}
```

### mboxId

(at.js 1.*x* parámetro)

Ya no se utiliza.

### mboxCount

(at.js 1.*x* parámetro)

Ya no se utiliza.

### mboxRid

(at.js 1.*x* parámetro)

Solicitar ID utilizado por los sistemas descendentes para ayudar a depurar.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "requestId": "2412234442342"
  ....
}
```

### mboxTime

(at.js 1.*x* parámetro)

Ya no se utiliza.

### mboxSession

(at.js 1.*x* parámetro)

El ID de sesión se envía como parámetro de cadena de consulta (`sessionId`) al extremo de la API de envío.

### mboxPC

(at.js 1.*x* parámetro)

El ID de TNT se pasa a `id > tntId`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "id": {
    "tntId": "ca5ddd7e33504c58b70d45d0368bcc70.21_3"
  }
  ....
}
```

### mboxMCGVID

(at.js 1.*x* parámetro)

El ID de visitante de Experience Cloud se pasa a `id > marketingCloudVisitorId`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "id": {
    "marketingCloudVisitorId": "797110122341429343505"
  }
  ....
}
```

### `vst.aaaa.id` y `vst.aaaa.authState`

(at.js 1.*x* parámetros)

Los ID de cliente se deben pasar a `id > customerIds`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "id": {
    "customerIds": [{
       "id": "1232131",
       "integrationCode": "aaaa",
       "authenticatedState": "....."
     }]
  }
  ....
}
```

### mbox3rdPartyId

(at.js 1.*x* parámetro)

ID de terceros de cliente utilizado para vincular diferentes [!DNL Target] ID.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "id": {
    "thirdPartyId": "1232312323123"
  }
  ....
}
```

### mboxMCSDID

(at.js 1.*x* parámetro)

SDID, también conocido como ID de datos suplementarios. Debe pasar a `experienceCloud > analytics > supplementalDataId`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "supplementalDataId": "1212321132123131"
    }
  }
  ....
}
```

### vst.trk

(at.js 1.*x* parámetro)

[!UICONTROL Servidor de seguimiento de Analytics. ] Debe pasar a `experienceCloud > analytics > trackingServer`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServer": "analytics.test.com"
    }
  }
  ....
}
```

### vst.trks

(at.js 1.*x* parámetro)

Servidor de seguimiento de Analytics seguro. Debe pasar a `experienceCloud > analytics > trackingServerSecure`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServerSecure": "secure-analytics.test.com"
    }
  }
  ....
}
```

### mboxMCGLH

(at.js 1.*x* parámetro)

Sugerencia de ubicación de Audience Manager. Debe pasar a `experienceCloud > audienceManager > locationHint`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "locationHint": 9
    }
  }
  ....
}
```

### mboxAAMB

(at.js 1.*x* parámetro)

Blob de Audience Manager. Debe pasar a `experienceCloud > audienceManager > blob`.

at.js 2.*x*  Carga útil JSON:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "blob": "2142342343242342"
    }
  }
  ....
}
```

### mboxVersion

(at.js 1.*x* parámetro)

La versión se envía como parámetro de cadena de consulta a través del parámetro de versión.

## Vídeo de formación: at.js 2.*x* diagrama arquitectónico ![Distintivo Información general](../../assets/overview.png)

at.js 2.*x*  mejora el Adobe [!DNL Target]SPA La compatibilidad de con la solución de se integra con otras soluciones de Experience Cloud y se integra con ella. Este vídeo explica cómo se vincula todo.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Consulte [Explicación de cómo at.js 2.*x* obras](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html) para obtener más información.
