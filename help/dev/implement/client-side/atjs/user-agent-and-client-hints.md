---
keywords: at.js, agente de usuario del explorador, agente de usuario, sugerencias del cliente, user-agent
description: Descubra cómo Adobe Target utiliza user-agent y Client Hints para calificar a los visitantes para la segmentación y personalización.
title: User Agent y Client Hints
feature: at.js
exl-id: e0d87d95-ee95-4ca9-8632-222ae1fb9a91
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 72%

---

# User-agent y Client Hints

Adobe Target utiliza user-agent para clasificar a los visitantes para la segmentación y personalización.

>[!NOTE]
>
>La información contenida en este artículo se aplica a la [versión 2.9.0 de at.js](target-atjs-versions.md) (o posterior).

Cada vez que un explorador web realiza una solicitud a un servidor, la información sobre el explorador y el entorno en el que se ejecuta se incluye en el encabezado de la solicitud. Desde los primeros días de Internet, estos datos se han agregado en una sola cadena denominada user-agent.

El siguiente texto es un ejemplo de user-agent de un equipo basado en Mac OS X que utiliza un explorador Safari:

```
Mozilla/5.0 (Linux; Android 12; SM-S908E) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Mobile Safari/537.36 
```

Desde este user-agent, el servidor que recibe la solicitud puede discernir la siguiente información sobre el explorador y el sistema operativo:

| Información | Detalles |
| --- | --- |
| Nombre del software | Chrome |
| Versión de software | 101 |
| Versión completa del software | 101.0.4951.41 |
| Nombre del motor de diseño | AppleWebKit |
| Versión del motor de diseño | 537.36 |
| Sistema operativo | Android |
| Versión del sistema operativo | Android 12 (Snow Cone) |
| Dispositivo | SM-S908E (Samsung Galaxy S22 Ultra) |

A lo largo de los años, la cantidad de información del explorador y del dispositivo incluida en la cadena del user-agent ha aumentado.

## Casos de uso del User-agent

User-agents se han utilizado durante mucho tiempo para proporcionar a los equipos de marketing y desarrollador información importante sobre cómo los navegadores, sistemas operativos y dispositivos muestran el contenido del sitio, así como la forma en que los usuarios interactúan con los sitios web. User-agents también se utilizan para bloquear el correo no deseado y filtrar bots que rastrean sitios por distintos motivos adicionales.

Sin embargo, en los últimos años, algunos propietarios de sitios y proveedores de marketing han utilizado user-agent junto con otra información incluida en los encabezados de solicitud para crear huellas digitales que pueden utilizarse como medio para identificar a usuarios sin su conocimiento. A pesar del importante propósito que cumple user-agent para los propietarios del sitio, los desarrolladores de navegadores han decidido realizar cambios en la forma en que user-agents trabajan para limitar los posibles problemas de privacidad de los visitantes del sitio.

Los desarrolladores de navegadores crearon User-Agent Client Hints como solución a este desafío. Las Client Hints siguen permitiendo que los sitios recopilen la información necesaria sobre el explorador, el sistema operativo y el dispositivo, a la vez que brindan una mayor protección contra los métodos de seguimiento encubiertos, como la huella digital.

## Client Hints

User-Agent Client Hints proporcionan a los propietarios de sitios web la capacidad de acceder a gran parte de la misma información disponible en el usuario-agente, pero de una manera que preserva la privacidad. Cuando los navegadores modernos envían user-agent a un servidor web, todo user-agent se envía en cada solicitud, independientemente de si es necesario. Por otro lado, las Client Hints refuerzan un modelo en el que el servidor debe solicitar al explorador la información adicional que desea conocer sobre el cliente. Al recibir esta solicitud, el explorador puede aplicar sus propias políticas o configuración de usuario para determinar qué datos se devuelven. En lugar de exponer a todo user-agent de forma predeterminada en todas las solicitudes, el acceso ahora se administra de forma explícita y auditable.

User-Agent Client Hints han estado disponibles en Chrome desde la versión 89. Las versiones recientes de exploradores basados en Chromium, como Microsoft Edge, Opera, Brave, Chrome Android, Opera Android y Samsung Internet, también admiten la API de Client Hints.

Las Client Hints contenidas en los encabezados de la primera solicitud realizada por el explorador a un servidor web contienen la marca del explorador, la versión principal del explorador y un indicador de si el cliente es un dispositivo móvil. Cada fragmento de datos tiene su propio valor de encabezado, en lugar de agruparse en una sola cadena de user-agent.

Por ejemplo, estas son algunas Client Hints:

```
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99" 
Sec-CH-UA-Mobile: ?0 
Sec-CH-UA-Platform: "macOS"
```

... mientras que este es el user-agent para el mismo explorador:

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36 
```

Aunque la información es similar, la primera solicitud al servidor contiene Client Hints que contienen solo un subconjunto de lo que está disponible en la cadena user-agent. Falta en la solicitud la arquitectura del sistema operativo, la versión completa del sistema operativo, el nombre del motor de diseño, la versión del motor de diseño y la versión completa del explorador. Sin embargo, en solicitudes posteriores, la API de Client Hints permite que los servidores web soliciten detalles adicionales de alta entropía sobre el dispositivo. Cuando se solicitan estos valores de entropía alta, según la política del explorador o la configuración del usuario, la respuesta del explorador puede incluir esa información.

El siguiente ejemplo es un objeto JSON devuelto por la API de Client Hints cuando se solicitan valores de entropía altos:

```
{ 

    "architecture":"x86", 
    "bitness":"64", 
    "brands":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100" 
        } 
    ], 
    "fullVersionList":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99.0.0.0" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100.0.4896.127" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100.0.4896.127" 
        } 
    ], 
    "mobile":false, 
    "model":"", 
    "platformVersion":"12.2.1" 
} 
```

Los valores de entropía altos incluyen varios fragmentos de información adicionales que no están disponibles en la información de Client Hints predeterminada. La siguiente tabla contiene detalles de qué datos están disponibles en la solicitud predeterminada frente a la información de User-Agent Client Hints de alta entropía.

| Encabezado HTTP | JavaScript | User-agent | Client hint | Client hint de alta entropía |
| --- | --- | --- | --- | --- |
| Sec-CH-UA | marcas | Sí | Sí | No |
| Sec-CH-UA-Platform | plataforma | Sí | Sí | No |
| Sec-CH-UA-Mobile | móvil | Sí | Sí | No |
| Sec-CH-UA-Platform-Version | platformVersion | Sí | No | Sí |
| Sec-CH-UA-Arch | arquitectura | Sí | No | Sí |
| Sec-CH-UA-Model | modelo | Sí | No | Sí |
| Sec-CH-UA-Bitness | Tasa de bits | Sí | No | Sí |
| Sec-CH-UA-Full-Version-List | fullVersionList | Sí | No | Sí |

## Migración a Client Hints

Actualmente, los exploradores basados en Chromium siguen enviando user-agent junto con Client Hints en los encabezados de las solicitudes realizadas a los servidores web. Sin embargo, a partir de abril de 2022 y hasta febrero de 2023, la cantidad de datos contenidos en la cadena user-agent se reducirá. Otros exploradores, como Safari y Firefox, seguirán aprovechando la cadena de user-agent; sin embargo, también reducirán la cantidad de información que contiene.

## Casos de uso de Target que requieren Client Hints

Los siguientes casos de uso en Target requieren Client Hints:

### Atributos de público

Si utiliza audiencias de Target y utiliza cualquiera de los atributos de audiencia siguientes, Target requiere que las Client Hints realicen la segmentación correcta:

* Explorador
* Sistema operativo
* Móvil

### Scripts de perfil

Si utiliza scripts de perfil y hace referencia al atributo `user.browser` (que hace referencia user-agent), es posible que tenga que actualizar el script de perfil para comprobar también una o más Client Hints. Puede acceder a cualquiera de las Client Hints mediante la función `user.clientHint('sec-ch-ua-xxxxx')`. El nombre del encabezado de Client Hint debe estar en minúscula.

El siguiente ejemplo muestra cómo detectar correctamente un sistema operativo Windows en un script de perfil:

```
"return (((user.browser != null) && (user.browser.indexOf(\"Windows\") > -1)) || " + 
      "((user.clientHint('sec-ch-ua-platform') != null) && 
(user.clientHint('sec-ch-ua-platform') === 'Windows')));" 
```

Esta es una tabla de Client Hints y la semántica de uso de scripts de perfil correspondiente.

| Encabezado de Client Hint | Entropía | Atributo de audiencia | Uso de script de perfil |
| --- | --- | --- | --- |
| [Sec-CH-UA](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA) | Bajo | Explorador | `user.clientHint('sec-ch-ua')` |
| [Sec-CH-UA-Arch](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Arch) | Alto | Expuesto a usuarios mediante scripts de perfil | `user.clientHint('sec-ch-ua-arch')` |
| [Sec-CH-UA-Bitness](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Bitness) | Alto | Expuesto a usuarios mediante scripts de perfil | `user.clientHint('sec-ch-ua-bitness')` |
| [Sec-CH-UA-Full-Version-List](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Full-Version-List) | Alto | Explorador | `user.clientHint('sec-ch-ua-full-version-list')` |
| [Sec-CH-UA-Mobile](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Mobile) | Bajo | Móvil | `user.clientHint('sec-ch-ua-mobile')` |
| [Modelo Sec-CH-UA](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Model) | Alto | Móvil | `user.clientHint('sec-ch-ua-model')` |
| [Sec-CH-UA-Platform](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform) | Bajo | Sistema operativo | `user.clientHint('sec-ch-ua-platform')` |
| [Sec-CH-UA-Platform-Version](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform-Version) | Alto | Expuesto a usuarios mediante scripts de perfil | `user.clientHint('sec-ch-ua-platform-version')` |

## Cómo pasar Client Hints a Adobe Target

Las secciones siguientes contienen más información sobre cómo pasar Client Hints, según la implementación de Target.

### at.js versión 2.9.0 (o posterior)

A partir de at.js 2.9.0, User Agent Client Hints se recopilarán automáticamente desde el explorador y se enviarán a Target cuando se llame a `getOffer/getOffers()`. De forma predeterminada, at.js recopila solo Client Hints de “baja entropía”. Si realiza la segmentación del público o utiliza secuencias de comandos de perfil basadas en datos clasificados como “alta entropía” desde las secciones anteriores, debe configurar at.js para que recopile Client Hints de “alta entropía” desde el explorador a través de `targetGlobalSettings`.

```
window.targetGlobalSettings = { allowHighEntropyClientHints: true };
```

### SDK del lado del servidor

Para obtener más información sobre cómo pasar Client Hints mediante SDK del lado del servidor, consulte [Client Hints](../../server-side/sdk-guides/core-principles/audience-targeting.md#client-hints) en la documentación de implementación del lado del servidor.
