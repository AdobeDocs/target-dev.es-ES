---
keywords: api, adobe i/o, classic, adobe developer console
description: Aprenda a pasar de las  [!DNL Adobe Target Classic] API a las [!DNL Target] API en [!DNL Adobe Developer Console].
title: ¿Cómo hago la transición de  [!DNL Target Classic] API a [!DNL Target] API en [!DNL Adobe Developer Console]?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# Transición de [!DNL Target Classic] API a [!DNL Target] API en [!DNL Adobe Developer Console]

Información para ayudarle con la transición de las API [!DNL Target Classic] a las API [!DNL Target] en [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Con la retirada del servicio de [!DNL Adobe Target Classic], las API conectadas a su cuenta de [!DNL Target Classic] tampoco estarán disponibles. Este artículo le ayudará con la transición de sus integraciones basadas en API de [!DNL Target Classic] a las API de [!DNL Target] con tecnología de [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Para obtener más información sobre las API de [!DNL Target], consulte [[!DNL Target] API](/help/dev/before-administer/target-api-overview.md). Para obtener más información sobre los SDK de [!DNL Target], consulte [[!DNL Target] Implementación del lado del servidor](/help/dev/implement/server-side/server-side-overview.md)

## Terminología  

| Término | Descripción |
|--- |--- |
| API clásica | API vinculadas a su cuenta de [!DNL Target Classic]. Estas llamadas a API se basan en una autenticación mediante nombre de usuario y contraseña, y utilizan el nombre de host `testandtarget.omniture.com`. Si las llamadas a la API contienen un nombre de usuario y una contraseña en la dirección URL de la solicitud, debe realizar la transición a las API [!DNL Adobe Developer Console]. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | [!DNL Adobe Developer Console] es la puerta de enlace para las API de [!DNL Target]. Estas API están conectadas a su cuenta de [!DNL Target Standard/Premium]. Las API [!DNL Target] en [!DNL Adobe Developer Console] utilizan una [autenticación basada en JWT](../../before-administer/configure-authentication.md), que es el estándar en la industria para las API de empresa seguras. |

## Cronología  

Las siguientes API se retiraron al retirar [!DNL Target Classic]:

| Fecha | Detalles |
|--- |--- |
| 17 de octubre de 2017 | Se han retirado todos los métodos API que realizan una operación de escritura (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent` y `setCampaignState`).<P>La fecha es la misma en la que todas las cuentas de usuario de [!DNL Target Classic] quedaron en estado de solo lectura. |
| 14 de noviembre de 2017 | Se han retirado las API restantes. Esta es la fecha en la que se retiró del mercado la interfaz de usuario [!DNL Target Classic] |

Las API [!DNL Recommendations Classic] no se vieron afectadas por esta cronología.

## Métodos equivalentes  

En la tabla siguiente se enumeran los métodos de API equivalentes de [!DNL Adobe Developer Console] para los métodos de API clásicos. Las API [!DNL Adobe Developer Console] devuelven JSON, mientras que las API clásicas devuelven XML.

Los métodos de API [!DNL Adobe Developer Console] están vinculados a la sección correspondiente del sitio de documentación de API. Se proporciona un ejemplo para cada método API. También puede usar la colección de Postman de la API de administración [!DNL Target] que contiene llamadas de API de ejemplo para todos los métodos de API de Adobe en [!DNL Adobe Developer Console].

| Grupo | Método de API clásico | Método de API [!DNL Adobe Developer Console] | Notas |
|--- |--- |--- |--- |
| Campaña/Actividad | Creación de campaña | [Crear actividad AB](https://developers.adobetarget.com/api/#create-ab-activity)<P>[Crear actividad XT](https://developers.adobetarget.com/api/#create-xt-activity) | Las nuevas API proporcionan métodos de creación distintos para AB y XT |
|  | Actualización de campaña | [Actualizar actividad AB](https://developers.adobetarget.com/api/#update-ab-activity)<P>[Actualizar actividad XT](https://developers.adobetarget.com/api/#update-xt-activity) |  |
|  | Copiar campaña | N/A | Se usan las API de creación de actividad |
|  | Lista de campañas | [Listar actividades](https://developers.adobetarget.com/api/#list-activities) |  |
|  | Estado de la campaña | [Actualizar el estado de la actividad](https://developers.adobetarget.com/api/#update-activity-state) |  |
|  | Vista de la campaña | [Obtener actividad AB por ID](https://developers.adobetarget.com/api/#get-ab-activity-by-id)<P>[Obtener actividad XT por ID](https://developers.adobetarget.com/api/#get-xt-activity-by-id) |  |
|  | ID de campaña de terceros | N/A | Si utiliza un thirdpartyID, pueden usarse los métodos de actividad relevantes |
| Ofertas | Creación de oferta | [Crear oferta](https://developers.adobetarget.com/api/#create-offer) |  |
|  | Obtención de oferta | [Obtener oferta por ID](https://developers.adobetarget.com/api/#get-offer-by-id) |  |
|  | Lista de ofertas | [Listar ofertas](https://developers.adobetarget.com/api/#list-offers) |  |
|  | Lista de carpetas | N/A | No se admiten carpetas en [!DNL Target Standard/Premium] |
| Creación de informes | Informe de rendimiento de la campaña | [Obtener informe de rendimiento AB](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[Obtener informe de rendimiento XT](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | Informe de auditoría | [Obtener informe de auditoría](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | Informe de contenido 1-1 | [Obtener informe de rendimiento AP](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| Configuración de la cuenta | Obtener grupos de hosts | [Listar entornos](https://developers.adobetarget.com/api/#list-environments) |  |

## Excepciones

Si necesita una excepción, póngase en contacto con el gestor de éxito de los clientes.

## Ayuda  

Póngase en contacto con [!DNL Adobe Target Client Care] (tt-support@adobe.com) si tiene alguna pregunta o necesita ayuda en la transición de las API clásicas a las API [!DNL Target] en [!DNL Adobe Developer Console].
