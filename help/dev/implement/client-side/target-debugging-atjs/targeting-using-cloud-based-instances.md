---
keywords: instancias en la nube, lista de sufijos públicos, sufijos públicos, cookie, cookie de origen, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com, targetGlobalSettings, cookieDomain, instancias en la nube5, instancias en la nube6, instancias en la nube7, instancias en la nube8, instancias en la nube9, lista de sufijos públicos0, lista de sufijos públicos1, lista de sufijos públicos2, lista de sufijos públicos3, lista de sufijos públicos4, lista de sufijos públicos5
description: Explorar problemas (con soluciones) a los que se enfrentan los clientes al usar instancias basadas en la nube para probar  [!DNL Adobe Target]  o con fines de prueba de concepto.
title: ¿Puedo usar  [!DNL Target] con instancias basadas en la nube?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
TQID: https://experienceleague.adobe.com/df63sTQxukCfa4pYc1X6FRvxV3cY2UG-ixk5v9Fqh-c
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 203
ht-degree: 46%

---

# Usar instancias basadas en la nube con [!DNL Target]

Información acerca de problemas que los clientes afrontan al usar instancias basadas en la nube para probar [!DNL Adobe Target].

Los clientes de [!DNL Target] utilizan en ocasiones instancias basadas en la nube con [!DNL Target] para realizar pruebas o simplemente exponer conceptos. Estas instancias podrían incluir los siguientes dominios:

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com` o `firebaseapp.com`.

Estos dominios, y muchos otros, son parte de la [Lista pública de sufijos](https://publicsuffix.org/list/public_suffix_list.dat).

**Problema:** los navegadores modernos no guardarán las cookies si utiliza estos dominios.

La biblioteca JavaScript de at.js usa cookies para realizar un seguimiento de los usuarios y garantizar que [!DNL [!DNL Target]] ofrezca siempre una experiencia coherente. Si la biblioteca JavaScript [!DNL Target] no puede guardar cookies, las solicitudes de Target se deshabilitarán.

**Solución:** Si piensa usar instancias basadas en la nube con dominios incluidos en la lista de sufijos públicos, es recomendable que se asegure de personalizar el ajuste `cookieDomain`. Para obtener más información, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).


