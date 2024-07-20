---
keywords: implementar target, implementación, implementar at.js, administrador de etiquetas, toma de decisiones en el dispositivo, en la toma de decisiones en el dispositivo
description: Obtenga información sobre cómo especificar la configuración (detalles de la cuenta, métodos de implementación, etc.) para implementar la biblioteca  [!DNL Adobe Target] at.js sin usar un administrador de etiquetas.
title: ¿Puedo implementar [!DNL Target]  sin un Administrador de etiquetas?
feature: Implement Server-side
exl-id: f675ae21-105d-4aa3-9926-59291f1136b5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 35%

---

# Implementar [!DNL Target] sin un administrador de etiquetas

Información acerca de la implementación de [!DNL Adobe Target] sin usar un administrador de etiquetas o etiquetas en [!DNL Adobe Experience Platform].

>[!NOTE]
>
>Las etiquetas de [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) son el método preferido para implementar [!DNL Target] y la biblioteca de at.js. La siguiente información no es aplicable cuando se usan etiquetas en [!DNL Adobe Experience Platform] para implementar [!DNL Target].

Para acceder a la página Implementación, haga clic en **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

Puede especificar la siguiente configuración en esta página:

* Detalles de la cuenta
* Métodos de implementación
* API de perfil
* Herramientas de depuración
* Privacidad

>[!NOTE]
>
>En lugar de definir la configuración en la interfaz de usuario de [!DNL Target] Standard/Premium, puede anular la configuración de la biblioteca at.js o usar las API de REST. Para obtener más información, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Detalles de la cuenta

Puede ver los siguientes detalles de la cuenta. Esta configuración no se puede cambiar.

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Client Code] | El código de cliente es una secuencia de caracteres específica del cliente que a menudo se requiere al usar las API [!DNL Target]. |
| [!UICONTROL IMS Organization ID] | Este ID vincula la implementación con su cuenta de Adobe Experience Cloud. |
| [!UICONTROL On-Device Decisioning] | Para habilitar la toma de decisiones en el dispositivo, deslice el conmutador a la posición &quot;activado&quot;.<p>La toma de decisiones en el dispositivo le permite almacenar en caché sus campañas A/B y de segmentación de experiencias (XT) en su servidor y realizar la toma de decisiones en memoria con una latencia cercana a cero. Para obtener más información, consulte [Introducción a la toma de decisiones en el dispositivo](../../../server-side/sdk-guides/on-device-decisioning/overview.md). |
| [!UICONTROL Include all existing on-device decisioning qualified activities in the artifact] | (Condicional) Esta opción se muestra si habilita la toma de decisiones en el dispositivo.<p>Deslice el conmutador a la posición &quot;Activado&quot; si desea que todas sus actividades activas de [!DNL Target] que cumplen los requisitos para la toma de decisiones en el dispositivo se incluyan automáticamente en el artefacto.<p>Si deja esta opción desactivada, debe volver a crear y activar cualquier actividad de toma de decisiones en el dispositivo para que se incluya en el artefacto de reglas generadas. |

## Métodos de implementación

En el panel Métodos de implementación se pueden configurar los siguientes ajustes:

### Configuración global

>[!NOTE]
>
>Esta configuración se aplica a todas las bibliotecas .js de [!DNL Target]. Después de realizar cambios en la sección Métodos de implementación, debe descargar la biblioteca y actualizarla en la implementación.

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Page load enabled (Auto-create global mbox)] | Seleccione si quiere incrustar la llamada de mbox global en el archivo at.js para que se active automáticamente cada vez que se cargue la página. |
| [!UICONTROL Global mbox] | Seleccione un nombre para el mbox global. De forma predeterminada, este nombre es target-global-mbox.<p>Pueden utilizarse caracteres especiales, incluido el símbolo &amp;, en los nombres de mbox con at.js. |
| [!UICONTROL Timeout (seconds)] | Si [!DNL Target] no responde con contenido dentro del periodo definido, se agota el tiempo de espera de la llamada del servidor y se muestra el contenido predeterminado. Se siguen realizando llamadas adicionales durante la sesión del visitante. El valor predeterminado es de 5 segundos.<p>La biblioteca at.js utiliza la configuración de tiempo de espera de `XMLHttpRequest`. El tiempo de espera comienza cuando se activa la solicitud y se detiene cuando [!DNL Target] obtiene una respuesta del servidor. Para obtener más información, consulte [XMLHttpRequest.timeout](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout) en Mozilla Developer Network.<p>Si el tiempo de espera especificado se agota antes de recibir una respuesta, se mostrará el contenido predeterminado y el visitante se podrá contar como un participante de una actividad, ya que la recopilación de datos se realizará en el perímetro de [!DNL Target]. Si la solicitud alcanza el límite de [!DNL Target], se contará al visitante.<p>Considere los siguientes puntos a la hora de configurar el tiempo de espera:<ul><li>Si el valor es demasiado bajo, los usuarios podrían ver el contenido predeterminado la mayor parte del tiempo, aunque se cuente al visitante como un participante de la actividad.</li><li>Si el valor es demasiado alto, los visitantes podrían ver áreas negras en la página web o páginas en blanco si oculta el cuerpo durante periodos muy largos.</li></ul>Para comprender mejor cómo funcionan los tiempos de respuesta de mbox, consulte la ficha Red en las herramientas para desarrolladores de su navegador. También puede utilizar herramientas de supervisión del rendimiento web de terceros, como Catchpoint.<p>**Nota**: La configuración de [visitorApiTimeout](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#visitorapitimeout) garantiza que [!DNL Target] no espere a la respuesta de la API del visitante durante demasiado tiempo. Esta configuración y la configuración Tiempo de espera para at.js descrita no se afectan entre sí. |
| [!UICONTROL Profile Lifetime] | Esta opción determina durante cuánto tiempo se almacenan los perfiles de los visitantes. De forma predeterminada, los perfiles se almacenan durante dos semanas. Esta configuración se puede aumentar hasta 90 días.<p>Para cambiar la configuración de Duración del perfil, comuníquese con [Atención al cliente](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C). |

### Método de implementación principal

>[!NOTE]
>
>[!DNL Adobe Target] admite at.js 1.*x* y at.js 2.*x*. Actualice a la actualización más reciente de cualquiera de las versiones principales de at.js para asegurarse de que dispone de una versión compatible.

Para descargar la versión de at.js que desee, haga clic en el botón **Descargar** correspondiente.

Para editar la configuración de at.js, haga clic en **[!UICONTROL Edit]** junto a la versión de at.js que desee.

>[!WARNING]
>
>Antes de cambiar esta configuración predeterminada, comuníquese con [Client Care](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C) para que no afecte a su implementación actual.

Además de la configuración explicada anteriormente, también está disponible la siguiente configuración específica de at.js:

| Configuración | Descripción |
|--- |--- |
| Entre Dominios | Para at.js v1.*x*, especifique si las funcionalidades entre dominios son `disabled` (los exploradores establecen cookies solo en su dominio (cookies de origen), `x only` (los exploradores establecen cookies solo en el dominio de Target) o ambas, seleccionando `enabled` (los exploradores establecen cookies de origen y de terceros). En at.js v2.10 y versiones posteriores, especifique si las funcionalidades entre dominios son `enabled` (los exploradores establecen cookies de origen y de terceros) o `disabled` (los exploradores no establecen cookies de terceros). |
| Encabezado de biblioteca personalizado | Añada código de JavaScript personalizado para incluirlo en la parte superior de la biblioteca. |
| Pie de biblioteca personalizado | Añada código de JavaScript personalizado para incluirlo en la parte inferior de la biblioteca. |

### API de perfil

Habilite o deshabilite la autenticación para actualizaciones en lote mediante API y genere un token de autenticación de perfil.

Para obtener más información, consulte [Configuración de la API del perfil](/help/dev/before-implement/methods-to-get-data-into-target/profile-api-settings.md).

### Herramientas de depuración

Genere un token de autorización para usar las herramientas de depuración avanzadas [!DNL Target]. Haga clic en **[!UICONTROL Generate New Authentication Token]**.

![Generar nuevo token de autenticación](../../../../before-implement/methods-to-get-data-into-target/assets/debugger-auth-token.png)

### Privacidad

Esta configuración le permite usar [!DNL Target] de conformidad con las leyes aplicables sobre privacidad de datos.

Elija la configuración que desee en la lista desplegable Proteger dirección IP del visitante:

* Ofuscación del último octeto
* Confusión de IP completa
* Ninguna

Para obtener más información, consulte [Privacidad](/help/dev/before-implement/privacy/privacy.md).

>[!NOTE]
>
>La opción Compatibilidad con navegadores anteriores estaba disponible en la versión 0.9.3 (y anteriores) de at.js. Esta opción se ha eliminado de la versión 0.9.4 de at.js. Para saber cuáles con los exploradores compatibles con at.js, consulte [Exploradores compatibles](/help/dev/before-implement/supported-browsers.md)<p>Los navegadores anteriores son navegadores más viejos que no admiten completamente CORS (Uso compartido de recursos de origen cruzado). Algunos de estos navegadores son: Internet Explorer antes de la versión 11 y Safari versión 6 y anteriores. Si se deshabilitó la compatibilidad con exploradores anteriores, [!DNL Target] no entregó contenido ni contó visitantes en los informes de estos exploradores. Si esta opción estaba habilitada, se recomienda realizar el control de calidad en los exploradores más antiguos para garantizar una buena experiencia del cliente.

## Descargar at.js

Instrucciones para descargar la biblioteca mediante la interfaz [!DNL Target] o la API de descarga.

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) es el método preferido para implementar [!DNL Target] y la biblioteca de at.js. La siguiente información no es aplicable cuando se usan etiquetas en [!DNL Adobe Experience Platform] para implementar [!DNL Target].
>
>[!DNL Adobe Target] admite at.js 1.*x* y at.js 2.*x*. Actualice a la actualización más reciente de cualquiera de las versiones principales de at.js para asegurarse de que dispone de una versión compatible. Para obtener información detallada sobre los cambios en cada versión de at.js, consulte [Detalles de las versiones de at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

### Descargar at.js mediante la interfaz [!DNL Target]

Para descargar at.js desde la interfaz [!DNL Target]:

1. Haga clic en **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. En la sección Métodos de implementación, haga clic en el botón **[!UICONTROL Download]** junto a la versión de at.js que desee.

### Descargar at.js mediante la API de descarga de [!DNL Target]

Para descargar at.js mediante la API de.

1. Obtenga el código de cliente.

   Su código de cliente está disponible en la parte superior de la página **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** de la interfaz [!DNL Target].

1. Obtenga su número de administrador.

   Cargue esta dirección URL:

   ```
   https://admin.testandtarget.omniture.com/rest/v1/endpoint/<varname>client code</varname>
   ```

   Reemplace `client code` con el código de cliente del paso 1.

   El resultado de cargar esta dirección URL debería parecerse al siguiente ejemplo:

   ```
   { 
     "api": "https://admin6.testandtarget.omniture.com/admin/rest/v1" 
   }
   ```

   En este ejemplo, “6” es el número del administrador.

1. Descargar at.js.

   Cargue esta dirección URL con la siguiente estructura. Al cargar esta URL, se inicia la descarga del archivo at.js personalizado.

   ```
   https://admin<varname>admin number</varname>.testandtarget.omniture.com/admin/rest/v1/libraries/atjs/download?client=<varname>client code</varname>&version=<version number>
   ```

   * Reemplace `admin number` con su número de administrador.
   * Reemplace `client code` con el código de cliente del paso 1.
   * Reemplace `version number` por el número de versión de at.js deseado (por ejemplo, 2.2).

>[!WARNING]
>
>El equipo [!DNL Target] mantiene solo dos versiones de at.js: la actual y la penúltima. Actualice at.js cuando sea posible para garantizar que dispone de una versión compatible. Para obtener información detallada sobre los cambios en cada versión de at.js, consulte [Detalles de las versiones de at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

## Implementación de at.js

at.js debe implementarse en el elemento `<head>` de cada página de su sitio web.

Una implementación típica de [!DNL Target] que no usa un administrador de etiquetas, como las etiquetas en [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md), tiene este aspecto:

```
<!doctype html> 
<html> 
<head> 
    <meta charset="utf-8"> 
    <title>Title of the Page</title> 
    <!--Preconnect and DNS-Prefetch to improve page load time--> 
    <link rel="preconnect" href="//<client code>.tt.omtrdc.net"> 
    <link rel="dns-prefetch" href="//<client code>.tt.omtrdc.net"> 
    <!--/Preconnect and DNS-Prefetch--> 
    <!--Data Layer to enable rich data collection and targeting--> 
    <script> 
        var digitalData = { 
            "page": { 
                "pageInfo": { 
                    "pageName": "Home" 
                } 
            } 
        }; 
    </script> 
    <!--/Data Layer--> 
    <!-- targetPageParams(), targetPageParamsAll(), Data Providers or targetGlobalSettings() functions to enrich the visitor profile or modify the library settings--> 
    <script> 
        targetPageParams = function() { 
            return { 
                "a": 1, 
                "b": 2, 
                "pageName": digitalData.page.pageInfo.pageName, 
                "profile": { 
                    "age": 26, 
                    "country": { 
                        "city": "San Francisco" 
                    } 
                } 
            }; 
        }; 
    </script> 
    <!--/targetPageParams()--> 
 
    <!--jQuery or other helper libraries should be implemented before at.js if you would like to use their methods in Target--> 
    <script src="jquery-3.3.1.min.js"></script> 
    <!--/jQuery--> 
    <!--Target's JavaScript SDK, at.js--> 
    <script src="at.js"></script> 
    <!--/at.js--> 
</head>
<body> 
    The default content of the page 
</body> 
</html>
```

Tenga en cuenta las siguientes notas importantes:

* Debe usarse el tipo de documento HTML5 (por ejemplo, `<!doctype html>`). Los tipos de documento no admitidos o anteriores podrían ocasionar que [!DNL Target] no pueda realizar una solicitud.
* Conexión previa y Recuperación previa son opciones que pueden ayudar a que sus páginas web se carguen más rápido. Si usa estas configuraciones, asegúrese de reemplazar `<client code>` por su propio código de cliente, que puede obtener de la página **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
* Si tiene una capa de datos es óptimo definir la mayor cantidad posible en el `<head>` de sus páginas antes de que se cargue at.js. Esta ubicación proporciona la máxima capacidad para utilizar esta información en [!DNL Target] para la personalización.
* Las funciones especiales de [!DNL Target], como `targetPageParams()`, `targetPageParamsAll()`, proveedores de datos y `targetGlobalSettings()` deben definirse después de la capa de datos y antes de que se cargue at.js. Alternativamente, estas funciones podrían guardarse en la sección Encabezado de biblioteca de la página Editar configuración de at.js y guardarse como parte de la propia biblioteca de at.js. Para obtener más información sobre estas funciones, consulte [funciones de at.js](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).
* Si usa las bibliotecas de ayuda de JavaScript, como jQuery, inclúyalas antes de [!DNL Target] para poder usar su sintaxis y sus métodos al crear experiencias de [!DNL Target].
* Incluya at.js en el `<head>` de sus páginas.

## Seguimiento de conversiones

El mbox de confirmación de pedido registra los detalles de los pedidos que se realizan en su sitio web y permite generar informes según los ingresos y los pedidos. El mbox de confirmación de pedido también puede realizar algoritmos de recomendaciones, como “Las personas que compraron el producto X también han comprado el producto Y”.

>[!NOTE]
>
>Si los usuarios realizan compras en su sitio web, Adobe recomienda implementar un mbox de confirmación de pedido aunque use los informes de Analytics para [!DNL Target] (A4T).

1. En la página de detalles del pedido, inserte el script de mbox siguiendo el modelo que aparece a continuación.
1. Reemplace las PALABRAS EN MAYÚSCULAS por valores dinámicos o estáticos del catálogo.

   >[!TIP]
   >
   >También puede pasar información de pedidos a cualquier mbox (no necesita llamarse `orderConfirmPage`). De igual modo, es posible pasar información de pedido a varios mbox dentro de la misma campaña.

   ```
   <script type="text/javascript"> 
   adobe.target.trackEvent({ 
       "mbox": "orderConfirmPage", 
       "params":{  
           "orderId": "ORDER ID FROM YOUR ORDER PAGE",  
           "orderTotal": "ORDER TOTAL FROM YOUR ORDER PAGE",  
           "productPurchasedId": "PRODUCT ID FROM YOUR ORDER PAGE, PRODUCT ID2, PRODUCT ID3"  
       } 
   }); 
   </script> 
   ```

>[!NOTE]
>
>En el mbox de confirmación de pedido, utilice la delimitación por comas para separar varios ID de producto.

El mbox de confirmación de pedido utiliza los siguientes parámetros:

| Parámetro | Descripción |
|--- |--- |
| orderId | Valor único para identificar un pedido de recuento de conversión.<p>El `orderId` debe ser único. Los pedidos duplicados se ignoran en los informes. |
| orderTotal | Valor monetario de la compra.<p>No pase el símbolo de moneda. Use un punto (no una coma) para indicar valores decimales. |
| productPurchasedId (opcional) | Lista de ID de productos comprados en el pedido, separados por comas.<p>Estos ID de producto se muestran en el informe de auditoría para admitir análisis de informes adicionales. |
