---
title: Información general de API de Adobe Target
description: Información general sobre las distintas API de Adobe Target, incluidas la API de envío, la API de informes, la API de administración, la API de perfil, la API de Recommendations y los vínculos a las colecciones de Postman.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/GbrWhrZxH-sTtpxotpJGbr-sHuIXrX7rZFQhju76-vM
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 448
ht-degree: 0%

---

# Resumen de API de Target

Este artículo describe las diferentes API de Target en general, antes de centrarse en los requisitos específicos de las API de administrador y perfil. Si desea administrar Target a través de la interfaz de usuario, consulte la sección [administración de la *Guía del usuario empresarial de Adobe Target*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).

## Tipos de API

Las API de Adobe Target son una colección de API que alimentan los productos de Adobe Target, como Adobe Recommendations. Estas API permiten la creación de interfaces de usuario enriquecidas con datos que puede utilizar para manipular e integrar datos.

Las API de Adobe Target se pueden agrupar según el tipo: Administración, Perfil, Envío y Creación de informes.

>[!NOTE]
>
>Las API de administrador y las API de perfil suelen denominarse de forma colectiva (&quot;API de administrador y de perfil&quot;), pero también pueden denominarse por separado (&quot;API de administrador&quot; y &quot;API de perfil&quot;). La API de Recommendations es una implementación específica de una API de administración de Target.

| Tipo de API | Lo que le permite hacer | Vínculo de descarga | Otros vínculos útiles |
| --- | --- | --- |--- |
| [Administrador](../administer/admin-api/admin-api-overview-new.md) | Cree, modifique y elimine actividades, audiencias, ofertas y otros objetos (incluidas entidades, criterios, diseños, etc. de Recommendations). Las API de Recommendations son un tipo de API de administrador). | <UL><li>[Colección de Postman de la API de administración de Target](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recopilación de Postman de la API de Recommendations](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL> | [Usar API de Recommendations](../before-administer/recs-api/overview.md) |
| Perfil | Recupere y modifique perfiles de usuario almacenados en Adobe Target. | [Colección de Postman de API de perfil de Target](https://developers.adobetarget.com/api/#profiles) |  |
| [Entrega](../implement/delivery-api/overview.md) | Recupere contenido optimizado y personalizado de Target para su entrega a un usuario final. | [Colección Postman de la API de envío de destino](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [Creación de informes](../administer/admin-api/admin-api-overview-new.md) | Exportar resultados de actividades y otros resultados de informes. | Las API de informes se incluyen en la [colección Postman de la API de administración de Target](https://developers.adobetarget.com/api/#admin-postman-collection). |  |
| [Modelos](../administer/models-api/models-api-overview.md) | Administre la lista de funciones que desea que Target excluya de sus modelos de aprendizaje automático (la &quot;lista de bloqueados&quot;). La API de modelos es un tipo de API de administración, pero se muestra aquí por separado debido a sus operaciones únicas con objetos (listas de bloqueados) a los que no se puede acceder mediante la interfaz de usuario. |  |  |

## Diferencias de API

Existen importantes distinciones entre las API de administrador de Target (incluidas las API de Recommendations) y las API de envío de Target:

* Las API de administrador permiten configurar varios aspectos de Target que también se pueden configurar en la interfaz de usuario de Target. La excepción a esto es la API de modelos, que le permite configurar aspectos de Target que no están disponibles en la interfaz de usuario. Independientemente, **todas las API de administrador requieren autenticación.**

* Las API de envío permiten recuperar contenido. Las API de envío no requieren autenticación.

Para usar las API de administrador de Target, debe configurar la autenticación mediante [Adobe Developer Console](https://developer.adobe.com/console/home). Para obtener más información, consulte [Cómo configurar la autenticación](../before-administer/configure-authentication.md).
