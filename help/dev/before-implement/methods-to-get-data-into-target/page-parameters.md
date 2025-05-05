---
keywords: implementar, implementar, configurar, configurar, parámetros de página
description: Obtener datos en  [!DNL Target] usando parámetros de página.
title: ¿Cómo obtengo datos en  [!DNL Target] usando parámetros de página?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 32%

---

# Parámetros de página

Los parámetros de página (también denominados &quot;parámetros de mbox&quot;) son pares de nombre/valor que se pasan directamente a través del código de página y que no se almacenan en el perfil del visitante para su uso futuro.

Los parámetros de página son útiles para enviar datos de página a [!DNL Adobe Target] que no necesitan almacenarse con el perfil del visitante para un uso de segmentación futuro. Estos valores, en cambio, se utilizan para describir la página o la acción realizada por el usuario en la página específica.

## Formato

Los parámetros de página se pasan a [!DNL Target] mediante una llamada al servidor como un par de nombre de cadena y valor. Los nombres y valores del parámetro se pueden personalizar, aunque hay algunos “nombres reservados” para usos específicos.

Estos son algunos ejemplos de parámetros de página

* `page=productPage`

* `categoryId=homeLoans`

## Casos de uso de ejemplo

* **Páginas de producto**: envía información sobre el producto específico visualizado (así es como funciona Recommendations)
* **Detalles del pedido**: envía el ID de pedido, el total, etc. para la colección de pedidos
* **Afinidad de la categoría**: envía información visualizada por categorías a [!DNL Target] para dar a conocer la afinidad del usuario con categorías concretas de sitios
* **Datos de terceros**: envía información de fuentes de datos de terceros, como proveedores de segmentación por tiempo, datos de la cuenta (por ejemplo, DemandBase), datos demográficos (por ejemplo, Experian) y más.

## Ventajas del método

Los datos se envían a [!DNL Target] en tiempo real y se pueden usar en la misma llamada de servidor de los datos en los que aparecen.

## Advertencias

* Se requiere la actualización del código de la página (directamente o a través de un sistema de administración de etiquetas).
* Si los datos deben utilizarse para la segmentación en una llamada posterior a la página o al servidor, deben traducirse a un script de perfil.
* Las cadenas de consulta sólo pueden contener caracteres según el estándar [Grupo de Trabajo de Ingeniería de Internet (IETF, Internet Engineering Task Force)](https://www.ietf.org/rfc/rfc3986.txt) .

  Además de los caracteres mencionados en el sitio IETF, [!DNL Target] permite los siguientes caracteres en las cadenas de consulta:

  ```< > # % " { } | \ ^ [ ] ` ``` {line-numbers=&quot;true&quot;}

  Todo lo demás debe tener codificación URL. El estándar especifica el siguiente formato ( [https://www.ietf.org/rfc/rfc1738.txt](https://www.ietf.org/rfc/rfc1738.txt) ), como se muestra a continuación:

  ![imagen alt](assets/ietf1.png)

  O, la lista completa para más simplicidad:

  ![imagen alt](assets/ietf2.png)

## Ejemplos de código

targetPageParamsAll (sustituye los parámetros en todas las llamadas mbox de la página):

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams (sustituye los parámetros en el mbox global de la página):

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## Vínculos a información relevante

Recommendations: [implementación según el tipo de página](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=es)

Confirmación del pedido: [Rastrear conversiones](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

Afinidad de la categoría: [afinidad de la categoría](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=es)
