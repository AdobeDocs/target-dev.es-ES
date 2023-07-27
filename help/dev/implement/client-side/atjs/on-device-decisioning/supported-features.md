---
keywords: implementación, biblioteca javascript, js, atjs, toma de decisiones en el dispositivo, toma de decisiones en el dispositivo, funciones compatibles, $8
description: Descubra qué funciones son compatibles con [!UICONTROL toma de decisiones en el dispositivo].
title: Qué funciones son compatibles con la toma de decisiones en el dispositivo
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 9%

---

# Funciones compatibles con [!UICONTROL toma de decisiones en el dispositivo]

El [!DNL Adobe Target] El SDK de JS ofrece a los clientes la flexibilidad de elegir entre el rendimiento y la actualización de los datos para la toma de decisiones. En otras palabras, si la entrega del contenido personalizado más relevante y atractivo a través del aprendizaje automático es lo más importante para usted, se debe realizar una llamada al servidor en directo. Sin embargo, cuando el rendimiento es más crítico, se debe tomar una decisión en el dispositivo y en la memoria. Para [!UICONTROL toma de decisiones en el dispositivo] para trabajar, consulte las siguientes secciones que enumeran las funciones compatibles.

## Tipos de actividades compatibles

La siguiente tabla indica qué [tipos de actividades](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) creado por el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) o [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) son compatibles o no con [!UICONTROL toma de decisiones en el dispositivo].

| Tipo de actividad | Compatible? |
| --- | --- |
| [Prueba A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Sí |
| [Asignación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | No |
| [Segmentación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![premium](../../../assets/premium.png) | No |
| [Prueba multivariada](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | No |
| [Segmentación de experiencias](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Sí |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | No |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![premium](../../../assets/premium.png) | No |
| [Actividades con Analytics para Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | Sí |

## Segmentación de audiencia

La siguiente tabla indica qué reglas de audiencia son compatibles o no con [!UICONTROL toma de decisiones en el dispositivo].

| Regla de audiencia | Compatible? |
| --- | --- |
| [Ubicación geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Sí |
| [Red](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | No |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | No |
| [Parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Sí |
| [Sistema operativo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Sí |
| [Páginas del sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Sí |
| [Navegador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Sí |
| [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | No |
| [Fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | No |
| [Periodo de tiempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Sí |
| Audiencias de Adobe Experience Cloud<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager], y [!DNL Adobe Experience Manager]) | No |

### Segmentación geográfica para [!UICONTROL toma de decisiones en el dispositivo]

Para mantener una latencia mínima de [!UICONTROL toma de decisiones en el dispositivo] actividades con audiencias basadas en regiones, Adobe recomienda que proporcione los valores geográficos usted mismo en la llamada a [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Establezca el objeto Geo en el contexto de la solicitud. Esto significa que desde el explorador puede determinar la ubicación de cada visitante. Por ejemplo, puede realizar una búsqueda de IP a geografía mediante un servicio que configure. Algunos proveedores de alojamiento, como Google Cloud, proporcionan esta funcionalidad a través de encabezados personalizados en cada `HttpServletRequest`.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
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

Sin embargo, si no puede realizar búsquedas de IP a geografía en el servidor, pero aún desea realizar [!UICONTROL toma de decisiones en el dispositivo] para [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) solicitudes que contienen audiencias basadas en entornos geográficos, esto también es compatible. La desventaja de este enfoque es que utiliza una búsqueda remota de IP a geografía, que añade latencia a cada `getOffers` llamada. Esta latencia debe ser inferior a `getOffers` Llamar a con la toma de decisiones del lado del servidor, ya que afecta a una CDN ubicada cerca del servidor. Proporcione únicamente el campo &quot;ipAddress&quot; en el objeto Geo en el contexto de la solicitud para que el SDK recupere la geolocalización de la dirección IP del visitante. Si se proporciona cualquier otro campo además de &quot;ipAddress&quot;, la variable [!DNL Target] El SDK no recuperará los metadatos de localización geográfica para su resolución.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
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

### Método de asignación

La siguiente tabla indica qué métodos de asignación son compatibles o no con [!UICONTROL toma de decisiones en el dispositivo].

| Método de asignación | Compatible? |
| --- | --- |
| Manual | Sí |
| [Asignar automáticamente a la mejor experiencia](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | No |
| [Segmentación automática para experiencias personalizadas](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | No |
