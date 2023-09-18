---
title: Inicializar SDK
description: Asegúrese de que siguen todos los pasos necesarios para cargar el [!DNL Adobe Target] La biblioteca JavaScript at.js se ejecuta en la secuencia correcta.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: f2587af68a76eb700378076ad9f20844061164ae
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 8%

---

# Inicializar SDK

Siga los pasos de la *Inicializar SDK* para asegurarse de que todas las tareas necesarias para cargar el [!DNL Adobe Target] La biblioteca JavaScript at.js se ejecuta en la secuencia correcta.

>[!TIP]
>
>Haga clic en las imágenes de este tema para expandirlas a pantalla completa.

## Inicializar diagrama de SDK {#diagram}

En el caso de las aplicaciones de varias páginas, este flujo se produce cada vez que la página se vuelve a cargar o el visitante navega a una nueva página del sitio web.

Los números de paso de la siguiente ilustración corresponden a las secciones siguientes.

![Inicializar diagrama de SDK](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Haga clic en los siguientes vínculos para desplazarse a las secciones deseadas:

* [1.1: cargar el SDK de la API de visitante](#load)
* [1.2: Establecer el ID de cliente](#set)
* [1.3: Configurar la solicitud automática de carga de página](#automatic)
* [1.4: Configurar la gestión de parpadeos](#flicker)
* [1.5: Configurar asignación de datos](#data-mapping)
* [1.6: Promoción](#promotion)
* [1.7: Criterios basados en el carro de compras](#cart)
* [1.8: Criterios basados en popularidad](#popularity)
* [1.9: Criterios basados en elementos](#item)
* [1.10: Criterios basados en el usuario](#user)
* [1.11: Criterios personalizados](#custom)
* [1.12: Proporcionar atributos utilizados en las reglas de inclusión](#inclusion)
* [1.13: Proporcionar excludedIds](#exclude)
* [1.14: Pasar el parámetro entity.event.detailsOnly=true](#true)
* [1.15: Configurar la asignación de datos remotos](#remote)
* [1.16: cargar at.js](#web)

## 1.1: cargar el SDK de la API de visitante {#load}

Este paso ayuda a garantizar que la variable `VisitorAPI.js` La biblioteca de se carga, configura e inicializa correctamente.

+++Ver detalles

![Cargar diagrama del SDK de API de visitante](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* Para utilizar el servicio de ID/API de visitante, su empresa debe estar habilitada para [!DNL Adobe Experience Cloud] y tienen un [!UICONTROL ID de organización]. Para obtener más información, consulte [Requisitos del Experience Cloud: ID de organización](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} en el *Ayuda del servicio de identidad* guía.
* Necesita el `VisitorAPI.js` archivo. Ya debería tener este archivo si tiene [!DNL Adobe Analytics] implementado. Este archivo también se puede agregar a través de la variable [[!DNL Adobe Experience Platform] extensión de etiquetas](https://experienceleague.adobe.com/docs/tags.html){target=_blank} or can be downloaded from the [Adobe Analytics Code Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}.

**Configure y consulte VisitorAPI.js**

Para obtener más información, consulte [Implementación del servicio de Experience Cloud para Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Lecturas**

* [Introducción al servicio de identidad del Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [Acerca del servicio de ID](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies y el servicio de Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Solicitud y configuración de ID con el servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Conceptos básicos de sincronización de ID y tasas de coincidencia](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Acciones**

* Incrustar el `VisitorAPI.js` en sus páginas web.
* Lea más información sobre [configuraciones disponibles para el servicio API/ID de visitante](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* Después del `VisitorAPI.js` cuando se cargue el archivo, utilice el `Visitor.getInstance` para inicializar con las configuraciones necesarias.
* Familiarícese con las [métodos disponibles](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.2: Establecer el ID de cliente {#set}

Este paso ayuda a garantizar que los ID conocidos de los visitantes (ID de CRM, ID de usuario, etc.) estén vinculados al ID anónimo de [!DNL Adobe] para la personalización entre dispositivos.

+++Ver detalles

![Establecimiento del ID de cliente](/help/dev/patterns/recs-atjs/assets/set-customer-id.png){width="400" zoomable="yes"}

**Requisitos previos**

* El ID conocido de los visitantes debe estar disponible en la capa de datos.

**Establecimiento del ID de cliente**
Para obtener más información, consulte [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Lecturas**

* [Sincronización de perfiles en tiempo real para mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Acciones**

* Uso `visitor.setCustomerIDs` para establecer el ID conocido del visitante.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.3: Configurar la solicitud automática de carga de página {#automatic}

Este paso permite que at.js recupere todas las experiencias que se deben procesar en la página al cargar el archivo de biblioteca JavaScript at.js.

+++Ver detalles

![Configurar la solicitud automática de carga de página](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request.png){width="400" zoomable="yes"}

**Requisitos previos**

* No todos los datos de la capa de datos deben enviarse a [!DNL Target]. Consulte con su equipo empresarial (equipo de marketing digital) para determinar qué datos son valiosos para la experimentación, la optimización y la personalización. Solo se deben enviar estos datos a [!DNL Target].
* Asegúrese de no enviar ningún dato de información de identificación personal (PII) a [!DNL Target].

**Configurar la solicitud automática de carga de página**

Para obtener más información, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Lecturas**

Obtenga información acerca de `pageLoadEnabled` configuración en [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Acciones**

* Modifique la `window.targetGlobalSettings` para habilitar solicitudes automáticas de carga de página.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.4: Configurar la gestión de parpadeos {#flicker}

Este paso ayuda a garantizar que no haya parpadeo en la página al enviar experiencias.

+++Ver detalles

![Configurar diagrama de control de parpadeo](/help/dev/patterns/recs-atjs/assets/flicker-handling.png){width="400" zoomable="yes"}

**Requisitos previos**

* Hable con el equipo responsable del rendimiento de la página web sobre los pros y los contras de controlar el parpadeo mediante el método predeterminado utilizado por at.js. Puede buscar patrones de diseño que le permitan utilizar una solución personalizada de control de parpadeo, como la animación del cargador. Si no encuentra ningún patrón, puede solicitar uno nuevo.

**Configuración del control de parpadeo**

Para obtener más información, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Configuración `bodyHidingEnabled` hasta `true` oculta el cuerpo completo de la página mientras la solicitud de carga de página está en curso. Si no ha habilitado la solicitud automática de carga de página por algún motivo (por ejemplo, si los datos no están listos más adelante), es mejor establecer esta configuración en `false`.

Si tiene deshabilitado `bodyHidingEnabled` dado que no desea activar APLR y desea activar la solicitud de página más adelante, o no necesita gestionar el parpadeo, debe implementar su propia gestión de parpadeo. Puede controlar el parpadeo de dos formas: ocultando las secciones en prueba o mostrando un pulsador en las secciones en prueba.

**Lecturas**

* [Cómo gestiona at.js el parpadeo](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Obtenga información sobre los objetos bodyHiddenStyle y bodyHidingEnabled en [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Acciones**

* Modifique la `window.targetGlobalSettings` objeto que se va a establecer `bodyHiddenStyle` y `bodyHidingEnabled`.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.5: Configurar asignación de datos {#data-mapping}

Este paso ayuda a garantizar que todos los datos que se deben enviar a [!DNL Target] está configurado.

+++Ver detalles

![Diagrama de asignación de datos](/help/dev/patterns/recs-atjs/assets/data-mapping.png){width="400" zoomable="yes"}

**Requisitos previos**

* La capa de datos debe estar lista con todos los datos que deben enviarse a [!DNL Target].
* Recommendations: enriquecer perfil.
   * Aprobado `entity.id` para capturar datos de artículos y criterios vistos recientemente según criterios basados en el último producto visto.
   * Aprobado `entity.id` para recopilar datos para los criterios de popularidad basados en la categoría favorita.
   * Pase el atributo de perfil si los criterios personalizados se basan en él o se utilizan en el filtrado de reglas de inclusión en cualquier criterio.
* Recommendations: ingerir datos de productos.
   * Se pueden pasar otros parámetros de entidad (reservados y personalizados) para introducir o actualizar el catálogo de productos en [!DNL Recommendations].
   * El catálogo de productos también se puede actualizar utilizando fuentes de entidad utilizando [!DNL Target] IU o API.

**Asignación de datos a[!DNL Target]**

Para obtener más información, consulte [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lecturas**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planificar e implementar Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Configurar el catálogo de Recommendations](/help/dev/implement/recommendations/recommendations.md)

**Acciones**

* Utilice el `targetPageParams()` para establecer todos los datos necesarios que deben enviarse a [!DNL Target].

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.6: Promoción {#promotion}

Añada elementos promocionados y controle su ubicación en su [!DNL Target Recommendations] [diseños](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Ver detalles

**Opciones disponibles**

* Promocionar por ID
* [Promocionar por colección](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promocionar por atributo](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Parámetros de entidad obligatorios**

* El atributo de elemento de la promoción debe pasarse al utilizar la opción &quot;promocionar por atributo&quot;.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.7: Criterios basados en el carro de compras {#cart}

Haga recomendaciones basadas en el contenido del carro de compras del usuario.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Los ususarios que vieron estos, vieron aquellos]
* [!UICONTROL Los ususarios que vieron esto, compraron aquello.]
* [!UICONTROL Los ususarios que compraron estos, compraron aquellos]

**Parámetros de entidad obligatorios**

* cartIds

**Lecturas**

* [Basado en el carro](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.8: Criterios basados en popularidad {#popularity}

Haga recomendaciones basadas en la popularidad general de un elemento en el sitio o en la popularidad de elementos dentro de la categoría, marca, género, etc. favoritos o más vistos de un usuario.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Más visitados en todo el sitio]
* [!UICONTROL Más visitados por categoría]
* [!UICONTROL Más visitados por atributo de artículo]
* [!UICONTROL Principales vendedores en todo el sitio]
* [!UICONTROL Principales vendedores por categoría]
* [!UICONTROL Principales vendedores por atributo de artículo]
* [!UICONTROL Superior por métrica de Analytics]

**Parámetros de entidad obligatorios**

* `entity.categoryId` o el atributo de artículo para la popularidad basada en si los criterios se basan en el artículo actual o en el atributo de artículo.
* No se debe pasar nada para los más visitados/más vendidos en el sitio.

**Lecturas**

* [Basado en popularidad](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.9: Criterios basados en elementos {#item}

Haga recomendaciones basadas en la búsqueda de artículos similares a los que el usuario está viendo o ha visto recientemente.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Los usuarios que vieron esto, vieron aquello.]
* [!UICONTROL Los usuarios que vieron esto, compraron aquello.]
* [!UICONTROL Los usuarios que compraron esto, compraron aquello.]
* [!UICONTROL Artículos con atributos similares]

**Parámetros de entidad obligatorios**

* `entity.id` o cualquier atributo de perfil utilizado como clave

**Lecturas**

* [Basado en elementos](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.10: Criterios basados en el usuario {#user}

Haga recomendaciones basadas en el comportamiento del usuario.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Artículos vistos recientemente. ]
* [!UICONTROL Recomendado para usted]

**Parámetros de entidad obligatorios**

* `entity.id`

**Lecturas**

* [Basado en el usuario](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.11: Criterios personalizados {#custom}

Cree recomendaciones basadas en un archivo personalizado que haya cargado.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Algoritmo personalizado]

**Parámetros de entidad obligatorios**

`entity.id` o el atributo utilizado como clave para el algoritmo personalizado

**Lecturas**

* [Criterios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.12: Proporcionar atributos utilizados en las reglas de inclusión {#inclusion}

+++Ver detalles

**Lecturas**

* [Uso de reglas de inclusión dinámicas y estáticas](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.13: Proporcionar excludedIds {#exclude}

Pase los ID de entidad de las entidades que desee excluir de las recomendaciones. Por ejemplo, quizás desee excluir artículos que ya se encuentren en el carro de compras.

+++Ver detalles

**Lecturas**

* [¿Puedo excluir dinámicamente una entidad? ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.14: Pasar el `entity.event.detailsOnly=true` parámetro {#true}

Use los atributos de entidad para pasar la información de producto o contenido a [!DNL Target Recommendations].

+++Ver detalles

**Lecturas**

* [Atributos de entidad](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.15: Configurar la asignación de datos remota (remota)

Este paso garantiza que todos los datos que deben enviarse a [!DNL Target] está configurado.

+++Ver detalles

![Diagrama de asignación de datos remotos](/help/dev/patterns/recs-atjs/assets/remote-data-mapping.png){width="400" zoomable="yes"}

**Requisitos previos**

* La capa de datos debe estar lista con todos los datos que deben enviarse a [!DNL Target].

**Configuración de proveedores de datos**

Para obtener más información, consulte [Proveedores de datos](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Lecturas**

[función targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Acciones**

Utilice el `targetPageParams()` para establecer todos los datos necesarios que deben enviarse a [!DNL Target].

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.16: cargar at.js {#web}

Este paso garantiza que la biblioteca JavaScript at.js se cargue e inicialice.

+++Ver detalles

![Cargar diagrama de SDK web de Adobe Target](/help/dev/patterns/recs-atjs/assets/load-web-sdk.png){width="400" zoomable="yes"}

**Requisitos previos**

* Descargue o pídale a su equipo de marketing digital el `at.js 2.*x*` Archivo de biblioteca JavaScript.

*Lecturas*

* [Cómo funciona Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [Cómo funciona at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Implementación de Target sin un administrador de etiquetas](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Acciones**

Incruste el archivo at.js en todas las páginas web donde se debe llevar a cabo la experimentación, la optimización, la personalización y la recopilación de datos.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)





























