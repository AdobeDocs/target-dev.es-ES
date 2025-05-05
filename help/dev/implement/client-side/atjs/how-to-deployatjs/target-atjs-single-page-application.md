---
keywords: SPA implementación de aplicación de una sola página, implementar aplicación de una sola página, spa, at.js 2.x, at.js, aplicación de una sola página, aplicación de una sola página, spa, implementación de aplicación de una sola página, aplicación de una sola página, aplicación de una sola página, implementación de aplicación de una sola página
description: SPA Aprenda a usar [!DNL Adobe Target] at.js 2.x para implementar [!DNL Target] para aplicaciones de una sola página ().
title: SPA ¿Puedo implementar  [!DNL Target] para aplicaciones de una sola página ()?
feature: Implement Server-side
exl-id: d59d7683-0a63-47a9-bbb5-0fe4a5bb7766
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 58%

---

# Implementación de aplicación de página única

Los sitios web tradicionales funcionaban en modelos de navegación “página a página”, conocidos como aplicaciones de varias páginas, en las que los diseños de sitios web estaban perfectamente asociados a las direcciones URL y las transiciones de una página web a otra requerían la carga de páginas. Las aplicaciones web modernas, como las Aplicaciones de una sola página (SPA), adoptan un modelo que impulsa el uso rápido de la representación de la interfaz de usuario del explorador, que a menudo es independiente de las recargas de página. Estas experiencias suelen desencadenarse mediante interacciones de clientes, como desplazamientos, clics y movimientos del cursor. A medida que los paradigmas de las webs modernas evolucionan, la importancia de los eventos genéricos tradicionales, como la carga de páginas, para implementar la personalización y la experimentación, ya no es tanta.

![Ciclo de vida de página tradicional vs. ciclo de vida de SPA](assets/trad-vs-spa.png)

at.js 2.x proporciona funciones enriquecidas que permiten que su empresa ejecute personalizaciones en tecnologías de próxima generación de lado del cliente. Esta versión se centra en mejorar at.js para tener interacciones armoniosas con las SPA.

Estos son algunos de los beneficios de utilizar at.js 2.x que no están disponibles en versiones anteriores:

* Capacidad de almacenar en caché todas las ofertas de carga de página para reducir varias llamadas al servidor a una sola llamada al servidor.
* Enorme mejora de las experiencias de los usuarios finales en su sitio, ya que las ofertas se muestran inmediatamente a través de la caché sin agotar el tiempo introducido por las llamadas tradicionales al servidor.
* Una sencilla línea de código y configuración de desarrollador único para permitir que sus especialistas en marketing creen y ejecuten actividades A/B y de segmentación de experiencias (XT) a través del VEC en sus SPA.

## [!DNL Adobe Target] vistas y aplicaciones de una sola página

SPA SPA El VEC de [!DNL Adobe Target] para la aprovecha un nuevo concepto llamado Vistas: un grupo lógico de elementos visuales que, juntos, constituyen una experiencia de la. Una SPA puede, por lo tanto, considerarse como una transición entre vistas (en lugar de las direcciones URL) según las interacciones del usuario. Una vista suele representar un sitio completo o elementos visuales agrupados dentro de un sitio.

Para explicar más sobre las vistas, vamos a navegar por este hipotético sitio de comercio electrónico en línea, implementado en React, y a explorar algunas de las vistas de ejemplo. Haga clic en los vínculos siguientes para abrir el sitio en una nueva pestaña del explorador.

**Vínculo: [Sitio principal](https://target.enablementadobe.com/react/demo/#/)**

![página de inicio](assets/home.png)

Si vamos a la página de inicio, podemos ver inmediatamente una imagen promocional de Pascua, así como los productos más recientes que venden en el sitio. En este caso, una vista puede definirse como toda la página de inicio. Es práctico tenerlo en cuenta porque se ampliará en la sección Implementación de [!DNL Adobe Target] vistas, que se muestra a continuación.

**Vínculo: [Sitio Del Producto](https://target.enablementadobe.com/react/demo/#/products)**

![sitio del producto](assets/product-site.png)

Como el producto que vende la empresa nos interesa, decidimos hacer clic en el vínculo Productos. De manera similar a la página de inicio, se puede definir todo el sitio del producto como una vista. Podemos asignar el nombre “productos” a esta vista al igual que el nombre de la ruta en `https://target.enablementadobe.com/react/demo/#/products)`.

![sitio del producto 2](assets/product-site-2.png)

Al principio de esta sección, definimos Vistas como el sitio completo o incluso un grupo de elementos visuales en un determinado sitio. Como mencionamos antes, los cuatro productos mostrados en el sitio también pueden agruparse y considerarse como una vista. Si queremos, podemos ponerle el nombre “productos” a esta vista.

![sitio del producto 3](assets/product-site-3.png)

Decidimos hacer clic en el botón Cargar más para explorar más productos en el sitio. En este caso, la dirección URL del sitio web no cambia. Sin embargo, aquí, una vista puede representar solamente la segunda fila de productos que se muestra arriba. El nombre de la vista puede ser “PRODUCTS-PAGE-2”.

**Vínculo: [Cierre de compra](https://target.enablementadobe.com/react/demo/#/checkout)**

![página de salida](assets/checkout.png)

Como nos gustaron algunos productos mostrados en el sitio, decidimos comprar un par. Ahora, en el sitio de compra se proporcionan algunas opciones para elegir el envío normal o el exprés. Como una vista puede ser cualquier grupo de elementos visuales en un sitio, podemos nombrar esta como “Ver preferencias de envío”.

Además, el concepto de Vistas puede ampliarse mucho más. Si los especialistas en marketing desean personalizar el contenido del sitio según las preferencias de envío que seleccione, se puede crear una vista para cada preferencia de entrega. En este caso, cuando seleccionamos Envío normal, la Vista puede llamarse “Envío normal”. Si se selecciona Envío exprés, la opción Vista puede llamarse “Envío exprés”.

Es posible que los especialistas en marketing deseen ejecutar una prueba A/B para ver si el cambio del color de azul a rojo cuando se selecciona la opción Envío exprés puede mejorar las conversiones en lugar de mantener el botón de color azul en ambas opciones de envío.

## Implementando [!DNL Adobe Target] vistas

SPA Ahora que hemos cubierto lo que son las vistas de [!DNL Adobe Target], podemos aprovechar este concepto en [!DNL Target] para permitir que los especialistas en marketing ejecuten pruebas A/B y XT en los VEC a través de las pruebas de VEC. Esto requiere una configuración de desarrollador única. Vamos a pasar por los pasos para configurar esto.

1. Instalar at.js 2.*x*.

   En primer lugar, es necesario instalar at.js 2.*x*. SPA Esta versión de at.js se desarrolló teniendo en cuenta las necesidades de los usuarios de la plataforma de desarrollo de la plataforma de datos de. SPA Las versiones anteriores de at.js no son compatibles con las vistas [!DNL Adobe Target] y con el VEC para las visitas en tiempo de ejecución de la versión de.

   Descargar at.js 2.*x* a través de la interfaz de usuario [!DNL Adobe Target] ubicada en **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. at.js 2.*x* también se puede implementar mediante etiquetas en [!DNL Adobe Experience Platform].

1. Implementar at.js 2.Función *x*, `[triggerView()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)` en sus sitios.

   SPA Después de definir las Vistas de la vista en la que desea ejecutar una prueba A/B o XT, implemente at.js 2.Función *x* `triggerView()` con las vistas pasadas como parámetro. Esto permite a los especialistas en marketing utilizar el VEC para diseñar y ejecutar las pruebas A/B y XT para esas vistas definidas. Si la función de `triggerView()` no está definida para estas vistas, el VEC no detectará las vistas y, por lo tanto, los especialistas en marketing no podrán utilizar el VEC para diseñar y ejecutar pruebas A/B y XT.

   >[!NOTE]
   >
   >Para admitir vistas en at.js, [viewsEnabled](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#viewsenbabled) debe establecerse en true; de lo contrario, se deshabilita toda la funcionalidad de vista.

   **`adobe.target.triggerView(viewName, options)`**

   | Parámetro | Tipo | ¿Requerido? | Información general | Descripción |
   | --- | --- | --- | --- | --- |
   | Nombre de vista | Cadena | Sí | 1. No hay espacios al final.<br />2. No puede estar vacío.<br />3. El nombre de la vista debe ser único para todas las páginas.<br />4. **Advertencia**: el nombre de la vista no debe comenzar ni finalizar con “`/`”. Esto se debe a que el cliente generalmente extraería el nombre de la vista de la ruta de la URL. Para nosotros, “home” y “`/home`” son diferentes.<br />5. **Advertencia**: la misma vista no debe activarse varias veces con la opción `{page: true}`. | Pase cualquier nombre como tipo de cadena que desee que represente la vista. Este nombre de vista se muestra en el panel **[!UICONTROL Modifications]** del VEC para que los especialistas en marketing creen acciones y ejecuten sus actividades A/B y XT. |
   | opciones | Objeto | No |  |  |
   | opciones > página | Booleano | No |  | **VERDADERO**: el valor predeterminado de la página es verdadero. Cuando `page=true`, las notificaciones se enviarán a los servidores de Edge para incrementar el recuento de impresiones.<br />**FALSO**: Cuando se `page=false`, las notificaciones no se enviarán para incrementar el recuento de impresiones. Debe utilizarse cuando desee volver a procesar un componente en una página con una oferta. |

   SPA Veamos algunos ejemplos de casos de uso sobre la invocación de la función `triggerView()` en React para nuestro hipotético servicio de comercio electrónico

   **Vínculo: [Sitio principal](https://target.enablementadobe.com/react/demo/#/)**

   ![home-react-1](assets/react1.png)

   Como especialistas en marketing, si queremos ejecutar pruebas A/B en todo el sitio principal, es posible que queramos nombrar la vista “home”:

```
 function targetView() {
   var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash

   viewName = viewName || 'home'; // view name cannot be empty

   // Sanitize viewName to get rid of any trailing symbols derived from URL
   if (viewName.startsWith('#') || viewName.startsWith('/')) {
     viewName = viewName.substr(1);
   }

   // Validate if the Target Libraries are available on your website
   if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
     adobe.target.triggerView(viewName);
   }
 }

 // react router v4
 const history = syncHistoryWithStore(createBrowserHistory(), store);
 history.listen(targetView);

 // react router v3
 <Router history={hashHistory} onUpdate={targetView} >
```

**Vínculo: [Sitio De Productos](https://target.enablementadobe.com/react/demo/#/products)**

Ahora, veamos un ejemplo que es un poco más complicado. Digamos que como especialistas en marketing queremos personalizar la segunda fila de los productos cambiando el color de la etiqueta Precio a rojo después de que un usuario haga clic en el botón Cargar más.

![Reacción de productos](assets/react4.png)

```
 function targetView(viewName) {
   // Validate if the Target Libraries are available on your website
   if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
     adobe.target.triggerView(viewName);
   }
 }

 class Products extends Component {
   render() {
     return (
       <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button>
     );
   }

   handleLoadMoreClicked() {
     var page = this.state.page + 1; // assuming page number is derived from component's state
     this.setState({page: page});
     targetView('PRODUCTS-PAGE-' + page);
   }
 }
```

**Vínculo: [Cierre de compra](https://target.enablementadobe.com/react/demo/#/checkout)**

![Reacción de finalización de compra](assets/react6.png)

Si los especialistas en marketing desean personalizar el contenido del sitio según las preferencias de envío que seleccione, se puede crear una vista para cada preferencia de entrega. En este caso, cuando seleccionamos Envío normal, la Vista puede llamarse “Envío normal”. Si se selecciona Envío exprés, la opción Vista puede llamarse “Envío exprés”.

Es posible que los especialistas en marketing deseen ejecutar una prueba A/B para ver si el cambio del color de azul a rojo cuando se selecciona la opción Envío exprés puede mejorar las conversiones en lugar de mantener el botón de color azul en ambas opciones de envío.

```
 function targetView(viewName) {
   // Validate if the Target Libraries are available on your website
   if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
     adobe.target.triggerView(viewName);
   }
 }

 class Checkout extends Component {
   render() {
     return (
       <div onChange={this.onDeliveryPreferenceChanged}>
         <label>
           <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/>
           <span> Normal Delivery (7-10 business days)</span>
         </label>

         <label>
           <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/>
           <span> Express Delivery* (2-3 business days)</span>
         </label>
       </div>
     );
   }
   onDeliveryPreferenceChanged(evt) {
     var selectedPreferenceValue = evt.target.value;
     targetView(selectedPreferenceValue);
   }
 }
```

## Diagramas de sistema de at.js 2.x

Los siguientes diagramas le ayudan a comprender el flujo de trabajo de at.js 2.x con Vistas y cómo esto mejora la integración de SPA. Para obtener una mejor introducción a los conceptos utilizados en at.js 2.x, consulte [Implementación de aplicación de una sola página](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

![Flujo de Target con at.js 2.x](../../assets/system-diagram-atjs-20.png)

| Paso | Detalles |
| --- | --- |
| 1 | La llamada devuelve el ID del Experience Cloud si el usuario se autentica; otra llamada sincroniza el ID del cliente. |
| 2 | La biblioteca de at.js carga de forma sincronizada y oculta el cuerpo del documento.at.js <br /> también se puede cargar de manera asíncrona con una opción de fragmento de ocultamiento previo implementado en la página. |
| 3 | Se solicita una carga de página que incluye todos los parámetros configurados (MCID, SDID y el ID del cliente). |
| 4 | Se ejecutan los scripts de perfiles y se incluyen en el Almacenamiento de perfiles. El Almacenamiento solicita audiencias de la Biblioteca de audiencias que cumplan los requisitos (por ejemplo, audiencias compartidas de Adobe Analytics, Gestión de público, etc.).<br />Se envían los atributos del cliente al Almacenamiento de perfiles en un procesamiento de lotes. |
| 5 | Según los parámetros de la solicitud de la URL y los datos de perfil, [!DNL Target] decide qué actividades y experiencias vuelven al visitante para la página actual y las vistas futuras. |
| 6 | El contenido dirigido se devuelve a la página, incluyendo, de manera opcional, los valores de perfil para una personalización adicional.<br />El contenido dirigido se muestra en la página actual lo más rápido posible y sin parpadeo del contenido predeterminado.<br />Contenido dirigido para vistas que se muestran como resultado de acciones del usuario en una SPA almacenada en caché en el explorador, de modo que se pueda aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas `triggerView()`. |
| 7 | Se envían los datos de Analytics a los servidores de recopilación de datos. |
| 8 | Los datos de destino coinciden con los datos de [!DNL Analytics] mediante el SDID y se procesan en el almacén de informes de [!DNL Analytics].Los datos de <br />Analytics se pueden ver en [!DNL Analytics] y [!DNL Target] a través de [!DNL Analytics] para los informes de [!DNL Target] (A4T). |

Ahora, independientemente de que se implemente `triggerView()` en la SPA, las vistas y acciones se recuperan de la caché y se muestran al usuario sin una llamada al servidor. `triggerView()` también realiza una solicitud de notificaciones al back-end [!DNL Target] para aumentar y registrar los recuentos de impresión.

![Flujo de Target at.js 2.x triggerView](../../assets/atjs-20-triggerview.png)

| Paso | Detalles |
| --- | --- |
| 1 | En la SPA, se llama a `triggerView()` para procesar la vista y aplicar acciones para modificar los elementos visuales. |
| 2 | El contenido dirigido para la vista se lee desde la caché. |
| 3 | El contenido dirigido se muestra lo más rápido posible y sin parpadeo del contenido predeterminado. |
| 4 | La solicitud de notificación se envía al Almacenamiento de perfiles de [!DNL Target] para contar al visitante en la actividad e incrementar las métricas. |
| 5 | Los datos de Analytics se envían a los servidores de recopilación de datos. |
| 6 | Los datos de destino coinciden con los datos de [!DNL Analytics] mediante el SDID y se procesan en el almacén de informes de [!DNL Analytics]. Los datos de [!DNL Analytics] se pueden ver en [!DNL Analytics] y [!DNL Target] mediante los informes de A4T. |

## Compositor de experiencias visuales para aplicaciones de una sola página

Después de completar la instalación de at.js 2.x y de agregar `triggerView()` al sitio, utilice el VEC para ejecutar actividades A/B y XT. Para obtener más información, consulte [Compositor de experiencias visuales de la aplicación de una sola página (SPA)](https://experienceleague.adobe.com/docs/target/using/experiences/spa-visual-experience-composer.html?lang=es).

>[!NOTE]
>
>El VEC para los SPA es realmente el mismo VEC que utiliza en las páginas web normales, pero algunas funcionalidades adicionales están disponibles al abrir una aplicación de página única implementada con `triggerView()`.

## SPA Utilice TriggerView para asegurarse de que A4T funciona correctamente con at.js 2.x y la versión 2.x de la aplicación de datos de usuario de at.js 20100000000000000000000000000000000000000000000000000000000000 0000000000000000000000000000000000000000000000000000000000000000000

Para asegurarse de que [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es) (A4T) funciona correctamente con at.js 2.x, asegúrese de enviar el mismo SDID en la solicitud [!DNL Target] y en la solicitud [!DNL Analytics].

Prácticas recomendadas relacionadas con los SPA:

* Utilice eventos personalizados para notificar que algo interesante sucede en la aplicación
* Active un evento personalizado antes de que la vista empiece a procesarse
* Active un evento personalizado cuando la vista termine de procesarse

at.js 2.x ha agregado una nueva función de API [triggerView()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md). Debe utilizar `triggerView()` para notificar a at.js que una vista comenzará a procesarse.

Para ver cómo combinar eventos personalizados, at.js 2.x y Analytics, veamos un ejemplo. Este ejemplo asume que la página HTML contiene la API de visitante, seguida de at.js 2.x y de AppMeasurement.

Supongamos que existen los siguientes eventos personalizados:

* `at-view-start` - Cuando la vista empieza a procesarse
* `at-view-end` - Cuando la vista termina de procesarse

Para asegurarse de que A4T funciona con at.js 2.x,

El controlador de inicio de vista debería tener un aspecto similar al siguiente:

```jsx {line-numbers="true"}
document.addEventListener("at-view-start", function(e) {
  var visitor = Visitor.getInstance("<your Adobe Org ID>");
  
  visitor.resetState();
  adobe.target.triggerView("<view name>");
});
```

El controlador final de vista debería tener un aspecto similar al siguiente:

```jsx {line-numbers="true"}
document.addEventListener("at-view-end", function(e) {
  // s - is the AppMeasurement tracker object
  s.t();
});
```

>[!NOTE]
>
>Debe activar los eventos `at-view-start` y `at-view-end`. Estos eventos no forman parte de los eventos personalizados de at.js.

Aunque estos ejemplos usan código JavaScript, todo esto se puede simplificar si usa un administrador de etiquetas, como las etiquetas en [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md).

Si se siguen los pasos anteriores, debe tener una solución A4T sólida para los SPA.

## Prácticas recomendadas de implementación

Las API at.js 2.x le permiten personalizar su implementación de [!DNL Target] de muchas maneras, pero es importante seguir el orden correcto de las operaciones durante este proceso.

La siguiente información describe el orden de las operaciones que debe seguir al cargar una aplicación de una sola página por primera vez en un explorador y para cualquier cambio de vista que se produzca posteriormente.

### Orden de las operaciones para la carga inicial de la página {#order}

| Paso  | Acción | Detalles |
| --- | --- | --- |
| 1 | Cargar VisitorAPI JS | Esta biblioteca es responsable de asignar un ECID al visitante. Otras soluciones de Adobe de la página web consumen posteriormente este ID. |
| 2 | Carga de at.js 2.x | at.js 2.x carga todas las API necesarias que utiliza para implementar [!DNL Target] solicitudes y vistas. |
| 3 | Ejecutar solicitud [!DNL Target] | Si tiene una capa de datos, le recomendamos que cargue los datos esenciales que se necesitan para enviar a [!DNL Target] antes de ejecutar la solicitud [!DNL Target]. Esto le permite usar `targetPageParams` para incluir cualquier dato que desee usar como destino.<P>Cuando `pageLoadEnabled` y `viewsEnabled` se establecen como true en [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md), at.js solicita automáticamente todas las ofertas de VEC [!DNL Target] para usted en el paso 2.<P>Tenga en cuenta que `getOffers` también se puede usar para obtener ofertas de VEC después de que se cargue la página. Para ello, asegúrese de que la solicitud incluya `execute>pageLoad` y `prefetch>views` en la llamada de API. |
| 4 | Llamar a `triggerView()` | Dado que la solicitud [!DNL Target] que inició en el paso 3 podría devolver experiencias tanto para la ejecución de la carga de página como para las vistas, asegúrese de llamar a `triggerView()` después de que se devuelva la solicitud [!DNL Target] y termine de aplicar las ofertas a la caché. Debe ejecutar este paso solo una vez por vista. |
| 5 | Llame a la señalización de vista de página [!DNL Analytics] | Esta señalización envía el SDID asociado con los pasos 3 y 4 a [!DNL Analytics] para la vinculación de datos. |
| 6 | Llamar a `triggerView({"page": false})` adicional | SPA Este es un paso opcional para los marcos de trabajo que podrían volver a procesar ciertos componentes de la página sin que se produzca un cambio en la vista. SPA En estas ocasiones, es importante que invoque esta API para asegurarse de que las experiencias de [!DNL Target] se vuelvan a aplicar después de que el marco de trabajo de la haya vuelto a procesar los componentes. SPA Puede ejecutar este paso tantas veces como desee para asegurarse de que las experiencias de [!DNL Target] persistan en las vistas de la. |

### SPA Orden de las operaciones para el cambio de vista de la vista de la (sin recarga de la página completa)

| Paso  | Acción | Detalles |
| --- | --- | --- |
| 1 | Llamar a `visitor.resetState()` | Esta API garantiza que el SDID se vuelva a generar para la nueva vista a medida que se carga. |
| 2 | Actualizar la caché llamando a la API `getOffers()` | Este es un paso opcional a tomar si este cambio de vista tiene el potencial de calificar al visitante actual para más actividades [!DNL Target] o de descalificarlo para actividades. En este punto, también puede optar por enviar datos adicionales a [!DNL Target] para habilitar capacidades de segmentación adicionales. |
| 3 | Llamar a `triggerView()` | Si ha ejecutado el paso 2, debe esperar la solicitud [!DNL Target] y aplicar las ofertas a la caché antes de ejecutar este paso. Debe ejecutar este paso solo una vez por vista. |
| 4 | Llamar a `triggerView()` | Si no ha ejecutado el paso 2, puede ejecutar este paso en cuanto complete el paso 1. Si ha ejecutado los pasos 2 y 3, debe omitir este paso. Debe ejecutar este paso solo una vez por vista. |
| 5 | Llame a la señalización de vista de página [!DNL Analytics] | Esta señalización envía el SDID asociado con los pasos 2, 3 y 4 a [!DNL Analytics] para la vinculación de datos. |
| 6 | Llamar a `triggerView({"page": false})` adicional | SPA Este es un paso opcional para los marcos de trabajo que podrían volver a procesar ciertos componentes de la página sin que se produzca un cambio en la vista. SPA En estas ocasiones, es importante que invoque esta API para asegurarse de que las experiencias de [!DNL Target] se vuelvan a aplicar después de que el marco de trabajo de la haya vuelto a procesar los componentes. SPA Puede ejecutar este paso tantas veces como desee para asegurarse de que las experiencias de [!DNL Target] persistan en las vistas de la. |

## Vídeos de formación

Los vídeos siguientes contienen más información:

### Descripción del funcionamiento de at.js 2.x

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Consulte [Descripción del funcionamiento de at.js 2.x](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html?lang=es) para obtener más información.

### Implementación de at.js 2.x en un SPA

>[!VIDEO](https://video.tv.adobe.com/v/26248/?quality=12)

Consulte [Implementar at.js 2.x de Adobe Target SPA en una aplicación de una sola página ()](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer-for-single-page-applications.html?lang=es) para obtener más información.

### SPA Uso del VEC para la en [!DNL Adobe Target]

>[!VIDEO](https://video.tv.adobe.com/v/26249/?quality=12)

SPA Consulte [Uso del Compositor de experiencias visuales para aplicaciones de una sola página (VEC) en Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer-for-single-page-applications.html?lang=es) para obtener más información.
