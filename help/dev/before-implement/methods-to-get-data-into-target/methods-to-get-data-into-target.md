---
keywords: implementar, implementar, configurar, configurar, parámetro de página, tomcat, codificación url, atributo de perfil en página, parámetro mbox, atributos de perfil en página, atributo de perfil en script, API de actualización de perfiles en lote, API de actualización de archivo único, atributos del cliente, implementar5, implementar6, implementar7, implementar8, implementar9, implementar0, implementar1, implementar2, implementar3, implementar4, implementar5, proveedores de datos, proveedor de datos, proveedor de datos
description: Introducción de datos en [!DNL Target] (parámetros de página, atributos de perfil, atributos de perfil de secuencia de comandos, proveedores de datos, API de actualización de perfiles únicas y masivas, atributos del cliente).
title: ¿Cómo puedo obtener datos en Target?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 44%

---

# Información general sobre métodos

Información sobre los distintos métodos que se pueden utilizar para introducir datos en Adobe Target.

Los métodos disponibles incluyen:

| Método | Detalles |
| --- | --- |
| [Parámetros de página](page-parameters.md)<br />(También denominados &quot;parámetros de mbox&quot;) | Los parámetros de página son pares de nombre-valor pasados directamente a través del código de página que no se almacenan en el perfil del visitante para un uso futuro.<br />Los parámetros de página son útiles para enviar datos de página a [!DNL Target] que no necesita almacenarse con el perfil del visitante para su uso futuro como objetivo. Estos valores, en cambio, se utilizan para describir la página o la acción realizada por el usuario en la página específica. |
| [Atributos de perfil en página](in-page-profile-attributes.md)<br />(También denominados &quot;atributos de perfil en mbox&quot;) | Los atributos de perfil en página son pares de nombre-valor pasados directamente a través del código de página que se almacenan en el perfil del visitante para un uso futuro.<br />Los atributos de perfil en página permiten que los datos específicos del usuario se almacenen en el perfil de Target para una posterior segmentación. |
| [Atributos de perfil en script](script-profile-attributes.md) | Los atributos de perfil de secuencia de comandos son pares de nombre/valor definidos en la variable [!DNL Target] solución. El valor se determina a partir de la ejecución de un fragmento JavaScript en el servidor de Target por llamada de servidor.<br />Los usuarios escriben pequeños fragmentos de código que se ejecutan mediante una llamada de mbox y antes de que el visitante se evalúe por audiencia y abono a la actividad. |
| [Proveedores de datos](data-providers.md) | Los proveedores de datos le permiten pasar fácilmente datos de terceros a Target. |
| [API de actualización de perfiles en lote](bulk-profile-update-api.md) | Mediante API, envíe un archivo .csv a [!DNL Target] con actualizaciones del perfil del visitante para muchos visitantes. Cada perfil de visitante se puede actualizar con varios atributos de perfil en página con una llamada. |
| [API de actualización de perfil único](single-profile-update-api.md) | Casi idéntico a la API de actualización de perfiles en lote, pero se actualiza un perfil de visitante a la vez, en línea en la llamada de API en lugar de con un archivo .csv. |
| [Atributos del cliente](customer-attributes.md) | Los atributos del cliente le permiten cargar datos de perfil del visitante a través del FTP a Experience Cloud. Una vez cargados, utilice los datos en Adobe Analytics y Adobe Target. |
