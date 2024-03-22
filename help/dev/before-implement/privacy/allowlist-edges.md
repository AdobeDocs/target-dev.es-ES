---
keywords: implementar, implementación, lista de admitidos, lista de admitidos, lista de permitidos, lista de permitidos, edge, edge, $9
description: Ver una lista de hosts para ayudarle en la lista de permitidos [!DNL Adobe Target] perímetros (nodos de servidor distribuidos geográficamente que garantizan tiempos de respuesta óptimos para los usuarios finales).
title: ¿Cómo puedo realizar la Lista de permitidos? [!DNL Target] ¿Nodos perimetrales?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 49b6572c0d414ab304712691c97794bb0b1e3781
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

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
| Edge41 (Bombay) | 3.6.2.221<br />13 235 112,4 <br />52.66.66.192 |
| Edge42 (Tokio) | 52.69.55.232<br />43 206 61 43 <br />13 113 73 214 |
| Edge44 (costa este de EE. UU.) | 54 164 192 223<br />52 86 86 203 <br />54 88 167 98 |
| Edge45 (costa oeste de EE. UU.) | 52.40.124.129<br />54 148 219 69 <br />54 189 208 212 |
| Edge46 (Sídney) | 54 253 144,4<br />54.66.198.142 <br />13 211 218 51 |
| Edge47 (Irlanda) | 52 208 136 136<br />54.170.28.19 <br />99 80 111 82 |
| Edge48 (Singapur) | 3.1.141.36<br />18 143 112 116 <br />52 76 61 44 |

## [!DNL Target] direcciones IP perimetrales

Lista de direcciones IP de [!DNL Target] bordes. Realice una lista de permitidos de estas direcciones IP si desea realizar llamadas de API a [!DNL Target] bordes.

Esta lista cambiará con frecuencia, a medida que los equilibradores de carga se amplíen y se reduzcan en función de los perfiles de tráfico.

| Ubicación de Edge | Dominio | Direcciones IP |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(donde CLIENTCODE es su [!DNL Target] ID de cliente) |  |
| Edge41 (Bombay) | `mboxedge41.tt.omtrdc.net` | 15.206.104.6<br />3.109.14.178 <br />13 234 139 131 |
| Edge42 (Tokio) | `mboxedge42.tt.omtrdc.net` | 52 194 84 34<br />3 115 158 39 <br />18 180 123 21 |
| Edge44 (costa este de EE. UU.) | `mboxedge44.tt.omtrdc.net` | 54 205 210 54<br />23.20.189.8 <br />35 169 173 155 |
| Edge45 (costa oeste de EE. UU.) | `mboxedge45.tt.omtrdc.net` | 35 161 163 45<br />44 230 114 101 <br />35 161 120 22 |
| Edge46 (Sídney) | `mboxedge46.tt.omtrdc.net` | 3 104 142 61<br />52.62.4.152 <br />54 253 105 140 |
| Edge47 (Irlanda) | `mboxedge47.tt.omtrdc.net` | 18 203 168 186<br />54 228 83 91 <br />54 217 181 83 |
| Edge48 (Singapur) | `mboxedge48.tt.omtrdc.net` | 54 179 6 70<br />13 215 150 94 <br />18 136 47 70 |

A medida que los equilibradores de carga detecten cambios en el perfil de tráfico, se ampliará o reducirá. El tiempo necesario para que Elastic Load Balancing se escale puede oscilar entre 1 y 7 minutos, según los cambios detectados. Cuando los equilibradores de carga se escalan, actualizan el registro DNS con la nueva lista de direcciones IP. Para asegurarse de que está aprovechando el aumento de la capacidad, Elastic Load Balancing utiliza una configuración TTL en el registro DNS de 60 segundos.
