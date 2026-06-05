---
keywords: implementación, biblioteca javascript, js, atjs, toma de decisiones en el dispositivo, toma de decisiones en el dispositivo, funciones compatibles, $8
description: Descubra qué funciones son compatibles con [!UICONTROL toma de decisiones en el dispositivo].
title: Qué funciones son compatibles con la toma de decisiones en el dispositivo
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
TQID: https://experienceleague.adobe.com/ummFURb6WnrNCbiQNDtzWmtZq05am9CMn9UXL0SPaXo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 747
ht-degree: 8%

---

# Funciones compatibles con [!UICONTROL toma de decisiones en el dispositivo]

[!DNL Adobe Target] JS SDK ofrece a los clientes la flexibilidad de elegir entre el rendimiento y la actualización de los datos para tomar decisiones. En otras palabras, si la entrega del contenido personalizado más relevante y atractivo a través del aprendizaje automático es lo más importante para usted, se debe realizar una llamada al servidor en directo. Sin embargo, cuando el rendimiento es más crítico, se debe tomar una decisión en el dispositivo y en la memoria. Para que [!UICONTROL la toma de decisiones en el dispositivo] funcione, consulte las siguientes secciones que enumeran las funciones compatibles.

## Tipos de actividades compatibles

La siguiente tabla indica qué [tipos de actividad](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) creados por el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) o el [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) son compatibles o no con [!UICONTROL decisiones en el dispositivo].

| Tipo de actividad | Compatible? |
| --- | --- |
| [Prueba A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Sí |
| [Asignación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | No |
| [Segmentación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | No |
| [Prueba multivariada](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | No |
| [Segmentación de experiencias](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Sí |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | No |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | No |
| [Actividades que usan Analytics for Target] (¿https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | Sí |

## Segmentación de audiencia

La siguiente tabla indica qué reglas de audiencia son compatibles o no con [!UICONTROL decisiones en el dispositivo].

| Regla de audiencia | Compatible? |
| --- | --- |
| [Ubicación geográfica](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Sí<P>Al utilizar la toma de decisiones en el dispositivo, se admiten los siguientes atributos geográficos:<ul><li>País/región</li><li>Ciudad</li><li>Latitud</li><li>Longitud</li></ul> |
| [Red](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | No |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | No |
| [Parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Sí |
| [Sistema operativo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Sí |
| [Páginas del sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Sí |
| [Explorador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Sí |
| [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | No |
| [Fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | No |
| [Lapso de tiempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Sí |
| Audiencias de Adobe Experience Cloud<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager] y [!DNL Adobe Experience Manager]) | No |

### Segmentación geográfica para [!UICONTROL toma de decisiones en el dispositivo]

Para mantener una latencia mínima de [!UICONTROL toma de decisiones en el dispositivo] con audiencias basadas en regiones, Adobe recomienda que proporcione los valores geográficos usted mismo en la llamada a [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Establezca el objeto Geo en el contexto de la solicitud. Esto significa que desde el explorador puede determinar la ubicación de cada visitante. Por ejemplo, puede realizar una búsqueda de IP a geografía mediante un servicio que configure. Algunos proveedores de alojamiento, como Google Cloud, proporcionan esta funcionalidad mediante encabezados personalizados en cada `HttpServletRequest`.

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

Sin embargo, si no puede realizar búsquedas de IP a geografía en su servidor, pero desea realizar [!UICONTROL decisiones en el dispositivo] para [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) solicitudes que contienen audiencias basadas en geografía, esto también se admite. El inconveniente de este enfoque es que utiliza una búsqueda remota de IP a geografía, que agrega latencia a cada llamada de `getOffers`. Esta latencia debe ser menor que una llamada de `getOffers` con toma de decisiones en el lado del servidor, ya que entra en una red de distribución de contenido (CDN) que se encuentra cerca del servidor. Proporcione únicamente el campo &quot;ipAddress&quot; en el objeto Geo en el contexto de la solicitud para que SDK recupere la geolocalización de la dirección IP del visitante. Si se proporciona cualquier otro campo además de &quot;ipAddress&quot;, el SDK [!DNL Target] no recuperará los metadatos de ubicación geográfica para la resolución.

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
