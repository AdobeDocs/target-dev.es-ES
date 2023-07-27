---
keywords: implementar, implementar, configurar, configurar, parámetro de página
description: Introducción de datos en [!DNL Target] uso de atributos de perfil en página.
title: ¿Cómo puedo obtener datos en? [!DNL Target] ¿Usar atributos de perfil en página?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 45%

---

# Atributos de perfil en página

Atributos de perfil en página en [!DNL Adobe Target] (también denominados &quot;atributos de perfil en mbox&quot;) son pares de nombre/valor que se pasan directamente a través del código de página y que se almacenan en el perfil del visitante para su uso futuro.

Los atributos de perfil en página permiten que los datos específicos del usuario se almacenen en el perfil de Target para una posterior segmentación.

## Formato

Los atributos de perfil en página se pasan a [!DNL Target] a través de una llamada al servidor como un par de nombre/valor de cadena con el prefijo &quot;perfil&quot;. antes del nombre del atributo.

Los nombres y valores del atributo se pueden personalizar, aunque hay algunos “nombres reservados” para usos específicos.

Estos son algunos ejemplos de atributos de perfil en página:

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## Casos de uso de ejemplo

* **Información de inicio de sesión**[!DNL Target]: comparta con datos con información que no permita identificar personalmente a los usuarios en función del inicio de sesión del usuario. Estos datos pueden ser el estado del abono, el historial de pedidos, etc.
* **Información de la tienda**: hace el seguimiento de cuál es la ubicación de la tienda preferida de este usuario.
* **Interacciones anteriores**: hace el seguimiento de las acciones realizadas anteriormente por el usuario en el sitio para proporcionar datos para una futura personalización.

## Ventajas del método

Los datos se envían a [!DNL Target] en tiempo real, y se pueden utilizar en la misma llamada de servidor en la que se incluyen los datos.

## Advertencias

Se requieren actualizaciones del código de la página (directamente o a través de un sistema de administración de etiquetas).

Los atributos y los valores son visibles en las llamadas de servidor, para que el visitante pueda ver los valores. Si comparte información, como rangos de crédito u otra información potencialmente privada, este método podría no ser el mejor enfoque.

## Ejemplos de código

targetPageParamsAll (sustituye los atributos en todas las llamadas mbox de la página):

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams (sustituye los atributos en el mbox global de la página):

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

Atributos en el código mboxCreate:

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## Vínculos a información relevante

[Atributos de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)

[Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html)
