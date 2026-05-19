---
keywords: ocultar previamente SDK, parpadeo, antiparpadeo, preocultación, preocultación, aleación, at.js, implementación, consentimiento, CMP, colocación de script, en línea, externo, selección de SDK
description: Aprenda a integrar  [!DNL Adobe Target] Preocultar SDK para eliminar el parpadeo del contenido no personalizado (parpadeo) durante la carga de la página. SDK funciona tanto con Adobe Alloy (Web SDK) como con at.js.
title: Preocultar guía de integración de SDK
feature: Implementation
hide: true
source-git-commit: 81818370d32ee8c3f3538e5d8d942f66c13e6a13
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 0%

---


# Preocultar guía de integración de SDK

Una pequeña biblioteca sincrónica de JavaScript que evita el parpadeo visual causado por la personalización de [!DNL Adobe Target] que reescribe una página en mitad del procesamiento. Agregue una etiqueta en línea `<script>` en la parte superior de `<head>` y la página se mostrará solo después de que el contenido personalizado esté listo o de que se active el temporizador de seguridad.

## Pasos de integración {#integration-steps}

1. Descargue el paquete.

   Utilice la interfaz de usuario de Flicker Manager para descargar `prehide.min.js`. El archivo está preconfigurado con el código de cliente y el tiempo de espera de protección, por lo que no se necesita ningún bloque `PrehideConfig`.

1. Incrustarlo en línea en la parte superior de `<head>`.

   Pegue el contenido de `prehide.min.js` directamente dentro de una etiqueta en línea `<script>` como el primer elemento secundario de `<head>`. Consulte [En línea frente a externo](#inline-vs-external) para ver por qué se prefiere la inclusión en línea.

   ```html
   <!-- 1. Prehide SDK: must be FIRST in <head> and BEFORE any Adobe SDK -->
   <script>
     // paste the contents of prehide.min.js here
   </script>
   
   <!-- 2. Then load Alloy.js OR at.js -->
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Opcional) Añada un bloque de configuración de tiempo de ejecución.

   Solo es necesario si aloja el paquete automáticamente sin descargarlo a través de la interfaz de usuario o si necesita anular la opción de SDK. Coloque el bloque de configuración antes del script de ocultamiento previo:

   ```html
   <script>
     window.PrehideConfig = {
       org: "your-client-code",
       sdk: "alloy"            // or "atjs" (defaults to "alloy")
     };
   </script>
   <script> /* prehide.min.js inline contents */ </script>
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Opcional) Consentimiento de transferencia.

   Si su implementación utiliza una plataforma de administración de consentimiento (CMP), llame a `window.Prehide.setConsent(...)` en cuanto se conozca el estado de consentimiento. Consulte [Administración de consentimiento](#consent-management).

1. Verificar.

   Abra DevTools y confirme que `<style id="alloy-prehiding">` (o `at-body-style` para at.js) aparece en `<head>` al pintar por primera vez y se quita una vez que SDK termina. Ejecute `window.Prehide.getState()` en la consola para inspeccionar el estado de tiempo de ejecución.

## Dónde colocar la secuencia de comandos {#script-placement}

>[!IMPORTANT]
>
>Prehide SDK debe ejecutarse antes que Alloy/at.js. Si Alloy se carga primero, la página procesa el contenido no personalizado y, a continuación, vuelve a procesarlo. Ese es el parpadeo exacto que esta SDK está diseñada para evitar.
></br>>No agregue `async` ni `defer` a la etiqueta de script de preocultar SDK. Se requiere una ejecución sincrónica para que la regla de ocultación se inserte antes de que el explorador empiece a mostrar la página.

El SDK de ocultación previa debe aparecer antes en el documento que el SDK [!DNL Adobe Target] que limpia después de él. El orden de carga no es negociable:

```html
<!doctype html>
<html>
<head>
  <!-- ① Prehide SDK FIRST. Inline. Synchronous. No async/defer. -->
  <script> /* prehide.min.js inline contents */ </script>

  <!-- ② Alloy or at.js loads next -->
  <script src="https://cdn.alloy.adobe.com/alloy.min.js"></script>

  <!-- ③ Then everything else: meta, css, third-party tags, ... -->
  <link rel="stylesheet" href="main.css">
</head>
<body> ... your page ... </body>
</html>
```

## En línea frente a externa {#inline-vs-external}

Existen dos maneras de incluir `prehide.min.js`:

| Método | Ejemplo | Notas |
| --- | --- | --- |
| En línea (preferido) | `<script>/* full contents of prehide.min.js pasted directly into the page */</script>` | Cero de ida y vuelta en la red. El SDK se ejecuta antes de que se procese cualquier otra cosa. |
| Externo (solo si es imposible integrar) | `<script src="/static/prehide.min.js"></script>` | Introduce una solicitud de red de bloqueo antes del primer procesamiento. Incluso con HTTP/2 y almacenamiento en caché perimetral, esto suele costar entre 30 y 80 ms. |

### Por qué se prefiere en línea

>[!TIP]
>
>Inserte el paquete directamente dentro de `<script>...</script>` en la plantilla de HTML. Trátelo como un bloque CSS crítico: pequeño, en línea y siempre en la parte superior.

* Sin captura de bloqueo de procesamiento. El propósito de Prehide SDK es insertar reglas de ocultación *antes* del primer procesamiento. Un(a) `<script src>` externo agrega un recorrido de ida y vuelta de red en exactamente esa ventana crítica.
* No hay nuevo modo de fallo. Un archivo externo puede tener un tiempo de espera 404 o estar bloqueado por un bloqueador de anuncios. Una copia en línea no puede.
* El paquete es pequeño (~6 KB). Inline cuesta menos que un favicon típico, y ningún beneficio de almacenamiento en caché es lo suficientemente grande como para compensar el viaje de ida y vuelta adicional al primer procesamiento.
* Compatible con caché. Cuando se integra en la respuesta de HTML, SDK se almacena en caché junto con el resto del documento mediante la capa de almacenamiento en caché existente (CDN o caché HTTP del explorador).
* Paquete específico del cliente. El archivo descargado tiene el código de cliente grabado en el momento de la descarga. La incorporación garantiza que cada visitante reciba el paquete personalizado correcto sin una solicitud adicional.

## Configuración {#configuration}

SDK acepta la configuración de dos fuentes, en orden de prioridad. Lee el que esté disponible primero.

### R: Marcadores de posición de tiempo de descarga (sin configuración de tiempo de ejecución)

Cuando descarga `prehide.min.js` desde la interfaz de usuario de Flicker Manager, el servidor sustituye tres marcadores de posición dentro del paquete:

| Marcador | Reemplazado por | Alternativa si no se sustituye |
| --- | --- | --- |
| `__FM_CLIENT_CODE__` | Su código de cliente (por ejemplo, `"acmecorp"`) | Lee `window.PrehideConfig.org` |
| `__FM_TIMEOUT__` | Duración del temporizador de protección en ms (por ejemplo, `"3000"`) | `5000` ms |
| `__FM_VERSION__` | Versión de SDK (por ejemplo, `"1.0.0"`) | `"0.0.0-dev"` |

Si usa el paquete descargado por la interfaz de usuario, no se necesita ningún bloque `PrehideConfig`. Solo hay que alinear el guión.

### B: tiempo de ejecución `window.PrehideConfig` (integración manual)

Para paquetes autoalojados o sin modificar, declare un objeto de configuración antes de ejecutar el script de ocultación previa:

```html
<script>
  window.PrehideConfig = {
    org: "acmecorp",        // required (or rely on baked-in __FM_CLIENT_CODE__)
    sdk: "alloy"             // optional: "alloy" (default) or "atjs"
  };
</script>
```

| Campo | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `org` | string | Sí (a menos que esté cocido) | Su código de cliente de. Se utiliza como segmento de organización de la dirección URL de CDN desde la que se recuperan las reglas de ocultación previa. |
| `sdk` | `"alloy"` \| `"atjs"` | No | El SDK de Adobe se cargó en la página. Ver [selección de SDK](#sdk-selection). |

## Selección de SDK {#sdk-selection}

[!DNL Adobe Target] ofrece dos SDK de envío: Alloy (el SDK web moderno) y at.js (la biblioteca clásica). Cada uno busca un elemento *diferente* `<style>` `id` cuando la personalización finaliza y lo quita para mostrar la página. Prehide SDK debe insertar el elemento `id` coincidente; de lo contrario, la página permanece oculta hasta que se active el temporizador de seguridad.

| Valor `sdk` | ID de etiqueta de estilo insertado | Eliminado por | Cuándo usar |
| --- | --- | --- | --- |
| `"alloy"` *(predeterminado)* | `<style id="alloy-prehiding">` | Alinear SDK al personalizar-completar | Estás cargando Alloy / Adobe Web SDK en esta página. |
| `"atjs"` | `<style id="at-body-style">` | at.js en personalization-complete | Está cargando la biblioteca clásica at.js en esta página. |

### Cómo se establece

```html
<!-- For at.js -->
<script>
  window.PrehideConfig = { org: "acmecorp", sdk: "atjs" };
</script>
<script> /* prehide.min.js inline */ </script>
<script src="https://cdn.adobe.com/.../at.js"></script>
```

>[!WARNING]
>
>Advertencia de no coincidencia. Si se establece `sdk: "alloy"` al cargar at.js (o viceversa), SDK no encontrará el elemento de ocultación previa que se debe eliminar. El temporizador de guardia eventualmente revelará la página, pero los visitantes experimentarán una ventana oculta más larga. Establezca siempre `sdk` para que coincida con la biblioteca que está cargando.

Los valores desconocidos o que faltan vuelven a `"alloy"`, por lo que las integraciones de Alloy existentes siguen funcionando sin ningún cambio de configuración.

## Gestión del consentimiento {#consent-management}

>[!NOTE]
>
>* El valor de consentimiento nunca se almacena en `window`. Solo se expone la función; el estado interno sigue siendo privado para SDK.
>* Las transiciones de `"out"` a `"in"` no vuelven a ocultar la página, ya que volver a ocultar el contenido procesado por completo podría causar problemas visuales.
>* Se puede llamar varias veces a `setConsent` dentro de una sola vista de página. Cada llamada reemplaza el estado anterior.

Preocultar SDK incluye una API según el consentimiento para coordinar con CMP. Su uso es opcional. Si nunca se llama a `setConsent`, SDK se comporta como una integración estándar sin consentimiento.

### Superficie de API

```js
// Single function call. Pass a status string.
window.Prehide.setConsent("pending");  // banner shown, awaiting decision
window.Prehide.setConsent("in");       // user accepted personalization
window.Prehide.setConsent("out");      // user declined personalization

// Read-only debug snapshot.
window.Prehide.getState();
// → { sdk, version, consentStatus, consentApiUsed,
//      rulesResolved, hasSelectorsToGuard, guardTimeout }
```

### Qué hace cada estado

| La llamada | Efecto en el temporizador de guardia | Efecto en el contenido oculto |
| --- | --- | --- |
| `setConsent("pending")` | Se ha borrado el temporizador activo. No hay seguridad para mostrar incendios hasta que se resuelva el consentimiento. | Los selectores permanecen ocultos indefinidamente. |
| `setConsent("in")` | Se borró y se reinició con el tiempo de espera configurado. Espera a que las reglas se resuelvan si aún no lo han hecho. | El contenido permanece oculto hasta que el SDK se personaliza o se activa el temporizador de seguridad. |
| `setConsent("out")` | Borrado. La página se muestra inmediatamente. | La página se muestra de inmediato. Las reglas que se resuelven más adelante hacen que *no* vuelva a ocultar el contenido. |
| *(nunca llamado)* | El temporizador predeterminado se ejecuta desde `init()` durante la duración configurada. | El contenido permanece oculto hasta que el SDK se personaliza o se activa el temporizador de seguridad. (Modo heredado compatible con versiones anteriores). |

### Patrón recomendado: fase pendiente explícita

1. Tan pronto como CMP muestre la interfaz de usuario de consentimiento, llame a `setConsent("pending")`. Esto borra el temporizador de seguridad, de modo que la página permanece oculta mientras el visitante toma la decisión, lo que evita un flash de contenido no personalizado detrás del titular.

   ```js
   window.Prehide.setConsent("pending");
   ```

1. Cuando el visitante acepte la personalización, llame a `setConsent("in")`. El temporizador de guardia se reinicia y Alloy/at.js toma el cargo, lo que revela la página una vez aplicada la personalización.

   ```js
   window.Prehide.setConsent("in");
   ```

1. Cuando el visitante rechaza la personalización, llama a `setConsent("out")`. La página se muestra inmediatamente y permanece visible. Las reglas de CDN que se resuelvan más adelante no lo volverán a ocultar.

   ```js
   window.Prehide.setConsent("out");
   ```

### Ejemplo: integración de estilo OneTrust

```js
// Called once OneTrust has rendered its banner.
function onOneTrustReady() {
  // Pause the guard timer while the banner is visible.
  window.Prehide.setConsent("pending");

  OneTrust.OnConsentChanged(function (event) {
    if (event.consentedToTargeting) {
      window.Prehide.setConsent("in");
    } else {
      window.Prehide.setConsent("out");
    }
  });
}
```

### Ejemplo: estilo TCF/IAB

```js
// Optional: pause the guard while UI is up.
window.Prehide.setConsent("pending");

// Your CMP eventually emits the final TC string.
function onTcData(tcData) {
  const hasTargetConsent = /* derive from tcData */;
  window.Prehide.setConsent(hasTargetConsent ? "in" : "out");
}
```

