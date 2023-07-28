---
title: Procesar experiencias
description: Asegúrese de que todos los pasos necesarios para procesar las experiencias se ejecutan en la secuencia correcta.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 18f070005685699e2d1feb12a31802faa17e35f3
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 5%

---

# Procesar experiencias

Siga los pasos de la *Experiencias de procesamiento* para garantizar que todas las tareas necesarias para procesar las experiencias se ejecuten en la secuencia correcta.

>[!TIP]
>
>Haga clic en las imágenes de este tema para expandirlas a pantalla completa.

## Representar diagrama de experiencias {#diagram}

La gestión automática de parpadeos predeterminada disponible con at.js solo tiene sentido cuando tiene [!UICONTROL Solicitud automática de carga de página] activado. Esta opción oculta todo el cuerpo del HTML al recuperar las experiencias de [!DNL Target]. En este caso, es su responsabilidad gestionar el parpadeo. Busque patrones de implementación disponibles para la gestión de parpadeos a modo de guía.

Los números de paso de la siguiente ilustración corresponden a las secciones siguientes.

![Representar diagrama de experiencias](/help/dev/patterns/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

Haga clic en los siguientes vínculos para desplazarse a las secciones deseadas:

* [3.1: Promoción](#promotion)
* [3.2: Criterios basados en el carro de compras](#cart)
* [3.3: Criterios basados en popularidad](#popularity)
* [3.4: Criterios basados en elementos](#item)
* [3.5: Criterios basados en el usuario](#user)
* [3.6: Criterios personalizados](#custom)
* [3.7: Proporcionar atributos utilizados en reglas de inclusión](#inclusion)
* [3.8: proporcionar excludedIds](#exclude)
* [3.9: proporcione atributos de entidad para actualizar el catálogo de productos para Recommendations](#entity-attributes)
* [3.10: Proporcionar atributos de perfil utilizados como claves para las reglas de inclusión](#keys)
* [3.11: Activar la solicitud de carga de página](#fire)
* [3.12: Activar la solicitud de ubicación regional](#location)

## 3.1: Promoción {#promotion}

Añada elementos promocionados y controle su ubicación en Target Recommendations [diseños](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Ver detalles

**Opciones disponibles**

* Promocionar por ID
* [Promocionar por colección](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promocionar por atributo](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Parámetros de entidad obligatorios**

* El atributo de elemento de las promociones debe pasarse al utilizar la opción &quot;promocionar por atributo&quot;.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.2: Criterios basados en el carro de compras {#cart}

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

## 3.3: Criterios basados en popularidad {#popularity}

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

* `entity.categoryId` o el atributo de artículo para la popularidad basada en si los criterios se basan en el atributo de artículo o el actual.
* No se debe pasar nada para los más visitados/más vendidos en el sitio.

**Lecturas**

* [Basado en popularidad](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.4: Criterios basados en elementos {#item}

Haga recomendaciones basadas en la búsqueda de artículos similares a los que el usuario está viendo o ha visto recientemente.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Los usuarios que vieron esto, vieron aquello.]
* [!UICONTROL Los usuarios que vieron esto, compraron aquello.]
* [!UICONTROL Los usuarios que compraron esto, compraron aquello.]
* [!UICONTROL Artículos con atributos similares]

**Parámetros de entidad obligatorios**

* `entity.id`
* Si se utiliza algún atributo de perfil como clave

**Lecturas**

* [Basado en elementos](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.5: Criterios basados en el usuario {#user}

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

## 3.6: Criterios personalizados {#custom}

Haga recomendaciones basadas en un archivo personalizado que haya cargado

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL Algoritmo personalizado]

**Parámetros de entidad obligatorios**

`entity.id` o el atributo utilizado como clave para el algoritmo personalizado

**Lecturas**

* [Criterios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.7: Proporcionar atributos utilizados en reglas de inclusión {#inclusion}

+++Ver detalles

**Lecturas**

* [Uso de reglas de inclusión dinámicas y estáticas](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.8: proporcionar excludedIds {#exclude}

Pase los ID de entidad de las entidades que desee excluir de las recomendaciones. Por ejemplo, quizás desee excluir artículos que ya se encuentren en el carro de compras.

+++Ver detalles

**Lecturas**

* [¿Puedo excluir dinámicamente una entidad? ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.9: Proporcione atributos de entidad para actualizar el catálogo de productos de [!DNL Recommendations] {#entity-attributes}

+++Ver detalles

**Lecturas**

* [Atributos de entidad](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

También puede llevar a cabo este paso creando fuentes de productos con el complemento [!DNL Target] IU para actualizar el catálogo de productos de [!DNL Recommendations].

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.10: Proporcionar atributos de perfil utilizados como claves para las reglas de inclusión {#keys}

Proporcione los atributos de perfil que se utilizan como claves para las reglas de inclusión en cualquier criterio de Recommendations mencionado anteriormente.

+++ Ver detalles

**Lecturas**

* [Atributos de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.11: Activar la solicitud de carga de página {#fire}

Este paso déclencheur un [!DNL Delivery API] llame a con `execute` > `pageLoad` carga útil en la solicitud. El `getOffers()` obtiene la experiencia y `applyOffers()` procesa la experiencia en la página. La solicitud pageLoad es necesaria para procesar experiencias creadas en [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++Ver detalles

![Activar diagrama de solicitud de carga de página](/help/dev/patterns/assets/fire-page-load-request.png){width="100" zoomable="yes"}

**Requisitos previos**

* Todas las asignaciones de datos deben realizarse utilizando `targetPageParams` función.

**Lecturas**

* [adobe. target. getoffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Acciones**

* Utilice el `getOffers` y `applyOffers` métodos para recuperar la experiencia mediante una llamada a la API de solicitud de carga de página.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.12: Activar la solicitud de ubicación regional (#location)

Este paso déclencheur un [!DNL Delivery API] llame a con `execute` > `mboxes` carga útil en su solicitud. El `getOffers` obtiene la experiencia y `applyOffers` procesa la experiencia en la página. Puede enviar más de un mbox en `execute` > `mboxes` carga útil.

+++Ver detalles

![Activar diagrama de solicitud de ubicación regional](/help/dev/patterns/assets/fire-regional-location-request.png){width="100" zoomable="yes"}

**Requisitos previos**

* Todas las asignaciones de datos deben realizarse utilizando `targetPageParams` función.

**Lecturas**

* [adobe. target. getoffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Acciones**

* Utilice el `getOffers` y `applyOffers` métodos para recuperar la experiencia mediante una llamada a la API de solicitud de carga de página.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)