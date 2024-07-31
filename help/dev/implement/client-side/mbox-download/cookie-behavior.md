---
keywords: Información general y referencia, webkit, cookies, origen, terceros, origen, terceros, terceros, 8 dólares
description: Obtenga información acerca del comportamiento de la cookie de Target (cookie de origen, cookie de terceros con cookie de origen o solo cookie de terceros).
title: ¿Dónde Puedo Encontrar Información Sobre Las Cookies De Target?
feature: at.js
role: Developer
source-git-commit: 39f390a0e5eedf8c6957333759d31d96ed11b321
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 53%

---

# Cookies de Target

El comportamiento de la cookie depende de si es una cookie de origen, una cookie de terceros con una cookie de origen o solo una cookie de terceros.

>[!NOTE]
>
>Este tema contiene información sobre `mboxSession` y `mboxPC`. Las prácticas recomendadas de implementación recomiendan que no vincule ni almacene información confidencial con los datos de cookies: `mboxSession` o `mboxPC`.

Vea también [Eliminar la cookie de Target](/help/dev/before-implement/privacy/cookie-deleting.md).

## Cuándo usar cookies de origen o de terceros

La configuración del sitio determina las cookies que se utilizarán. A la hora de saber cuándo usar cookies de origen y cookies de terceros, resulta útil conocer el modo en que funciona Target. Consulte [Funcionamiento de Adobe Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) para obtener más información.

Hay tres casos principales para el uso de cookies:

1. Un dominio.

   Todas las pruebas se realizan en un dominio de nivel superior (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, etc.).

   Método: usar solo cookies de origen (el valor predeterminado).

1. Los usuarios cruzan dominios y quiere rastrear y comprobar su comportamiento en estos dominios.

   Ejemplo: un usuario visita su sitio para comprar pero cierra la compra a través de establecimientos de Yahoo. Tres métodos (acuda al representante de la cuenta para saber cuál es el más adecuado):

   * Habilitar cookies de origen y de terceros.
   * Habilitar solo las de terceros (no es habitual, pero presenta la ventaja de mantener la cookie de mbox fuera de su dominio).
   * Activar solo las cookies de origen y transmitir el parámetro `mboxSession` al cruzar el dominio.

     Se debe pasar el parámetro `mboxSession` a una página de destino y se debe hacer referencia al mismo desde la biblioteca JavaScript (SDK web de Adobe Experience Platform o at.js). No puede ser una página de redirector intermedia.

1. En un sitio de terceros, solo se usan AdBoxes o Flashboxes.

   Dos métodos (acuda al representante de su cuenta para determinar cuál es el más adecuado):

   * Habilitar cookies de origen y de terceros.

     Se requieren cookies de origen y de terceros para los Flashboxes y los elementos creativos dinámicos.

   * Habilitar solo las cookies de terceros.

     Este método solo se aplica en el más que improbable caso de que se usen implementaciones de AdBoxes sin segmentación en el sitio.

## Comportamiento de cookie de origen

La cookie de origen se almacena en clientdomain.com, donde `clientdomain` es su dominio.

La biblioteca JavaScript genera un `mboxSession ID` y lo almacena en la cookie de Target. La primera respuesta de mbox contiene la oferta y el JavaScript para almacenar el `mboxPC ID` generado por la aplicación en la cookie de mbox.

>[!NOTE]
>
>La cookie de origen AMCV_###@AdobeOrg siempre se establece con el ID de visitante de Experience Cloud.

## Comportamiento de cookie de terceros

La cookie de terceros se almacena en clientcode.tt.omtrdc.net y la de origen en clientdomain.com, donde `clientdomain` es su dominio.

La biblioteca JavaScript genera un `mboxSession ID`. La primera solicitud de ubicación devuelve encabezados de respuesta HTTP que intentan establecer cookies de terceros denominadas `mboxSession` y `mboxPC`, y se devuelve una solicitud de redirección con un parámetro extra (`mboxXDomainCheck=true`).

Si el navegador acepta cookies de terceros, la solicitud de redirección incluye dichas cookies y la oferta se devuelve.

Si el navegador rechaza cookies de terceros, la solicitud de redirección no incluye dichas cookies y se muestra el contenido predeterminado de todas las ubicaciones en la página. Como no hay cookies definidas, el mismo proceso anterior se vuelve a producir en cada solicitud de página.

>[!NOTE]
>
>La cookie demdex.net se establece si las cookies de terceros no están bloqueadas.

## Comportamiento de cookies de terceros y de origen

La cookie de terceros se almacena en clientcode.tt.omtrdc.net y la de origen en clientdomain.com, donde `clientdomain` es su dominio.

La biblioteca JavaScript genera un `mboxSession ID`. La primera solicitud de ubicación devuelve encabezados de respuesta HTTP que intentan establecer cookies de terceros denominadas `mboxSession` y `mboxPC`, y se devuelve una solicitud de redirección con un parámetro extra (`mboxXDomainCheck=true`).

Si el navegador acepta cookies de terceros, la solicitud de redirección incluye dichas cookies y la oferta se devuelve.

Algunos navegadores rechazan las cookies de terceros. Si se bloquea la cookie de terceros, la cookie de origen seguirá funcionando. Target intenta establecer la cookie de terceros y, en caso de no poder, Target solo puede realizar el seguimiento en el dominio específico del cliente. El seguimiento entre dominios no funciona si la cookie de terceros está bloqueada, a menos que `mboxSession` se anexe al vínculo entre dominios. En dicho caso, se definirá otra cookie de origen que se sincronizará con la cookie de origen del dominio anterior.

## Configuración de la cookie

La cookie tiene varias configuraciones predeterminadas. Puede cambiar esta configuración si es necesario, excepto durante la duración de la cookie. Acuda al representante de la cuenta cuando vaya a cambiar la configuración de la cookie.

| Configuración | Información |
|--- |--- |
| Nombre de la cookie | mbox. |
| Dominio de la cookie | Niveles segundo y superior de los dominios desde los que se proporciona el contenido. Dado que se proporciona desde el dominio de la compañía, se trata de una cookie de origen.<br />Ejemplo: `mycompany.com`. |
| Dominio del servidor | `clientcode.tt.omtrdc.net`, usando el código de cliente de su cuenta. |
| Duración de la cookie | La cookie permanece en el explorador del visitante dos semanas después del último inicio de sesión. La duración de la cookie no se puede cambiar. |
| Directiva P3P | Tal y como precisa la configuración predeterminada de la mayoría de los navegadores, la cookie se publica con una directiva P3P. Una directiva P3P indica a un explorador que sirve la cookie y cómo se utiliza la información. |

La cookie conserva varios valores para administrar la forma en que los visitantes viven las campañas de

| Valor | Definición |
|--- |--- |
| session ID | ID único para una sesión de usuario. De forma predeterminada, tiene una duración de 30 minutos. |
| pc ID | Identificador semipermanente del navegador de un visitante. Dura 14 días. |
| check | Sencillo valor de prueba que sirve para averiguar si un visitante admite cookies. Se establece cada vez que un visitante solicita una página. |
| disable | Se establece si el tiempo de carga de un visitante supera el tiempo de espera fijado en el archivo de biblioteca de JavaScript. De forma predeterminada, tiene una duración de una hora. |

## Impacto en Target de los cambios que Apple ha introducido en el seguimiento de WebKit para visitantes con Safari

**¿Cómo funciona el seguimiento de Adobe Target?**

| Cookies | Detalles |
|--- |--- |
| Dominios de origen | Implementación estándar para clientes de Target. La cookie “mbox” se establece en el dominio del cliente. |
| Seguimiento de terceros | El seguimiento de terceros es importante para los casos de uso de publicidad y segmentación en Target y en Adobe Audience Manager AAM (). El seguimiento de terceros requiere técnicas de ejecución de scripts en sitios múltiples. Target utiliza dos cookies, “mboxSession” y “mboxPC”, que se establecen en el dominio `clientcode.tt.omtrd.net`. |

**¿Cuál es el enfoque de Apple?**

De Apple:

“La prevención inteligente del seguimiento es una nueva función de WebKit que reduce el seguimiento entre sitios mediante una mayor limitación de las cookies y otros datos de sitios web”.

“Esto es lo que se denomina seguimiento entre sitios, y la cookie empleada por `example-tracker.com` se denomina cookie de terceros. En nuestras pruebas hemos hallado sitios web populares con más de 70 de estos rastreadores, todos ellos dedicados a recopilar en silencio datos sobre los usuarios.”

| Enfoque | Detalles |
|--- |--- |
| Prevención inteligente del seguimiento | Para obtener más información, consulte [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) en el sitio del motor de navegación web de código abierto WebKit (en inglés). |
| Cookies | Cómo gestiona Safari las cookies:<ul><li>Las cookies de terceros que no están en un dominio al que el usuario accede directamente no se guardan nunca. Este comportamiento no es nuevo. Safari ya no admite las cookies de terceros.</li><li>Las cookies de terceros establecidas en un dominio al que el usuario accede directamente se purgan pasadas 24 horas.</li><li>Las cookies de origen se purgan pasados 30 días si el dominio de origen está clasificado como uno que realiza un seguimiento de los usuarios entre sitios. Esto podría aplicarse a las grandes empresas que envían a los usuarios a distintos dominios en línea. Apple no ha dejado claro cómo se clasifican exactamente estos dominios, o cómo un dominio puede determinar si se han clasificado como usuarios de seguimiento entre sitios.</li></ul> |
| Aprendizaje automático para identificar dominios que abarcan varios sitios | Desde Apple:<br />Clasificador de aprendizaje automático: se utiliza un modelo de aprendizaje automático para clasificar qué dominios superiores de control privado pueden realizar un seguimiento de los usuarios entre sitios, según las estadísticas recopiladas. De las distintas estadísticas recopiladas, tres vectores resultaron especialmente significativos para la clasificación, basándose en las prácticas de seguimiento actuales: subrecurso bajo número de dominios exclusivos, submarco bajo número de dominios exclusivos y número de dominios exclusivos a los que se redirecciona. Toda la recopilación y clasificación de datos se produce en el dispositivo.<br />Sin embargo, si el usuario interactúa con `example.com` como dominio principal, denominado con frecuencia dominio de origen, la prevención inteligente de seguimiento lo considera una señal de que el usuario está interesado en el sitio web y ajusta temporalmente su comportamiento como se muestra en esta cronología:<br />Si el usuario interactuó con `example.com` en las últimas 24 horas, sus cookies están disponibles cuando `example.com` es de terceros. Esta práctica permite situaciones de inicio de sesión del tipo &quot;Iniciar sesión con mi cuenta X en Y&quot;.<ul><li>Los dominios visitados como dominio de nivel superior no se ven afectados. Sitios como OKTA, por ejemplo</li><li>Identifica los dominios que son subdominios o submarcos de la página actual en varios dominios únicos.</li></ul> |

**¿Cómo se ve afectado el Adobe?**

| Funcionalidad afectada | Detalles |
|--- |--- |
| Soporte para la no participación | Los cambios de Apple en el seguimiento de WebKit interrumpen el soporte para la no participación.<br />La no participación en Target emplea una cookie en el dominio `clientcode.tt.omtrdc.net`. Para obtener más información, consulte [Privacidad](/help/dev/before-implement/privacy/privacy.md).<br />Target admite dos formas de no participación:<ul><li>Una por cliente (el cliente gestiona el vínculo de no participación).</li><li>Una mediante Adobe, que excluye al usuario de toda funcionalidad de Target para todos los clientes.</li></ul>Ambos métodos utilizan una cookie de terceros. |
| Actividades de Target | Los clientes pueden elegir su [duración de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) para sus cuentas de Target (hasta 90 días). El problema es que si la duración del perfil de la cuenta supera los 30 días y se purga la cookie de origen porque el dominio del cliente se ha marcado como un seguimiento de usuarios entre sitios, el comportamiento para los visitantes de Safari se ve afectado en las siguientes áreas de Target:<br />**[!UICONTROL Target reports]**: Si un usuario de Safari entra en una actividad, regresa pasados 30 días y luego convierte ese usuario, cuenta como dos visitantes y una conversión.<br />Este comportamiento es el mismo para las actividades que usan Analytics como fuente de informes (A4T).<br />**[!UICONTROL Profile & activity membership]**:<ul><li>Los datos de perfil se borran al caducar la cookie de origen.</li><li>La pertenencia a actividades se borra al caducar la cookie de origen.</li><li> Target no funciona en Safari para cuentas que utilizan una implementación de cookie de terceros, o de cookies de origen y de terceros. Este comportamiento no es nuevo. Safari lleva tiempo sin permitir cookies de terceros.</li></ul><br />**[!UICONTROL Suggestions]**: si existe preocupación en cuanto a que el dominio del cliente pueda marcarse como uno que realiza un seguimiento de los visitantes entre sesiones, lo más seguro es establecer en Target la duración del perfil en 30 días o menos. Este límite garantiza que los usuarios reciban un seguimiento similar en Safari y en todos los demás navegadores. |
