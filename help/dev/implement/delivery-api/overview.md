---
title: Información general de API de envío Adobe Target
description: Información general de API de envío Adobe Target
keywords: API de envío
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/gPXGax6ccvZZPklT3jnZbqyOj3mCClEfSpdufAFPtSs
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: b6b447ccb88925a8efb6ff6a80ae475c8780dbc8
workflow-type: tm+mt
source-wordcount: 244
ht-degree: 0%

---

# Resumen de API de envío

[!DNL Adobe Target Delivery API] se basa en REST. Esta documentación describe los recursos que componen [!DNL Adobe Target] [!DNL Delivery API]. Los métodos HTTP se utilizan para ejecutar operaciones en esos recursos.

>[!IMPORTANT]
>
>El(la) [!DNL Delivery API] documentado(a) aquí está destinado(a) a [!DNL at.js] e implementaciones directas del lado del servidor. Si va a implementar [!DNL Target] mediante [!DNL Adobe Experience Platform Web SDK], use la API de Interact, a la que se tiene acceso mediante el comando `sendEvent` a través de [!UICONTROL Experience Platform Edge Network], en lugar de llamar directamente a [!DNL Delivery API]. Consulte [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md) y [Compare la biblioteca at.js con Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) para obtener más información.

Con la [!UICONTROL API de envío de Adobe Target], puede:

* Ofrezca experiencias en toda la web, incluidas las SPA y los canales móviles, así como dispositivos de IoT no basados en el explorador, como un TV conectado, un quiosco o una pantalla digital en la tienda.
* Ofrezca experiencias desde cualquier plataforma o aplicación del lado del servidor que pueda realizar llamadas HTTP/S.
* Ofrezca experiencias coherentes y personalizadas a un usuario, independientemente del canal o los dispositivos que este haya utilizado en su negocio.
* Almacene en caché las experiencias de un usuario dentro de una sesión en su servidor para que se puedan evitar múltiples llamadas a la API y, como resultado, lograr un mejor rendimiento.
* Se integra perfectamente con [!DNL Adobe Experience Cloud] productos como [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] y [!DNL Experience Cloud ID Service] del lado del servidor.

>[!NOTE]
>
>Puede seguir teniendo acceso a la [documentación heredada de la API /v1/mbox y /v2/batchmbox](https://developers.adobetarget.com/api/legacy-api/index.html). Sin embargo, se desarrollarán funciones en la API de envío (como se documenta aquí) que no se transferirán a las API heredadas.
