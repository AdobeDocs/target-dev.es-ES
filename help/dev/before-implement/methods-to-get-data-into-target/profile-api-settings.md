---
keywords: implementación, api, perfil, configuración de la api de perfil, token de autenticación
description: Obtenga información sobre cómo configurar la autenticación para actualizaciones por lotes mediante  [!DNL Adobe Target] API y generar un token de autenticación de perfil.
title: ¿Cómo utilizo la configuración de la API del perfil para habilitar o deshabilitar las actualizaciones por lotes?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
TQID: https://experienceleague.adobe.com/-KYSphaCrm0ICK7g92v9x-uK--nwirs4-DWBR3G5rTM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 363
ht-degree: 31%

---

# Configuración de la API de perfil

Habilite o deshabilite la autenticación para actualizaciones en lote mediante las API [!DNL Adobe Target] y genere un token de autenticación de perfil.

[!DNL Adobe Target] crea y mantiene un perfil para cada usuario individual. Este perfil se almacena en el clúster perimetral [!DNL Target] y se actualiza en tiempo real después de cada visita. También puede actualizar un perfil de forma individual o en lote mediante API.

Como seguridad adicional, puede requerir que la llamada a la API de actualización por lotes solicite que se pase un token de acceso válido en el encabezado de la solicitud.

**Para requerir autenticación y generar un token de acceso mediante la interfaz de usuario de [!DNL Target]:**

1. Haga clic en **[!UICONTROL Administración]** > **[!UICONTROL Implementación]**.
1. En la **[!UICONTROL API de perfil]**, deslice la opción **[!UICONTROL Requerir autenticación]** a la posición habilitada o deshabilitada.

   ![imagen alt](assets/profile_api_settings.png)

1. (Condicional) Si habilitó el requisito de autenticación, haga clic en **[!UICONTROL Generar nuevo token de autenticación de perfil]**.

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

1. Haga clic en **[!UICONTROL Generar nuevo token de autenticación de perfil]** para volver a generar el token según sea necesario.

>[!WARNING]
>
>Restablecer este token provoca que las llamadas a API realizadas con el token actual resulten fallidas. Deberá actualizar cualquier script o aplicación que utilice este token.
