---
user-guide-title: Guía para desarrolladores de Adobe Target
breadcrumb-title: Guía para desarrolladores de Target
user-guide-description: Aprenda a adaptar y personalizar la experiencia de sus clientes para que pueda maximizar los ingresos de sus sitios web y móviles, aplicaciones, medios sociales y otros canales digitales.
source-git-commit: b1b0424bfe61fb8b4e88723e6bb2c565d75f8351
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 41%

---


# Guía para desarrolladores de Adobe Target {#developer}

+ [Guía para desarrolladores de Adobe Target](overview.md)
+ Primeros pasos {#implementation}
   + Antes de la implementación {#before-implement}
      + [Antes de la implementación](before-implement/considerations-before-you-implement-target.md)
      + [Preparación para implementar Target](before-implement/prepare-to-implement-target.md)
   + Privacidad y seguridad {#privacy}
      + [Información general sobre la privacidad](before-implement/privacy/privacy.md)
      + [Reglamentos de protección de datos y privacidad](before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)
      + [Cookies de Target](before-implement/privacy/cookie-behavior.md)
      + [Eliminar la cookie de Target](before-implement/privacy/cookie-deleting.md)
      + [Impacto en Target (at.js) de la desaprobación de cookies de terceros](/help/dev/before-implement/privacy/third-party-cookie-deprecation.md)
      + [Políticas de cookies de Google Chrome samesite](before-implement/privacy/google-chrome-samesite-cookie-policies.md)
      + [Prevención inteligente del seguimiento de Apple (ITP) 2.x](before-implement/privacy/apple-itp-2x.md)
      + [Directivas de la política de seguridad de contenido (CSP)](before-implement/privacy/content-security-policy.md)
      + [Inclusión en la lista de permitidos de los nodos de Edge de Target](before-implement/privacy/allowlist-edges.md)
   + Métodos para obtener los datos en Target {#methods}
      + [Información general sobre métodos](before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md)
      + [Parámetros de página](before-implement/methods-to-get-data-into-target/page-parameters.md)
      + [Atributos de perfil en página](before-implement/methods-to-get-data-into-target/in-page-profile-attributes.md)
      + [Atributos de perfil en script](before-implement/methods-to-get-data-into-target/script-profile-attributes.md)
      + [Proveedores de datos](before-implement/methods-to-get-data-into-target/data-providers.md)
      + [API de actualización de perfil en lote](before-implement/methods-to-get-data-into-target/bulk-profile-update-api.md)
      + [API de actualización de perfil único](before-implement/methods-to-get-data-into-target/single-profile-update-api.md)
      + [Atributos del cliente](before-implement/methods-to-get-data-into-target/customer-attributes.md)
      + [Configuración de la API de perfil](before-implement/methods-to-get-data-into-target/profile-api-settings.md)
   + [Información general sobre la seguridad de Target](before-implement/target-security-overview.md)
   + [Navegadores admitidos](before-implement/supported-browsers.md)
   + [Cambios en el cifrado de TLS (Seguridad de capa de transporte)](before-implement/tls-transport-layer-security-encryption.md)
   + [CNAME y Adobe Target](before-implement/implement-cname-support-in-target.md)
+ Implementación del lado del cliente {#client-side}
   + [Información general: implementación de Target para la web del lado del cliente](implement/client-side/overview.md)
   + Implementación de Adobe Experience Platform Web SDK {#aep}
      + [Información general sobre la implementación de Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)
      + [Uso de Adobe Target y Web SDK para la personalización](/help/dev/implement/client-side/aep-web-sdk/target-overview.md)
      + [Implementación de aplicación de una sola página](/help/dev/implement/client-side/aep-web-sdk/spa-implementation.md)
      + [Tokens de respuesta de acceso](/help/dev/implement/client-side/aep-web-sdk/accessing-response-tokens.md)
      + [usar mbox3rdPartyId](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)
      + [Comparación de la biblioteca at.js con Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md)
   + Implementación de at.js {#at-js-implementation}
      + Cómo funciona at.js {#at-js}
         + [Información general sobre la biblioteca JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)
         + [Resumen del funcionamiento de at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
         + [Cómo gestiona at.js el parpadeo](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
         + [Integraciones de at.js](/help/dev/implement/client-side/atjs/how-atjs-works/target-atjs-integrations.md)
      + Cómo implementar at.js {#deploy-at-js}
         + [Cómo implementar at.js](implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)
         + [Implementación Target de mediante Adobe Experience Platform](implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)
         + [Implementación de Target sin un administrador de etiquetas](implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)
         + [Implementación de Target mediante el administrador dinámico de etiquetas (DTM)](implement/client-side/atjs/how-to-deployatjs/implement-target-using-dtm.md)
         + [Implementación de Target para aplicaciones de una sola página (SPA)](implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)
      + Toma de decisiones en el dispositivo {#on-device-decisioning}
         + [Información general sobre la toma de decisiones en el dispositivo](implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md)
         + [Funciones compatibles](implement/client-side/atjs/on-device-decisioning/supported-features.md)
         + [Artefacto de regla](implement/client-side/atjs/on-device-decisioning/rule-artifact.md)
         + [Resolución de problemas](implement/client-side/atjs/on-device-decisioning/troubleshooting-on-device-decisioning.md)
      + Funciones de at.js {#functions-overview}
         + [Información general sobre las funciones de at.js](implement/client-side/atjs/atjs-functions/atjs-functions.md)
         + [adobe.target.getOffer()](implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)
         + [adobe.target.getOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
         + [adobe.target.applyOffer()](implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)
         + [adobe.target.applyOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)
         + [adobe.target.triggerView() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)
         + [adobe.target.trackEvent()](implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
         + [mboxCreate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)
         + [targetGlobalSettings()](implement/client-side/atjs/atjs-functions/targetglobalsettings.md)
         + [mboxDefine() and mboxUpdate(): at.js 1.x](implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)
         + [targetPageParams()](implement/client-side/atjs/atjs-functions/targetpageparams.md)
         + [targetPageParamsAll()](implement/client-side/atjs/atjs-functions/targetpageparamsall.md)
         + [registerExtension(): at.js 1.x](implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)
         + [sendNotifications() - at.js 2.1](implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)
         + [Eventos personalizados de at.js](implement/client-side/atjs/atjs-functions/atjs-custom-events.md)
         + [Depurar at.js mediante Adobe Experience Cloud Debugger](implement/client-side/target-debugging-atjs/target-debugging-atjs.md)
         + [Uso de instancias basadas en la nube con Target](implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md)
      + [Preguntas más frecuentes de at.js](implement/client-side/atjs/target-atjs-faq.md)
      + [Detalles de las versiones de at.js](implement/client-side/atjs/target-atjs-versions.md)
      + [Actualización de at.js 1.x a at.js 2.x](implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)
      + [Cookies de at.js](implement/client-side/atjs/atjs-cookies.md)
   + [User-agent y Client Hints](implement/client-side/atjs/user-agent-and-client-hints.md)
   + Comprender el mbox global {#global-mbox}
      + [Información general sobre mbox global](implement/client-side/atjs/global-mbox/global-mbox-overview.md)
      + [Personalización de un mbox global](implement/client-side/atjs/global-mbox/customize-global-mbox.md)
      + [Uso de un mbox global desde una implementación heredada](implement/client-side/atjs/global-mbox/mbox-global-target-standard.md)
      + [Pase de parámetros a un mbox global](implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)
      + [Preguntas frecuentes sobre mbox global](implement/client-side/atjs/global-mbox/global-mbox-faq.md)
+ Implementación del servidor {#server-side}
   + [Servidor: información general sobre la implementación de Target](implement/server-side/server-side-overview.md)
   + [Introducción a los SDK de Target](implement/server-side/sdk-guides/getting-started/getting-started.md)
   + [Aplicaciones de ejemplo](implement/server-side/sdk-guides/sample-apps/sample-apps.md)
   + [Transición de las API heredadas de Target a Adobe I/O](implement/server-side/transition-from-target-classic-apis.md)
   + Principios básicos {#core-principles}
      + [Resumen de principios básicos](implement/server-side/sdk-guides/core-principles/overview.md)
      + [ID de usuario y agrupamiento](implement/server-side/sdk-guides/core-principles/user-identification-and-bucketing.md)
      + [Segmentación de audiencia](implement/server-side/sdk-guides/core-principles/audience-targeting.md)
      + [Seguimiento de eventos](implement/server-side/sdk-guides/core-principles/event-tracking.md)
      + [Permisos y propiedades de usuario](implement/server-side/sdk-guides/core-principles/user-permissions-and-properties.md)
   + Integración {#integration}
      + [Resumen de integración](implement/server-side/sdk-guides/integration-with-experience-cloud/overview.md)
      + [Servicio de Experience Cloud ID (ECID)](implement/server-side/sdk-guides/integration-with-experience-cloud/ecid.md)
      + [Creación de informes en Analytics for Target (A4T)](implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md)
      + [Segmentos de AAM](implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md)
   + Toma de decisiones en el dispositivo {#on-device-decisioning}
      + [Información general sobre la toma de decisiones en el dispositivo](implement/server-side/sdk-guides/on-device-decisioning/overview.md)
      + Artefacto de regla {#rule-artifact}
         + [Resumen de artefactos de regla](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)
         + [Descargar mediante Adobe Target SDK](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-sdk.md)
         + [Descargar mediante carga útil JSON](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-json.md)
         + [Ejemplo de artefacto de regla](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-example.md)
      + [Ejecución de pruebas A/B con indicadores de funcionalidad](implement/server-side/sdk-guides/on-device-decisioning/execute-ab-tests-with-feature-flags.md)
      + [Ejecución de pruebas de funciones con atributos](implement/server-side/sdk-guides/on-device-decisioning/execute-feature-tests-with-attributes.md)
      + [Administración de despliegues para pruebas de funciones](implement/server-side/sdk-guides/on-device-decisioning/manage-rollouts-for-feature-tests.md)
      + [Entrega de personalización](implement/server-side/sdk-guides/on-device-decisioning/deliver-personalization.md)
      + [Información general sobre funciones compatibles](implement/server-side/sdk-guides/on-device-decisioning/supported-features.md)
      + [Resolución de problemas de la toma de decisiones en el dispositivo](implement/server-side/sdk-guides/on-device-decisioning/troubleshooting.md)
      + [Prácticas recomendadas  ](implement/server-side/sdk-guides/best-practices/best-practices.md)
   + Referencia de SDK de Node.js {#node-js}
      + [Información general sobre Node.js SDK](implement/server-side/node-js/overview.md)
      + [Instalación de Node.js en SDK](implement/server-side/node-js/install-sdk.md)
      + [Inicialice el SDK de Node.js](implement/server-side/node-js/initialize-sdk.md)
      + [Obtener ofertas (Node.js)](implement/server-side/node-js/get-offers.md)
      + [Obtener atributos (Node.js)](implement/server-side/node-js/get-attributes.md)
      + [Enviar notificaciones (Node.js)](implement/server-side/node-js/send-notifications.md)
      + [Eventos de SDK (Node.js)](implement/server-side/node-js/sdk-events.md)
      + [Registrador (Node.js)](implement/server-side/node-js/logger.md)
      + [Configuración de proxy (Node.js)](implement/server-side/node-js/proxy-configuration.md)
   + Referencia de SDK en Java {#java}
      + [Información general sobre Java SDK](implement/server-side/java/overview.md)
      + [Instalación de Java SDK](implement/server-side/java/install-sdk.md)
      + [Inicialización de Java SDK](implement/server-side/java/initialize-sdk.md)
      + [Obtener ofertas (Java)](implement/server-side/java/get-offers.md)
      + [Obtener atributos (Java)](implement/server-side/java/get-attributes.md)
      + [Envío de notificaciones (Java)](implement/server-side/java/send-notifications.md)
      + [Eventos de SDK (Java)](implement/server-side/java/sdk-events.md)
      + [Registrador (Java)](implement/server-side/java/logger.md)
      + [Solicitudes asincrónicas (Java)](implement/server-side/java/asynchronous-requests.md)
      + [Configuración de proxy (Java)](implement/server-side/java/proxy-configuration.md)
      + [Configuración personalizada de cliente HTTP (Java)](implement/server-side/java/custom-http-client.md)
      + [Métodos de utilidad (Java)](implement/server-side/java/utility-methods.md)
   + Referencia de .NET SDK {#net}
      + [Información general sobre .NET SDK](implement/server-side/net/overview.md)
      + [Instalar .Net SDK](implement/server-side/net/install-sdk.md)
      + [Inicializar .NET SDK](implement/server-side/net/initialize-sdk.md)
      + [Obtener ofertas (.NET)](implement/server-side/net/get-offers.md)
      + [Obtener atributos (.NET)](implement/server-side/net/get-attributes.md)
      + [Enviar notificaciones (.NET)](implement/server-side/net/send-notifications.md)
      + [Eventos de SDK (.NET)](implement/server-side/net/sdk-events.md)
      + [Solicitudes asincrónicas (.NET)](implement/server-side/net/asynchronous-requests.md)
   + Referencia de SDK en Python {#python}
      + [Información general sobre Python SDK](implement/server-side/python/overview.md)
      + [Instalación de Python SDK](implement/server-side/python/install-sdk.md)
      + [Inicialización de Python SDK](implement/server-side/python/initialize-sdk.md)
      + [Obtener ofertas (Python)](implement/server-side/python/get-offers.md)
      + [Obtener atributos (Python)](implement/server-side/python/get-attributes.md)
      + [Envío de notificaciones (Python)](implement/server-side/python/send-notifications.md)
      + [Eventos de SDK (Python)](implement/server-side/python/sdk-events.md)
      + [Solicitudes asincrónicas (Python)](implement/server-side/python/asynchronous-requests.md)
      + [Registrador (Python)](implement/server-side/python/logger.md)
+ [Implementación híbrida](implement/hybrid/hybrid-overview.md)
+ Analytics for Target (A4T) con Experience Platform SDK {#a4t}
   + [Registro de Adobe Analytics for Target (A4T) en Experience Platform Web SDK](/help/dev/implement/a4t/overview-a4t.md)
   + [Registro del lado del cliente para datos de A4T en Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
   + [Registro del lado del servidor para datos de A4T en Experience Platform Web SDK](/help/dev/implement/a4t/server-side-a4t.md)
+ [Implementación de Recommendations](implement/recommendations/recommendations.md)
+ [Implementación de Recommendations beta](/help/dev/implement/recommendations/recommendations-beta.md)
+ Implementación de aplicación móvil {#mobile-apps}
   + [Información general sobre Target para aplicaciones móviles](implement/mobile/overview.md)
   + [Vista previa para móviles en Target](implement/mobile/target-mobile-preview.md)
   + [Uso del servicio de ubicación](implement/mobile/use-location-service.md)
   + [Preguntas frecuentes sobre Target para aplicaciones móviles](implement/mobile/mobile-faq.md)
   + [Implementar Target con AEP Mobile SDK en una aplicación nativa con vistas web](/help/dev/implement/mobile/native-app.md)
+ Implementación de correo electrónico {#implement-email}
   + [Correo electrónico: información general sobre la implementación de Target](implement/email/overview.md)
   + [Creación de un AdBox para una imagen](implement/email/testing-content-with-the-adbox.md)
   + [Comprobación de un AdBox de imagen de correo electrónico](implement/email/testing-email-image-adbox.md)
   + [Trabajar con redirectores](implement/email/working-with-redirectors.md)
+ Guías de API {#api}
   + [Resumen de API de Target](/help/dev/before-administer/target-api-overview.md)
   + [Configuración de la autenticación para las API de Target](/help/dev/before-administer/configure-authentication.md)
   + Guía de API de envío {#delivery-api}
      + [Resumen de API de envío](/help/dev/implement/delivery-api/overview.md)
      + [SDK para interactuar con la API de envío](/help/dev/before-implement/delivery-api-overview/sdks.md)
      + [Primeros pasos](/help/dev/before-implement/delivery-api-overview/getting-started.md)
      + [Permisos de usuario (Premium)](/help/dev/before-implement/delivery-api-overview/user-permissions.md)
      + [Identificación de visitantes](/help/dev/before-implement/delivery-api-overview/identifying-visitors.md)
      + [Entrega única o por lotes](/help/dev/before-implement/delivery-api-overview/single-or-batch.md)
      + [Precarga](/help/dev/before-implement/delivery-api-overview/prefetch.md)
      + [Notificaciones](/help/dev/before-implement/delivery-api-overview/notifications.md)
      + [Integración con Experience Cloud](before-implement/delivery-api-overview/integration.md)
      + [Consideraciones y limitaciones conocidas](/help/dev/before-implement/delivery-api-overview/known-limitations.md)
      + [Client Hints](/help/dev/before-implement/delivery-api-overview/client-hints.md)
      + [API de entrega](/help/dev/implement/delivery-api/delivery-api.md)
   + API de administración {#admin-api}
      + [Resumen de API de administración](before-administer/admin-api-overview/admin-api-overview.md)
      + [API de administración de Adobe Target](/help/dev/administer/admin-api/admin-api-overview-new.md)
   + API de perfil {#profile-apis}
      + [Resumen de API de perfiles](/help/dev/administer/profile-api/profiles-api.md)
      + [Recuperación de perfiles](/help/dev/administer/profile-api/profile-fetch.md)
      + [Actualización de perfiles](/help/dev/administer/profile-api/profile-api-overview.md)
      + [API de actualización de perfil único](/help/dev/administer/profile-api/profile-single-api.md)
      + [API de actualización de perfil en lote](/help/dev/administer/profile-api/profile-bulk-api.md)
   + [API de informes](/help/dev/administer/reporting-api/reporting-api.md)
   + API de Recommendations {#recommendations-api}
      + [Resumen de API de Recommendations](before-administer/recs-api/overview.md)
      + [Administración del catálogo con API](before-administer/recs-api/manage-catalog.md)
      + [Administrar criterios personalizados](before-administer/recs-api/manage-custom-criteria.md)
      + [Uso de la API de envío con Recommendations](before-administer/recs-api/fetch-recs-server-side-delivery-api.md)
      + [API de Recommendations](/help/dev/administer/recommendations-api/recommendations-api.md)
   + API de modelos {#models-api}
      + [Información general sobre la API de modelos (Inclusión en la lista de bloqueados)](before-administer/models-api.md)
      + [API de modelos](/help/dev/administer/models-api/models-api-overview.md)
   + [API de Adobe Admin Console](/help/dev/before-implement/delivery-api-overview/adobe-console-api.md)
   + [API de servidor de Adobe Experience Platform Edge Network](/help/dev/before-implement/delivery-api-overview/aep-edge-network-server-api.md)
+ Patrones de implementación {#implementation-patterns}
   + [Información general sobre patrones de implementación](/help/dev/patterns/pattern-overview.md)
   + Patrón de implementación de Recommendations mediante at.js {#atjs}
      + [Patrón de implementación de Recommendations mediante la información general de at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md)
      + [Inicializar SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
      + [Configuración de la recopilación de datos](/help/dev/patterns/recs-atjs/data-collection.md)
      + [Procesar experiencias](/help/dev/patterns/recs-atjs/render-experiences.md)
      + [Notificar al destinatario](/help/dev/patterns/recs-atjs/notify-target.md)