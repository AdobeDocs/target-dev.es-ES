---
keywords: Recommendations, configuración, preferencias, sector, criterios incompatibles de filtro, grupo de hosts predeterminado, URL de base en miniatura, token de api de recomendaciones,
description: Aprenda a implementar actividades de [!UICONTROL Recommendations] en [!DNL Adobe Target].
title: ¿Cómo Implemento Actividades De [!UICONTROL Recommendations]?
feature: Recommendations
hide: true
exl-id: 0a9c9649-195b-44e2-987e-d02eaf98cc54
TQID: https://experienceleague.adobe.com/A7j0oJbyO3oei-a2l02I58o9I0vCPrRcqWC-QgQUxBo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 929e1f10bc5dd0741f0fe28cd46435e680a4a308
workflow-type: tm+mt
source-wordcount: 1734
ht-degree: 17%

---

# Planificar e implementar [!UICONTROL Recommendations]

Información para ayudarle a planificar e implementar [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Además de este artículo, la [Guía para profesionales de Adobe Target](https://experienceleague.adobe.com/es/docs/target/using/target-home){target=_blank} contiene información detallada acerca de [Target Recommendations](https://experienceleague.adobe.com/es/docs/target/using/recommendations/recommendations){target=_blank}.

Antes de configurar su primera actividad [!UICONTROL Recommendations] en [!DNL Adobe Target], complete los siguientes pasos:

1. [Implemente [!UICONTROL Target]](#implement-target) en las superficies web y de aplicaciones móviles que desee usar para capturar el comportamiento del usuario y enviar recomendaciones.
1. [Configure su catálogo [!UICONTROL Recommendations]](#set-up-your-recommendations-catalog) de productos o contenido que desee recomendar a sus usuarios.
1. [Pase información de comportamiento y contexto](#pass-behavioral-information-and-context) a [!DNL Target Recommendations] para permitirle entregar recomendaciones personalizadas.
1. [Configurar exclusiones globales](#configure-global-exclusions).
1. [Configurar la configuración de [!UICONTROL Recommendations]](#configure-recommendations-settings).
1. (Opcional) [Administrar [!UICONTROL Recommendations] mediante las API de administrador](#administer-recommendations-using-admin-apis).

## &#x200B;1. Implementar [!UICONTROL Target]

[!DNL Target Recommendations] requiere que implemente [!DNL Adobe Experience Platform Web SDK] o at.js 0.9.2 (o posterior). Consulte las [[!UICONTROL guías de implementación del lado del cliente de Target]](../client-side/overview.md) para obtener más información.

## &#x200B;2. Configurar el catálogo [!UICONTROL Recommendations]

Para ofrecer recomendaciones de alta calidad, [!UICONTROL Target] debe conocer los productos o el contenido que desea recomendar. Los catálogos suelen incluir tres tipos de información sobre los artículos recomendados. Supongamos que recomienda películas. Incluya lo siguiente:

1. Datos que desea mostrar al usuario que recibe la recomendación. Por ejemplo, puede mostrar el nombre de la película y una dirección URL para una imagen en miniatura del póster de la película.
1. Datos que son útiles para aplicar controles de marketing y comercialización. Por ejemplo, puede mostrar la clasificación de la película para que no recomiende las de mayores de 17 años.
1. Datos que son útiles para determinar la similitud de elementos con otros elementos. Por ejemplo, puede mostrar el género de la película y el director de la película.

[!UICONTROL Target] ofrece varias opciones de integración para rellenar el catálogo. Estas opciones se pueden utilizar en combinación para actualizar distintos artículos del catálogo o para actualizar atributos de artículos diferentes en distintas frecuencias.

| Método | Qué es | Cuándo utilizarla | Información adicional |
| --- | --- | --- | --- |
| Fuente de catálogo | Programe una fuente (CSV, [!DNL Google] XML de producto o [!UICONTROL Clasificaciones de productos de Analytics]) para que se cargue e ingiera diariamente. | Para enviar información sobre varios elementos a la vez. Para enviar información que cambia con poca frecuencia. | Ver [Fuentes](https://experienceleague.adobe.com/es/docs/target/using/recommendations/entities/feeds). |
| API de entidades | Llame a una API para enviar actualizaciones al minuto de un solo elemento. | Para enviar actualizaciones a medida que se producen en un elemento a la vez. Para enviar información que cambia con frecuencia (por ejemplo, nivel de precio, inventario/stock). | Consulte la [documentación para desarrolladores de API de entidades](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Pasar actualizaciones en la página | Envíe actualizaciones de un solo elemento al minuto mediante JavaScript en la página o mediante la API de envío. | Para enviar actualizaciones a medida que se producen en un elemento a la vez. Para enviar información que cambia con frecuencia (por ejemplo, nivel de precio, inventario/stock). | Ver [vistas de artículos/páginas de productos](#item-views-or-product-pages) a continuación. |

La mayoría de los clientes deben implementar al menos una fuente. A continuación, puede elegir complementar su fuente con actualizaciones para atributos o elementos que se cambian con frecuencia mediante la API de entidades o el método en la página.

## &#x200B;3. Pasar información y contexto de comportamiento

La información de comportamiento y el contexto que debe pasar a [!UICONTROL Target] dependen de la acción que esté realizando el visitante, que a menudo se asocia con el tipo de página con la que interactúa.

### Vistas de elementos o páginas de productos

En las páginas en las que un visitante está viendo un solo artículo, como una página de detalles del producto, debe pasar la identidad del artículo que el visitante está viendo. Pase también la categoría más granular del elemento que el visitante está viendo para permitir recomendaciones de filtrado a la categoría actual.

También puede pasar ciertos atributos que cambian rápidamente en la propia página del producto. Por ejemplo, puede pasar el precio (`value`) y el nivel de inventario/existencias.

#### Pasar precio e inventario

```js {line-numbers="true"}
<script type="text/javascript">
function targetPageParams() { 
   return { 
      "entity": { 
         "id": "32323", 
         "categoryId": "running-shoes", 
         "value": 119.99, 
         "inventory": 329 
      } 
   } 
}
</script>
```

### Vistas de categorías/páginas de categorías

En una página de categoría, es probable que desee restringir las recomendaciones a productos o contenido dentro de esa categoría. Para ello, asegúrese de pasar la identidad de la categoría visualizada actualmente.

#### Pasar categoría actual

```js {line-numbers="true"}
function targetPageParams() { 
   return { 
      "entity": { 
         "categoryId": "running-shoes" 
      } 
   } 
}
```

### Adiciones al carro de compras/vistas del carro de compras/páginas de cierre de compra

En una página de carro de compras, puede recomendar elementos basados en el contenido del carro de compras actual del visitante. Para ello, pase los identificadores de todos los elementos del carro de compras actual del visitante utilizando el parámetro especial `cartIds`.

#### Pasar elementos actualmente en el carro

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Para obtener más información sobre las recomendaciones basadas en el carro de compras, consulte [Basado en el carro de compras](https://experienceleague.adobe.com/es/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key#cart-based) en la *[!DNL Adobe Target]Guía para profesionales de negocios*.

### Excluir elementos que ya están en el carro de compras del visitante

En páginas de todo el sitio, puede excluir algunos artículos de las recomendaciones. Por ejemplo, es posible que no desee recomendar elementos que ya están en el carro de compras actual del visitante. Para ello, pase los identificadores de todos los elementos que desee excluir mediante el parámetro especial `excludedIds`.

#### Pasar elementos que excluir

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Páginas de confirmación de pedidos/compras

Cuando se produce un evento de compra, pasa la identidad del artículo o artículos comprados. Consulte [Rastrear conversiones](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) en el artículo de [Cómo implementar at.js > Implementar [!UICONTROL Target] sin un administrador de etiquetas](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

## &#x200B;4. Configuración de exclusiones globales

Excluya cualquier elemento de nivel global que no quiera que se recomiende a un visitante. Consulte [Exclusiones](https://experienceleague.adobe.com/es/docs/target/using/recommendations/entities/exclusions) en la *[!DNL Adobe Target]Guía para profesionales de negocios*.

## &#x200B;5. Configurar [!UICONTROL Recommendations]

Utilice la configuración para administrar la implementación de [!UICONTROL Recomendaciones].

Para obtener acceso a las opciones de **[!UICONTROL Configuración de Recommendations]**, abra [!DNL Target] en [!DNL Adobe Experience Cloud] y, a continuación, haga clic en **[!UICONTROL Administración]** > **[!UICONTROL Recommendations]**.

![Página de configuración de Recommendations](/help/dev/implement/recommendations/assets/recs-settings-new.png)

Configure las siguientes opciones:

### [!UICONTROL Token de la API de Recommendations]

Las siguientes opciones están disponibles en la sección [!UICONTROL Token de API de Recommendations]:

#### [!UICONTROL Código de cliente]

El [!DNL Target] [!UICONTROL código de cliente].

Si no conoce su [!UICONTROL código de cliente], en la interfaz de usuario de [!DNL Target], haga clic en **[!UICONTROL Administración]** > **[!UICONTROL Implementación]**. El [!UICONTROL código de cliente] se muestra en la sección [!UICONTROL Detalles de la cuenta].

#### Token de autenticación

Las API de administrador de [!DNL Adobe Target], incluidas las API de [!DNL Recommendations Admin], están protegidas con autenticación para garantizar que solo los usuarios autorizados las usen para acceder a [!DNL Adobe Target]. Use [Adobe Developer Console](https://developer.adobe.com/console/home) para administrar esta autenticación en todos los [!DNL Adobe Experience Cloud solutions], incluido [!DNL Adobe Target].

Para obtener más información, consulte [Configurar la autenticación para las API de Adobe Target](/help/dev/before-administer/configure-authentication.md).

>[!WARNING]
>
>Tenga cuidado al generar un nuevo token de autenticación. La generación de un nuevo token provoca que las llamadas a API realizadas con el token actual resulten fallidas. Actualice los scripts o las aplicaciones con el nuevo token de autenticación generado.

### Criterios

Conocer el sector industrial del sitio ayuda a Target a elegir criterios para las recomendaciones.

Los criterios de [!DNL Recommendations] son reglas que determinan qué productos o contenido recomendar en función de un conjunto predeterminado de comportamientos del visitante. Los criterios se pueden basar en tendencias populares, los comportamientos actuales y pasados de un visitante o productos y contenido similares. Puede probar distintos tipos de recomendaciones entre sí si se agregan varios criterios.

Para obtener más información, consulte [Criterios](https://experienceleague.adobe.com/es/docs/target/using/recommendations/criteria/algorithms){target=_blank} en la *Guía para profesionales de Adobe Target Business.*

La siguiente configuración está disponible en la sección [!UICONTROL Criterios]:

#### [!UICONTROL Sector/Vertical]

El sector se usa para ayudarle a categorizar los criterios de recomendaciones. Esta información ayuda a los miembros de su equipo a encontrar criterios que tienen sentido para una página en particular, como los criterios que son mejores para la página del carro de compras o para una página multimedia.

Las siguientes categorías están disponibles en la lista desplegable:

* No hay Personalization
* Venta minorista/Comercio electrónico
* Generación de vanguardia/B2B/Servicios financieros
* Medios/Publicación

#### [!UICONTROL Criterios incompatibles de filtro]

Habilite esta opción para mostrar únicamente aquellos criterios donde la página seleccionada pasa los datos necesarios. No todos los criterios se ejecutan correctamente en cada página. La página o el mbox deben pasar `entity.id` o `entity.categoryId` para que las recomendaciones de la categoría actual o el elemento actual sean compatibles.

En general, se recomienda mostrar solamente criterios compatibles. Sin embargo, si desea que haya disponibles criterios incompatibles para la actividad, no active esta opción.

Adobe recomienda deshabilitar esta opción si se usa una solución de administración de etiquetas.

Para obtener más información sobre esta opción, consulte [[!UICONTROL Preguntas frecuentes]](https://experienceleague.adobe.com/es/docs/target/using/recommendations/recommendations-faq/recommendations-faq){target=_blank} de Recommendations en la *[!DNL Adobe Target]Guía para profesionales de la empresa*.

### [!UICONTROL Catálogo de productos]

Las siguientes opciones están disponibles en la sección [!UICONTROL Catálogo de productos]:

#### [!UICONTROL Grupo de hosts predeterminado]

Seleccione su grupo de hosts predeterminado.

El grupo de hosts puede utilizarse para separar los elementos disponibles en el catálogo para usos diferentes. Por ejemplo, puede utilizar grupos de hosts para entornos de desarrollo y producción, marcas diferentes o regiones geográficas diferentes. De forma predeterminada, la vista previa de los resultados en Búsqueda de catálogo, Colecciones y Exclusiones se basa en el grupo de hosts predeterminado. (También puede seleccionar otro grupo de hosts para obtener una vista previa de los resultados mediante el filtro Entorno). De forma predeterminada, los elementos recién añadidos están disponibles en todos los grupos de hosts a menos que se especifique un ID de entorno al crear o actualizar el elemento. Las recomendaciones enviadas dependen del grupo de hosts especificado en la solicitud.

Si no ve sus productos, asegúrese de que esté usando el grupo de hosts correcto. Por ejemplo, si configura que la recomendación use un entorno de ensayo y establece el grupo de hosts en Ensayo, puede que tenga que volver a crear las colecciones en el entorno de ensayo para que se puedan mostrar los productos. Para ver qué productos están disponibles en cada entorno, use Búsqueda en catálogo con cada entorno. También puede obtener una vista previa del contenido de [!UICONTROL Recommendations] colecciones y exclusiones de un entorno seleccionado (grupo de hosts).

>[!NOTE]
>
>Después de cambiar el entorno seleccionado, debe hacer clic en **[!UICONTROL Buscar]** para actualizar los resultados devueltos.

El filtro **[!UICONTROL Entorno]** está disponible en los siguientes lugares de la interfaz de usuario de Target:

* Buscar en el catálogo (**[!UICONTROL Recommendations]** > **[!UICONTROL Buscar en el catálogo]**)
* Colecciones (**[!UICONTROL Recommendations]** > **[!UICONTROL Colecciones]**)
* Cuadro de diálogo Crear colección (**[!UICONTROL Recommendations]** > **[!UICONTROL Colecciones]** > **[!UICONTROL Crear colección]**)
* Cuadro de diálogo Actualizar colección (**[!UICONTROL Recommendations]** > **[!UICONTROL Colecciones]** > **[!UICONTROL Editar]**)
* Cuadro de diálogo Crear exclusión (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusiones]** > **[!UICONTROL Crear exclusión]**)
* Cuadro de diálogo Actualizar exclusión (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusiones]** > **[!UICONTROL Editar]**)

Para obtener más información, consulte [Hosts](https://experienceleague.adobe.com/es/docs/target/using/administer/hosts){target=_blank} en la *[!DNL Adobe Target]Guía para profesionales de la empresa*.

#### [!UICONTROL Base de miniatura]

Al establecer una dirección URL de base para su catálogo de productos, es posible usar direcciones URL relativas al especificar vistas en miniatura de sus productos al pasar su dirección URL de vista en miniatura.

Por ejemplo:

`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`

establece una dirección URL relativa para la dirección URL de base de vista en miniatura.

### [!UICONTROL Configuración de clave de atributo personalizada]

Base sus recomendaciones en un elemento almacenado en el perfil del visitante. Por ejemplo, &quot;último elemento añadido al carro de compras&quot; o &quot;último vídeo visto hasta el 90 % o más&quot;.

Haga clic en **[!UICONTROL Agregar]** para crear una nueva configuración, especifique un nombre para la configuración, seleccione el atributo de perfil deseado y haga clic en **[!UICONTROL Guardar]**.

## &#x200B;6. (Opcional) Administrar [!UICONTROL Recommendations] mediante las API de administrador

Consulte la guía práctica [Use [!UICONTROL Recommendations] API](../../before-administer/recs-api/overview.md) para aprender a configurar y usar las API de administración y envío de [!UICONTROL Target] para [!UICONTROL Recommendations].
