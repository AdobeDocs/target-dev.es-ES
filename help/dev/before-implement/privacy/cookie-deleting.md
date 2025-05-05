---
keywords: cookie, cookies, eliminar cookie, eliminar  [!DNL Target] cookie, google chrome, chrome, mozilla firefox, firefox, microsoft edge, safari, cookie1
description: Aprenda a eliminar las cookies de su explorador  [!DNL Target] para que pueda validar sus experiencias.
title: ¿Cómo elimino la cookie  [!DNL Target] ?
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 3%

---

# Eliminar la cookie [!DNL Target]

Puede eliminar la cookie del explorador [!DNL Adobe Target] (mbox) para validar todas las experiencias durante la prueba.

Si no hay una cookie [!DNL Target] (mbox), se le considerará un visitante nuevo y se le mostrará una experiencia nueva. Existen varias formas de eliminar el mbox sin eliminar todas las cookies del explorador.

>[!NOTE]
>
>Las siguientes instrucciones son correctas para los exploradores y versiones enumerados. Busque en Internet las instrucciones de su navegador o versión específica.

## Eliminar la cookie [!DNL Target] de Google Chrome

Versión 84.0.4147,105

1. Haga clic en el menú **[!UICONTROL Chrome]** > **[!UICONTROL Preferences]**.
1. Haga clic en la ficha **[!UICONTROL Privacy and Security]**.
1. Haga clic en **[!UICONTROL Cookies and other site data]**.
1. Haga clic en **[!UICONTROL See all cookies and site data]**.
1. Expanda la sección `adobe.com`, seleccione la cookie **mbox** y haga clic en el icono Eliminar (X).

## Eliminar la cookie [!DNL Target] de Mozilla Firefox

Versión 79.0

### Eliminar todas las cookies asociadas con `adobe.com`

1. Haga clic en el menú **[!UICONTROL Firefox]** > **[!UICONTROL Preferences]**.
1. Haga clic en la ficha **[!UICONTROL Privacy and Security]**.
1. En **Cookies y datos del sitio*, haga clic en &#x200B;** [!UICONTROL Manage Data]**.
1. Seleccione el sitio `adobe.com` y luego haga clic en **[!UICONTROL Remove Selected]**.

>[!WARNING]
>
>Se eliminarán todas las cookies asociadas con el sitio `adobe.com`. Si desea eliminar una cookie individual para un sitio, siga las instrucciones a continuación.

### Eliminar una cookie individual (mbox)

1. En Firefox, haga clic en **[!UICONTROL Tools]** > **[!UICONTROL Web Developer]** > **[!UICONTROL Storage Inspector]**.
1. Haga clic en la ficha **[!UICONTROL Advanced]**.
1. Vaya a la página web que contiene la cookie que desea eliminar.
1. Expanda la sección **[!UICONTROL Cookies]** y haga clic en `https://experience.adobe.com`.
1. Haga clic con el botón derecho en la cookie **[!UICONTROL mbox]** y luego haga clic en **[!UICONTROL Delete]**.

## Eliminar la cookie [!DNL Target] de Microsoft Edge

Versión 84.0.522.52

1. Haga clic en el menú **[!UICONTROL Microsoft Edge]** > **[!UICONTROL Preferences]**.
1. Haga clic en la ficha **[!UICONTROL Site Permissions]**.
1. Haga clic en **[!UICONTROL Cookies and site data]**.
1. Haga clic en **[!UICONTROL See all cookies and site data]**.
1. Expanda la sección `adobe.com`, seleccione la cookie **mbox** y haga clic en el icono Eliminar (X).

## Eliminar la cookie [!DNL Target] de Apple Safari

Versión 13.1.2

### Eliminar todas las cookies asociadas con `adobe.com`

1. Haga clic en el menú **[!UICONTROL Safari]** > **[!UICONTROL Preferences]**.
1. Haga clic en la ficha **[!UICONTROL Privacy]**.
1. Haga clic en **[!UICONTROL Manage Website Data]**.
1. Seleccione los sitios para las cookies que desea eliminar y luego haga clic en **[!UICONTROL Remove]**.

>[!WARNING]
>
>Se eliminarán todas las cookies asociadas con el sitio `adobe.com`. Si desea eliminar una cookie individual para un sitio, siga las instrucciones a continuación.

### Eliminar una cookie individual (mbox)

1. Haga clic en el menú **[!UICONTROL Safari]** > **[!UICONTROL Preferences]**.
1. Haga clic en la ficha **[!UICONTROL Advanced]**.
1. Seleccione la opción **[!UICONTROL Show Develop menu in menu bar]**.
1. Vaya a la página web que contiene la cookie que desea eliminar.
1. Haga clic en el menú **[!UICONTROL Develop]** > **[!UICONTROL Show Web Inspector]**.
1. Haga clic en la ficha **[!UICONTROL Storage]**.
1. Expanda la sección **[!UICONTROL Cookies]** y haga clic en `www.adobe.com`.
1. Haga clic con el botón derecho en la cookie **mbox** y luego haga clic en **[!UICONTROL Delete]**.
