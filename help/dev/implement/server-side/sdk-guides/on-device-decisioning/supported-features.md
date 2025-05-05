---
title: ¿Qué funciones se admiten en la toma de decisiones en el dispositivo?
description: Aprenda a ofrecer el contenido personalizado más relevante y atractivo mediante el aprendizaje automático mediante una llamada al servidor en directo.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 13%

---

# Información general sobre funciones compatibles

Los SDK del lado del servidor de [!DNL Adobe Target] proporcionan a los desarrolladores la flexibilidad de elegir entre el rendimiento y la actualización de los datos para tomar decisiones. En otras palabras, si la entrega del contenido personalizado más relevante y atractivo a través del aprendizaje automático es lo más importante para usted, se debe realizar una llamada al servidor en directo. Pero cuando el rendimiento es más crítico, se debe tomar una decisión en el dispositivo. Para que [!UICONTROL on-device decisioning] funcione, consulte la siguiente lista de funciones compatibles:

* Tipos de actividad
* Segmentación de audiencia
* Método de asignación

## Tipos de actividades. 

La siguiente tabla indica qué [tipos de actividad](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=es) creados con el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=es&) son compatibles o no con [!UICONTROL on-device decisioning].

| Tipo de actividad | Admitido |
| --- | --- |
| [Prueba A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=es) | Sí |
| [Asignación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=es) | No |
| [Segmentación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=es) | No |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es) (A4T) | Sí |
| [Prueba multivariada](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=es) (MVT) | No |
| [Segmentación de experiencias](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=es) (XT) | Sí |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=es) (AP) | No |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=es) | No |


## Segmentación de audiencia

La siguiente tabla indica qué reglas de audiencia son compatibles o no con [!UICONTROL on-device decisioning].

| Regla de audiencia | Toma de decisiones en el dispositivo |
| --- | --- |
| [Ubicación geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=es) | Sí |
| [Red](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=es) | No |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=es) | No |
| [Parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=es) | Sí |
| [Sistema operativo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=es) | Sí |
| [Páginas del sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=es) | Sí |
| [Explorador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=es) | Sí |
| [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=es) | No |
| [Fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=es) | No |
| [Lapso de tiempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=es) | Sí |
| [Audiencias de Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=es) (Audiencias de Adobe Audience Manager, Adobe Analytics y Adobe Experience Manager | No |

### Segmentación geográfica para [!UICONTROL on-device decisioning]

Para mantener una latencia cercana a cero en las actividades [!UICONTROL on-device decisioning] con audiencias basadas en regiones, Adobe recomienda que proporcione los valores geográficos usted mismo en la llamada a `getOffers`. Para ello, configure el objeto `Geo` en `Context` de la solicitud. Esto significa que el servidor necesitará una forma de determinar la ubicación de cada usuario final. Por ejemplo, el servidor puede realizar una búsqueda de IP a geografía mediante un servicio que configure. Algunos proveedores de alojamiento, como Google Cloud, proporcionan esta funcionalidad mediante encabezados personalizados en cada `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Nodo.js]

```csharp {line-numbers="true"}
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

>[!TAB Java]

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

Sin embargo, si no tiene la capacidad de realizar búsquedas de IP a geografía en su servidor, pero aún desea realizar [!UICONTROL on-device decisioning] para `getOffers` solicitudes que contienen audiencias basadas en regiones geográficas, esto también se admite. La desventaja de este enfoque es que usará una búsqueda remota de IP a geografía, que agregará latencia a cada llamada de `getOffers`. Esta latencia debe ser menor que una llamada a `getOffers` remota, ya que entra en una red de distribución de contenido (CDN) ubicada cerca del servidor. Solo debe proporcionar el campo `ipAddress` en el objeto `Geo` de la `Context` de su solicitud para que el SDK pueda recuperar la geolocalización de la dirección IP del usuario. Si se proporciona cualquier otro campo además de `ipAddress`, el SDK de [!DNL Target] no recuperará los metadatos de ubicación geográfica para la resolución.


>[!BEGINTABS]

>[!TAB Nodo.js]

```csharp {line-numbers="true"}
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

>[!TAB Java]

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

## Método de asignación

La siguiente tabla indica qué métodos de asignación son compatibles o no con [!UICONTROL on-device decisioning].

| Método de asignación | Admitido |
| --- | --- |
| Manual | Sí |
| [Asignar automáticamente a la mejor experiencia](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=es) | No |
| [Segmentación automática para experiencias personalizadas](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html?lang=es) | No |
