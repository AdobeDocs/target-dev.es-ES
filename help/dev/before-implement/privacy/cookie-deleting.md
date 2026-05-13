---
keywords: cookie, cookies, eliminar cookie, eliminar  [!DNL Target] cookie, google chrome, chrome, mozilla firefox, firefox, microsoft edge, safari, cookie1
description: Aprenda a eliminar las cookies de su explorador  [!DNL Target] para que pueda validar sus experiencias.
title: ¿Cómo elimino la cookie  [!DNL Target] ?
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
TQID: https://experienceleague.adobe.com/t4ieDzmphu8NHTM9eGnaZMoeXk-Y1G05E4K6spdSs6Y
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d095671a-1355-40aa-8b5f-06c33c68080bid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 352
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
1. En ** Cookies y datos del sitio*, haga clic en **[!UICONTROL Manage Data]**.
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
