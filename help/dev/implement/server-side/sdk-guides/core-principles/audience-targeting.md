---
title: Segmentación de audiencia
description: Las audiencias se pueden usar para segmentar las actividades de experimentación y personalización. [!DNL Adobe Target] ofrece soporte para innumerables funcionalidades de segmentación de audiencia predeterminadas.
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 25%

---

# Segmentación de audiencia

## Información general

Las audiencias se pueden usar para segmentar las actividades de experimentación y personalización. [!DNL Adobe Target] admite innumerables funcionalidades de segmentación de audiencia eficaces de forma predeterminada. Los atributos siguientes están disponibles para [segmentación de audiencia](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/create-audience.html):

### Biblioteca [!DNL Target]

Para obtener más información, consulte [[!DNL Target] Biblioteca](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-library.html).
palo de golf
* Conducido por Bing
* Explorador Chrome
* Explorador Firefox
* Conducido por Google
* Internet Explorer
* Sistema operativo Linux
* Sistema operativo Mac OS
* Visitantes nuevos
* Visitantes habituales
* Explorador Safari
* Dispositivo de tableta
* Sistema operativo Windows
* Conducido por Yahoo

### Geografía

Para obtener más información, consulte [Información geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html).
escafandra&#x200B;
* País/región
* Estado
* Ciudad
* Código postal
* Latitud
* Longitud
* DMA
* Operador de telefonía móvil

### Red

Para obtener más información, consulte [Red](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html).

* ISP
* Nombre de dominio
* Velocidad de conexión

### Móvil

Para obtener más información, consulte [Móvil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html).

* Nombre de marketing del dispositivo
* Modelo de dispositivo
* Proveedor de dispositivo
* Es dispositivo móvil
* Es un teléfono móvil
* Es una tableta
* Sistema operativo
* Altura de la pantalla (px)
* Anchura de la pantalla (px)

### Personalizado

Para obtener más información, vea [Parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html).

* cualquier par clave/valor

### Sistema operativo

Para obtener más información, consulte [Sistema operativo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html).

* Linux
* Macintosh
* Windows

### Páginas del sitio

Para obtener más información, consulte [Páginas de sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html).

* Página actual
* Página anterior
* Página de aterrizaje
* Encabezado HTTP

### Explorador

Para obtener más información, consulte [Explorador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html).

* Tipo
* Idioma 
* Versión 

### Perfil del visitante

Para obtener más información, consulte [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html).

* cualquier par clave/valor que se mantenga.

### Informe de

Para obtener más información, consulte [Fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html).

* Desde Baidu
* Desde Bing
* Desde Google
* Desde Yahoo
* Página de aterrizaje que deriva: dirección URL
* Página de aterrizaje que deriva: dominio
* Página de aterrizaje que deriva: consulta

### Periodo de tiempo

Para obtener más información, consulte [Periodo de tiempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html).

* Fecha inicial / Fecha final

## Client Hints

[!DNL Adobe Target] requiere Client Hints para la segmentación correcta de los atributos de audiencia del explorador, sistema operativo y móvil, así como ciertas instancias de scripts de perfil. Para obtener más información, consulte [User Agent y Client Hints](../../../client-side/atjs/user-agent-and-client-hints.md).

### Cómo pasar Client Hints a [!DNL Adobe Target]

A partir del SDK v2.4.0 de Node.js y el SDK v2.3.0 de Java, las Client Hints se pueden enviar a [!DNL Target] mediante llamadas `getOffers()`. Las Client Hints deben incluirse en el objeto `request.context`, junto con el agente de usuario.

>[!BEGINTABS]

>[!TAB SDK de Node.js]

```js {line-numbers="true"}
targetClient.getOffers({ 
    request: { 
        context: { 
            channel: "mobile" 
            userAgent: "Mozilla/5.0 (Linux; Android 12; Pixel 4a) AppleWebKit/537.36 (KHTML, like Gecko) Mobile Safari/537.36", 
            clientHints: { 
                mobile: "true", 
                platform: "Linux", 
                platformVersion: "12.1", 
                model: "Pixel 4a", 
                browserUAWithMajorVersion: "\"Not A;Brand\";v=\"98\", \"Chromium\";v=\"98\", \"Google Chrome\";v=\"98\"", 
                browserUAWithFullVersion: "\" Not A;Brand\";v=\"98.0.0.0\", \"Chromium\";v=\"98.0.4844.83\", \"Google Chrome\";v=\"98.0.4758.101\"", 
                bitness: "64", 
                architecture: "x86" 
            } 
        }, 
        execute: { 
            mboxes: [{ 
                name: "home", 
                index: 1 
            }] 
        } 
    } 
});
```

>[!TAB SDK de Java]

```javascript {line-numbers="true"}
import com.adobe.target.delivery.v1.model.ClientHints; 
import com.adobe.target.delivery.v1.model.Context; 
import com.adobe.target.delivery.v1.model.ExecuteRequest; 
import com.adobe.target.edge.client.model.TargetDeliveryRequest; 

 
ClientHints clientHints = new ClientHints(); 
clientHints.setMobile(true); 
clientHints.setPlatform("macOS"); 
clientHints.setArchitecture("x86"); 
clientHints.setPlatformVersion("11.3.1"); 
clientHints.setBrowserUAWithMajorVersion( 
  "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"99\", \"Google Chrome\";v=\"99\""); 
String userAgent = 
  "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36"; 

 
TargetDeliveryRequest request = TargetDeliveryRequest.builder() 
        .execute(new ExecuteRequest().pageLoad(pageLoad)) 
        .context(new Context().clientHints(clientHints).userAgent(userAgent)) 
        .build(); 
```

>[!ENDTABS]

## Toma de decisiones en el dispositivo

La siguiente tabla indica qué reglas de audiencia son compatibles o no con la toma de decisiones en el dispositivo.

| Regla de audiencia | Toma de decisiones en el dispositivo |
| --- | --- |
| [Ubicación geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Sí |
| [Red](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | No |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | No |
| [Parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Sí |
| [Sistema operativo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Sí |
| [Páginas del sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Sí |
| [Explorador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Sí |
| [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | No |
| [Fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | No |
| [Lapso de tiempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Sí |
| [Audiencias de Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Audiencias de Adobe Audience Manager, Adobe Analytics y Adobe Experience Manager | No |

### Segmentación geográfica para la toma de decisiones en el dispositivo

Para mantener una latencia cercana a cero en las actividades de toma de decisiones en el dispositivo con audiencias basadas en regiones geográficas, Adobe recomienda que proporcione los valores geográficos usted mismo en la llamada a `getOffers`. Para ello, configure el objeto `Geo` en `Context` de la solicitud. Esto significa que el servidor necesitará una forma de determinar la ubicación de cada usuario final. Por ejemplo, el servidor puede realizar una búsqueda de IP a geografía mediante un servicio que configure. Algunos proveedores de alojamiento, como Google Cloud, proporcionan esta funcionalidad mediante encabezados personalizados en cada `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB SDK de Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
    request: {
        context: {
            geo: {
                city: "SAN FRANCISCO",
                countryCode: "US",
                stateCode: "CA",
                latitude: 37.75,
                longitude: -122.4
            }
        },
        execute: {
            pageLoad: {}
        }
    }
})
```

>[!TAB SDK de Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(ipToGeoLookup(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

    public static Geo ipToGeoLookup(String ip) {
        GeoResult geoResult = geoLookupService.lookup(ip);
        return new Geo()
            .city(geoResult.getCity())
            .stateCode(geoResult.getStateCode())
            .countryCode(geoResult.getCountryCode());
    }
}
```

>[!ENDTABS]

Sin embargo, si no tiene la capacidad de realizar búsquedas de IP a geografía en el servidor, pero desea realizar la toma de decisiones en el dispositivo para `getOffers` solicitudes que contienen audiencias basadas en regiones geográficas, esto también se admite. La desventaja de este enfoque es que usará una búsqueda remota de IP a geografía, que agregará latencia a cada llamada de `getOffers`. Esta latencia debe ser menor que una llamada a `getOffers` remota, ya que entra en una red de distribución de contenido (CDN) ubicada cerca del servidor. Debe **solamente** proporcionar el campo `ipAddress` en el objeto `Geo` en `Context` de su solicitud, a fin de que el SDK recupere la ubicación geográfica de la dirección IP del usuario. Si se proporciona cualquier otro campo además de `ipAddress`, el SDK de [!DNL Target] no recuperará los metadatos de ubicación geográfica para la resolución.

>[!BEGINTABS]

>[!TAB SDK de Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
    request: {
        context: {
            geo: {
                ipAddress: "127.0.0.1"
            }
        },
        execute: {
            pageLoad: {}
        }
    }
})
```

>[!TAB SDK de Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(new Geo().ipAddress(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

}
```

>[!ENDTABS]

## Toma de decisiones del lado del servidor

La siguiente tabla indica qué reglas de audiencia son compatibles o no con la toma de decisiones en el lado del servidor.

| Regla de audiencia | Toma de decisiones del lado del servidor |
| --- | --- |
| [Ubicación geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Sí |
| [Red](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Sí |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Sí |
| [Parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Sí |
| [Sistema operativo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Sí |
| [Páginas del sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Sí |
| [Explorador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Sí |
| [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Sí |
| [Fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Sí |
| [Lapso de tiempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Sí |
| [Audiencias de Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Audiencias de Adobe Audience Manager, Adobe Analytics y Adobe Experience Manager | Sí |
