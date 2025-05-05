---
keywords: diagrama del sistema, parpadeo, at.js, implementación, biblioteca javascript, js, atjs, $8
description: Aprenda cómo funciona la biblioteca JavaScript  [!DNL Target]  at.js, incluidos diagramas del sistema para ayudarle a comprender el flujo de trabajo a medida que se cargan las páginas.
title: ¿Cómo funciona la biblioteca Javascript at.js?
feature: at.js
exl-id: 9183797c-857b-4b7f-a573-6bb1d583f7b1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 66%

---

# Cómo funciona at.js

Para implementar [!DNL Adobe Target] del lado del cliente, debe utilizar la biblioteca JavaScript at.js.

En una implementación del lado del cliente de [!DNL Adobe Target], [!DNL Target] envía las experiencias asociadas a una actividad directamente al explorador del cliente. El explorador decide qué experiencia mostrar y lo hace. Con una implementación del lado del cliente, puede utilizar un editor WYSIWYG, el [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es) (VEC) o una interfaz no visual, el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=es), para crear experiencias de prueba y personalización.

## ¿Qué es at.js?

La biblioteca at.js es la biblioteca de implementación para la implementación del lado del cliente de [!DNL Adobe Target]. La biblioteca at.js mejora los tiempos de carga de página en implementaciones web y proporciona mejores opciones de implementación en aplicaciones de una sola página. at.js es la biblioteca de implementación recomendada y se actualiza con frecuencia con nuevas capacidades. Recomendamos que todos los clientes implementen o migren a la [última versión de at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

Para obtener más información, consulte [Bibliotecas de JavaScript de Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=es#libraries).

En la implementación [!DNL Target]que se muestra a continuación, se han implementado las siguientes soluciones de Adobe Experience Cloud: [!DNL Analytics], Target y [!DNL Audience Manager]. Además, se han implementado los siguientes [!DNL Experience Cloud] servicios principales: [!DNL Adobe Experience Platform], [!UICONTROL Audiences] y [!UICONTROL Visitor ID Service].

## ¿Cuál es la diferencia entre los diagramas de flujo de trabajo de at.js 1.*x* y at.js 2.x?

Para obtener más información sobre las diferencias introducidas en 2.O de 1, consulte [Actualización de at.js 1.x a at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md).*x*.

En términos generales, existen un par de diferencias entre las dos versiones:

* at.js 2 no tiene un concepto de solicitud de mbox global sino una solicitud de carga de página. La solicitud de carga de página se puede ver como una solicitud para recuperar contenido que debería aplicarse en la carga inicial de página del sitio web.
* SPA at.js 2.x administra los conceptos de [!UICONTROL Views], que se utilizan para las aplicaciones de una sola página (). at.js 1.*x* no tiene en cuenta este concepto.

## Diagramas de at.js 2.x

SPA Los siguientes diagramas le ayudan a comprender el flujo de trabajo de at.js 2.x con [!UICONTROL Views] y cómo esto mejora la integración de la. Para obtener una mejor introducción a los conceptos utilizados en at.js 2.x, consulte [Implementación de aplicación de una sola página](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Haga clic en la imagen para ampliarla a ancho completo).

![Flujo de Target con at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "Flujo de Target con at.js 2.x"){zoomable="yes"}

| Paso | Detalles |
| --- | --- |
| 1 | La llamada devuelve el [!UICONTROL Experience Cloud ID] si el usuario se autentica, y otra llamada sincroniza el ID del cliente. |
| 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento.<br />at.js también se puede cargar de manera asíncrona con una opción de fragmento de ocultamiento previo implementado en la página. |
| 3 | Se solicita una carga de página que incluye todos los parámetros configurados (MCID, SDID y el ID del cliente). |
| 4 | Se ejecutan los scripts de perfil y se incluyen en [!UICONTROL Profile Store]. Detenervuelve a solicitar audiencias del [!UICONTROL Audience Library] que cumplan los requisitos (por ejemplo, audiencias compartidas de [!DNL Adobe Analytics], [!DNL Audience Manager], etc.).<br />Los atributos del cliente se envían a [!UICONTROL Profile Store] en un procesamiento de lotes. |
| 5 | Según los parámetros de la solicitud de la URL y los datos de perfil, [!DNL Target] decide qué actividades y experiencias vuelven al visitante para la página actual y las vistas futuras. |
| 6 | El contenido dirigido se devuelve a la página, incluyendo, de manera opcional, los valores de perfil para una personalización adicional.<br />El contenido dirigido se muestra en la página actual lo más rápido posible y sin parpadeo del contenido predeterminado.<br />Contenido dirigido para vistas que se muestran como resultado de acciones del usuario en una SPA almacenada en caché en el explorador, de modo que se pueda aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas `triggerView()`. |
| 7 | Los datos de Analytics se han enviado a [!UICONTROL Data Collection] servidores. |
| 8 | Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de [!DNL Analytics].Los datos de <br />[!DNL Analytics] se pueden ver en [!DNL Analytics] y [!DNL Target] mediante informes de (A4T). |

SPA Ahora, dondequiera que `triggerView()` esté implementado en su, [!UICONTROL Views] y las acciones se recuperan de la caché y se muestran al usuario sin una llamada al servidor. `triggerView()` también realiza una solicitud de notificaciones al back-end [!DNL Target] para aumentar y registrar los recuentos de impresión. Para obtener más información sobre at.js para las SPA con vistas, consulte [Implementación de aplicación de una sola página](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Haga clic en la imagen para ampliarla a ancho completo).

![Flujo de Target at.js 2.x triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Flujo de Target at.js 2.x triggerView"){zoomable="yes"}

| Paso | Detalles |
| --- | --- |
| 1 | SPA Se llama a `triggerView()` en el para procesar [!UICONTROL View] y aplicar acciones para modificar elementos visuales. |
| 2 | El contenido dirigido para la vista se lee desde la caché. |
| 3 | El contenido dirigido se muestra lo más rápido posible y sin parpadeo del contenido predeterminado. |
| 4 | La solicitud de notificación se envía a [!DNL Target] [!UICONTROL Profile Store] para contar al visitante en la actividad e incrementar las métricas. |
| 5 | [!DNL Analytics] datos enviados a [!UICONTROL Data Collection Servers]. |
| 6 | Se compararon los datos de [!DNL Target] con los datos de [!DNL Analytics] mediante el SDID y se procesaron en el almacén de informes de [!DNL Analytics]. Los datos de [!DNL Analytics] se pueden ver en [!DNL Analytics] y [!DNL Target] mediante los informes de A4T. |

### Vídeo: Diagrama arquitectónico de at.js 2.x

at.js 2.x mejora la compatibilidad de Adobe Target con las SPA e integra otras soluciones de Experience Cloud. Este vídeo explica cómo se vincula todo.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Consulte [Descripción del funcionamiento de at.js 2.x](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html?lang=es) para obtener más información.

## Diagrama de at.js 1.x

Los siguientes diagramas le ayudan a comprender el flujo de trabajo de at.js 1.x.

(Haga clic en la imagen para ampliarla a ancho completo).

![Flujo de Target at.js 1.x](/help/dev/implement/client-side/assets/target-flow.png "Flujo de Target at.js 1.x"){zoomable="yes"}

| Paso   | Descripción | La llamada | Descripción |
|--- |--- |--- |--- |
| 1 | La llamada devuelve el ID del Experience Cloud (MCID) si el usuario se autentica; otra llamada sincroniza el ID del cliente. | 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento. |
| 3 | Se realiza una solicitud de mbox global que incluye todos los parámetros, MCID, SDID e ID de cliente (opcional) configurados. | 4 | Se ejecutan los scripts de perfiles y se incluyen en el Almacenamiento de perfiles. El Almacenamiento solicita audiencias de la Biblioteca de audiencias que cumplan los requisitos (por ejemplo, audiencias compartidas de Adobe Analytics, Audience Manager, etc.).<br />Se envían los atributos del cliente al Almacenamiento de perfiles en un procesamiento de lotes. |
| 5 | Según la URL, los parámetros de mbox y los datos de perfil, [!DNL Target] decide qué actividades y experiencias vuelven al visitante. | 6 | Se devuelve el contenido dirigido a la página, incluyendo de manera opcional los valores de perfil para una personalización adicional.<br />Se muestra la experiencia lo más rápido posible sin parpadeos del contenido predeterminado. |
| 7 | Se envían los datos de Analytics a los servidores de recopilación de datos. | 8 | Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics.Los datos de <br />Analytics se pueden ver en Analytics y en [!DNL Target] a través de los informes [!UICONTROL Analytics for Target] (A4T). |

### Vídeo: Tutorías: Sugerencias y descripción general de at.js (26 de junio de 2019)

Este vídeo es una grabación de &quot;Horario de oficina&quot;, una iniciativa dirigida por el equipo [!UICONTROL Adobe Customer Care].

* Ventajas de utilizar at.js
* Configuración de at.js
* Control de parpadeo
* Depurar at.js
* Problemas conocidos
* Preguntas más frecuentes

>[!VIDEO](https://video.tv.adobe.com/v/27959/?quality=12)

## Cómo procesa at.js ofertas con contenido HTML

Al procesar ofertas con contenido HTML, at.js aplica el siguiente algoritmo:

1. Las imágenes se cargan previamente (si el contenido HTML tiene etiquetas `<img>`).

1. El contenido HTML se adjunta al nodo DOM.

1. Se ejecutan scripts en línea (código delimitado por etiquetas `<script>`).

1. Los scripts remotos se cargan de forma asíncrona y se ejecutan (etiquetas `<script>` con atributos `src`).

Notas importantes:

* at.js no proporciona garantías en el orden de ejecución del script remoto, ya que estos se cargan de forma asincrónica.
* Los scripts en línea no deberían tener dependencias en scripts remotos, ya que se cargan y ejecutan más adelante.
