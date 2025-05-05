---
title: Inicializar SDK
description: Asegúrese de que todos los pasos necesarios para cargar la biblioteca JavaScript  [!DNL Adobe Target] at.js se ejecuten en la secuencia correcta.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 250a8382-1fdd-4a70-b712-a25af5adad71
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 5%

---

# Inicializar SDK

Siga los pasos del diagrama *Inicializar SDK* para asegurarse de que todas las tareas necesarias para cargar la biblioteca JavaScript at.js de [!DNL Adobe Target] se ejecuten en la secuencia correcta.

>[!TIP]
>
>Haga clic en las imágenes de este tema para expandirlas a pantalla completa.

## Inicializar diagrama de SDK {#diagram}

En el caso de las aplicaciones de varias páginas, este flujo se produce cada vez que la página se vuelve a cargar o el visitante navega a una nueva página del sitio web.

>[!NOTE]
>
>Los números de paso de la siguiente ilustración corresponden a las secciones siguientes. Los números de paso no están en un orden particular y no reflejan el orden de los pasos realizados en la interfaz de usuario de [!DNL Target] al crear la actividad.

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

Este paso ayuda a garantizar que la biblioteca `VisitorAPI.js` se carga, configura e inicializa correctamente.

+++Ver detalles

![Cargar diagrama de SDK de API de visitante](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* Para usar el servicio API/ID de visitante, su compañía debe estar habilitada para [!DNL Adobe Experience Cloud] y tener un [!UICONTROL Organization ID]. Para obtener más información, consulte [Requisitos del Experience Cloud: ID de organización](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?lang=es&){target=_blank} en la guía *Ayuda del servicio de identidad*.
* Necesita el archivo `VisitorAPI.js`. Ya debería tener este archivo si tiene [!DNL Adobe Analytics] implementado. Este archivo también se puede agregar mediante la [[!DNL Adobe Experience Platform] extensión de etiquetas](https://experienceleague.adobe.com/docs/tags.html?lang=es){target=_blank} o se puede descargar desde el [Administrador de códigos Adobe Analytics](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=es){target=_blank}.

**Configurar y hacer referencia a VisitorAPI.js**

Para obtener más información, consulte [Implementar el servicio de Experience Cloud para Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=es){target=_blank}.

**Lecturas**

* [Descripción general del servicio de identidad del Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es){target=_blank}
* [Acerca del servicio de ID](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html?lang=es){target=_blank}
* [Cookies y el servicio de identidad del Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=es){target=_blank}
* [Solicitud y configuración de ID con el servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html?lang=es){target=_blank}
* [Explicación de la sincronización de ID y tasas de coincidencia](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html?lang=es){target=_blank}

**Acciones**

* Incruste el archivo `VisitorAPI.js` en sus páginas web.
* Obtenga información acerca de las [configuraciones disponibles para el servicio API/ID de visitante](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?lang=es){target=_blank}.
* Una vez cargado el archivo `VisitorAPI.js`, use el método `Visitor.getInstance` para inicializar con las configuraciones necesarias.
* Familiarícese con los [métodos disponibles](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html?lang=es){target=_blank}.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.2: Establecer el ID de cliente {#set}

Este paso ayuda a garantizar que los ID conocidos de los visitantes (ID de CRM, ID de usuario, etc.) estén vinculados al ID anónimo de [!DNL Adobe] para la personalización entre dispositivos.

+++Ver detalles

![Establecer ID de cliente](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* El ID conocido de los visitantes debe estar disponible en la capa de datos.

**Establecer ID de cliente**
Para obtener más información, consulte [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=es){target=_blank}.

**Lecturas**

* [Sincronización de perfiles en tiempo real para mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=es){target=_blank}

**Acciones**

* Use `visitor.setCustomerIDs` para establecer el ID conocido del visitante.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.3: Configurar la solicitud automática de carga de página {#automatic}

Este paso permite que at.js recupere todas las experiencias que se deben procesar en la página al cargar el archivo de biblioteca JavaScript at.js.

+++Ver detalles

![Configurar solicitud automática de carga de página](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* No todos los datos de la capa de datos deben enviarse a [!DNL Target]. Consulte con su equipo empresarial (equipo de marketing digital) para determinar qué datos son valiosos para la experimentación, la optimización y la personalización. Solo se deben enviar estos datos a [!DNL Target].
* Asegúrese de no enviar ningún dato de información de identificación personal (PII) a [!DNL Target].

**Configurar solicitud automática de carga de página**

Para obtener más información, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Lecturas**

Obtenga información acerca de la configuración `pageLoadEnabled` en [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Acciones**

* Modifique el objeto `window.targetGlobalSettings` para habilitar las solicitudes automáticas de carga de página.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.4: Configurar la gestión de parpadeos {#flicker}

Este paso ayuda a garantizar que no haya parpadeo en la página al enviar experiencias.

+++Ver detalles

![Configurar diagrama de control de parpadeo](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* Hable con el equipo responsable del rendimiento de la página web sobre los pros y los contras de controlar el parpadeo mediante el método predeterminado utilizado por at.js. Puede buscar patrones de diseño que le permitan utilizar una solución personalizada de control de parpadeo, como la animación del cargador. Si no encuentra ningún patrón, puede solicitar uno nuevo.

**Configurar la administración de parpadeos**

Para obtener más información, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Si se establece `bodyHidingEnabled` en `true`, se oculta todo el cuerpo de la página mientras la solicitud de carga de página está en curso. Si no ha habilitado la solicitud automática de carga de página por algún motivo (por ejemplo, si los datos no están listos más adelante), es mejor establecer esta configuración en `false`.

Si ha deshabilitado `bodyHidingEnabled` porque no desea activar el APLR y desea activar la solicitud de página más adelante, o no necesita controlar el parpadeo, debe implementar su propia gestión del parpadeo. Puede controlar el parpadeo de dos formas: ocultando las secciones en prueba o mostrando un pulsador en las secciones en prueba.

**Lecturas**

* [Cómo gestiona at.js el parpadeo](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Obtenga información acerca de los objetos bodyHiddenStyle y bodyHidingEnabled en [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Acciones**

* Modifique el objeto `window.targetGlobalSettings` para establecer `bodyHiddenStyle` y `bodyHidingEnabled`.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.5: Configurar asignación de datos {#data-mapping}

Este paso ayuda a garantizar que se establezcan todos los datos que deben enviarse a [!DNL Target].

+++Ver detalles

![Diagrama de asignación de datos](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* La capa de datos debe estar lista con todos los datos que deben enviarse a [!DNL Target].
* Recommendations: enriquecer perfil.
   * Pase `entity.id` para capturar los datos de los criterios y artículos vistos recientemente según los criterios basados en el último producto visto.
   * Pase `entity.id` para capturar datos para los criterios de popularidad basados en la categoría de favoritos.
   * Pase el atributo de perfil si los criterios personalizados se basan en él o se utilizan en el filtrado de reglas de inclusión en cualquier criterio.
* Recommendations: ingerir datos de productos.
   * Se pueden pasar otros parámetros de entidad (reservados y personalizados) para introducir o actualizar el catálogo de productos en [!DNL Recommendations].
   * El catálogo de productos también se puede actualizar usando fuentes de entidad usando la interfaz de usuario o la API de [!DNL Target].

**Asignar datos a[!DNL Target]**

Para obtener más información, consulte [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lecturas**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planificar e implementar Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Configurar el catálogo de Recommendations](/help/dev/implement/recommendations/recommendations.md)

**Acciones**

* Utilice la función `targetPageParams()` para establecer todos los datos necesarios que deben enviarse a [!DNL Target].

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.6: Promoción {#promotion}

Agregue elementos promocionados y controle su ubicación en sus [!DNL Target Recommendations] [diseños](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=es){target=_blank}.

+++Ver detalles

**Opciones disponibles**

* Promocionar por ID
* [Promocionar por colección](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html?lang=es){target=_blank}
* [Promocionar por atributo](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=es){target=_blank}

**Se requieren parámetros de entidad**

* El atributo de elemento de la promoción debe pasarse al utilizar la opción &quot;promocionar por atributo&quot;.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.7: Criterios basados en el carro de compras {#cart}

Haga recomendaciones basadas en el contenido del carro de compras del usuario.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**Se requieren parámetros de entidad**

* cartIds

**Lecturas**

* [Basado en el carro de compras](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=es#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.8: Criterios basados en popularidad {#popularity}

Haga recomendaciones basadas en la popularidad general de un elemento en el sitio o en la popularidad de elementos dentro de la categoría, marca, género, etc. favoritos o más vistos de un usuario.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**Se requieren parámetros de entidad**

* `entity.categoryId` o el atributo de elemento para popularidad basada en si los criterios se basan en el elemento actual o en el atributo de elemento.
* No se debe pasar nada para los más visitados/más vendidos en el sitio.

**Lecturas**

* [Basado en popularidad](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=es#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.9: Criterios basados en elementos {#item}

Haga recomendaciones basadas en la búsqueda de artículos similares a los que el usuario está viendo o ha visto recientemente.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Se requieren parámetros de entidad**

* `entity.id` o cualquier atributo de perfil utilizado como clave

**Lecturas**

* [Basado en elemento](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=es#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.10: Criterios basados en el usuario {#user}

Haga recomendaciones basadas en el comportamiento del usuario.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**Se requieren parámetros de entidad**

* `entity.id`

**Lecturas**

* [Basado en usuario](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=es#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.11: Criterios personalizados {#custom}

Cree recomendaciones basadas en un archivo personalizado que haya cargado.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Custom algorithm]

**Se requieren parámetros de entidad**

`entity.id` o el atributo utilizado como clave para el algoritmo personalizado

**Lecturas**

* [Criterios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=es#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.12: Proporcionar atributos utilizados en las reglas de inclusión {#inclusion}

+++Ver detalles

**Lecturas**

* [Usar reglas de inclusión dinámicas y estáticas](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html?lang=es){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.13: Proporcionar excludedIds {#exclude}

Pase los ID de entidad de las entidades que desee excluir de las recomendaciones. Por ejemplo, quizás desee excluir artículos que ya se encuentren en el carro de compras.

+++Ver detalles

**Lecturas**

* [¿Puedo excluir dinámicamente una entidad?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=es#exclude){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.14: pasar el parámetro `entity.event.detailsOnly=true` {#true}

Use los atributos de entidad para pasar la información de producto o contenido a [!DNL Target Recommendations].

+++Ver detalles

**Lecturas**

* [Atributos de entidad](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=es){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.15: Configurar la asignación de datos remota (remota)

Este paso garantiza que todos los datos que deben enviarse a [!DNL Target] estén establecidos.

+++Ver detalles

![Diagrama de asignación de datos remotos](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* La capa de datos debe estar lista con todos los datos que deben enviarse a [!DNL Target].

**Configurar proveedores de datos**

Para obtener más información, consulte [Proveedores de datos](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Lecturas**

[función targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Acciones**

Utilice la función `targetPageParams()` para establecer todos los datos necesarios que deben enviarse a [!DNL Target].

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 1.16: cargar at.js {#web}

Este paso garantiza que la biblioteca JavaScript at.js se cargue e inicialice.

+++Ver detalles

![Cargar diagrama at.js de Adobe Target](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* Descargue o solicite a su equipo de marketing digital el archivo de biblioteca JavaScript `at.js 2.*x*`.

*Lecturas*

* [Cómo funciona Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=es){target=_blank}
* [Cómo funciona at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Implementación de Target sin un administrador de etiquetas](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Acciones**

Incruste el archivo at.js en todas las páginas web donde se debe llevar a cabo la experimentación, la optimización, la personalización y la recopilación de datos.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

Continúe con el paso 2: [Configurar la recopilación de datos](/help/dev/patterns/recs-atjs/data-collection.md).
