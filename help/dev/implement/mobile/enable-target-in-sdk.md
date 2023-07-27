---
keywords: aplicación móvil, sdk de aplicación móvil, segmentar por aplicación móvil, sdk de target móvil, sdk de aplicación móvil, habilitar target en sdk
description: Obtenga información sobre cómo añadir el SDK de Adobe Mobile Services a su aplicación móvil.
title: ¿Cómo habilito? [!DNL Target] en el [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 49%

---

# Activar [!DNL Target] en el SDK

Añada el [!UICONTROL SDK de Adobe Mobile Services] a su aplicación.

>[!IMPORTANT]
>
>Compatibilidad con el [!DNL Adobe Mobile] versión 4.*x* SDK finalizó el 31 de agosto de 2021 y ya no se recomienda para [!DNL Adobe Target] usuarios móviles.
>
>El [SDK de Adobe Experience Platform para aplicaciones móviles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} es la solución recomendada para alimentar [!DNL Adobe Experience Cloud] soluciones y servicios en sus aplicaciones móviles.

1. Si todavía no ha instalado el SDK de Adobe Mobile Services en su aplicación, use las credenciales de Analytics o Experience Cloud y descargue el SDK desde el sitio web de [Adobe Mobile Services](https://mobilemarketing.adobe.com/).

1. Añada el [!DNL Adobe Mobile Services SDK] a su aplicación.

   Encontrará las instrucciones en [Implementación básica y ciclo de vida](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html).

1. Añada código de cliente, tiempo de espera y habilite SSL.

   En Experience Cloud, abra Mobile Services y vaya a **[!UICONTROL Administrar configuración de aplicación]** > **[!UICONTROL Opciones de Target de SDK]**.

   Añada su [!DNL Target] clientcode y timeout. El código de cliente es exclusivo de la cuenta o compañía. El tiempo de espera es el tiempo en número de segundos hasta el cual [!DNL Target] esperará una respuesta antes de mostrar el contenido predeterminado. Compruebe que la opción **[!UICONTROL Utilizar HTTPS]** esté marcada en la página Administrar configuración de aplicación de Adobe Mobile Services. Si HTTPS no está habilitado, todas las llamadas que se realicen en iOS9 y versiones posteriores se bloquearán a menos que realice la lista de permitidos de [!DNL Target] servidor.

   ![imagen alt](assets/mobile-clientcode.png)

1. Cuando haya creado o encontrado la aplicación, busque la configuración de la aplicación y descargue el SDK que desee.

   ![imagen alt](assets/download-sdk.png)

>[!WARNING]
>
> Si no tiene acceso a la interfaz de marketing móvil, puede hacer los cambios directamente en el archivo de configuración en el código de la aplicación, pero no se sincronizarán con la página de configuración de la interfaz de usuario.
