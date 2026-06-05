---
keywords: Implementación, at.js sin javascript, AdBox, redirector, mbox
description: Aprenda a implementar  [!DNL Adobe Target] en situaciones que no son de JavaScript, como el uso de un AdBox o un redirector.
title: ¿Cómo implemento [!DNL Target] for Email?
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
TQID: https://experienceleague.adobe.com/NeITIa97pW-yiB6EB-ajqRuBgp9mx-uzdwlREdgotj8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: c94a34eb-b51c-4dd1-a6a4-46b0d84ccccd
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e9001ce2-5245-4a8e-8601-dd958009072f
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 441
ht-degree: 62%

---

# Correo electrónico: implementar [!DNL Target]

Información acerca de la implementación de [!DNL Target] en escenarios que no son de JavaScript, como el uso de un AdBox o un redirector.

Puede realizar un seguimiento de las visitas a los anuncios y otro contenido sin conexión. También se puede identificar al mismo usuario en el sitio y fuera de él y ofrecer una experiencia coherente en la web. Con una sola dirección URL, el AdBox permite realizar pruebas sin JavaScript ni at.js.

Un AdBox es útil para los sitios que no tienen at.js, como los de empresas afiliadas. En caso de que la actividad necesite elementos creativos dinámicos (por ejemplo, debe mostrar un producto en la publicidad que no llegó a completarse en el carro de compras), no podrá usar un AdBox.

Tanto la publicidad de AdBox como redirector se pueden usar en cualquier tipo de actividad. En la siguiente tabla se comparan un redirector y un AdBox, y se indica cuándo usar cada uno de ellos:

| | Finalidad | Cuándo se utiliza | Estructura de la dirección URL | Tipo de oferta | Contenido de la oferta |
|--- |--- |--- |--- |--- |--- |
| AdBox | Devuelve distintas imágenes a la publicidad | Cambiar el contenido de una publicidad | `clientcode&#x200B;.tt.&#x200B;omtrdc&#x200B;.net/&#x200B;m2&#x200B;/&#x200B;clientcode/ubox/&#x200B;image?` | oferta de redireccionamiento | Dirección URL de una imagen |
| Redirector | Redirige a un visitante a otra página Web | Cambiar la página de aterrizaje de una publicidad | `clientcode&#x200B;.tt.omtrdc.net/&#x200B;m2/clientcode&#x200B;/ubox/page?` | oferta de redireccionamiento | Dirección URL de una página |

## Prácticas recomendadas de seguridad

Tenga en cuenta que con el redirector, puede estar expuesto a un riesgo de vulnerabilidad de redireccionamiento abierto. Para evitar el uso no autorizado de vínculos de redirector por parte de terceros, se recomienda utilizar &quot;hosts autorizados&quot; para la lista de permitidos de los dominios de URL de redireccionamiento predeterminados. [!DNL Target] usa hosts para la lista de permitidos de dominios a los que desea permitir redirecciones. Para obtener más información, consulte [Crear Listas de permitidos que especifiquen hosts con autorización para enviar llamadas de mbox a [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) en *Hosts*.

## Restricciones

* No existe la posibilidad de que se produzcan tiempos de espera de lado de cliente, como sucede con los mboxes estándar. Si [!DNL Target] está completamente inactivo, los visitantes del anuncio no verán el contenido, ni siquiera el predeterminado.
* Para realizar el seguimiento de las visitas se emplean cookies de terceros. Si los PCId son distintos, de forma predeterminada las cookies de terceros del visitante se combinan con cualquier perfil de origen existente.
* Para usar cookies de origen en el propio AdBox, será necesario transmitir la sesión de mBox en la dirección URL. Póngase en contacto con el representante de la cuenta para llevar esto a cabo.
* Para usar cookies de origen con objeto de rastrear clics de publicidad, transmita la sesión de mbox en la dirección URL. Póngase en contacto con el representante de la cuenta para llevar esto a cabo.
* Para usar más de un AdBox en la misma página, deberá transmitir la sesión de mbox en la dirección URL. Póngase en contacto con el representante de la cuenta para llevar esto a cabo. Se puede tener un AdBox y un vínculo de redirector en la misma página (ya que, en realidad, el redirector se encuentra en otra página).
