---
title: Procesar experiencias
description: Asegúrese de que todos los pasos necesarios para procesar las experiencias se ejecutan en la secuencia correcta.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 7cf0c70b-a4bc-46f4-9b33-099bdb7dd9a9
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 4%

---

# Procesar experiencias

Siga los pasos del diagrama de *Experiencias de procesamiento* para asegurarse de que todas las tareas necesarias para procesar experiencias se ejecuten en la secuencia correcta.

>[!NOTE]
>
>Si ha habilitado la solicitud de carga de página automática durante el paso [Configurar solicitud de carga de página automática](/help/dev/patterns/recs-atjs/initialize-sdk.md#automatic) en *Inicializar SDK* , puede omitir esta actividad a menos que desee llamar al SDK para Adobe Target para procesar experiencias adicionales mediante una solicitud de ubicación regional.

>[!TIP]
>
>Haga clic en las imágenes de este tema para expandirlas a pantalla completa.

## Representar diagrama de experiencias {#diagram}

La administración automática de parpadeos predeterminada disponible con at.js solo tiene sentido cuando tiene [!UICONTROL Automatic Page Load Request] habilitado. Esta opción oculta todo el cuerpo del HTML al recuperar las experiencias de [!DNL Target]. En este caso, es su responsabilidad gestionar el parpadeo. Busque patrones de implementación disponibles para la gestión de parpadeos a modo de guía.

>[!NOTE]
>
>Los números de paso de la siguiente ilustración corresponden a las secciones siguientes. Los números de paso no están en un orden particular y no reflejan el orden de los pasos realizados en la interfaz de usuario de [!DNL Target] al crear la actividad.

![Diagrama de experiencias de procesamiento](/help/dev/patterns/recs-atjs/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

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

Agregue elementos promocionados y controle su ubicación en el diseño de recomendaciones eligiendo promociones principales o secundarias en la interfaz de usuario de [!DNL Target] al crear la actividad.

+++Ver detalles

**Opciones disponibles**

* Promocionar por ID
* [Promocionar por colección](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html?lang=es){target=_blank}
* [Promocionar por atributo](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=es){target=_blank}

**Se requieren parámetros de entidad**

* Los atributos de elemento de las promociones deben pasarse al utilizar la opción &quot;promocionar por atributo&quot;.

**Lecturas**

* [Agregar promociones](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/adding-promotions.html?lang=es){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.2: Criterios basados en el carro de compras {#cart}

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

## 3.3: Criterios basados en popularidad {#popularity}

Haga recomendaciones basadas en la popularidad general de un elemento en el sitio o en la popularidad de elementos dentro de la categoría, marca, género, etc. favoritos o más vistos de un visitante.

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

* `entity.categoryId` o el atributo de elemento para popularidad basada en si los criterios se basan en el atributo de elemento o actual.
* No se debe pasar nada para los más visitados/más vendidos del sitio.

**Lecturas**

* [Basado en popularidad](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=es#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.4: Criterios basados en elementos {#item}

Haga recomendaciones basadas en la búsqueda de artículos similares a los que el usuario está viendo o ha visto recientemente.

+++Ver detalles

**Criterios disponibles**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Se requieren parámetros de entidad**

* `entity.id`
* Si se utiliza algún atributo de perfil como clave

**Lecturas**

* [Basado en elemento](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=es#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.5: Criterios basados en el usuario {#user}

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

## 3.6: Criterios personalizados {#custom}

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

## 3.7: Proporcionar atributos utilizados en reglas de inclusión {#inclusion}

+++Ver detalles

**Lecturas**

* [Usar reglas de inclusión dinámicas y estáticas](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html?lang=es){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.8: proporcionar excludedIds {#exclude}

Pase los ID de entidad de las entidades que desee excluir de las recomendaciones. Por ejemplo, quizás desee excluir artículos que ya se encuentren en el carro de compras.

+++Ver detalles

**Lecturas**

* [¿Puedo excluir dinámicamente una entidad?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=es#exclude){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.9: proporcione atributos de entidad para actualizar el catálogo de productos de [!DNL Recommendations] {#entity-attributes}

+++Ver detalles

**Lecturas**

* [Atributos de entidad](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=es){target=_blank}

También puede realizar este paso creando [fuentes de productos](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html?lang=es){target=_blank} con la interfaz de usuario de [!DNL Target] para actualizar el catálogo de productos de [!DNL Recommendations].

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.10: Proporcionar atributos de perfil utilizados como claves para las reglas de inclusión {#keys}

Proporcione los atributos de perfil que se utilizan como claves para las reglas de inclusión en cualquier criterio de Recommendations mencionado anteriormente.

+++ Ver detalles

**Lecturas**

* [Atributos de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=es){target=_blank}

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.11: Activar la solicitud de carga de página {#fire}

Este paso almacena en déclencheur una llamada a [!DNL Delivery API] con `execute` > `pageLoad` carga útil en la solicitud. El método `getOffers()` recupera la experiencia y `applyOffers()` la procesa en la página. La solicitud `pageLoad` es necesaria para procesar experiencias creadas en el [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es){target=_blank} (VEC).

+++Ver detalles

![Activar diagrama de solicitud de carga de página](/help/dev/patterns/recs-atjs/assets/fire-page-load-request-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* Toda la asignación de datos debe realizarse utilizando la función `targetPageParams`.

**Lecturas**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Acciones**

* Utilice los métodos `getOffers` y `applyOffers` para recuperar la experiencia mediante una llamada a la API de solicitud de carga de página.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 3.12: Activar la solicitud de ubicación regional (#location)

Este paso almacena en déclencheur una llamada a [!DNL Delivery API] con la carga útil `execute` > `mboxes` en su solicitud. El método `getOffers` recupera la experiencia y `applyOffers` la procesa en la página. Puede enviar más de un mbox bajo la carga útil `execute` > `mboxes`.

+++Ver detalles

![Activar diagrama de solicitud de ubicación regional](/help/dev/patterns/recs-atjs/assets/fire-regional-location-request-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* Toda la asignación de datos debe realizarse utilizando la función `targetPageParams`.

**Lecturas**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Acciones**

* Utilice los métodos `getOffers` y `applyOffers` para recuperar la experiencia mediante una llamada a la API de solicitud de carga de página.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

Continúe con el paso 4: [Notificar al destinatario](/help/dev/patterns/recs-atjs/notify-target.md).
