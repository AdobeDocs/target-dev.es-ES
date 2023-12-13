---
keywords: serverstate, targetGlobalSettings, targetglobalsettings, globalSettings, globalsettings, global settings, at.js, funciones, función, clientCode, clientcode, serverDomain, serverdomain, cookieDomain, serverstate5, serverstate6, serverstate7, serverstate8, serverstate9, targetGlobalSettings0, targetGlobalSettings1, targetGlobalSettings2, targetGlobalSettings3, targetGlobalSettings4, targetGlobalSettings5, cookieDomain, crossDomain, crossDomain, timeout, globalMMS boxAutoCreate, visitorApiTimeout, defaultContentHiddenStyle, defaultContentVisibleStyle, bodyHiddenStyle, bodyHidingEnabled, imsOrgId, secureOnly, overrideMboxEdgeServer, overrideMboxEdgeServerTimeout, cookiedomain5, cookiedomain6, cookiedomain7, cookiedomain8, cookiedomain9, crossDomain0, crossDomain1, crossDomain2, crossDomain3, crossDomain4, crossDomain Domain5, optoutEnabled, optout, opt out, selectorsPollingTimeout, dataProviders, personalización híbrida, deviceIdLifetime
description: Utilice el [!UICONTROL targetGlobalSettings()] para la función [!DNL Adobe Target] La biblioteca JavaScript de at.js para anular la configuración en lugar de utilizar [!DNL Target] API de IU o REST.
title: ¿Cómo utilizo el [!UICONTROL targetGlobalSettings()] ¿Función?
feature: at.js
exl-id: f6218313-6a70-448e-8555-b7b039e64b2c
source-git-commit: 12cf430b65695d38d1651f2a97df418d82d231f3
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 58%

---

# [!UICONTROL targetGlobalSettings()]

Puede anular la configuración de la biblioteca at.js de mediante `[!UICONTROL targetGlobalSettings()]`, en lugar de configurarlas en la [!DNL Target] IU o mediante las API de REST.

## Configuración

Las configuraciones que se pueden anular son las siguientes:

### aepSandboxId

* **Tipo**: String
* **Valor predeterminado**: nulo
* **Descripción**: Parámetro opcional utilizado para enviar [!DNL Adobe Experience Platform] ID de zona protegida para compartir [!DNL Adobe Experience Platform] destinos creados en la zona protegida no predeterminada con [!DNL Target]. If `aepSandboxId` no es nulo, `aepSandboxName` también debe proporcionarse.

### aepSandboxName

* **Tipo**: String
* **Valor predeterminado**: nulo
* **Descripción**: Parámetro opcional utilizado para enviar [!DNL Adobe Experience Platform] nombre de zona protegida para compartir [!DNL Adobe Experience Platform] destinos creados en la zona protegida no predeterminada con [!DNL Target]. If `aepSandboxName` no es nulo, `aepSandboxId` también debe proporcionarse.

### artifactLocation

* **Tipo**: String
* **Valor predeterminado**: Ninguno
* **Descripción**: una URL completa para el [artefacto de regla de decisión en el dispositivo](../../../server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)

### bodyHiddenStyle

* **Tipo**: String
* **Valor predeterminado**: body { opacity: 0 }
* **Descripción**: solo se usa cuando `globalMboxAutocreate === true` para minimizar los parpadeos.

  Para obtener más información, consulte [Cómo gestiona at.js el parpadeo](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

### bodyHidingEnabled

* **Tipo**: booleano
* **Valor predeterminado**: true
* **Descripción**: se usa para controlar los parpadeos cuando `target-global-mbox` se utiliza para publicar ofertas creadas en el Compositor de experiencias visuales, también denominadas ofertas visuales.

### clientCode

* **Tipo**: String
* **Valor predeterminado**: valor establecido mediante la IU.
* **Descripción**: representa el código de cliente.

### cookieDomain

* **Tipo**: String
* **Valor predeterminado**: si es posible, establezca en el dominio de nivel superior.
* **Descripción**: representa el dominio que se usa al guardar las cookies.

### crossDomain

* **Tipo**: String
* **Valor predeterminado**: valor establecido mediante la IU.
* **Descripción**: indica si el seguimiento entre dominios está activado o no. Los valores permitidos dependen de la versión de at.js. Para at.js v1.*x*, especifique si las capacidades entre dominios son `disabled` (los exploradores establecen cookies solo en su dominio (cookies de origen), `x only` (los exploradores establecen cookies en [!DNL Target]solo el dominio de ), o ambos, seleccionando `enabled` (los exploradores establecen cookies de origen y de terceros). En la versión 2.10 y posteriores de at.js, especifique si las capacidades entre dominios son `enabled` (los exploradores establecen cookies de origen y de terceros) o `disabled` (los exploradores no establecen cookies de terceros).

### cspScriptNonce

* **Tipo**: consulte [Política de seguridad de contenido](#content-security-policy) a continuación.
* **Valor predeterminado**: consulte [Política de seguridad de contenido](#content-security-policy) a continuación.
* **Descripción**: consulte [Política de seguridad de contenido](#content-security-policy) a continuación.

### cspStyleNonce

* **Tipo**: consulte [Política de seguridad de contenido](#content-security-policy) a continuación.
* **Valor predeterminado**: consulte [Política de seguridad de contenido](#content-security-policy) a continuación.
* **Descripción**: consulte [Política de seguridad de contenido](#content-security-policy) a continuación.

### dataProviders

* **Tipo**: consulte [Proveedores de datos](#data-providers) más adelante.
* **Valor predeterminado**: consulte [Proveedores de datos](#data-providers) a continuación.
* **Descripción**: consulte [Proveedores de datos](#data-providers) a continuación.

### decisioningMethod

* **Tipo**: String
* **Valor predeterminado**: del lado del servidor
* **Otros valores**: en el dispositivo, híbrido
* **Descripción**: Consulte Métodos de toma de decisiones a continuación.

  **Métodos de decisión**

  Con la toma de decisiones en el dispositivo, [!DNL Target] introduce una nueva configuración denominada Método de decisión que dicta cómo at.js ofrece sus experiencias. El `decisioningMethod` tiene tres valores: solo del lado del servidor, solo en el dispositivo e híbrido. Cuando `decisioningMethod` se configura en `targetGlobalSettings()`, actúa como el método de toma de decisiones predeterminado para todas las decisiones de [!DNL Target].

  **Solo del lado del servidor**:

  Solo del lado del servidor es el método de toma de decisiones predeterminado que se establece por defecto cuando at.js 2.5+ se implementa y despliega en las propiedades web.

  Usar solo del lado del servidor como configuración predeterminada significa que todas las decisiones se toman en la [!DNL Target] red perimetral, que implica una llamada al servidor de bloqueo. Este método puede introducir la latencia incremental, pero también ofrece beneficios importantes, como la posibilidad de aplicar [!DNL Target]Las funciones de aprendizaje automático de que incluyen [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) y [Segmentación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) actividades.

  Además, puede mejorar sus experiencias personalizadas utilizando [!DNL Target]El perfil de usuario de, que se mantiene en todas las sesiones y canales, puede proporcionar potentes resultados para su empresa.

  Por último, solo del lado del servidor permite utilizar Adobe Experience Cloud y ajustar las audiencias a las que se puede dirigir mediante segmentos de Audience Manager y Adobe Analytics.

  **Solo en el dispositivo**:

  Solo en el dispositivo es el método de toma de decisiones que debe configurarse en at.js 2.5+ cuando las decisiones en el dispositivo deben utilizarse solo en sus páginas web.

  La toma de decisiones en el dispositivo puede ofrecer sus experiencias y actividades de personalización a una velocidad asombrosa, ya que las decisiones se toman a partir de un artefacto de reglas en caché que contiene todas las actividades que cumplen los requisitos para la toma de decisiones en el dispositivo.

  Para obtener más información acerca de las actividades que cumplen los requisitos para la toma de decisiones en el dispositivo, consulte la sección Funciones compatibles.

  Este método de toma de decisiones solo debe usarse si el rendimiento es muy crítico en todas las páginas que requieren decisiones de [!DNL Target]. Además, tenga en cuenta que, cuando se selecciona este método de toma de decisiones, las actividades de [!DNL Target] que no cumplen los requisitos para la toma de decisiones en el dispositivo no se entregarán ni ejecutarán. La biblioteca at.js 2.5+ está configurada para buscar solo el artefacto de reglas en caché para tomar decisiones.

  **Híbrido**:

  Híbrido es el método de toma de decisiones que debe configurarse en at.js 2.5+ cuando las decisiones en el dispositivo y las actividades que requieren una llamada de red a [!DNL Adobe Target] Se debe ejecutar la red perimetral.

  Cuando administra actividades de toma de decisiones en el dispositivo y actividades del lado del servidor, puede resultar un poco complicado y tedioso pensar en cómo implementar y aprovisionar [!DNL Target] en sus páginas. Con el método de toma de decisiones híbrido, [!DNL Target] sabe cuándo debe realizar una llamada al servidor a [!DNL Adobe Target] Red perimetral para actividades que requieren ejecución del lado del servidor y también cuando solo se ejecutan decisiones en el dispositivo.

  El artefacto de reglas JSON incluye metadatos para informar a at.js de si un mbox tiene una actividad del lado del servidor en ejecución o una actividad de toma de decisiones en el dispositivo. Este método de toma de decisiones garantiza que las actividades que desea que se entreguen rápidamente se realicen mediante la toma de decisiones en el dispositivo y que, para las actividades que requieren una personalización basada en ML más potente, dichas actividades se realicen a través del [!DNL Adobe Target] Red perimetral.

### defaultContentHiddenStyle

* **Tipo**: String
* **Valor predeterminado**: visibilidad: oculto
* **Descripción**: solo se usa para ajustar mboxes que utilizan DIV con el nombre de clase “mboxDefault” y que se ejecutan a través de `mboxCreate()`, `mboxUpdate()` o `mboxDefine()` para ocultar contenido predeterminado.

### defaultContentVisibleStyle

* **Tipo**: String
* **Valor predeterminado**: visibilidad: visible
* **Descripción**: solo se usa para ajustar mboxes que utilizan DIV con el nombre de clase “mboxDefault” y que se ejecutan a través de `mboxCreate()`, `mboxUpdate()` o `mboxDefine()` para mostrar la oferta aplicada (si corresponde) o el contenido predeterminado.

### deviceIdLifetime

* **Tipo**: número
* **Valor predeterminado**: 63244800000 ms = 2 años
* **Descripción**: la cantidad de tiempo que `deviceId` se mantiene en las cookies.

>[!NOTE]
>
>La configuración deviceIdLifetime se puede sobrescribir en la versión 2.3.1 o posterior de at.js.

### enabled

* **Tipo**: booleano
* **Valor predeterminado**: true
* **Descripción**: cuando está habilitada, se ejecuta automáticamente una solicitud de [!DNL Target] para recuperar experiencias y la manipulación DOM para procesar las experiencias. Además, las llamadas de [!DNL Target] se pueden ejecutar manualmente mediante `getOffer(s)` o `applyOffer(s)`.

  Cuando está desactivada, las solicitudes de [!DNL Target] no se ejecutan automática o manualmente.

### globalMboxAutoCreate

* **Tipo**: número
* **Valor predeterminado**: valor establecido mediante la IU.
* **Descripción**: indica si la solicitud de mbox global se debe activar o no.

### imsOrgId

* **Tipo**: String
* **Valor predeterminado**: true
* **Descripción**: representa el ID de organización de IMS.

### optinEnabled

* **Tipo**: booleano
* **Valor predeterminado**: false
* **Descripción**: [!DNL Target] proporciona soporte de funcionalidad opcional a través de Adobe Experience Platform para ayudar a respaldar su estrategia de gestión de consentimiento. La funcionalidad de inclusión permite a los clientes controlar cómo y cuándo se inicia la etiqueta de [!DNL Target]. También hay una opción a través de Adobe Experience Platform para aprobar previamente la [!DNL Target] etiqueta. Para activar la posibilidad de utilizar la inclusión en la biblioteca at.js de [!DNL Target], debe utilizar y añadir la configuración `optinEnabled=true`. En Adobe Experience Platform, debe seleccionar &quot;habilitar&quot; en la lista desplegable Opt-In del RGPD de la vista de instalación de extensión. Consulte la [Documentación de Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) para obtener más información. Para obtener más información sobre esta configuración en relación con las normas de privacidad y protección de datos, incluido el Reglamento general de protección de datos (RGPD) de la Unión Europea y la Ley de Privacidad del Consumidor de California (CCPA), consulte [Reglamentos de protección de datos y privacidad](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

### optoutEnabled

* **Tipo**: booleano
* **Valor predeterminado**: false
* **Descripción**: indica si [!DNL Target] debe llamar a la API de visitante `isOptedOut()` función. Esto forma parte de la habilitación de Device Graph.

### overrideMboxEdgeServer

* **Tipo**: booleano
* **Valor predeterminado**: true (verdadero a partir de la versión 1.6.2 de at.js)
* **Descripción**: indica si se debe utilizar el dominio `<clientCode>.tt.omtrdc.net` o el `mboxedge<clusterNumber>.tt.omtrdc.net`.

  Si este valor es “true”, el dominio `mboxedge<clusterNumber>.tt.omtrdc.net` se guarda en una cookie. Actualmente no funciona con [CNAME](/help/dev/before-implement/implement-cname-support-in-target.md) al utilizar versiones de at.js anteriores a at.js 1.8.2 y at.js 2.3.1. Si esto es un problema para usted, considere la posibilidad de [actualizar at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md) a una versión más reciente y compatible.

### overrideMboxEdgeServerTimeout

* **Tipo**: número
* **Valor predeterminado**: 1860000 => 31 minutos
* **Descripción**: indica la vida útil de la cookie que contiene el valor `mboxedge<clusterNumber>.tt.omtrdc.net`.

### pageLoadEnabled

* **Tipo**: booleano
* **Valor predeterminado**: true
* **Descripción**: cuando esté habilitado, recupere automáticamente las experiencias que deben devolverse al cargar la página.

### pollingInterval

* **Tipo**: número
* **Valor predeterminado**: 300000 (cinco minutos en milisegundos)
* **Descripción**: Intervalo en el que at.js recupera una nueva versión de un artefacto de toma de decisiones en el dispositivo y actualiza la caché. 300000 es el valor mínimo permitido para `pollingInterval`.

### secureOnly

* **Tipo**: booleano
* **Valor predeterminado**: false
* **Descripción**: indica si at.js debería utilizar solo HTTPS o se le debería permitir alternar entre HTTP y HTTPS según el protocolo de la página. Cuando se establece en true, secureOnly también establece los atributos Secure y SameSite en la cookie de mbox.

### selectorsPollingTimeout

* **Tipo**: número
* **Valor predeterminado**: 5000 ms = 5 s
* **Descripción**: en la versión 0.9.6 de at.js, [!DNL Target] introdujo este nuevo ajuste que se puede anular mediante `targetGlobalSettings`.

  El ajuste `selectorsPollingTimeout` representa cuánto está dispuesto a esperar el cliente para que todos los elementos identificados por selectores aparezcan en la página.

  Las actividades creadas por medio del Compositor de experiencias visuales (VEC) tienen ofertas que contienen selectores.

### serverDomain

* **Tipo**: String
* **Valor predeterminado**: valor establecido mediante la IU.
* **Descripción**: representa el [!DNL Target] servidor Edge.

### serverState

* **Tipo**: consulte [Personalización híbrida](#hybrid-personalization) a continuación.
* **Valor predeterminado**: consulte [Personalización híbrida](#hybrid-personalization) a continuación.
* **Descripción**: consulte [Personalización híbrida](#hybrid-personalization) a continuación.

### telemetryEnabled

* **Tipo**: booleano
* **Valor predeterminado**: true
* **Descripción**: cuando se habilita, el Adobe recopila datos sobre el uso de las funciones y la telemetría de rendimiento del SDK. Los datos personales no se recopilan.

### timeout

* **Tipo**: número
* **Valor predeterminado**: valor establecido mediante la IU.
* **Descripción**: representa el tiempo de espera de la solicitud de [!DNL Target] perimetral.

### viewsEnabled {#viewsenabled}

* **Tipo**: booleano
* **Valor predeterminado**: true
* **Descripción**: cuando se habilita, las vistas se recuperan automáticamente cuando se carga la página. Cuándo `triggerView` se llama, las vistas aplicables se muestran en el explorador. Si esta opción está deshabilitada, las vistas no se recuperan al cargar la página y `triggerView` no hace nada. Las vistas son compatibles con at.js 2.Solamente *x.*

### visitorApiTimeout

* **Tipo**: número
* **Valor predeterminado**: 2000 ms = 2 s
* **Descripción**: representa el tiempo de espera de la solicitud de API del visitante.

## Uso

Esta función puede definirse antes de que se cargue at.js o en **Administración** > **Implementación** > **Editar la configuración de at.js** > **Configuración del código** > **Encabezado de la biblioteca**.

En el campo Encabezado de la biblioteca se puede introducir JavaScript de formato libre. El código de personalización debe parecerse al del ejemplo siguiente:

```javascript {line-numbers="true"}
window.targetGlobalSettings = {
   timeout: 200, // using custom timeout
   visitorApiTimeout: 500, // using custom API timeout
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com
};
```

## Proveedores de datos   {#data-providers}

Esta configuración permite a los clientes recopilar datos de proveedores de datos de terceros, como Demandbase, BlueKai y servicios personalizados, y pasar los datos a [!DNL Target] como parámetros de mbox en la solicitud de mbox global. Admite la recopilación de datos de múltiples proveedores a través de solicitudes de desincronización y sincronización. El uso de este enfoque facilita la administración del parpadeo del contenido predeterminado de la página, al tiempo que incluye tiempos de espera independientes para cada proveedor para limitar el impacto en el rendimiento de la página.

>[!NOTE]
>
>Proveedores de datos requiere at.js 1.3 o posterior.

Los vídeos siguientes contienen más información:

| Vídeo | Descripción |
|--- |--- |
| [Uso de Proveedores de datos en Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html) | Proveedores de datos es una funcionalidad que permite pasar fácilmente datos de terceros a Target. Un tercero podría ser un servicio de pronóstico del clima, un DMP o incluso su propio servicio web. Puede usar estos datos para crear audiencias, dirigir contenido y enriquecer el perfil del visitante. |
| [Implementación de Proveedores de datos en Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html) | Detalles de implementación y ejemplos de uso del Adobe [!DNL Target]Función dataProviders de para recuperar datos de proveedores de datos de terceros y pasarlos en el [!DNL Target] solicitud. |

La configuración `window.targetGlobalSettings.dataProviders` es una matriz de proveedores de datos.

Cada proveedor de datos tiene la siguiente estructura:

| Clave | Tipo | Descripción |
|--- |--- |--- |
| name | Cadena | Nombre del proveedor |
| version | Cadena | Versión del proveedor. Esta clave se usará para la evolución del proveedor. |
| timeout | Número | Representa el tiempo de espera del proveedor si se trata de una solicitud de red.  Esta clave es opcional. |
| provider | Función | La función que contiene la lógica de búsqueda de datos del proveedor.<p>La función tiene un solo parámetro requerido: `callback`. El parámetro de llamada de retorno es una función que debe invocarse solo cuando los datos se han recuperado correctamente o si hay un error.<p>La devolución de llamada espera dos parámetros:<ul><li>error: indica si ocurrió un error. Si todo está bien, entonces este parámetro debe establecerse en nulo.</li><li>params: Un objeto JSON, que representa los parámetros que se enviarán en un [!DNL Target] solicitud.</li></ul> |

El siguiente ejemplo muestra dónde está utilizando la ejecución de sincronización el proveedor de datos:

```javascript {line-numbers="true"}
var syncDataProvider = {
  name: "simpleDataProvider",
  version: "1.0.0",
  provider: function(callback) {
    callback(null, {t1: 1});
  }
};

window.targetGlobalSettings = {
  dataProviders: [
    syncDataProvider
  ]
};
```

Después de que at.js procese `window.targetGlobalSettings.dataProviders`, el [!DNL Target] La solicitud contendrá un nuevo parámetro: `t1=1`.

A continuación se muestra un ejemplo si los parámetros que desea agregar a la variable [!DNL Target] Las solicitudes de se recuperan de un servicio de terceros, como BlueKai, Demandbase, etc.:

```javascript {line-numbers="true"}
var blueKaiDataProvider = {
   name: "blueKai",
   version: "1.0.0",
   provider: function(callback) {
      // simulating network request
     setTimeout(function() {
       callback(null, {t1: 1, t2: 2, t3: 3});
     }, 1000);
   }
}

window.targetGlobalSettings = {
   dataProviders: [
      blueKaiDataProvider
   ]
};
```

Después de que at.js procese `window.targetGlobalSettings.dataProviders`, el [!DNL Target] la solicitud contendrá parámetros adicionales: `t1=1`, `t2=2` y `t3=3`.

El siguiente ejemplo utiliza proveedores de datos para recopilar datos de la API meteorológica y enviarlos como parámetros en un [!DNL Target] solicitud. El [!DNL Target] La solicitud tendrá parámetros adicionales, como `country` y `weatherCondition`.

```javascript {line-numbers="true"}
var weatherProvider = {
      name: "weather-api",
      version: "1.0.0",
      timeout: 2000,
      provider: function(callback) {
        var API_KEY = "caa84fc6f5dc77b6372d2570458b8699";
        var lat = 44.426767399999996;
        var lon = 26.1025384;
        var url = "//api.openweathermap.org/data/2.5/weather?";
        var data = {
          lat: lat,
          lon: lon,
          appId: API_KEY
        }

        $.ajax({
          type: "GET",
                url: url,
          dataType: "json",
          data: data,
          success: function(data) {
            console.log("Weather data", data);
            callback(null, {
              country: data.sys.country,
              weatherCondition: data.weather[0].main
            });
          },
          error: function(err) {
            console.log("Error", err);
            callback(err);
          }
        });
      }
    };

    window.targetGlobalSettings = {
      dataProviders: [weatherProvider]
    };
```

Tenga en cuenta lo siguiente al trabajar con la configuración `dataProviders`:

* Si los proveedores de datos agregados a `window.targetGlobalSettings.dataProviders` son asincrónicos, se ejecutarán en paralelo. La solicitud de API del visitante se ejecutará en paralelo con las funciones agregadas a `window.targetGlobalSettings.dataProviders` para permitir un tiempo de espera mínimo.
* at.js no intentará almacenar en caché los datos. Si el proveedor de datos obtiene datos solo una vez, el proveedor de datos debe asegurarse de que los datos estén en caché y, cuando se invoque la función del proveedor, sirva los datos de caché para la segunda invocación.

## Política de seguridad de contenido

at.js 2.3.0+ es compatible con la configuración de nonces de la Política de seguridad de contenido en las etiquetas SCRIPT y STYLE añadidas al DOM de la página al aplicar [!DNL Target] ofertas.

Las funciones SCRIPT y STYLE deben configurarse en `targetGlobalSettings.cspScriptNonce` y `targetGlobalSettings.cspStyleNonce` en consecuencia, antes de la carga de at.js 2.3.0+. Vea el ejemplo siguiente:

```javascript {line-numbers="true"}
...
<head>
 <script nonce="<script_nonce_value>">
window.targetGlobalSettings = {
  cspScriptNonce: "<csp_script_nonce_value>",
  cspStyleNonce: "<csp_style_nonce_value>"
};
 </script>
 <script nonce="<script_nonce_value>" src="at.js"></script>
...
</head>
...
```

Después `cspScriptNonce` y `cspStyleNonce` Si se especifica la configuración, at.js 2.3.0+ las establece como atributos nonce en todas las etiquetas SCRIPT y STYLE que adjunta al DOM al aplicar [!DNL Target] ofertas.

## Personalización híbrida

`serverState` es una configuración disponible en at.js v2.2 o posterior que se puede utilizar para optimizar el rendimiento de la página cuando una integración híbrida de [!DNL Target] se ha implementado. La integración híbrida significa que está utilizando at.js v2.2 o posterior del lado del cliente y la API de entrega o un [!DNL Target] SDK en el lado del servidor para ofrecer experiencias. `serverState` permite a at.js v2.2, u otra versión posterior, aplicar experiencias directamente desde el contenido recuperado en el servidor y devuelto al cliente como parte de la página que se está sirviendo.

### Requisitos previos

Debe tener una integración híbrida de [!DNL Target].

* **Del lado del servidor**: debe utilizar el [API de envío](/help/dev/implement/delivery-api/overview.md) o [SDK de Target](/help/dev/implement/server-side/sdk-guides/getting-started/getting-started.md).
* **Del lado del cliente**: debe utilizar la versión 2.2 o posterior de [at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

### Ejemplos de código

Para comprender mejor cómo funciona, consulte los ejemplos de código siguientes que tendría en su servidor. El código supone que está utilizando el [SDK de Target de Node.js](https://github.com/adobe/target-nodejs-sdk).

```javascript {line-numbers="true"}
// First, we fetch the offers via Target Node.js SDK API, as usual
const targetResponse = await targetClient.getOffers(options);
// A successfull response will contain Target Delivery API request and response objects, which we need to set as serverState
const serverState = {
  request: targetResponse.request,
  response: targetResponse.response
};
// Finally, we should set window.targetGlobalSettings.serverState in the returned page, by replacing it in a page template, for example
const PAGE_TEMPLATE = `
<!doctype html>
<html>
<head>
  ...
  <script>
    window.targetGlobalSettings = {
      overrideMboxEdgeServer: true,
      serverState: ${JSON.stringify(serverState, null, " ")}
    };
  </script>
  <script src="at.js"></script>
</head>
...
</html>
`;
// Return PAGE_TEMPLATE to the client ...
```

Un objeto JSON de muestra `serverState` para la recuperación previa de vista tiene el siguiente aspecto:

```javascript {line-numbers="true"}
{
 "request": {
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "context": {
   "channel": "web",
   "timeOffsetInMinutes": 0
  },
  "experienceCloud": {
   "analytics": {
    "logging": "server_side",
    "supplementalDataId": "7D3AA246CC99FD7F-1B3DD2E75595498E"
   }
  },
  "prefetch": {
   "views": [
    {
     "address": {
      "url": "my.testsite.com/"
     }
    }
   ]
  }
 },
 "response": {
  "status": 200,
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "testclient",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
   "views": [
    {
     "name": "home",
     "key": "home",
     "options": [
      {
       "type": "actions",
       "content": [
        {
         "type": "setHtml",
         "selector": "#app > DIV.app-container:eq(0) > DIV.page-container:eq(0) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
         "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
         "content": "<span style=\"color:#FF0000;\">Latest</span> Products for 2020"
        }
       ],
       "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
       "responseTokens": {
        "profile.memberlevel": "0",
        "geo.city": "dublin",
        "activity.id": "302740",
        "experience.name": "Experience B",
        "geo.country": "ireland"
       }
      }
     ],
     "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    }
   ]
  }
 }
}
```

Una vez que la página se carga en el explorador, at.js aplica todas las ofertas de [!DNL Target] de `serverState` inmediatamente, sin activar ninguna llamada de red contra el perímetro de [!DNL Target]. Además, at.js oculta únicamente los elementos DOM para los que las ofertas de [!DNL Target] están disponibles en el contenido recuperado del lado del servidor, lo que afecta positivamente al rendimiento de carga de página y a la experiencia del usuario final.

### Notas importantes

Tenga en cuenta lo siguiente al utilizar `serverState`:

* Por el momento, at.js v2.2 solo admite la entrega de experiencias mediante serverState para:

   * Actividades creadas por VEC que se ejecutan al cargar la página.
   * Vistas previamente recuperadas.

     SPA En caso de que se utilice la [!DNL Target] Vistas y `triggerView()` en la API de at.js, at.js v2.2 almacena en caché el contenido de todas las vistas previamente recuperadas del lado del servidor y las aplica en cuanto cada vista se activa mediante `triggerView()`, de nuevo sin activar ninguna llamada de recuperación de contenido adicional a [!DNL Target].

   * **Nota**: Actualmente, los mboxes recuperados del lado del servidor no son compatibles con `serverState`.

* Al aplicar `serverState` ofertas, at.js tiene en cuenta `pageLoadEnabled` y `viewsEnabled` , por ejemplo, las ofertas de carga de página no se aplicarán si la variable `pageLoadEnabled` La configuración es falsa.

  Para activar esta configuración, active la opción **Administración > Implementación > Editar > Carga de página habilitada**.

  ![Configuración de carga de página habilitada](../../assets/page-load-enabled-setting.png)

* Se ha agregado texto para indicar que si usa las etiquetas `serverState` y `<script>` en el contenido devuelto, debe asegurarse de que el contenido HTML use `<\/script>` en lugar de `</script>`. Si utiliza `</script>`, el explorador interpreta `</script>` como el final de un SCRIPT en línea y podría romper la página HTML.

### Recursos adicionales

Para obtener más información sobre cómo funciona `serverState`, consulte los siguientes recursos:

* [Código de muestra](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/advanced-atjs-integration-serverstate).
* [Aplicación de ejemplo de aplicación de una sola página (SPA) con `serverState`](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/react-shopping-cart-demo).
