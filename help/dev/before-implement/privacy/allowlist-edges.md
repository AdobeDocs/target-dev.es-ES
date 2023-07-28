---
keywords: implementar, implementación, lista de admitidos, lista de admitidos, lista de permitidos, lista de permitidos, edge, edge, $9
description: Ver una lista de hosts para ayudarle en la lista de permitidos [!DNL Adobe Target] perímetros (nodos de servidor distribuidos geográficamente que garantizan tiempos de respuesta óptimos para los usuarios finales).
title: ¿Cómo puedo realizar la Lista de permitidos? [!DNL Target] ¿Nodos perimetrales?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 3f4147d521b1fb3ee12e879e52a48d459f6b24b9
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 6%

---

# Lista de permitidos [!DNL Target] nodos perimetrales

Información y una lista actualizada de hosts que le ayudarán con la lista de permitidos [!DNL Adobe Target] bordes.

Un perímetro es una arquitectura de servidores distribuidos geográficamente que garantiza tiempos de respuesta óptimos para usuarios finales que solicitan contenido desde cualquier ubicación. Cada nodo perimetral tiene toda la información necesaria para responder a la solicitud de contenido del usuario y realizar un seguimiento de los datos de análisis de esa solicitud. Las solicitudes de los usuarios se dirigen al nodo perimetral más cercano. Para obtener más información, consulte [La red de Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Puede realizar la lista de permitidos [!DNL Target] nodos de Edge, si lo desea.

>[!IMPORTANT]
>
>Además de la inclusión en la lista de permitidos de las direcciones IP de traducción de direcciones de red (NAT) de [!DNL Target] bordes y [!DNL Target] direcciones IP perimetrales que se describen en el artículo. También debe crear una lista de permitidos de todas las direcciones IP [!DNL Adobe Analytics] Bloques de direcciones IP.
>
>Para obtener más información, consulte [Todos los bloqueos de direcciones IP de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} en el *Notas técnicas de Adobe Analytics* documentación.
>
>[!DNL Adobe Target] La infraestructura de se está actualizando y los clientes que deseen crear direcciones de lista de permitidos deben utilizar ambos conjuntos de direcciones IP. Si no se hace esto, esto afectará a los clientes que usan implementaciones del lado del servidor o híbridas en las que las llamadas de la API de Target para recuperar experiencias se originan dentro de una red detrás de un firewall configurado para usar una lista de permitidos.
>
>Todos los Edge4 *x* Las direcciones enumeradas en ambas tablas a continuación están programadas para actualizarse el 9 de agosto de 2023.

## Direcciones IP de traducción de direcciones de red (NAT) de [!DNL Target] bordes

Lista de direcciones IP de salida de [!DNL Target] bordes. Lista de permitidos estas direcciones IP si planea tener [!DNL Target] póngase en contacto con sus servicios de.

| Ubicación de Edge | Direcciones IP de salida |
| --- | --- |
| Edge31 (Bombay) | 13.126.131.246<br />13.234.229.8 |
| Edge32 (Tokio) | 3.115.154.28<br />3.115.227.146 |
| Edge34 (costa este de EE. UU.) | 34.232.149.249<br />52.21.139.93 |
| Edge35 (costa oeste de EE. UU.) | 52.10.11.139<br />44.231.171.161 |
| Edge36 (Sídney) | 13.237.227.20<br />13.210.93.142 |
| Edge37 (Irlanda) | 54.72.21.68<br />52.208.139.19 |
| Edge38 (Singapur) | 18.141.132.96<br />54.179.187.167 |
| Edge41 (Bombay) | 3.6.2.221<br />13.235.112.4 <br />52.66.66.192 |
| Edge42 (Tokio) | 52.69.55.232<br />43.206.61.43 <br />13.113.73.214 |
| Edge44 (costa este de EE. UU.) | 54.164.192.223<br />52.86.86.203 <br />54.88.167.98 |
| Edge45 (costa oeste de EE. UU.) | 52.40.124.129<br />54.148.219.69 <br />54.189.208.212 |
| Edge46 (Sídney) | 54.253.144.4<br />54.66.198.142 <br />13.211.218.51 |
| Edge47 (Irlanda) | 52.208.136.136<br />54.170.28.19 <br />99.80.111.82 |
| Edge48 (Singapur) | 3.1.141.36<br />18.143.112.116 <br />52.76.61.44 |

## [!DNL Target] direcciones IP perimetrales

Lista de direcciones IP de [!DNL Target] bordes. Realice una lista de permitidos de estas direcciones IP si desea realizar llamadas de API a [!DNL Target] bordes.

Esta lista cambiará con frecuencia, a medida que los equilibradores de carga se amplíen y se reduzcan en función de los perfiles de tráfico.

| Ubicación de Edge | Dominio | Direcciones IP |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(donde CLIENTCODE es su [!DNL Target] ID de cliente) |  |
| Edge31 (Bombay) | `mboxedge31.tt.omtrdc.net` | 13.235.211.15<br />35.154.193.2<br />35.154.53.50<br />15.206.4.195<br />13.234.45.112<br />3.7.14.31<br />3.7.182.1<br />52.66.52.225<br />3.6.64.110<br />65.0.222.85<br />65.1.67.35<br />43.205.52.220 |
| Edge32 (Tokio) | `mboxedge32.tt.omtrdc.net` | 3.112.121.190<br />54.65.158.134<br />52.199.9.11<br />54.95.35.22<br />52.68.152.188<br />52.196.181.152<br />54.150.112.230<br />52.198.235.210 |
| Edge34 (costa este de EE. UU.) | `mboxedge34.tt.omtrdc.net` | 44.195.255.231<br />52.207.142.243<br />52.54.50.225<br />35.169.35.160<br />52.71.135.138<br />35.169.227.120<br />23.22.33.42<br />52.54.152.40<br />54.243.116.94<br />3.233.250.116<br />50.16.29.53<br />54.86.98.238<br />44.210.41.177<br />3.211.200.163<br />54.210.15.1<br />34.199.251.113 |
| Edge35 (costa oeste de EE. UU.) | `mboxedge35.tt.omtrdc.net` | 44.238.17.94<br />52.27.37.224<br />52.89.178.205<br />52.24.182.215<br />44.241.83.238<br />52.24.177.17<br />35.165.241.91<br />52.36.84.148<br />52.40.70.235<br />52.11.244.25<br />35.83.17.210<br />52.42.219.24<br />54.218.0.208<br />34.218.165.70<br />44.239.131.209<br />52.37.121.114<br />35.164.96.150<br />52.40.11.173<br />52.32.91.22<br />35.82.102.174<br />50.112.233.80<br />44.241.57.139<br />44.233.4.154<br />54.69.42.127<br />34.211.73.73<br />54.148.130.206<br />44.238.29.100<br />44.228.116.36<br />52.40.119.218<br />52.25.253.33 |
| Edge36 (Sídney) | `mboxedge36.tt.omtrdc.net` | 54.206.232.103<br />54.206.183.241<br />3.24.158.129<br />54.253.0.242 |
| Edge37 (Irlanda) | `mboxedge37.tt.omtrdc.net` | 54.77.63.43<br />63.35.113.29<br />63.34.224.124<br />54.246.171.67<br />99.80.163.253<br />34.253.167.75<br />52.211.90.101<br />54.246.201.164<br />34.249.148.170<br />54.76.19.168<br />52.209.9.253 |
| Edge38 (Singapur) | `mboxedge38.tt.omtrdc.net` | 52.220.75.199<br />52.221.116.71 |
| Edge41 (Bombay) | `mboxedge41.tt.omtrdc.net` | 15.206.104.6<br />3.109.14.178 <br />13.234.139.131 |
| Edge42 (Tokio) | `mboxedge42.tt.omtrdc.net` | 52.194.84.34<br />3.115.158.39 <br />18.180.123.21 |
| Edge44 (costa este de EE. UU.) | `mboxedge44.tt.omtrdc.net` | 54.205.210.54<br />23.20.189.8 <br />35.169.173.155 |
| Edge45 (costa oeste de EE. UU.) | `mboxedge45.tt.omtrdc.net` | 35.161.163.45<br />44.230.114.101 <br />35.161.120.22 |
| Edge46 (Sídney) | `mboxedge46.tt.omtrdc.net` | 3.104.142.61<br />52.62.4.152 <br />54.253.105.140 |
| Edge47 (Irlanda) | `mboxedge47.tt.omtrdc.net` | 18.203.168.186<br />54.228.83.91 <br />54.217.181.83 |
| Edge48 (Singapur) | `mboxedge48.tt.omtrdc.net` | 54.179.6.70<br />13.215.150.94 <br />18.136.47.70 |

A medida que los equilibradores de carga detecten cambios en el perfil de tráfico, se ampliará o reducirá. El tiempo necesario para que Elastic Load Balancing se escale puede oscilar entre 1 y 7 minutos, según los cambios detectados. Cuando los equilibradores de carga se escalan, actualizan el registro DNS con la nueva lista de direcciones IP. Para asegurarse de que está aprovechando el aumento de la capacidad, Elastic Load Balancing utiliza una configuración TTL en el registro DNS de 60 segundos.
