---
title: Información general de API de envío Adobe Target
description: Información general de API de envío Adobe Target
keywords: api de envío
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
source-git-commit: ccc27e66207e58dcd33865e5d28a51644e8e1931
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Resumen de API de envío

[!DNL Adobe Target Delivery API] se basa en REST. Esta documentación describe los recursos que componen [!DNL Adobe Target] [!DNL Delivery API]. Los métodos HTTP se utilizan para ejecutar operaciones en esos recursos.

Con [!UICONTROL Adobe Target's Delivery API], puede:

* Ofrezca experiencias en toda la web, incluidas las SPA y los canales móviles, así como dispositivos de IoT no basados en el explorador, como un TV conectado, un quiosco o una pantalla digital en la tienda.
* Ofrezca experiencias desde cualquier plataforma o aplicación del lado del servidor que pueda realizar llamadas HTTP/S.
* Ofrezca experiencias coherentes y personalizadas a un usuario, independientemente del canal o los dispositivos que este haya utilizado en su negocio.
* Almacene en caché las experiencias de un usuario dentro de una sesión en su servidor para que se puedan evitar múltiples llamadas a la API y, como resultado, lograr un mejor rendimiento.
* Se integra perfectamente con [!DNL Adobe Experience Cloud] productos como [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] y [!DNL Experience Cloud ID Service] del lado del servidor.

>[!IMPORTANT]
>
>Tenga cuidado al actualizar su [!DNL Recommendations] [!UICONTROL Catalog] a través de [!DNL Delivery API]. [!DNL Delivery API] es público, por lo que debe evitar utilizarlo para rellenar elementos en los que se puede hacer clic en su catálogo de recomendaciones. Al hacerlo, se puede introducir contenido invalidado y contaminar el catálogo.
>
>Prácticas recomendadas:
>
>Usar [!DNL Delivery API] solo para actualizar atributos de catálogo que:
>* Cambie con frecuencia (por ejemplo, precio o nivel de stock).
>* Siga un formato predefinido que se pueda validar fácilmente en su sitio web.
>* No lo utilice para agregar o modificar elementos en los que se puede hacer clic u otro contenido no verificado.
>
>Si es necesario, puede solicitar al servicio de atención al cliente que deshabilite las actualizaciones del catálogo a través de la API de envío.

Para obtener más información, consulte la documentación de [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}.

>[!NOTE]
>
>Puede seguir teniendo acceso a la [documentación heredada de la API /v1/mbox y /v2/batchmbox](https://developers.adobetarget.com/api/legacy-api/index.html). Sin embargo, se desarrollarán funciones en la API de envío (como se documenta aquí) que no se transferirán a las API heredadas.
