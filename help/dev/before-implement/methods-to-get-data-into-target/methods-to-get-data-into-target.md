---
keywords: implementar, implementar, configurar, configurar, parámetro de página, tomcat, codificación url, atributo de perfil en página, parámetro mbox, atributos de perfil en página, atributo de perfil en script, API de actualización de perfiles en lote, API de actualización de archivo único, atributos del cliente, implementar5, implementar6, implementar7, implementar8, implementar9, implementar0, implementar1, implementar2, implementar3, implementar4, implementar5, proveedores de datos, proveedor de datos, proveedor de datos
description: Obtenga datos en  [!DNL Target] (parámetros de página, atributos de perfil, atributos de perfil de secuencia de comandos, proveedores de datos, API de actualización de perfiles únicas y masivas, atributos del cliente).
title: ¿Cómo puedo obtener datos en Target?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
TQID: https://experienceleague.adobe.com/pmlPWRHb9tnrdSFm7s5OZ-RRsJJOxw-ntBY5AeswIcM
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 377
ht-degree: 27%

---

# Información general sobre métodos

Información sobre los distintos métodos que se pueden utilizar para introducir datos en Adobe Target.

Los métodos disponibles incluyen:

| Método | Detalles |
| --- | --- |
| [Parámetros de página](page-parameters.md)<br />(también denominados &quot;parámetros de mbox&quot;) | Los parámetros de página son pares de nombre-valor pasados directamente a través del código de página que no se almacenan en el perfil del visitante para un uso futuro.<br />Los parámetros de página son útiles para enviar datos de página a [!DNL Target] que no necesitan almacenarse con el perfil del visitante para un uso de segmentación futuro. Estos valores, en cambio, se utilizan para describir la página o la acción realizada por el usuario en la página específica. |
| [Atributos de perfil en página](in-page-profile-attributes.md)<br />(también denominados &quot;atributos de perfil en mbox&quot;) | Los atributos de perfil en página son pares de nombre/valor que pasan directamente a través del código de página y que se almacenan en el perfil del visitante para su uso futuro.<br />Los atributos de perfil en página permiten que los datos específicos del usuario se almacenen en el perfil de Target para su segmentación y direccionamiento posteriores. |
| [Atributos de perfil en script](script-profile-attributes.md) | Los atributos de perfil de script son pares de nombre/valor definidos en la solución [!DNL Target]. El valor se determina a partir de la ejecución de un fragmento JavaScript en el servidor de Target por llamada de servidor.<br />Los usuarios escriben pequeños fragmentos de código que se ejecutan por llamada de mbox y antes de que se evalúe la pertenencia de un visitante a audiencias y actividades. |
| [Proveedores de datos](data-providers.md) | Los proveedores de datos le permiten pasar fácilmente datos de terceros a Target. |
| [API de actualización de perfiles en lote](bulk-profile-update-api.md) | Mediante API, envíe un archivo .csv a [!DNL Target] con actualizaciones del perfil del visitante para muchos visitantes. Cada perfil de visitante se puede actualizar con varios atributos de perfil en página con una llamada. |
| [API de actualización de perfil único](single-profile-update-api.md) | Casi idéntico a la API de actualización de perfiles en lote, pero se actualiza un perfil de visitante a la vez, en línea en la llamada de API en lugar de con un archivo .csv. |
| [Atributos del cliente](customer-attributes.md) | Los atributos del cliente le permiten cargar datos de perfil del visitante a través del FTP a Experience Cloud. Una vez cargados, utilice los datos en Adobe Analytics y Adobe Target. |
