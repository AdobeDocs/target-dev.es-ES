---
keywords: tls, tls 1.0, seguridad de la capa de transporte, cifrado, tls 1.1, tls 1.2
description: Descubra cómo [!DNL Target] utiliza el protocolo TLS (Transport Layer Security) para mantener los estándares de seguridad más altos y fomentar la seguridad de los datos de sus clientes.
title: ¿Cómo [!DNL Target] ¿Usar TLS para proporcionar seguridad?
feature: Privacy & Security
exl-id: f5ea2272-27ab-49c9-b096-b15dd277d4e5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 52%

---

# Cambios en el cifrado de TLS (Seguridad de capa de transporte)

Información sobre cambios en el modo de [!DNL Adobe] y [!DNL Adobe Target] utilice TLS (Transport Layer Security) para mantener los estándares de seguridad más altos y promover la seguridad de los datos de los clientes.

Seguridad de capa de transporte (TLS) es el protocolo de seguridad más implementado que se usa hoy en día para navegadores web y otras aplicaciones que requieren que los datos se intercambien de forma segura en una red. Adobe tiene estándares de cumplimiento de seguridad que requieren la discontinuación de protocolos más viejos y exigen el uso de TLS 1.2 para tener en uso la versión más actualizada y segura.

>[!WARNING]
>
>A partir del 1 de marzo de 2020, [!DNL Target] ya no es compatible con el cifrado TLS 1.1 para el Compositor de experiencias visuales (VEC), el Compositor de experiencias mejorado (EEC), el envío de actividades, las API, etc. Actualice a TLS 1.2 para evitar problemas.

No esperamos que esto tenga un impacto significativo en los datos de los clientes ni en los informes.

## Compositor de experiencias visuales (VEC) con Compositor de experiencias mejorado (EEC) habilitado

TLS 1.2 es el predeterminado a partir del 1 de marzo de 2020 y TLS 1.1 ya no será compatible.

Adobe realizará la migración de sus clientes por etapas a TLS 1.2. Para aquellos cuyos dominios ya cumplan con 1.2, los pasaremos a TLS 1.2 sin que usted tenga que hacer ningún cambio. La mayoría de los dominios de los clientes ya son compatibles con TLS 1.2; sin embargo, si su dominio no es compatible con TLS 1.2, mantendremos esos dominios en TLS 1.1 como en el día de hoy (hasta marzo de 2020).

No debería tener ningún problema durante esta fase de migración. Si el VEC ha dejado de cargar un sitio que antes funcionaba,   [abra un ticket de Client Care](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C) citando esta migración como causa posible.

Sin embargo, si es uno de esos clientes que utilizan TSL 1.1 sin compatibilidad con TLS 1.2, debe planificar el movimiento de sus dominios/infraestructura a TLS 1.2. Seguiremos admitiendo el protocolo TLS 1.1 hasta el 1 de marzo de 2020. A partir del 1 de marzo de 2020, [!DNL Target] no es compatible con el protocolo TLS 1.1 que se va a usar para el VEC mediante la capacidad Enhanced Experience Composer.

Aunque recomendamos encarecidamente que todos estén en TLS 1.2 de ahora en adelante, si usted es un nuevo cliente, pero *NO* admite TLS 1.2, póngase en contacto con el Servicio de atención al cliente para informarles de que necesita estar en TLS 1.1 para el Compositor de experiencias mejorado. Sin embargo, piense en pasar a TLS 1.2, ya que también no será compatible más allá del 1 de marzo de 2020.

## Entrega de actividades

A partir del 1 de marzo de 2020, [!DNL Target] Los servidores de ya no admitirán TLS 1.1. Con este cambio, [!DNL Target] Los servidores de ya no aceptarán solicitudes de visitantes con dispositivos antiguos o exploradores web que no sean compatibles con TLS 1.2 (o posterior). Como resultado, los dispositivos y navegadores más antiguos y que solo admitan TLS 1.1 (o que admitan TLS 1.1 de forma predeterminada) no recibirán de Adobe Target contenido de actividades. Se mostrará el contenido predeterminado del sitio.

Algunos de los dispositivos y navegadores antiguos que se verán afectados son:

* Google Chrome (Chrome para Android) versiones 29 y anteriores
* Opera Browser (Opera Mobile) versiones 12.17 y anteriores
* Mozilla Firefox (Firefox para móviles) versiones 26 y anteriores
* Android 4.3 y versiones anteriores
* Internet Explorer 8-10 en Windows 7 y versiones anteriores
* Internet Explorer 10 en Windows Phone 8.0
* Safari 6.0.4/OS X10.8.4 y versiones anteriores

Cuando planee realizar este cambio, tenga en cuenta lo siguiente (tenga en cuenta que la fecha límite del 1 de marzo de 2020 afecta a todos estos elementos):

* Debe asegurarse de que el sitio predeterminado esté listo en una manera que sea utilizable para dispositivos y navegadores que cumplan los requisitos.
* Tenga en cuenta que el número de visitantes en su [!DNL Target] Los informes de pueden observar una caída insignificante en el número de visitantes.
* Es posible que tenga que cambiar las audiencias creadas específicamente para segmentar dispositivos o navegadores más antiguos que no sean compatibles con TLS 1.2. La entrega a estos dispositivos y navegadores ya no funcionará.

Para conocer más detalles sobre exploradores compatibles y sus versiones, consulte   [Exploradores admitidos](supported-browsers.md).

## [!DNL Adobe Target] API

A partir del 1 de marzo de 2020, [!DNL Target] Las API ya no serán compatibles con el cifrado TLS 1.1. Los clientes que acceden a la API deben verificar que no se verán afectados.

* Los clientes de API que usen Java 7 con la configuración predeterminada necesitarán modificaciones para ser compatibles con TLS 1.2. Para obtener más información, consulte “[Cambiar la versión del protocolo TLS predeterminado para clientes y extremos activos: de TLS 1.0 a TLS 1.2](https://www.java.com/en/configure_crypto.html)” en el sitio web de Java.
* Los clientes de API que usen Java 8 no deberían tener problemas, ya que la configuración predeterminada es TLS 1.2.
* Los clientes de API que usen otros módulos deben ponerse en contacto con su proveedor para obtener más información acerca de la compatibilidad con TLS 1.2.

## Acceso a las interfaces de soluciones de Experience Cloud

Debido a que el [!DNL Target] La interfaz Standard/Premium ya requiere un [navegador web moderno](supported-browsers.md), no se esperan problemas. Si no puede conectarse a Target, deberá actualizar el navegador a la última versión.

## Cómo comprobar la versión de TLS que utiliza el explorador

Para comprobar la versión TLS en el sitio web mediante Google Chrome:

1. Abra el sitio web afectado en Chrome.
1. En el menú Chrome (las tres elipses verticales), haga clic en Más herramientas > Herramientas para desarrolladores.

   ![Herramientas para desarrolladores Chrome](assets/chrome-developer-tools.png)

1. Abra la pestaña Seguridad y, a continuación, examine la información de la versión TLS en Conexión:

   ![Detalles de versión de TLS](assets/chrome-tls-version.png)

>[!NOTE]
>
>Estas instrucciones se encuentran actualizadas en el momento de la publicación y están sujetas a cambios. Una búsqueda rápida en Internet debería ayudar si estas instrucciones cambian. Otros exploradores tienen pasos similares.

## Comportamiento esperado con los exploradores que admiten versiones TLS inferiores a 1.2

En esta sección se describe lo que cabe esperar de los navegadores que admiten versiones de TLS inferiores a 1.2 solo cuando se utiliza una implementación de at.js. Con fines de comparación, esta sección también describe qué cabe esperar de los exploradores compatibles con TLS 1.2.

### Extremos centrales

| [!DNL Target] Implementación de JavaScript | Detalles |
|--- |--- |
| at.js | Con TLS 1.0 o TLS 1.1 habilitado:<ul><li>Al usar herramientas de desarrollo del navegador, en la pestaña Red, verá “200 OK”. Esto significa que la solicitud ha resultado satisfactoria.</li><li>El usuario ve el mensaje “No se puede conectar de forma segura a esta página”. El mensaje explica que esto puede deberse a que el sitio utiliza configuraciones de seguridad TLS no actualizadas o inseguras.</li><li>No se muestran errores de la consola.</li></ul>Con TLS 1.2 habilitado:<ul><li>archivo at.js descargado.</li></ul> |

### Extremos de Edge

| [!DNL Target] Implementación de JavaScript | Detalles |
|--- |--- |
| SDK web de Adobe Experience Platform | Con TLS 1.0 o TLS 1.1 habilitado:<ul><li>Al usar herramientas de desarrollo del navegador, en la pestaña Red, verá “200 OK”. Esto significa que la solicitud ha resultado satisfactoria.</li><li>El usuario ve el mensaje “No se puede conectar de forma segura a esta página”. El mensaje explica que esto puede deberse a que el sitio utiliza configuraciones de seguridad TLS no actualizadas o inseguras.</li><li>No se muestran errores de la consola.</li><li>Se proporciona el contenido predeterminado.</li></ul>Con TLS 1.2 habilitado:<ul><li>Se proporciona el contenido de oferta predeterminado.</li></ul> |
| at.js | Con TLS 1.0 o TLS 1.1 habilitado:<ul><li>Al usar herramientas de desarrollo del navegador, en la pestaña Red, verá “200 OK”. Esto significa que la solicitud ha resultado satisfactoria.</li><li>El usuario ve el mensaje “No se puede conectar de forma segura a esta página”. El mensaje explica que esto puede deberse a que el sitio utiliza configuraciones de seguridad TLS no actualizadas o inseguras.</li><li>No se muestran errores de la consola.</li><li>Se proporciona el contenido predeterminado.</li></ul>Con TLS 1.2 habilitado:<ul><li>Se proporciona el contenido de oferta predeterminado.</li></ul> |

### Actividad segmentada con audiencia de versión de explorador (Internet Explorer, versiones 6, 7 u 8)

Las audiencias dejan de funcionar.

| [!DNL Target] Implementación de JavaScript | Detalles |
|--- |--- |
| SDK web de Adobe Experience Platform | El SDK de Platform no es compatible con versiones de Internet Explorer anteriores a la 10. |
| at.js | at.js no es compatible con las versiones anteriores a la 10 de Internet Explorer. |
