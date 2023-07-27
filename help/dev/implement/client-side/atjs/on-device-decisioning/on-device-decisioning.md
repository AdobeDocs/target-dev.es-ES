---
keywords: implementación, biblioteca javascript, js, atjs, toma de decisiones en el dispositivo, toma de decisiones en el dispositivo, at.js, en el dispositivo, en el dispositivo, implementación0
description: Aprenda a realizar [!UICONTROL toma de decisiones en el dispositivo] con la biblioteca at.js
title: ¿Cómo funciona la toma de decisiones en el dispositivo con la biblioteca JavaScript at.js?
feature: at.js
exl-id: bd0e062f-c259-46f3-adba-e380af058ac8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '3689'
ht-degree: 14%

---

# [!UICONTROL Decisiones en el dispositivo] para at.js

A partir de la versión 2.5.0, las ofertas de at.js [!UICONTROL toma de decisiones en el dispositivo]. [!UICONTROL Decisiones en el dispositivo] le permite almacenar en caché su [Prueba A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) y [Segmentación de experiencias](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) en el explorador para realizar la toma de decisiones en memoria sin una solicitud de red de bloqueo a [!DNL Adobe Target] Edge Network.

>[!NOTE]
>
>[!UICONTROL Decisiones en el dispositivo] está disponible tanto para implementaciones del lado del cliente como del lado del servidor. Este artículo describe [!UICONTROL toma de decisiones en el dispositivo] para del lado del cliente. Para obtener información sobre [!UICONTROL toma de decisiones en el dispositivo] para obtener información sobre el lado del servidor, consulte la documentación de implementación del lado del servidor [aquí](../../../server-side/sdk-guides/on-device-decisioning/overview.md).

[!DNL Target] también ofrece la flexibilidad de ofrecer la experiencia más relevante y actualizada de sus actividades de experimentación y personalización impulsadas por el aprendizaje automático (impulsadas por ML) a través de una llamada al servidor en directo. En otras palabras, cuando el rendimiento es más importante, puede elegir utilizar [!UICONTROL toma de decisiones en el dispositivo]. Sin embargo, cuando se necesita la experiencia más relevante, actualizada y basada en ML, se puede realizar una llamada al servidor en su lugar.

## ¿Cuáles son los beneficios de [!UICONTROL toma de decisiones en el dispositivo]?

Las ventajas de [!UICONTROL toma de decisiones en el dispositivo] incluir:

* **Ofrezca experiencias y decisiones increíblemente rápidas.** La agrupación y la toma de decisiones se realizan en la memoria y en el explorador para evitar el bloqueo de solicitudes de red.
* **Mejorar el rendimiento de la aplicación.** Ejecute experimentos y proporcione personalización a sus clientes y usuarios sin poner en riesgo las experiencias de los usuarios finales.
* **Mejore la puntuación de calidad del sitio Google.** Cuando las decisiones se toman en memoria, mejore la puntuación de calidad del sitio Google de su negocio en línea para que los consumidores puedan descubrirlo mejor.
* **Aprenda de los análisis en tiempo real.** Obtenga información sobre el rendimiento de su actividad en tiempo real mediante [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) Informes de (A4T). A4T le permite pivotar su estrategia en momentos críticos.

## Funciones compatibles

El [!DNL Adobe Target] El SDK de JS ofrece a los clientes la flexibilidad de elegir entre el rendimiento y la actualización de los datos para la toma de decisiones. En otras palabras, si la entrega del contenido personalizado más relevante y atractivo a través del aprendizaje automático es lo más importante para usted, se debe realizar una llamada al servidor en directo. Sin embargo, cuando el rendimiento es más crítico, se debe tomar una decisión en el dispositivo y en la memoria. Para [!UICONTROL toma de decisiones en el dispositivo] para funcionar, consulte la lista de funciones compatibles:

* Tipos de actividades. 
* Segmentación de audiencia
* Método de asignación

Para obtener más información, consulte [Funciones compatibles con [!UICONTROL toma de decisiones en el dispositivo]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

## ¿Cómo? [!UICONTROL toma de decisiones en el dispositivo] ¿trabajar?

Al implementar e inicializar at.js con [!UICONTROL toma de decisiones en el dispositivo] habilitado, a [artefacto de regla](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) que incluye su [!UICONTROL toma de decisiones en el dispositivo] para actividades A/B y XT, audiencias y recursos, se descarga desde la CDN de Akamai más cercana a su visitante y se almacena en caché localmente en el explorador del visitante. Cuando se realiza una solicitud desde at.js para recuperar una experiencia, la decisión con respecto a la experiencia que se va a devolver se realiza en memoria, en función de los metadatos codificados en el artefacto de regla en caché.

## Método de toma de decisiones

Con [!UICONTROL toma de decisiones en el dispositivo], [!DNL Target] introduce una nueva configuración denominada Método de toma de decisiones. La configuración Método de toma de decisiones dicta cómo at.js envía sus experiencias. El método de toma de decisiones tiene tres valores:

* Solo del lado del servidor
* Solo en el dispositivo
* Híbrido

### Solo del lado del servidor

Solo del lado del servidor es el método de toma de decisiones predeterminado que se establece por defecto cuando at.js 2.5.0+ se implementa y despliega en las propiedades web.

Usar solo del lado del servidor como configuración predeterminada significa que todas las decisiones se toman en la red perimetral de [!DNL Target], lo que implica una llamada al servidor de bloqueo. Este método puede introducir la latencia incremental, pero también ofrece beneficios importantes, como la posibilidad de aplicar [!DNL Target]Las funciones de aprendizaje automático de que incluyen [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) y [Segmentación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) actividades.

Además, puede mejorar sus experiencias personalizadas utilizando [!DNL Target]El perfil de usuario de, que se mantiene en todas las sesiones y canales, puede proporcionar potentes resultados para su empresa.

Por último, solo del lado del servidor permite utilizar Adobe Experience Cloud y ajustar las audiencias a las que se puede dirigir mediante segmentos de Audience Manager y Adobe Analytics.

El diagrama siguiente ilustra la interacción entre su visitante, el explorador, at.js 2.5.0+, y el [!DNL Adobe Target] Red perimetral. Este diagrama de flujo captura los nuevos visitantes y los visitantes que regresan.

(Haga clic en la imagen para ampliarla a ancho completo).

![Diagrama de flujo solo del lado del servidor](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/server-side-only.png "Diagrama de flujo solo del lado del servidor"){zoomable=&quot;yes&quot;}

La siguiente lista corresponde a los números del diagrama:

| Paso   | Descripción |
| --- | --- |
| 1 | El ID de visitante de Experience Cloud se recupera del [Servicio de identidad de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html?). |
| 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento.<br />   La biblioteca at.js también se puede cargar de forma asíncrona con un fragmento de ocultamiento previo opcional implementado en la página. |
| 3 | La biblioteca at.js oculta el cuerpo para evitar parpadeos. |
| 4 | Se realiza una solicitud de carga de página que incluye todos los parámetros configurados, como (ECID, ID de cliente, parámetros personalizados, perfil de usuario, etc.) |
| 5 | Se ejecutan los scripts de perfiles y se incluyen en el Almacenamiento de perfiles.<br />El Almacenamiento de perfiles solicita audiencias de la Biblioteca de audiencias que cumplan los requisitos (por ejemplo, audiencias compartidas de Adobe Analytics, Adobe Audience Manager, etc.).<br />Se envían los atributos del cliente al Almacenamiento de perfiles en un procesamiento de lotes. |
| 6 | El Almacenamiento de perfiles se utiliza para la calificación de audiencias y el agrupamiento para filtrar actividades. |
| 7 | El contenido resultante se selecciona después de que la experiencia se determine desde la versión activa [!DNL Target] actividades. |
| 8 | La biblioteca at.js oculta los elementos correspondientes de la página que están asociados con la experiencia que se debe procesar. |
| 9 | La biblioteca at.js muestra el cuerpo para que el resto de la página se pueda cargar para que la vea el visitante. |
| 10 | La biblioteca at.js manipula el DOM para procesar la experiencia desde el [!DNL Target] Edge Network. |
| 11 | La experiencia se procesa para el visitante. |
| 12 | Se carga toda la página web. |
| 13 | Se envían los datos de Analytics a los servidores de recopilación de datos. |
| 14 | Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics. Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en [!DNL Target] mediante los informes de [!UICONTROL Analytics for Target] (A4T). |

### Solo en el dispositivo

Solo en el dispositivo es el método de toma de decisiones que debe configurarse en at.js 2.5.0+ cuando [!UICONTROL toma de decisiones en el dispositivo] solo debe usarse en todas las páginas web.

[!UICONTROL Decisiones en el dispositivo] puede ofrecer sus experiencias y actividades de personalización a una velocidad asombrosa, ya que las decisiones se toman a partir de un artefacto de reglas en caché que contiene todas las actividades para las que es apto [!UICONTROL toma de decisiones en el dispositivo].

Para obtener más información sobre las actividades para las que cumplen los requisitos [!UICONTROL toma de decisiones en el dispositivo], consulte [Funciones compatibles con [!UICONTROL toma de decisiones en el dispositivo]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

Este método de toma de decisiones solo debe usarse si el rendimiento es muy crítico en todas las páginas que requieren decisiones de Target. Además, tenga en cuenta que, cuando se selecciona este método de toma de decisiones, las actividades de [!DNL Target] que no cumplen los requisitos para la toma de decisiones en el dispositivo no se entregarán ni ejecutarán.  La biblioteca at.js 2.5.0+ está configurada para buscar solo el artefacto de reglas en caché para tomar decisiones.

El diagrama siguiente ilustra la interacción entre su visitante, el explorador, at.js 2.5.0+ y la CDN de Akamai. La CDN de Akamai almacena en caché el artefacto de reglas para la primera visita del visitante. Para la primera visita a la página de un visitante nuevo, el artefacto de reglas JSON debe descargarse de la CDN de Akamai para almacenarse en la caché local en el explorador del visitante. Una vez descargado el artefacto de reglas JSON, la decisión se toma inmediatamente sin una llamada de red de bloqueo. El siguiente diagrama de flujo captura los nuevos visitantes.

(Haga clic en la imagen para ampliarla a ancho completo).

![Diagrama de flujo solo en el dispositivo](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only.png "Diagrama de flujo solo en el dispositivo"){zoomable=&quot;yes&quot;}

La siguiente lista corresponde a los números del diagrama:

>[!NOTE]
>
>[!DNL Adobe Target] Los servidores de administración clasifican todas sus actividades que cumplen los requisitos para [!UICONTROL toma de decisiones en el dispositivo], genera el artefacto de reglas JSON y lo propaga a la CDN de Akamai. Sus actividades se monitorizan continuamente en busca de actualizaciones para generar un nuevo artefacto de reglas JSON que se propagará a la CDN de Akamai.

| Paso   | Descripción |
| --- | --- |
| 1 | El ID de visitante de Experience Cloud se recupera del [Servicio de identidad de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento.<br />La biblioteca at.js también se puede cargar de forma asíncrona con un fragmento de ocultamiento previo opcional implementado en la página. |
| 3 | La biblioteca at.js oculta el cuerpo para evitar parpadeos. |
| 4 | La biblioteca at.js realiza una solicitud para recuperar el artefacto de regla JSON de la CDN de Akamai más cercana al visitante. |
| 5 | La CDN de Akamai responde con el artefacto de regla JSON. |
| 6 | El artefacto de regla JSON se almacena localmente en caché en el explorador del visitante. |
| 7 | La biblioteca at.js interpreta el artefacto de regla JSON y ejecuta la decisión de recuperar la experiencia y oculta los elementos probados. |
| 8 | La biblioteca at.js muestra el cuerpo para que el resto de la página se pueda cargar para que la vea el visitante. |
| 9 | La biblioteca at.js manipula el DOM para procesar la experiencia desde el artefacto de regla JSON en caché. |
| 10 | La experiencia se procesa para el visitante. |
| 11 | Se carga toda la página web. |
| 12 | Se envían los datos de Analytics a los servidores de recopilación de datos. Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics. Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en [!DNL Target] mediante los informes de [!UICONTROL Analytics for Target] (A4T). |

El diagrama siguiente ilustra la interacción entre el visitante, el explorador, at.js 2.5.0+ y el artefacto de reglas JSON en caché para la visita individual a la página o la visita recurrente posterior del visitante. Dado que el artefacto de reglas JSON ya se almacena en caché y está disponible en el explorador, la decisión se toma inmediatamente sin una llamada de red de bloqueo. Este diagrama de flujo captura la navegación posterior por la página o los visitantes que regresan.

(Haga clic en la imagen para ampliarla a ancho completo).

![Diagrama de flujo solo en el dispositivo para la navegación de páginas subsiguiente y las visitas repetidas](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only-subsequent.png "Diagrama de flujo solo en el dispositivo para la navegación de páginas subsiguiente y las visitas repetidas"){zoomable=&quot;yes&quot;}

La siguiente lista corresponde a los números del diagrama:

>[!NOTE]
>
>[!DNL Adobe Target] Los servidores de administración clasifican todas sus actividades que cumplen los requisitos para [!UICONTROL toma de decisiones en el dispositivo], genera el artefacto de reglas JSON y lo propaga a la CDN de Akamai. Sus actividades se monitorizan continuamente en busca de actualizaciones para generar un nuevo artefacto de reglas JSON que se propagará a la CDN de Akamai.

| Paso   | Descripción |
| --- | --- |
| 1 | El ID de visitante de Experience Cloud se recupera del [Servicio de identidad de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento.<br />La biblioteca at.js también se puede cargar de forma asíncrona con un fragmento de ocultamiento previo opcional implementado en la página. |
| 3 | La biblioteca at.js oculta el cuerpo para evitar parpadeos. |
| 4 | La biblioteca at.js interpreta el artefacto de regla JSON y ejecuta la decisión en la memoria para recuperar la experiencia. |
| 5 | Los elementos probados están ocultos. |
| 6 | La biblioteca at.js muestra el cuerpo para que el resto de la página se pueda cargar para que la vea el visitante. |
| 7 | La biblioteca at.js manipula el DOM para procesar la experiencia desde el artefacto de regla JSON en caché. |
| 8 | La experiencia se procesa para el visitante. |
| 9 | Se carga toda la página web. |
| 10 | Se envían los datos de Analytics a los servidores de recopilación de datos. Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics. Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en [!DNL Target] mediante los informes de [!UICONTROL Analytics for Target] (A4T). |

### Híbrido

Híbrido es el método de toma de decisiones que debe configurarse en at.js 2.5.0+ cuando tanto [!UICONTROL toma de decisiones en el dispositivo] y actividades que requieren una llamada de red al [!DNL Adobe Target] Se debe ejecutar la red perimetral.

Cuando se gestionan ambas [!UICONTROL toma de decisiones en el dispositivo] actividades y actividades del lado del servidor, puede resultar un poco complicado y tedioso pensar en cómo implementar y aprovisionar [!DNL Target] en sus páginas. Con el método de toma de decisiones hibrido, [!DNL Target] sabe cuándo debe realizar una llamada al servidor a la red de Edge para actividades que requieren ejecución del lado del servidor y también cuándo ejecutar únicamente decisiones en el dispositivo.[!DNL Adobe Target]

El artefacto de reglas JSON incluye metadatos para informar a at.js de si un mbox tiene una actividad del lado del servidor en ejecución o una [!UICONTROL toma de decisiones en el dispositivo] actividad. Este método de toma de decisiones garantiza que las actividades que desea que se entreguen rápidamente se realicen mediante [!UICONTROL toma de decisiones en el dispositivo] y para las actividades que requieren una personalización basada en ML más potente, esas actividades se realizan mediante el complemento [!DNL Adobe Target] Red perimetral.

El diagrama siguiente ilustra la interacción entre su visitante, el explorador, at.js 2.5.0+, la CDN de Akamai y la [!DNL Adobe Target] Red perimetral para un nuevo visitante que visita su página por primera vez. La conclusión de este diagrama es que el artefacto de reglas JSON se descarga asincrónicamente mientras que las decisiones se toman a través de [!DNL Adobe Target] Red perimetral.

Este enfoque garantiza que el tamaño del artefacto, que puede incluir muchas actividades, no influya negativamente en la latencia de la decisión. La descarga del artefacto de reglas JSON sincrónicamente y la toma de decisiones a partir de entonces también pueden tener efectos adversos para la latencia y pueden ser incoherentes. Por lo tanto, el método de toma de decisiones híbrido es una recomendación de práctica recomendada para realizar siempre una llamada del lado del servidor para la decisión de un nuevo visitante y, como el artefacto de reglas JSON se almacena en caché en paralelo. Para cualquier visita posterior a la página y visita de retorno, las decisiones se toman desde la caché y en memoria a través del artefacto de reglas JSON.

(Haga clic en la imagen para ampliarla a ancho completo).

![Diagrama de flujo híbrido para un visitante primerizo](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-first-time-visitor.png "Diagrama de flujo híbrido para un visitante primerizo"){zoomable=&quot;yes&quot;}

La siguiente lista corresponde a los números del diagrama:

>[!NOTE]
>
>[!DNL Adobe Target] Los servidores de administración clasifican todas sus actividades que cumplen los requisitos para [!UICONTROL toma de decisiones en el dispositivo], genera el artefacto de reglas JSON y lo propaga a la CDN de Akamai. Sus actividades se monitorizan continuamente en busca de actualizaciones para generar un nuevo artefacto de reglas JSON que se propagará a la CDN de Akamai.

| Paso   | Descripción |
| --- | --- |
| 1 | El ID de visitante de Experience Cloud se recupera del [Servicio de identidad de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento.<br />La biblioteca at.js también se puede cargar de forma asíncrona con un fragmento de ocultamiento previo opcional implementado en la página. |
| 3 | La biblioteca at.js oculta el cuerpo para evitar parpadeos. |
| 4 | Se realiza una solicitud de carga de página al [!DNL Adobe Target] Edge Network, incluidos todos los parámetros configurados como (ECID, ID de cliente, parámetros personalizados, perfil de usuario, etc.). |
| 5 | Al mismo tiempo, at.js realiza una solicitud para recuperar el artefacto de regla JSON de la CDN de Akamai más cercana al visitante. |
| 6 | ([!DNL Adobe Target] Red perimetral) Se ejecutan los scripts de perfil y se incluyen en el almacén de perfiles. El Almacenamiento de perfiles solicita audiencias de la Biblioteca de audiencias que cumplan los requisitos (por ejemplo, audiencias compartidas de Adobe Analytics, Adobe Audience Manager, etc.). |
| 7 | La CDN de Akamai responde con el artefacto de regla JSON. |
| 8 | El Almacenamiento de perfiles se utiliza para la calificación de audiencias y el agrupamiento para filtrar actividades. |
| 9 | El contenido resultante se selecciona después de que la experiencia se determine desde la versión activa [!DNL Target] actividades. |
| 10 | La biblioteca at.js oculta los elementos correspondientes de la página que están asociados con la experiencia que se debe procesar. |
| 11 | La biblioteca at.js muestra el cuerpo para que el resto de la página se pueda cargar para que la vea el visitante. |
| 12 | La biblioteca at.js manipula el DOM para procesar la experiencia desde el [!DNL Target] Edge Network. |
| 13 | La experiencia se procesa para el visitante. |
| 14 | Se carga toda la página web. |
| 15 | Se envían los datos de Analytics a los servidores de recopilación de datos. Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics. Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en [!DNL Target] mediante los informes de [!UICONTROL Analytics for Target] (A4T). |

El diagrama siguiente ilustra la interacción entre el visitante, el explorador, at.js 2.5.0+ y el artefacto de reglas JSON en caché para una navegación de página posterior o una visita recurrente. En este diagrama, concéntrese únicamente en el caso de uso en el que se toma una decisión en el dispositivo para la navegación de páginas o la visita de retorno subsiguientes. Tenga en cuenta que, según qué actividades estén activas para determinadas páginas, se puede realizar una llamada del lado del servidor para ejecutar decisiones del lado del servidor.

(Haga clic en la imagen para ampliarla a ancho completo).

![Diagrama de flujo híbrido para la navegación de páginas subsiguiente y las visitas repetidas](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-subsequent.png "Diagrama de flujo híbrido para la navegación de páginas subsiguiente y las visitas repetidas"){zoomable=&quot;yes&quot;}

La siguiente lista corresponde a los números del diagrama:

>[!NOTE]
>
>[!DNL Adobe Target] Los servidores de administración clasifican todas sus actividades que cumplen los requisitos para [!UICONTROL toma de decisiones en el dispositivo], genera el artefacto de reglas JSON y lo propaga a la CDN de Akamai. Sus actividades se monitorizan continuamente en busca de actualizaciones para generar un nuevo artefacto de reglas JSON que se propagará a la CDN de Akamai.

| Paso   | Descripción |
| --- | --- |
| 1 | El ID de visitante de Experience Cloud se recupera del [Servicio de identidad de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento.<br />La biblioteca at.js también se puede cargar de forma asíncrona con un fragmento de ocultamiento previo opcional implementado en la página. |
| 3 | La biblioteca at.js oculta el cuerpo para evitar parpadeos. |
| 4 | Se realiza una solicitud para recuperar una experiencia. |
| 5 | La biblioteca at.js confirma que el artefacto de regla JSON ya se ha almacenado en caché y ejecuta la decisión en la memoria para recuperar la experiencia. |
| 6 | Los elementos probados están ocultos. |
| 7 | La biblioteca at.js muestra el cuerpo para que el resto de la página se pueda cargar para que la vea el visitante. |
| 8 | La biblioteca at.js manipula el DOM para procesar la experiencia desde el artefacto de regla JSON en caché. |
| 9 | La experiencia se procesa para el visitante. |
| 10 | Se carga toda la página web. |
| 11 | Se envían los datos de Analytics a los servidores de recopilación de datos. Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics. Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en [!DNL Target] mediante los informes de [!UICONTROL Analytics for Target] (A4T). |

## ¿Cómo habilito [!UICONTROL toma de decisiones en el dispositivo]?

[!UICONTROL Decisiones en el dispositivo] está disponible para todos [!DNL Target] clientes que utilizan At.js 2.5.0 o posterior.

Para habilitar [!UICONTROL toma de decisiones en el dispositivo]:

>[!NOTE]
>
>Debe tener el administrador o aprobador [función de usuario](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) para habilitar o deshabilitar la opción Toma de decisiones en el dispositivo.

1. Clic **[!UICONTROL Administration]** > **[!UICONTROL Implementación]** > **[!UICONTROL Detalles de la cuenta]**.
1. En **[!UICONTROL Detalles de la cuenta]**, deslice el **[!UICONTROL Toma de decisiones en el dispositivo]** cambie a la posición &quot;on&quot;.

   ![[!UICONTROL Decisiones en el dispositivo] alternar](assets/on-device-decisioning-toggle.png)

   La opción &quot;Incluir todos los existentes&quot; [!UICONTROL toma de decisiones en el dispositivo] actividades cualificadas en la opción &quot;artefacto&quot; se muestra si activa [!UICONTROL toma de decisiones en el dispositivo].
1. (Condicional) Deslice el botón de alternancia a la posición &quot;on&quot; si desea que todos sus live [!DNL Target] actividades que cumplen los requisitos para [!UICONTROL toma de decisiones en el dispositivo] para que se incluya automáticamente en el artefacto.

   Si deja esta opción desactivada, debe volver a crear y activar cualquier [!UICONTROL toma de decisiones en el dispositivo] actividades para que se incluyan en el artefacto de reglas generadas. En otras palabras, cualquier actividad en estado activo antes de activar la opción Toma de decisiones en el dispositivo no se incluye en el artefacto de reglas.

Después de habilitar la opción Toma de decisiones en el dispositivo, [!DNL Target] comienza a generar y propagar [artefactos de regla](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) para su cliente.

>[!WARNING]
>
>Asegúrese de habilitar la opción antes de inicializar el [!DNL Adobe Target] SDK que utilizar [!UICONTROL toma de decisiones en el dispositivo]. Los artefactos de regla primero deben generarse y propagarse a las CDN de Akamai para [!UICONTROL toma de decisiones en el dispositivo] para trabajar. La propagación puede tardar entre cinco y diez minutos en generarse y propagarse el primer artefacto de regla a la CDN de Akamai.

## ¿Cómo configuro at.js 2.5.0+ para que use [!UICONTROL toma de decisiones en el dispositivo]?

1. Clic **[!UICONTROL Administration]** > **[!UICONTROL Implementación]** > **[!UICONTROL Detalles de la cuenta]**.
1. En **[!UICONTROL Métodos de implementación]** > **[!UICONTROL Método de implementación principal]**, haga clic en **[!UICONTROL Editar]** junto a su versión de at.js (debe ser at.js 2.5.0 o posterior).

   ![Editar configuración del método de implementación principal](assets/main-implementation-method.png)

   >[!WARNING]
   >
   >Antes de cambiar esta configuración predeterminada, póngase en contacto con Atención al cliente para evitar que esto afecte a su implementación actual.

1. Seleccione el método de toma de decisiones deseado:

   * Solo del lado del servidor
   * Solo en el dispositivo
   * Híbrido

   ![Editar el panel de configuración de at.js](assets/global-settings.png)

### Configuración global

Puede configurar un método de toma de decisiones predeterminado para todos los [!DNL Target] decisiones. Los distintos métodos de toma de decisiones son solo del lado del servidor, solo en el dispositivo e híbrido. El método de toma de decisiones seleccionado en la variable [!DNL Target] La IU está configurada en `window.targetGlobalSettings` en el `decisioningMethod` field. Obtenga más información acerca de `decisioningMethod` in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#decisioningmethod).

```javascript {line-numbers="true"}
<head> 
    <script type="text/javascript">

        window.targetGlobalSettings = { 
            clientCode: "yourClientCodeHere", 
            imsOrgId: "imsOrgId@AdobeOrg", 
            decisioningMethod: "on-device"

        }; 
    </script>

    <script type="text/javascript" src="at.js"></script> 
</head>
```

### Configuración personalizada

Si establece la variable `decisioningMethod` in `window.targetGlobalSettings`, pero desea anular la `decisioningMethod` para cada [!DNL Adobe Target] decisión según el caso de uso, puede realizar este procedimiento especificando lo siguiente `decisioningMethod` en at.js2.5.0+ [getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) llamada.

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
});
```

>[!NOTE]
>
>Para utilizar &quot;en el dispositivo&quot; o &quot;híbrido&quot; como método de toma de decisiones en la llamada a getOffers(), asegúrese de que la configuración global tenga `decisioningMethod` como &quot;en el dispositivo&quot; o &quot;híbrido&quot;. La biblioteca at.js 2.5.0 o posterior debe saber si desea descargar y almacenar en caché el artefacto de reglas JSON inmediatamente después de cargarse en la página. Si el método de toma de decisiones para la configuración global se establece en &quot;lado del servidor&quot; y el método de toma de decisiones &quot;en el dispositivo&quot; o &quot;híbrido&quot; se pasa a la llamada getOffers(), at.js 2.5.0+ no tendría el artefacto de regla JSON en la caché para ejecutar sus decisiones en el dispositivo.

### TTL de caché de artefactos

Target representa las actividades para las que cumple los requisitos [!UICONTROL toma de decisiones en el dispositivo] como un artefacto que consta de metadatos, reglas y condiciones. Este artefacto se almacena en caché en la CDN de Akamai. Durante la primera visita del usuario, el explorador del usuario descarga y almacena en caché el artefacto que representa su [!UICONTROL toma de decisiones en el dispositivo] actividades.

En las visitas posteriores al sitio, el explorador comprueba automáticamente si debe descargar una versión más reciente del artefacto. Esta comprobación añade latencia. El TTL Caché de artefactos define el número de minutos que no desea que el explorador compruebe si hay un artefacto actualizado desde la última descarga correcta. Cuanto más largo sea el lapso de tiempo, mejor será el rendimiento. Cuanto más corto sea el lapso de tiempo, mejor será la actualización de los datos, pero al coste de la latencia añadida.

## ¿Cómo sé si una actividad es [!UICONTROL toma de decisiones en el dispositivo] elegible?

Después de crear una actividad que es [!UICONTROL toma de decisiones en el dispositivo] Un elegible, una etiqueta que dice Elegible para la toma de decisiones en el dispositivo, está visible en la página Información general de la actividad.

![Etiqueta elegible para la toma de decisiones en el dispositivo en la página Información general de la actividad.](assets/on-device-decisioning-eligible-label.png)

Esta etiqueta no significa que la actividad se entregue siempre a través de [!UICONTROL toma de decisiones en el dispositivo]. Solo cuando at.js 2.5.0+ está configurado para usar [!UICONTROL toma de decisiones en el dispositivo] ¿esta actividad se ejecutará en el dispositivo? Si at.js 2.5.0+ no está configurado para utilizar en el dispositivo, esta actividad se entregará a través de una llamada al servidor realizada desde at.js.

Puede filtrar para todas las actividades que sean [!UICONTROL toma de decisiones en el dispositivo] apto en la página Actividades a través del filtro Apto para la toma de decisiones en el dispositivo.

![Filtro apto para la toma de decisiones en el dispositivo en la página Actividades.](assets/on-device-decisioning-filter.png)

>[!NOTE]
>
>Después de crear y activar una actividad que es [!UICONTROL toma de decisiones en el dispositivo] Como elegible, puede tardar entre cinco y diez minutos antes de que se incluya en el artefacto de reglas que se genera y propaga al punto de presencias de la CDN de Akamai.

## Resumen de los pasos para garantizar mi [!UICONTROL toma de decisiones en el dispositivo] Las actividades de se entregan a través de At.js 2.5.0+?

1. Acceda a la [!DNL Adobe Target] IU de y navegue hasta **[!UICONTROL Administration]** > **[!UICONTROL Implementación]** > **[!UICONTROL Detalles de cuenta]** para habilitar el **[!UICONTROL Toma de decisiones en el dispositivo]** alternar.
1. Habilite la **[!UICONTROL &quot;Incluir todos los existentes [!UICONTROL toma de decisiones en el dispositivo] actividades calificadas en el artefacto&quot;]** alternar.

   La primera generación de artefactos de reglas JSON puede tardar hasta 10 minutos.

1. Creación y activación de un [tipo de actividad compatible con [!UICONTROL toma de decisiones en el dispositivo]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md)y compruebe que lo es [!UICONTROL toma de decisiones en el dispositivo] elegible.
1. Configure las variables **[!UICONTROL Método de toma de decisiones]** a **[!UICONTROL &quot;Híbrido&quot;]** o **[!UICONTROL &quot;Solo en el dispositivo&quot;]** a través de la interfaz de usuario de configuración de at.js.
1. Descargue e implemente at.js 2.5.0+ en sus páginas.
