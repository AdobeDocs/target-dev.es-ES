---
title: Configuración de la recopilación de datos
description: Asegúrese de que todas las tareas necesarias para la recopilación de datos se ejecutan en la secuencia correcta.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 66e0f18d-c78c-463b-8c47-132ef6332927
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# Configuración de la recopilación de datos

Siga los pasos del diagrama *Recopilación de datos* para asegurarse de que todas las tareas necesarias para la recopilación de datos se ejecutan en la secuencia correcta.

>[!TIP]
>
>Haga clic en las imágenes de este tema para expandirlas a pantalla completa.

La capa de datos está lista durante la carga de página o bien la capa de datos cambia después de la carga de página.

Si ya asignó datos durante la [fase de inicialización del SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md), debe ejecutar los pasos de este diagrama si:

* La capa de datos se ha aumentado de cualquier manera en la misma página y desea enviar esos datos adicionales a [!DNL Target]
* Desea enviar los datos del catálogo de productos a [!DNL Target Recommendations]

## Recopilar diagrama de datos {#diagram}

Los números de paso de la siguiente ilustración corresponden a las secciones siguientes.

![Diagrama de recopilación de datos](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Haga clic en los siguientes vínculos para desplazarse a las secciones deseadas:

* [2.1: Configurar asignación de datos](#configure)
* [2.2 Vínculo a atributos de entidad](#entity-attributes)
* [2.3 Activar la API de seguimiento de Adobe Target](#fire-api)

## 2.1: Configurar asignación de datos {#configure}

Este paso ayuda a garantizar que se establezcan todos los datos que deben enviarse a [!DNL Adobe Target].

+++Ver detalles

![Configurar diagrama de asignación de datos](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* La capa de datos debe estar lista con todos los datos que deben enviarse a [!DNL Target].

**Lecturas**

[función targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Acciones**

Utilice la función `targetPageParams()` para establecer todos los datos necesarios que deben enviarse a [!DNL Target].

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 2.2: Vínculo a atributos de entidad {#entity-attributes}

Vínculo a atributos de entidad para actualizar el catálogo de productos de [!DNL Target Recommendations].

+++Ver detalles

**Lecturas**

* [Atributos de entidad](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=es){target=_blank}

**Consideraciones**

* Una forma alternativa de pasar atributos de entidad es actualizar el catálogo de productos en la interfaz de usuario de [!DNL Target] para usar [fuentes de productos de Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html?lang=es){target=_blank}.
* El paso de atributos de entidad solo es aplicable en páginas donde los datos del catálogo de productos están disponibles en la capa de datos.
* Pasar el parámetro `entity.event.detailsOnly=true` en cualquier llamada tiene prioridad.

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

## 2.3 Activar la API de seguimiento de Adobe Target {#fire-api}

Este paso ayuda a garantizar que se envíen todos los datos que deben enviarse a [!DNL Target].

+++Ver detalles

![Activar el diagrama de API de seguimiento de Adobe Target](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**Requisitos previos**

* Toda la asignación de datos debe haberse realizado con la [función targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lecturas**

* [adobe.target.trackEvent(), método](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Acciones**

Use el [método adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) para enviar todos los datos que deben enviarse a [!DNL Target].

+++

[Vuelva al diagrama situado en la parte superior de esta página.](#diagram)

Continúe con el paso 3: [Procesar experiencias](/help/dev/patterns/recs-atjs/render-experiences.md)
