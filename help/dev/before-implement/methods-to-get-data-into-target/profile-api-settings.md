---
keywords: implementación, api, perfil, configuración de la api de perfil, token de autenticación
description: Obtenga información sobre cómo configurar la autenticación para actualizaciones por lotes mediante  [!DNL Adobe Target] API y generar un token de autenticación de perfil.
title: ¿Cómo utilizo la configuración de la API del perfil para habilitar o deshabilitar las actualizaciones por lotes?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 28%

---

# Configuración de la API de perfil

Habilite o deshabilite la autenticación para actualizaciones en lote mediante las API [!DNL Adobe Target] y genere un token de autenticación de perfil.

[!DNL Adobe Target] crea y mantiene un perfil para cada usuario individual. Este perfil se almacena en el clúster perimetral [!DNL Target] y se actualiza en tiempo real después de cada visita. También puede actualizar un perfil de forma individual o en lote mediante API.

Para mayor seguridad, puede requerir que la llamada a la API de actualización masiva requiera que se pase un token de acceso válido en el encabezado de la solicitud.

**Para requerir autenticación y generar un token de acceso mediante la interfaz de usuario de [!DNL Target]:**

1. Haga clic en **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. En **[!UICONTROL Profile API]**, deslice el conmutador **[!UICONTROL Require Authentication]** a la posición habilitada o deshabilitada.

   ![imagen alt](assets/profile_api_settings.png)

1. (Condicional) Si habilitó el requisito de autenticación, haga clic en **[!UICONTROL Generate New Profile Authentication Token]**.

   ![imagen alt](assets/profile_api_settings_2.png)

   El token caduca según el tiempo indicado en el cuadro Caduca en.

   Debe tener uno de los siguientes permisos de usuario para generar un token de autenticación:

   * Función de administrador o tener al menos derechos de aprobador

     Para obtener más información para los clientes de Target Standard, consulte [Especificar funciones y permisos](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) en *Usuarios*. Para obtener más información para los clientes de [!DNL Target Premium], consulte [Configuración de permisos de Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Función de administrador en el nivel de espacio de trabajo/perfil de producto

     Los espacios de trabajo solo están disponibles para los clientes de [!DNL Target Premium]. Para obtener más información, consulte [Permisos de usuario de Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Derechos de administrador (permiso Sysadmin) en el nivel de producto [!DNL Adobe Target]

También puede generar un token de autentificación de perfil mediante API. Para obtener más información, consulte &quot;Perfiles&quot; en la [guía de API de perfil y administrador de Adobe Target](../../administer/admin-api/admin-api-overview-new.md).

1. Copie el token e inclúyalo en el encabezado de la solicitud con el formato: &quot;Autorización&quot; : &quot;Portador&quot;.

1. Haga clic en **[!UICONTROL Generate New Profile Authentication Token]** para regenerar el token según sea necesario.

>[!WARNING]
>
>Restablecer este token provoca que las llamadas a API realizadas con el token actual resulten fallidas. Deberá actualizar cualquier script o aplicación que utilice este token.
