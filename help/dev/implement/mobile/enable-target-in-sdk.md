---
keywords: aplicación móvil, sdk de aplicación móvil, segmentar por aplicación móvil, sdk de target móvil, sdk de aplicación móvil, habilitar target en sdk
description: Obtenga información sobre cómo añadir el SDK de Adobe Mobile Services a su aplicación móvil.
title: ¿Cómo habilito  [!DNL Target] en [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 29%

---

# Habilitar [!DNL Target] en el SDK

Agregue [!UICONTROL Adobe Mobile Services SDK] a su aplicación.

>[!IMPORTANT]
>
>Compatibilidad con [!DNL Adobe Mobile] versión 4.Los SDK de *x* finalizaron el 31 de agosto de 2021 y ya no se recomiendan para [!DNL Adobe Target] usuarios móviles.
>
>El SDK de [Adobe Experience Platform para aplicaciones móviles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} es la solución recomendada para impulsar [!DNL Adobe Experience Cloud] soluciones y servicios en sus aplicaciones móviles.

1. Si no ha instalado el SDK de Adobe Mobile Services en su aplicación, use sus credenciales de Analytics o de Experience Cloud y descargue el SDK del sitio web de [Adobe Mobile Services](https://mobilemarketing.adobe.com/).

1. Agregue [!DNL Adobe Mobile Services SDK] a su aplicación.

   Encontrará las instrucciones en [Implementación básica y ciclo de vida](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html).

1. Añada código de cliente, tiempo de espera y habilite SSL.

   En el Experience Cloud, abra Mobile Services y vaya a **[!UICONTROL Manage App Settings]** > **[!UICONTROL SDK Target Options]**.

   Agregue su código de cliente [!DNL Target] y tiempo de espera. El código de cliente es exclusivo de la cuenta o compañía. El tiempo de espera es el tiempo en número de segundos hasta el cual [!DNL Target] esperará una respuesta antes de mostrar el contenido predeterminado. Asegúrese de que la opción **[!UICONTROL Use HTTPS]** esté marcada en la página Administrar configuración de aplicación de Adobe Mobile Services. Si HTTPS no está habilitado, todas las llamadas que se hagan en iOS9 y versiones posteriores se bloquearán a menos que realice una lista de permitidos del servidor [!DNL Target].

   ![imagen alt](assets/mobile-clientcode.png)

1. Cuando haya creado o encontrado la aplicación, busque la configuración de la aplicación y descargue el SDK que desee.

   ![imagen alt](assets/download-sdk.png)

>[!WARNING]
>
> Si no tiene acceso a la interfaz de marketing móvil, puede hacer los cambios directamente en el archivo de configuración en el código de la aplicación, pero no se sincronizarán con la página de configuración de la interfaz de usuario.
