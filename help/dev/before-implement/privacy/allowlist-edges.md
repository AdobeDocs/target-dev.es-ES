---
keywords: implementar, implementación, lista de admitidos, lista de admitidos, lista de permitidos, lista de permitidos, edge, edge, $9
description: Vea una lista de hosts para ayudarle a realizar la lista de permitidos de  [!DNL Adobe Target] perímetros (nodos de servidores distribuidos geográficamente que garantizan tiempos de respuesta óptimos para los usuarios finales).
title: ¿Cómo Lista de permitidos  [!DNL Target] Nodos De Edge?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 662d415bc3c216bcd038f07dcaa0fd83f6518690
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Lista de permitidos [!DNL Target] nodos perimetrales

Información y una lista actualizada de hosts que le ayudarán a realizar la lista de permitidos de [!DNL Adobe Target] perímetros.

Un perímetro es una arquitectura de servidores distribuidos geográficamente que garantiza tiempos de respuesta óptimos para usuarios finales que solicitan contenido desde cualquier ubicación. Cada nodo perimetral tiene toda la información necesaria para responder a la solicitud de contenido del usuario y realizar un seguimiento de los datos de análisis de esa solicitud. Las solicitudes de los usuarios se dirigen al nodo perimetral más cercano. Para obtener más información, consulte [La red perimetral](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Si lo desea, puede realizar la lista de permitidos de [!DNL Target] nodos perimetrales.

>[!IMPORTANT]
>
>Además de la inclusión en la lista de permitidos de las direcciones IP de traducción de direcciones de red (NAT) de [!DNL Target] extremos y [!DNL Target] direcciones IP perimetrales que se describen en el artículo, también debe realizar la lista de permitidos de todos los [!DNL Adobe Analytics] bloques de direcciones IP.
>
>Para obtener más información, consulte [Todos los bloques de direcciones IP de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} en la documentación de *Notas técnicas de Adobe Analytics*.
>
>Se está actualizando la infraestructura de [!DNL Adobe Target] y los clientes que deseen direcciones de lista de permitidos deben utilizar ambos conjuntos de direcciones IP. Si no se hace esto, esto afectará a los clientes que usan implementaciones del lado del servidor o híbridas en las que las llamadas de la API de Target para recuperar experiencias se originan dentro de una red detrás de un firewall configurado para usar una lista de permitidos.

Para garantizar el acceso ininterrumpido a [!DNL Target] a través de [!DNL Experience Edge Connector], los clientes pueden actualizar sus configuraciones de red para permitir el tráfico al servicio proxy.

## Introducción al servicio Proxy

* **Punto final de servicio**: `https://tnt-web-proxy.adobe.io`.
* **Infraestructura**: Alojada en la plataforma Ethos [!DNL Adobe].
* **Nota**: Este servicio usa enrutamiento DNS basado en latencia y no depende de direcciones IP estáticas.

## Destinos CNAME

El servicio proxy enruta el tráfico dinámicamente entre varias regiones mediante registros CNAME. Estos son los objetivos actuales:

| Ubicación de Edge | Direcciones IP de salida |
| --- | --- |
| Región | Destino CNAME |
| Europa (eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| Este de EE. UU. (us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| Este de EE. UU. (us-east-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

## Entradas de lista de permitidos recomendadas

Para garantizar una conectividad fiable, lista de permitidos los siguientes nombres de host:

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

## Opcional: detección de IP

Si las directivas de red requieren una inclusión en la lista de permitidos basada en IP, puede ver las direcciones IP públicas actuales asociadas al servicio proxy con esta herramienta:

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`