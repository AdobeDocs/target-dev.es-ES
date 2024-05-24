---
keywords: Recommendations, configuración, preferencias, sector, criterios incompatibles de filtro, grupo de hosts predeterminado, url de base en miniatura, token de api de recomendaciones, $9
description: Obtenga información sobre cómo implementar [!UICONTROL Recommendations] actividades en [!DNL Adobe Target].
title: ¿Cómo puedo implementar [!UICONTROL Recommendations] ¿Actividades?
feature: Recommendations
exl-id: af1e8b60-6dbb-451b-aa4f-e167d1800d1c
source-git-commit: 777c8b9aeb866e1b20ec24e85532a99f57d1fe72
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 25%

---

# Planificar e implementar [!UICONTROL Recommendations]

Información para ayudarle a planificar e implementar [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Además de este artículo, la variable [Guía para profesionales de Adobe Target Business](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=es){target=_blank} contiene información detallada acerca de [Target Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html){target=_blank}.

Antes de configurar la primera [!UICONTROL Recommendations] actividad en [!DNL Adobe Target], complete los siguientes pasos:

1. [Implementación [!UICONTROL Target]](#implement-target) en las superficies web y de aplicaciones móviles que desee utilizar para capturar el comportamiento del usuario y enviar recomendaciones.
1. [Configure su [!UICONTROL Recommendations] catalogar](#set-up-your-recommendations-catalog) de productos o contenido que desea recomendar a los usuarios.
1. [Pasar información y contexto de comportamiento](#pass-behavioral-information-and-context) hasta [!DNL Target Recommendations] para permitirle enviar recomendaciones personalizadas.
1. [Configuración de exclusiones globales](#configure-global-exclusions).
1. [Configurar [!UICONTROL Recommendations] configuración](#configure-recommendations-settings).
1. (Opcional) [Administrar [!UICONTROL Recommendations] uso de API de administrador](#administer-recommendations-using-admin-apis).

## 1. Implementar [!UICONTROL Target]

[!DNL Target Recommendations] requiere la implementación del SDK web de Adobe Experience Platform o at.js 0.9.2 (o posterior). Consulte la [[!UICONTROL Target] guías de implementación del lado del cliente](../client-side/overview.md) para obtener más información.

## 2. Configure su [!UICONTROL Recommendations] catalogar

Para ofrecer recomendaciones de alta calidad, [!UICONTROL Target] debe conocer los productos o el contenido que desea recomendar. Los catálogos suelen incluir tres tipos de información sobre los artículos recomendados. Supongamos que recomienda películas. Incluya lo siguiente:

1. Datos que desea mostrar al usuario que recibe la recomendación. Por ejemplo, puede mostrar el nombre de la película y una dirección URL para una imagen en miniatura del póster de la película.
1. Datos que son útiles para aplicar controles de marketing y comercialización. Por ejemplo, puede mostrar la clasificación de la película para que no recomiende las de mayores de 17 años.
1. Datos que son útiles para determinar la similitud de elementos con otros elementos. Por ejemplo, puede mostrar el género de la película y el director de la película.

[!UICONTROL Target] ofrece varias opciones de integración para rellenar el catálogo. Estas opciones se pueden utilizar en combinación para actualizar distintos artículos del catálogo o para actualizar atributos de artículos diferentes en distintas frecuencias.

| Método | Qué es | Cuándo utilizarla | Información adicional |
| --- | --- | --- | --- |
| Fuente de catálogo | Programe una fuente (CSV, XML de producto de Google o Clasificaciones de productos de Analytics) para que se cargue e incorpore diariamente. | Para enviar información sobre varios elementos a la vez. Para enviar información que cambia con poca frecuencia. | Consulte [Fuentes](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html). |
| API de entidades | Llame a una API para enviar actualizaciones al minuto de un solo elemento. | Para enviar actualizaciones a medida que se producen en un elemento a la vez. Para enviar información que cambia con frecuencia (por ejemplo, nivel de precio, inventario/stock). | Consulte la [Documentación para desarrolladores de API de entidades](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Pasar actualizaciones en la página | Envíe actualizaciones de último minuto para un solo elemento con JavaScript en la página o mediante la API de envío. | Para enviar actualizaciones a medida que se producen en un elemento a la vez. Para enviar información que cambia con frecuencia (por ejemplo, nivel de precio, inventario/stock). | Consulte [Vistas de elementos/páginas de productos](#item-views-or-product-pages) más abajo. |

La mayoría de los clientes deben implementar al menos una fuente. A continuación, puede elegir complementar su fuente con actualizaciones para atributos o elementos que se cambian con frecuencia mediante la API de entidades o el método en la página.

## 3. Pasar información y contexto de comportamiento

La información de comportamiento y el contexto que debe pasar a [!UICONTROL Target] depende de la acción que esté realizando el visitante, que a menudo está asociada al tipo de página con la que interactúa.

### Vistas de elementos o páginas de productos

En las páginas en las que un visitante está viendo un solo artículo, como una página de detalles del producto, debe pasar la identidad del artículo que el visitante está viendo. También debe pasar la categoría más granular del elemento que el visitante está viendo para permitir recomendaciones de filtrado a la categoría actual.

También puede pasar ciertos atributos que cambian rápidamente en la propia página del producto. Por ejemplo, puede pasar el precio (`value`) y nivel de inventario/stock.

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

En una página de carro de compras, puede recomendar elementos basados en el contenido del carro de compras actual del visitante. Para ello, pase los ID de todos los elementos del carro de compras actual del visitante utilizando el parámetro especial `cartIds`.

#### Pasar elementos actualmente en el carro

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Para obtener más información sobre las recomendaciones basadas en el carro de compras, consulte [Basado en el carro](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based) en el *[!DNL Adobe Target]Guía para profesionales de negocios*.

### Excluir elementos que ya están en el carro de compras del visitante

En páginas de todo el sitio, puede excluir algunos artículos de las recomendaciones. Por ejemplo, es posible que no desee recomendar elementos que ya están en el carro de compras actual del visitante. Para ello, pase los ID de todos los elementos que desee excluir mediante el parámetro especial `excludedIds`.

#### Pasar elementos que excluir

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Páginas de confirmación de pedidos/compras

Cuando se produce un evento de compra, pasa la identidad del artículo o artículos comprados. Consulte [Seguimiento de conversiones](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) en el [Implementación de at.js > Implementación [!UICONTROL Target] sin un administrador de etiquetas](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) artículo.

## 4. Configurar exclusiones globales

Excluya cualquier elemento de nivel global que no quiera que se recomiende a un visitante. Consulte [Exclusiones](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/exclusions.html) en el *[!DNL Adobe Target]Guía para profesionales de negocios*.

## 5. Configurar [!UICONTROL Recommendations] configuración

Utilice la configuración para administrar la implementación de [!UICONTROL Recommendations].

Para acceder a **[!UICONTROL Recommendations Settings]** , abra Target en la pestaña [!DNL Adobe Experience Cloud], luego haga clic en **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]**.

![Página Configuración de Recommendations](/help/dev/implement/recommendations/assets/recs_settings.png)

Las opciones disponibles son las siguientes:

| Configuración | Descripción |
|--- |--- |
| Mbox global personalizado | (Opcional) Especifique el mbox global personalizado que se usa para aprovisionar actividades de [!UICONTROL Target]. De forma predeterminada, el mbox global que utiliza [!UICONTROL Target] se usa para [!UICONTROL Recommendations].<P>Nota: Esta opción se configura en la variable [!UICONTROL Target] **[!UICONTROL Administration]** página. Abrir [!UICONTROL Target], luego haga clic en **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]**. |
| Sector | El sector se usa para ayudarle a categorizar los criterios de recomendaciones. Esta información ayuda a los miembros de su equipo a encontrar criterios que tienen sentido para una página en particular, como los criterios que son mejores para la página del carro de compras o para una página multimedia. |
| Criterios incompatibles de filtro | Habilite esta opción para mostrar únicamente aquellos criterios donde la página seleccionada pasa los datos necesarios. No todos los criterios se ejecutan correctamente en cada página. La página o el mbox deben pasar `entity.id` o `entity.categoryId` para que las recomendaciones de la categoría actual o el artículo actual sean compatibles. En general, se recomienda mostrar solamente criterios compatibles. Sin embargo, si desea que haya disponibles criterios incompatibles para la actividad, desactive esta opción.<P>Se recomienda deshabilitar esta opción si se usa una solución de administración de etiquetas.<P>Para obtener más información sobre esta opción, consulte [[!UICONTROL Recommendations] FAQ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html) en el *[!DNL Adobe Target]Guía para profesionales de negocios*. |
| Grupo de hosts predeterminado | Seleccione el grupo de hosts predeterminado.<P>El grupo de hosts puede utilizarse para separar los elementos disponibles en el catálogo para usos diferentes. Por ejemplo, puede utilizar grupos de hosts para entornos de desarrollo y producción, marcas diferentes o regiones geográficas diferentes. De forma predeterminada, la vista previa de los resultados en Búsqueda de catálogo, Colecciones y Exclusiones se basa en el grupo de hosts predeterminado. (También puede seleccionar otro grupo de hosts para obtener una vista previa de los resultados mediante el filtro Entorno). De forma predeterminada, los elementos recién añadidos están disponibles en todos los grupos de hosts a menos que se especifique un ID de entorno al crear o actualizar el elemento. Las recomendaciones enviadas dependen del grupo de hosts especificado en la solicitud.<P>Si no ve sus productos, asegúrese de que esté usando el grupo de hosts correcto. Por ejemplo, si configura que la recomendación use un entorno de ensayo y establece el grupo de hosts en Ensayo, puede que tenga que volver a crear las colecciones en el entorno de ensayo para que se puedan mostrar los productos. Para ver qué productos están disponibles en cada entorno, use Búsqueda en catálogo con cada entorno. También puede obtener una vista previa del contenido de [!UICONTROL Recommendations] colecciones y exclusiones para un entorno seleccionado (grupo de hosts).<P>**Nota:** Después de cambiar el entorno seleccionado, debe hacer clic en Buscar para actualizar los resultados devueltos.<P> **[!UICONTROL The Environment]** Este filtro está disponible en los siguientes lugares de la interfaz de usuario de Target:<ul><li>Búsqueda en el catálogo (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)</li><li>Cuadro de diálogo Crear colección (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create New]**)</li><li>Cuadro de diálogo Actualizar colección (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)</li><li>Cuadro de diálogo Crear exclusión (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create New]**)</li><li>Cuadro de diálogo Actualizar exclusión (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)</li></ul>Para obtener más información, consulte [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) en el *[!DNL Adobe Target]Guía para profesionales de negocios*. |
| Dirección URL de base en miniatura | Al establecer una dirección URL de base para su catálogo de productos, es posible usar direcciones URL relativas al especificar vistas en miniatura de sus productos al pasar su dirección URL de vista en miniatura.<P>Por ejemplo:<P>`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`<P>establece una dirección URL relativa para la dirección URL de base de vista en miniatura. |
| [!UICONTROL Recommendations] Token de API | Utilice este token en [!UICONTROL Recommendations] Llamadas a la API, como la API de descarga. |

## 6. (Opcional) Administrar [!UICONTROL Recommendations] uso de API de administrador

Consulte la [Uso [!UICONTROL Recommendations] API](../../before-administer/recs-api/overview.md) guía práctica para aprender a configurar y utilizar el [!UICONTROL Target] API de administración y envío para [!UICONTROL Recommendations].
