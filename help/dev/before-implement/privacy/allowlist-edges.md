---
keywords: implementar, implementación, lista de admitidos, lista de admitidos, lista de permitidos, lista de permitidos, edge, edge, $9
description: Vea una lista de hosts para ayudarle a realizar la lista de permitidos de  [!DNL Adobe Target] perímetros (nodos de servidores distribuidos geográficamente que garantizan tiempos de respuesta óptimos para los usuarios finales).
title: ¿Cómo Lista de permitidos  [!DNL Target] Nodos De Edge?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 275c3fabdcaf3152d7d6161f3c325e54c840c805
workflow-type: tm+mt
source-wordcount: '563'
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
>
>Todas las direcciones Edge4 *x* enumeradas en las tablas siguientes están programadas para actualizarse el 9 de agosto de 2023.

## Direcciones IP de traducción de direcciones de red (NAT) de [!DNL Target] extremos

Lista de direcciones IP de salida de [!DNL Target] extremos. Lista de permitidos estas IP si planea que [!DNL Target] se ponga en contacto con sus servicios.

| Ubicación de Edge | Direcciones IP de salida |
| --- | --- |
| Edge41 (Bombay) | 3.6.2.221<P>13.235.112.4 <P>52.66.66.192 |
| Edge42 (Tokio) | 52.69.55.232<P>43.206.61.43 <P>13.113.73.214 |
| Edge44 (costa este de EE. UU.) | 54.164.192.223<P>52.86.86.203 <P>54.88.167.98 |
| Edge45 (Costa oeste de EE. UU.) | 52.40.124.129<P>54.148.219.69 <P>54.189.208.212 |
| Edge46 (Sídney) | 54.253.144.4<P>54.66.198.142 <P>13.211.218.51 |
| Edge47 (Irlanda) | 52.208.136.136<P>54.170.28.19 <P>99.80.111.82 |
| Edge48 (Singapur) | 3.1.141.36<P>18.143.112.116 <P>52.76.61.44 |

## [!DNL Target] direcciones IP perimetrales

Lista de direcciones IP de [!DNL Target] extremos. Lista de permitidos estas direcciones IP si desea realizar llamadas de API a [!DNL Target] perímetros.

Esta lista cambiará con frecuencia, a medida que los equilibradores de carga se amplíen y se reduzcan en función de los perfiles de tráfico.

| Ubicación de Edge | Dominio | Direcciones IP |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(donde CLIENTCODE es su ID de cliente [!DNL Target]) |  |
| Edge41 (Bombay) | `mboxedge41.tt.omtrdc.net` | 3.6.2.221<P>52.66.66.192<P>13.235.112.4 |
| Edge42 (Tokio) | `mboxedge42.tt.omtrdc.net` | 43.206.61.43<P>13.113.73.214<P>52.69.55.232 |
| Edge44 (costa este de EE. UU.) | `mboxedge44.tt.omtrdc.net` | 54.88.167.98<P>54.164.192.223<P>52.86.86.203 |
| Edge45 (Costa oeste de EE. UU.) | `mboxedge45.tt.omtrdc.net` | 52.40.124.129<P>54.148.219.69<P>54.189.208.212 |
| Edge46 (Sídney) | `mboxedge46.tt.omtrdc.net` | 54.66.198.142<P>54.253.144.4<P>13.211.218.51 |
| Edge47 (Irlanda) | `mboxedge47.tt.omtrdc.net` | 54.170.28.19<P>52.208.136.136<P>99.80.111.82 |
| Edge48 (Singapur) | `mboxedge48.tt.omtrdc.net` | 52.76.61.44<P>3.1.141.36<P>18.143.112.116 |

A medida que los equilibradores de carga detecten cambios en el perfil de tráfico, se ampliará o reducirá. El tiempo necesario para que Elastic Load Balancing se escale puede oscilar entre 1 y 7 minutos, según los cambios detectados. Cuando los equilibradores de carga se escalan, actualizan el registro DNS con la nueva lista de direcciones IP. Para asegurarse de que está aprovechando el aumento de la capacidad, Elastic Load Balancing utiliza una configuración TTL en el registro DNS de 60 segundos.

## Requisitos de inclusión en la lista de permitidos para el servicio proxy [!DNL Target]

Para garantizar el acceso ininterrumpido a [!DNL Target] a través de [!DNL Experience Edge Connector] (EEC), es posible que los clientes tengan que actualizar sus configuraciones de red para permitir el tráfico al servicio proxy.

### Introducción al servicio Proxy

* **Punto final de servicio**: `https://tnt-web-proxy.adobe.io`.
* **Infraestructura**: Alojada en la plataforma Ethos [!DNL Adobe].
* **Nota**: Este servicio usa enrutamiento DNS basado en latencia y no depende de direcciones IP estáticas.

### Destinos CNAME

El servicio proxy enruta el tráfico dinámicamente entre varias regiones mediante registros CNAME. Estos son los objetivos actuales:

| Ubicación de Edge | Direcciones IP de salida |
| --- | --- |
| Región | Destino CNAME |
| Europa (eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| Este de EE. UU. (us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| Este de EE. UU. (us-east-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

### Entradas de lista de permitidos recomendadas

Para garantizar una conectividad fiable, lista de permitidos los siguientes nombres de host:

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

### Opcional: detección de IP

Si las directivas de red requieren una inclusión en la lista de permitidos basada en IP, puede ver las direcciones IP públicas actuales asociadas al servicio proxy con esta herramienta:

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`