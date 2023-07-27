---
keywords: adobe.target.getOffers, getOffers, getoffers, obtener oferta, at.js, funciones, función, $8
description: Utilice el [!UICONTROL adobe.target.getOffers()] y sus opciones para la función [!DNL Adobe Target] Biblioteca at.js para activar solicitudes y obtener varias [!DNL Target] ofertas. (at.js 2.x)
title: ¿Cómo utilizo el [!UICONTROL adobe.target.getOffers()] ¿Función?
feature: at.js
exl-id: b96a3018-93eb-49e7-9aed-b27bd9ae073a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 64%

---

# [!UICONTROL adobe.target.getOffers()] - at.js 2.x

Esta función le permite recuperar varias ofertas pasando varios mboxes. Además, se pueden recuperar varias ofertas para todas las vistas de actividades activas.

>[!NOTE]
>
>Esta función se introdujo en at.js 2.x. Esta función no está disponible para la at.js versión 1.*x*.

| Clave | Tipo | ¿Requerido? | Descripción |
| --- | --- | --- | --- |
| `consumerId` | Cadena | No | Si no se proporciona, el valor predeterminado es el mbox global del cliente. Esta clave se utiliza para generar el ID de datos suplementario (SDID) utilizado para la integración de A4T.<P>Al utilizar `getOffers()`, cada llamada genera un SDID nuevo. Si tiene varias solicitudes de mbox en la misma página y desea conservar el SDID (de modo que coincida con el SDID de target-global-mbox y el [!DNL Adobe Analytics] SDID), utilice el `consumerId` parámetro.<P>If `getOffers()` incluye tres mboxes (llamados &quot;mbox1&quot;, &quot;mbox2&quot; y &quot;mbox3&quot;), que incluyen: `consumerId: "mbox1, mbox2, mbox3"` en el `getOffers()` llamada. |
| `decisioningMethod` | Cadena | No | &quot;del lado del servidor&quot;, &quot;en el dispositivo&quot;, &quot;híbrido&quot; |
| `request` | Objeto | Sí | Consulte la tabla Solicitudes a continuación. |
| `timeout` | Número | No | Tiempo de espera de la solicitud. Si no se especifica, se usará el tiempo de espera predeterminado en at.js. |

## Solicitud

>[!NOTE]
>
>Consulte la [Documentación de API de envío](/help/dev/implement/delivery-api/overview.md) para obtener información sobre los tipos aceptables para todos los campos enumerados a continuación.

| Nombre del campo | ¿Requerido? | Limitaciones | Descripción |
| --- | --- | --- | --- |
| solicitud > id | No |  | Uno de `tntId`, `thirdPartyId` o `marketingCloudVisitorId` es obligatorio. |
| Solicitud > ID > thirdPartyId | No | Tamaño máximo = 128  |  |  |
| Request > experienceCloud | No |  |  |
| Request > experienceCloud > analytics | No |  | Integración de Adobe Analytics |
| Request > experienceCloud > analytics > logging | No | Se debe implementar lo siguiente en la página:<ul><li>Servicio de ID de visitante</li><li>AppMeasurement.js</li></ul> | Se admiten los siguientes valores:<P>**client_side**: cuando se especifica, se devuelve una carga útil de Analytics al que ha realizado la llamada, que debe utilizarse para enviar a [!UICONTROL Adobe Analytics] a través de [!UICONTROL API de inserción de datos].<P>**server_side**[!DNL Target][!DNL Analytics]: Este es el valor predeterminado en el que el backend de y usará el SDID para unir las llamadas con fines de informes. |
| Solicitud > Captura previa | No |  |  |
| Solicitud > Captura previa > Vistas | No | Recuento máximo 50.<P>Nombre no en blanco.<P>Longitud del nombre `<=` 128.<P>Longitud del valor `<=` 5000.<P>El nombre no debe comenzar con &quot;perfil&quot;.<P>Nombres no permitidos: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | Pase parámetros para utilizarlos para recuperar vistas relevantes en actividades activas. |
| Solicitud > Captura previa > Vistas > profileParameters | No | Recuento máximo 50.<P>Nombre no en blanco.<P>Longitud del nombre `<=` 128.<P>Longitud del valor `<=` 5000.<P>Solo acepta valores de cadena.<P>El nombre no debe comenzar con &quot;perfil&quot;. | Pase parámetros de perfil para utilizarlos para recuperar vistas relevantes en actividades activas. |
| Solicitud > Captura previa > Vistas > Producto | No |  |  |
| Solicitud > Captura previa > Vistas > Producto > Id. | No | No en blanco.<P>tamaño máximo = 128. | Pase los ID de producto para que se utilicen para recuperar vistas relevantes en actividades activas. |
| Solicitud > Captura previa > Vistas > Producto > categoryId | No | No en blanco.<P>tamaño máximo = 128. | Pase los ID de categoría de producto para que se utilicen para recuperar vistas relevantes en las actividades. |
| Solicitud > Captura previa > Vistas > Pedido | No |  |  |
| Solicitud > Captura previa > Vistas > Pedido > Id. | No | Longitud máxima = 250  | Pase los ID de pedido para que se utilicen para recuperar vistas relevantes en actividades activas. |
| Solicitud > Captura previa > Vistas > Pedido > Total | No | Total `>=` 0  | Pase los totales del pedido para que se utilicen para recuperar vistas relevantes en actividades activas. |
| Solicitud > Captura previa > Vistas > Pedido > purchasedProductIds | No | No hay valores en blanco.<P>Longitud máxima de cada valor 50.<P>Concatenado y separado por una coma.<P>Longitud total de ID de producto `<=` 250. | Pase los ID de productos comprados para que se utilicen para recuperar vistas relevantes en actividades activas. |
| Solicitud > Ejecutar | No |  |  |
| Solicitud > Ejecutar > pageLoad | No |  |  |
| Solicitud > Ejecutar > pageLoad > Parámetros | No | Recuento máximo 50.<P>Nombre no en blanco.<P>Longitud del nombre `<=` 128.<P>Longitud del valor `<=` 5000.<P>Solo acepta valores de cadena.<P>El nombre no debe comenzar con &quot;perfil&quot;.<P>Nombres no permitidos: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | Recupere ofertas con parámetros especificados cuando se carga la página. |
| Solicitar > Ejecutar > pageLoad > profileParameters | No | Recuento máximo 50.<P>Nombre no en blanco.<P>Longitud del nombre `<=` 128.<P>Longitud del valor `<=`256.<P>El nombre no debe comenzar con &quot;perfil&quot;.<P>Solo acepta valores de cadena. | Recupere ofertas con parámetros de perfil especificados cuando se carga la página. |
| Solicitar > Ejecutar > pageLoad > Producto | No |  |  |
| Solicitud > Ejecutar > pageLoad > Producto > Id. | No | No en blanco.<P>Tamaño máximo = 128. | Recupere ofertas con ID de productos especificadas cuando se carga la página. |
| Solicitud > Ejecutar > pageLoad > Producto > categoryId | No | No en blanco.<P>Tamaño máximo = 128. | Recupere ofertas con ID de categoría de productos especificadas cuando se carga la página. |
| Solicitar > Ejecutar > pageLoad >Pedido | No |  |  |
| Solicitar > Ejecutar > pageLoad > Pedido > ID | No | Longitud máxima = 250  | Recupere ofertas con ID de pedidos especificados cuando se carga la página. |
| Solicitar > Ejecutar > pageLoad > Pedido > Total | No | `>=` 0  | Recupere ofertas con totales de pedidos especificados cuando se carga la página. |
| Solicitud > Ejecutar > pageLoad > Pedido > purchasedProductIds | No | No hay valores en blanco.<P>Longitud máxima de cada valor 50.<P>Concatenado y separado por una coma.<P>Longitud total de ID de producto `<=` 250. | Recupere ofertas con ID de productos comprados cuando se carga la página. |
| Solicitud > Ejecutar > mboxes | No | Tamaño máximo = 50.<P>No hay elementos nulos. |  |
| Solicitud > Ejecutar > mboxes > mbox | Sí | No en blanco.<P>Sin sufijo &quot;-clicked&quot;.<P>Tamaño máximo = 250.<P>Caracteres permitidos: `'-, ._\/=:;&!@#$%^&*()_+|?~[]{}'` | Nombre del mbox. |
| Solicitud > Ejecutar > mboxes > mbox > Índice | Sí | No es nulo.<P>Único.<P>`>=` 0. | Tenga en cuenta que el índice no representa el orden en que se procesarán los mboxes. Al igual que en una página web con varios mboxes regionales, no se puede especificar el orden en que se procesarán. |
| Solicitud > Ejecutar > mboxes > mbox > Parámetros | No | Recuento máximo = 50.<P>Nombre no en blanco.<P>Longitud del nombre `<=` 128.<P>Solo acepta valores de cadena.<P>Longitud del valor `<=` 5000.<P>El nombre no debe comenzar con &quot;perfil&quot;.<P>Nombres no permitidos: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | Recupere ofertas para un mbox determinado con los parámetros especificados. |
| Solicitud > Ejecutar > mboxes > mbox > profileParameters | No | Recuento máximo = 50.<P>Nombre no en blanco.<P>Longitud del nombre `<=` 128.<P>Solo acepta valores de cadena.<P>Longitud del valor `<=`256.<P>El nombre no debe comenzar con &quot;perfil&quot;. | Recupere ofertas para un mbox determinado con los parámetros de perfil especificados. |
| Solicitud > Ejecutar > mboxes > mbox > Producto | No |  |  |
| Solicitud > Ejecutar > mboxes > mbox > Producto > ID | No | No en blanco.<P>Tamaño máximo = 128. | Recupere ofertas para un mbox determinado con los ID de producto especificados. |
| Solicitud > Ejecutar > mboxes > mbox > Producto > categoryId | No | No en blanco.<P>Tamaño máximo = 128. | Recupere ofertas para un mbox determinado con los ID de categoría de producto especificados. |
| Solicitar > Ejecutar > mboxes > mbox > Pedido | No |  |  |
| Solicitud > Ejecutar > mboxes > mbox > Pedido > ID | No | Longitud máxima = 250  | Recupere ofertas para un mbox determinado con los ID de pedidos especificados. |
| Solicitud > Ejecutar > mboxes > mbox > Pedido > Total | No | `>=` 0  | Recupere ofertas para un mbox determinado con los totales de pedidos especificados. |
| Solicitud > Ejecutar > mboxes > mbox > Pedido > purchasedProductIds | No | No hay valores en blanco.<P>Longitud máxima de cada valor = 50.<P>Concatenado y separado por una coma.<P>Longitud total de ID de producto `<=` 250. | Recupere ofertas para un mbox determinado con los ID de pedido especificada del producto comprado. |

## Llamada [!UICONTROL getOffers()] para todas las vistas

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
      prefetch: {
        views: [{}]
    }
  }
});
```

## Llamada [!UICONTROL getOffers()] para tomar una decisión en el dispositivo

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

## Llamada [!UICONTROL getOffers()] para recuperar las vistas más recientes con los parámetros pasado y de perfil

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    "prefetch": {
      "views": [
        {
          "parameters": {
            "ad": "1"
          },
          "profileParameters": {
            "age": 23
          }
        }
      ]
    }
  }
});
```

## Llamada [!UICONTROL getOffers()] para recuperar mboxes con parámetros y parámetros de perfil pasados.

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    execute: {
      mboxes: [
        {
          index: 0,
          name: "first-mbox"
        },
        {
          index: 1,
          name: "second-mbox",
          parameters: {
            a: 1
          },
          profileParameters: {
            b: 2
          }
        }
      ]
    }
  }
});
```

## Llamada [!UICONTROL getOffers()] para recuperar la carga útil de analytics del lado del cliente

```javascript {line-numbers="true"}
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

**Respuesta**:

```javascript {line-numbers="true"}
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

La carga útil se puede reenviar a [!DNL Adobe Analytics] a través de [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

## Buscar y procesar datos de varios mboxes mediante [!UICONTROL getOffers()] y [!UICONTROL applyOffers()]

at.js 2.x le permite recuperar varios mboxes a través de la API de `[!UICONTROL getOffers()]`. También puede buscar datos para varios mboxes y, después, utilizar `[!UICONTROL applyOffers()]` para representar los datos en diferentes ubicaciones identificadas por un selector de CSS.

El siguiente ejemplo muestra una página HTML sencilla con at.js 2.x implementado:

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>at.js 2.x, multiple selectors and multiple mboxes</title>
  <script src="at.js"></script>
</head>
<body>
  <div id="container1">Default content 1</div>
  
  <div id="container2">Default content 2</div>

  <div id="container3">Default content 3</div>
</body>
</html>
```

Supongamos que tiene tres contenedores que desea modificar a través del contenido recibido de [!DNL Target]. Puede construir una sola solicitud para tres mboxes en los que cada uno tiene contenido que procesar en su respectivo contenedor.

La solicitud y el código de procesamiento pueden tener el siguiente aspecto:

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "mbox1"
        },
        {
          index: 1,
          name: "mbox2"
        },
        {
          index: 2,
          name: "mbox3"
        }
      ]
    }
  }
})
.then(response => {
  // get all mboxes from response
  const mboxes = response.prefetch.mboxes;
  let count = 1;

  mboxes.forEach(el => {
    adobe.target.applyOffers({
      selector: "#container" + count,
      response: {
        prefetch: {
          mboxes: [el]
        }
      }
    });

    count += 1;
  });
});
```

En la sección `request > prefetch > mboxes`, hay tres mboxes diferentes. Si la solicitud se completó correctamente, recibe la respuesta de `response > prefetch > mboxes` para cada mbox. Una vez que tenga las respuestas y las ubicaciones que desee utilizar para la representación, puede invocar a `applyOffers()` para representar el contenido obtenido de [!DNL Target]. En este ejemplo tenemos la siguiente asignación:

* mbox 1 > selector CSS #contenedor 1
* mbox 2 > selector CSS #contenedor 2
* mbox 3 > selector CSS #contenedor 3

Este ejemplo utiliza la variable de recuento para construir los selectores CSS. En una situación real, podría utilizar una asignación diferente entre el selector CSS y el mbox.

Tenga en cuenta que este ejemplo utiliza `prefetch > mboxes`, pero también puede utilizar `execute > mboxes`. Asegúrese de que, si utiliza la crga previa en `getOffers()`, también debe utilizar la carga previa en la invocación de `applyOffers()`.

## Llamada [!UICONTROL getOffers()] para realizar un pageLoad

El siguiente ejemplo muestra cómo realizar un pageLoad mediante [!UICONTROL getOffers()] con at.js 2.*x*  

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {
                parameters: {}
            }
        }
    }
});
```
