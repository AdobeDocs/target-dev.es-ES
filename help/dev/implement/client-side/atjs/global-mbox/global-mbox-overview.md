---
keywords: mbox global, implementar at.js
description: Obtenga información acerca del mbox global en la implementación de  [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] .
title: Qué es un mbox global?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
TQID: https://experienceleague.adobe.com/MXEGvHHY8tFMfS6bMHcZYaG9mZtOWEkuODKH24JifZI
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 201
ht-degree: 61%

---

# Comprender el mbox global

Información sobre el mbox global, un nombre usado para hacer referencia a la llamada al servidor única que se realiza en la parte superior de cada página web en su implementación de [!DNL Adobe Target].

El nombre predeterminado del mbox global es `target-global-mbox`. Si fuera necesario, puede cambiarse el nombre para su cuenta.

Hay muchas diferencias entre un mbox normal (mbox no global) y el mbox global, entre las que se incluyen:

| Mbox normal | Mbox global |
|--- |--- |
| Un mbox normal suele encapsular contenido con una etiqueta `<DIV>`. | El mbox global está “vacío” y no encapsula ningún contenido. |
| El contenido de una sola actividad puede entregarse en un mbox normal. | El contenido de varias actividades puede entregarse en una sola respuesta a un mbox global. |

Si se envían varias actividades a través del mbox global o a través de varios mboxes normales, el objetivo [determina la prioridad](https://experienceleague.adobe.com/docs/target/using/activities/priority.html) mediante la cual la actividad (o actividades) se envía a una página web.

Pueden enviarse a [!DNL Target] datos adicionales a nivel de página junto con el mbox global con la función `[!UICONTROL targetPageParams]`. Esta opción es parecida a la funcionalidad de parámetro de mbox. Para obtener más información, consulte [Transferencia de parámetros a un mbox global](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).
