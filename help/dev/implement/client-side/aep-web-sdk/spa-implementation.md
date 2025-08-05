---
title: Implementación de aplicación de una sola página para [!DNL Adobe Experience Platform Web SDK]
description: Aprenda a crear una implementación de aplicación de una sola página (SPA) de  [!DNL Adobe Experience Platform Web SDK]usando [!DNL Target].
keywords: target;adobe target;vistas xdm; vistas;aplicaciones de una sola página;SPA;ciclo de vida de SPA;lado del cliente;prueba AB;segmentación de experiencias;XT;VEC
feature: AEP Web SDK
source-git-commit: 9a2c35b2d150638fbda00be866f84d2a6faa4300
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 2%

---


# Implementación de aplicación de una sola página

[!DNL Adobe Experience Platform Web SDK] proporciona funciones enriquecidas que permiten a su empresa ejecutar personalizaciones en tecnologías de próxima generación del lado del cliente, como aplicaciones de una sola página (SPA).

Los sitios web tradicionales utilizaban modelos de navegación &quot;página a página&quot;, también denominados aplicaciones de varias páginas. En estos sitios web, los diseños están estrechamente vinculados a las direcciones URL y el movimiento entre páginas requería una carga de página completa.

Las aplicaciones web modernas, como las aplicaciones de una sola página, han adoptado un modelo que impulsa el uso rápido de la representación de la interfaz de usuario del explorador, que a menudo es independiente de las recargas de página. Estas experiencias se activan mediante interacciones de clientes, como desplazamientos, clics y movimientos del cursor. A medida que los paradigmas de la web moderna evolucionan, la importancia de los eventos genéricos tradicionales, como la carga de páginas, para implementar la personalización y la experimentación, ya no es tanta.

![Diagrama que muestra el ciclo de vida de la SPA comparado con el ciclo de vida de la página tradicional.](/help/dev/implement/client-side/aep-web-sdk/assets/spa-vs-traditional-lifecycle.png)

## Beneficios de [!DNL Experience Platform Web SDK] para SPA

Estas son algunas ventajas de usar [!DNL Adobe Experience Platform Web SDK] para las aplicaciones de una sola página:

* Capacidad de almacenar en caché todas las ofertas de carga de página para reducir varias llamadas al servidor a una sola llamada al servidor.
* Mejore la experiencia del usuario en su sitio, ya que las ofertas se muestran inmediatamente a través de la caché sin el tiempo de retraso introducido por las llamadas tradicionales al servidor.
* Una sola línea de código y configuración de desarrollador único permite a los especialistas en marketing crear y ejecutar actividades [!UICONTROL A/B Test] y [!UICONTROL Experience Targeting] (XT) a través del [!UICONTROL Visual Experience Composer] (VEC) en su SPA.

## Vistas de XDM y aplicaciones de una sola página

El VEC [!UICONTROL Adobe Target] para SPA aprovecha un concepto denominado [!UICONTROL Views]: un grupo lógico de elementos visuales que, juntos, constituyen una experiencia de SPA. Por lo tanto, una aplicación de una sola página puede considerarse como una transición entre vistas (en lugar de las direcciones URL) según las interacciones del usuario. Un [!UICONTROL View] suele representar un sitio completo o elementos visuales agrupados dentro de un sitio.

Para explicar con más detalle qué son las vistas, el siguiente ejemplo utiliza un sitio hipotético de comercio electrónico en línea implementado en [!DNL React] para explorar el ejemplo [!UICONTROL Views].

Después de navegar al sitio principal, una imagen promociona una venta de Pascua, así como los productos más recientes disponibles en el sitio. En este caso, se podría definir un [!UICONTROL View] para toda la pantalla de inicio. Este(a) [!UICONTROL View] podría llamarse simplemente &quot;home&quot;.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

A medida que el cliente se interese más por los productos que vende la empresa, decide hacer clic en el vínculo **Productos**. De forma similar al sitio de inicio, se puede definir todo el sitio de productos como [!UICONTROL View]. Este(a) [!UICONTROL View] podría(n) llamarse &quot;products-all&quot;.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, con todos los productos mostrados.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Dado que [!UICONTROL View] se puede definir como un sitio completo o un grupo de elementos visuales en un sitio. Los cuatro productos mostrados en el sitio de productos podrían agruparse y considerarse como un [!UICONTROL View]. Esta vista podría llamarse &quot;productos&quot;.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, con productos de ejemplo mostrados.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

Cuando el cliente decide hacer clic en el botón **Cargar más** para explorar más productos en el sitio, la dirección URL del sitio web no cambia en este caso. Sin embargo, se puede crear un(a) [!UICONTROL View] aquí para representar solamente la segunda fila de productos que se muestran. El nombre de [!UICONTROL View] podría ser &quot;products-page-2&quot;.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, con productos de ejemplo mostrados en una página adicional.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

El cliente decide adquirir algunos productos en el sitio y pasa a la pantalla de pago. En el sitio de cierre de compra, el cliente tiene la opción de elegir entre envío normal o exprés. Un(a) [!UICONTROL View] puede ser cualquier grupo de elementos visuales en un sitio, por lo que se podría crear un(a) [!UICONTROL View] para las preferencias de envío y llamarse &quot;Preferencias de envío&quot;.

![Imagen de muestra de una página de desprotección de aplicación de una sola página en una ventana del explorador.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

El concepto de [!UICONTROL Views] se puede ampliar mucho más allá de este escenario. Estos escenarios son solo algunos ejemplos de [!UICONTROL Views] que se pueden definir en un sitio.

## Implementando [!UICONTROL XDM Views]

[!UICONTROL XDM Views] se puede aprovechar en [!DNL Target] para permitir que los especialistas en marketing ejecuten pruebas A/B y XT en SPA a través de [!UICONTROL Visual Experience Composer]. Para hacerlo, es necesario realizar los siguientes pasos para completar una configuración de desarrollador única:

1. Instalar [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
2. Determine todos(as) los/las [!UICONTROL XDM Views] de la aplicación de una sola página que desee personalizar.
3. Después de definir [!UICONTROL XDM Views], para entregar actividades A/B o XT VEC, implemente la función `sendEvent()` con `renderDecisions` establecido en `true` y el [!UICONTROL XDM View] correspondiente en su aplicación de una sola página. Se debe pasar [!UICONTROL XDM View] en `xdm.web.webPageDetails.viewName`. Este paso permite a los especialistas en marketing aprovechar [!UICONTROL Visual Experience Composer] para iniciar pruebas A/B y XT para esos XDM.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>En la primera llamada de `sendEvent()`, se recuperarán y almacenarán en caché todos los [!UICONTROL XDM Views] que se deban representar para el usuario final. Las llamadas subsiguientes `sendEvent()` con [!UICONTROL XDM Views] transferidas se leen desde la caché y se procesan sin una llamada al servidor.

## `sendEvent()` ejemplos de funciones

En esta sección se describen tres ejemplos que muestran cómo invocar la función `sendEvent()` en React para un SPA de comercio electrónico hipotético.

### Ejemplo 1: página principal de la prueba A/B

El equipo de marketing desea ejecutar pruebas A/B en toda la página de inicio.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-1.png)

Para ejecutar pruebas A/B en todo el sitio principal, `sendEvent()` debe invocarse con el XDM `viewName` establecido en `home`:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Ejemplo 2: Productos personalizados

El equipo de mercadotecnia desea personalizar la segunda fila de productos cambiando el color de la etiqueta de precio a rojo después de que un usuario haga clic en **Cargar más**.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, que muestra ofertas personalizadas.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
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
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Ejemplo 3: Preferencias de envío de la prueba A/B

El equipo de marketing desea ejecutar una prueba A/B para ver si se cambia el color del botón de azul a rojo cuando se selecciona **Envío exprés**. El equipo cree que este cambio puede mejorar las conversiones (en lugar de mantener el botón de color azul en ambas opciones de envío).

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, con pruebas A/B.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-3.png)

Para personalizar el contenido del sitio según las preferencias de envío que se seleccionen, se puede crear un [!UICONTROL View] para cada preferencia de entrega. Cuando se selecciona **Entrega normal**, el [!UICONTROL View] puede llamarse &quot;checkout-normal&quot;. Si se selecciona **Envío exprés**, el [!UICONTROL View] puede llamarse &quot;checkout-express&quot;.

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
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
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Usar [!UICONTROL Visual Experience Composer] para una SPA

Cuando haya terminado de definir su [!UICONTROL XDM Views] e implementado `sendEvent()` con los [!UICONTROL XDM Views] pasados, el VEC puede detectar estos [!UICONTROL Views] y permitir a los usuarios crear acciones y modificaciones para actividades A/B o XT.

>[!NOTE]
>
>Para usar el VEC para tu SPA, debes instalar y activar la extensión [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome VEC Helper Extension](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension).

### [!UICONTROL Modifications] panel

El panel [!UICONTROL Modifications] captura las acciones creadas para un(a) [!UICONTROL View] en particular. Todas las acciones de [!UICONTROL View] se agrupan en ese(a) [!UICONTROL View].

### Acciones

Al hacer clic en una acción se resalta el elemento del sitio donde se aplica esta acción. Cada acción de VEC creada en un(a) [!UICONTROL View] tiene los iconos siguientes: **Información**, **Editar**, **Clonar**, **Mover** y **Eliminar**. Estos iconos se explican con más detalle en la tabla siguiente.

| Icono | Descripción |
|---|---|
| Información | Muestra los detalles de esta acción. |
| Editar | Permite editar las propiedades de esta acción directamente. |
| Clonar | Clona la acción a uno o más [!UICONTROL Views] que existen en el panel [!UICONTROL Modifications] o a uno o más [!UICONTROL Views] a los que ha navegado en el VEC. La acción no tiene que existir necesariamente en el panel [!UICONTROL Modifications].<br/><br/>**Nota:** Después de realizar una operación de clonación, debe navegar a [!UICONTROL View] en el VEC a través de [!UICONTROL Browse] para ver si la acción clonada era una operación válida. Si la acción no se puede aplicar a [!UICONTROL View], verá un error. |
| Mover   | Mueve la acción a [!UICONTROL Page Load Event] o a cualquier otro [!UICONTROL View] que ya exista en el panel [!UICONTROL Modifications].<br/><br/>**Evento de carga de página:** Todas las acciones correspondientes al evento de carga de página se aplican en la carga inicial de la página web. <br/><br/>**Nota:** Después de realizar una operación de movimiento, debe navegar a [!UICONTROL View] en el VEC a través de [!UICONTROL Browse] para ver si el movimiento era una operación válida. Si la acción no se puede aplicar a [!UICONTROL View], vea un error. |
| Eliminar | Elimina la acción. |

## Uso del VEC para ejemplos de SPA

Esta sección describe tres ejemplos de cómo usar [!UICONTROL Visual Experience Composer] para crear acciones y modificaciones para actividades A/B o XT.

### Ejemplo 1: Actualizar la vista &quot;principal&quot;

Anteriormente en este artículo, se definió un(a) [!UICONTROL View] denominado(a) &quot;home&quot; para todo el sitio principal. Ahora, el equipo de marketing desea actualizar la vista &quot;principal&quot; de las siguientes maneras:

* Cambie los botones **Agregar al carro** y **Me gusta** por un tono más claro de azul. Este cambio debe producirse durante la carga de la página, ya que implica el cambio de componentes del encabezado.
* Cambie la etiqueta **Productos más recientes para 2026** por **Productos de prueba para 2026** y cambie el color del texto a morado.

Para realizar estas actualizaciones en el VEC, seleccione **Componer** y aplique esos cambios a la vista &quot;Inicio&quot;.

![Página de muestra del Compositor de experiencias visuales.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Ejemplo 2: Cambiar etiquetas de producto

Para la &quot;página de productos-2&quot; [!UICONTROL View], el equipo de mercadotecnia desea cambiar la etiqueta de **Precio** a **Precio de venta** y cambiar el color de la etiqueta a rojo.

Para realizar estas actualizaciones en el VEC, se requieren los siguientes pasos:

1. Seleccione **Examinar** en el VEC.
2. Seleccione **Productos** en la barra de navegación superior del sitio.
3. Seleccione **Cargar más** una vez para ver la segunda fila de productos.
4. Seleccione **Componer** en el VEC.
5. Aplique acciones para cambiar la etiqueta de texto a **Precio de venta** y el color a rojo.

![Página de muestra del Compositor de experiencias visuales con etiquetas de producto.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Ejemplo 3: Personalizar el estilo de preferencias de entrega

[!UICONTROL Views] se puede definir en un nivel granular, como un estado o una opción de un botón de opción. Anteriormente en este artículo [!UICONTROL Views] se definieron para las preferencias de envío, &quot;checkout-normal&quot; y &quot;checkout-express&quot;. El equipo de marketing desea cambiar el color del botón a rojo para la vista &quot;checkout-express&quot;.

Para realizar estas actualizaciones en el VEC, se requieren los siguientes pasos:

1. Seleccione **Examinar** en el VEC.
2. Agregar productos al carro de compras en el sitio.
3. Seleccione el icono de carro de compras en la esquina superior derecha del sitio.
4. Seleccione **Finalizar compra**.
5. Seleccione el botón de opción **Envío exprés** en **Preferencias de envío**.
6. Seleccione **Componer** en el VEC.
7. Cambia el color del botón **Pagar** a rojo.

>[!NOTE]
>
>El mensaje &quot;checkout-express&quot; [!UICONTROL View] no aparece en el panel [!UICONTROL Modifications] hasta que se seleccione el botón de opción **Envío exprés**. Esto se debe a que la función `sendEvent()` se ejecuta cuando se selecciona el botón de opción **Envío exprés**, por lo que el VEC no tiene en cuenta el mensaje &quot;checkout-express&quot; [!UICONTROL View] hasta que se selecciona el botón de opción.

![Compositor de experiencias visuales muestra el selector de preferencias de envío.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
