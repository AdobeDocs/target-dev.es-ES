---
keywords: api, adobe i/o, classic, adobe developer console
description: Aprenda a realizar la transición desde el [!DNL Adobe Target Classic] API para [!DNL Target] API en [!DNL Adobe Developer Console].
title: ¿Cómo puedo realizar la transición desde [!DNL Target Classic] API para [!DNL Target] API en [!DNL Adobe Developer Console]?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 34%

---

# Transición desde [!DNL Target Classic] API para [!DNL Target] API en [!DNL Adobe Developer Console]

Información para ayudarle con la transición desde [!DNL Target Classic] API para [!DNL Target] API en [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Con la clausura de [!DNL Adobe Target Classic], las API conectadas a su [!DNL Target Classic] La cuenta de también se ha bloqueado. Este artículo le ayudará con la transición de su [!DNL Target Classic] Integraciones basadas en API con [!DNL Target] API con tecnología de [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Para obtener más información acerca de [!DNL Target] API, consulte [[!DNL Target] API](/help/dev/before-administer/target-api-overview.md). Para obtener más información acerca de [!DNL Target] SDK, consulte [[!DNL Target] Implementación del lado del servidor](/help/dev/implement/server-side/server-side-overview.md)

## Terminología  

| Término | Descripción |
|--- |--- |
| API clásica | API vinculadas a su [!DNL Target Classic] cuenta. Estas llamadas a API se basan en una autenticación mediante nombre de usuario y contraseña, y utilizan el nombre de host `testandtarget.omniture.com`. Si las llamadas de API contienen un nombre de usuario y una contraseña en la dirección URL de la solicitud, debe realizar la transición a la variable [!DNL Adobe Developer Console] API. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | El [!DNL Adobe Developer Console] es la puerta de enlace para [!DNL Target] API. Estas API están conectadas a su [!DNL Target Standard/Premium] cuenta. El [!DNL Target] API en [!DNL Adobe Developer Console] use un [Autenticación basada en JWT](../../before-administer/configure-authentication.md), que es el estándar en la industria para las API seguras para empresas. |

## Cronología  

Las siguientes API se retiraron al [!DNL Target Classic] se ha retirado del mercado:

| Fecha | Detalles |
|--- |--- |
| 17 de octubre de 2017 | Se han retirado todos los métodos API que realizan una operación de escritura (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent` y `setCampaignState`).<P>Es la misma fecha en que todos los [!DNL Target Classic] las cuentas de usuario se han establecido en estado de solo lectura. |
| 14 de noviembre de 2017 | Se han retirado las API restantes. Esta es la fecha en la que [!DNL Target Classic] se ha retirado la interfaz de usuario |

[!DNL Recommendations Classic] Las API no se vieron afectadas por esta cronología.

## Métodos equivalentes  

La siguiente tabla enumera el equivalente [!DNL Adobe Developer Console] Métodos de API para los métodos de API clásicos. El [!DNL Adobe Developer Console] Las API devuelven JSON, mientras que las API clásicas devuelven XML.

El [!DNL Adobe Developer Console] Los métodos de API están vinculados a la sección correspondiente del sitio de documentación de la API. Se proporciona un ejemplo para cada método API. También puede utilizar la variable [!DNL Target] Recopilación de Postman de la API de administración que contiene llamadas de API de ejemplo para todos los métodos de API de Adobe en la [!DNL Adobe Developer Console].

| Grupo | Método de API clásico | [!DNL Adobe Developer Console] Método de API | Notas |
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
|  | Lista de carpetas | N/A | Las carpetas no son compatibles con [!DNL Target Standard/Premium] |
| Creación de informes | Informe de rendimiento de la campaña | [Obtener informe de rendimiento AB](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[Obtener informe de rendimiento XT](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | Informe de auditoría | [Obtener informe de auditoría](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | Informe de contenido 1-1 | [Obtener informe de rendimiento AP](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| Configuración de la cuenta | Obtener grupos de hosts | [Listar entornos](https://developers.adobetarget.com/api/#list-environments) |  |

## Excepciones

Si necesita una excepción, póngase en contacto con el gestor de éxito de los clientes.

## Ayuda  

Póngase en contacto con [!DNL Adobe Target Client Care] (tt-support@adobe.com) si tiene alguna pregunta o necesita ayuda en la transición de las API clásicas a la [!DNL Target] API en [!DNL Adobe Developer Console].
