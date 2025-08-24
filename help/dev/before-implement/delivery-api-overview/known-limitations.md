---
title: Consideraciones de la API de envío de Adobe Target y limitaciones conocidas
description: ¿Qué consideraciones y limitaciones conocidas debo tener en cuenta al usar [!UICONTROL Adobe Target Delivery API]?
keywords: api de envío
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 413b16ed0b098de6914558fa29b9ca59aaba958e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 3%

---

# Consideraciones y limitaciones conocidas

La siguiente información enumera consideraciones y limitaciones conocidas con el uso de [!DNL Adobe Target] [!DNL Delivery API].

* No hay autenticación para las API de entrega de [!DNL Target].
* Esta API no procesa cookies ni redirige llamadas.
* Los nombres de encabezado HTTP/1.1 y HTTP/2 no distinguen entre mayúsculas y minúsculas; sin embargo, HTTP/2 exige nombres de encabezado en minúsculas. Para obtener más información, consulte la [Documentación del Protocolo de transferencia de hipertexto versión 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Si utiliza un punto de conexión que dirija a los visitantes a través de su nueva infraestructura de equilibrador de carga, sus conexiones se actualizan automáticamente a HTTP/2. Este proceso de actualización convierte los encabezados de solicitud en encabezados en minúsculas para que no se consideren con un formato incorrecto.

  Este problema puede suponer un problema para los clientes si sus bibliotecas están configuradas para buscar encabezados de solicitud/respuesta que distingan entre mayúsculas y minúsculas (específicamente, no en minúsculas).

* Tenga cuidado al actualizar su [!DNL Recommendations] [!UICONTROL Catalog] a través de [!DNL Delivery API]. [!DNL Delivery API] es público, por lo que debe evitar utilizarlo para rellenar elementos en los que se puede hacer clic en su catálogo de recomendaciones. Al hacerlo, se puede introducir contenido invalidado y contaminar el catálogo.

  **Prácticas recomendadas**:

  Usar [!DNL Delivery API] solo para actualizar atributos de catálogo que:
   * Cambie con frecuencia (por ejemplo, precio o nivel de stock).
   * Siga un formato predefinido que se pueda validar fácilmente en su sitio web.
   * No lo utilice para agregar o modificar elementos en los que se puede hacer clic u otro contenido no verificado.
   * Si es necesario, puede solicitar al servicio de atención al cliente que deshabilite las actualizaciones del catálogo a través de la API de envío.

  Para obtener más información, consulte la documentación de [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}.
