---
keywords: Información general y referencia, webkit, cookies, origen, terceros, origen, terceros,
description: Más información [!DNL Target] comportamiento de la cookie (cookie de origen, cookie de terceros con cookie de origen o solo cookie de terceros).
title: ¿Dónde puedo encontrar información sobre [!DNL Target] ¿Galletas?
feature: at.js
exl-id: d44e02ce-8920-4130-bcad-699ca77c0dad
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 57%

---

# [!DNL Target] cookies

El comportamiento de la cookie depende de si es una cookie de origen, una cookie de terceros con una cookie de origen o solo una cookie de terceros.

>[!NOTE]
>
>Para obtener información detallada sobre las distintas cookies que utiliza [!DNL Target], consulte [[!DNL Adobe Target] galletas](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-target.html?lang=es){target=_blank} en el *Guía de componentes de la interfaz central de Experience Cloud*.
>
>Este tema contiene información sobre `mboxSession` y `mboxPC`. Las prácticas recomendadas de implementación recomiendan que no vincule ni almacene información confidencial con los datos de las cookies: `mboxSession` o `mboxPC`.

Consulte también [Elimine el [!DNL Target] cookie](cookie-deleting.md).

## Cuándo usar cookies de origen o de terceros

La configuración del sitio determina las cookies que se utilizarán. Es útil entender cómo [!DNL Target] funciona al intentar comprender las cookies de origen y de terceros. Consulte [Cómo [!DNL Adobe] [!DNL Target] Funciona](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) para obtener más información.

Hay tres casos principales para el uso de cookies:

1. Un dominio.

   Todas las pruebas tienen lugar en un dominio de primer nivel (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, etc.).

   Método: usar solo cookies de origen (el valor predeterminado).

1. Los usuarios cruzan dominios y quiere rastrear y comprobar su comportamiento en estos dominios.

   Ejemplo: un usuario visita su sitio para comprar pero cierra la compra a través de establecimientos de Yahoo. Tres métodos (acuda al representante de la cuenta para saber cuál es el más adecuado):

   * Habilitar cookies de origen y de terceros.
   * Habilitar solo las de terceros (no es habitual, pero presenta la ventaja de mantener la cookie de mbox fuera de su dominio).
   * Activar solo las cookies de origen y transmitir el parámetro `mboxSession` al cruzar el dominio.

     El `mboxSession` se debe pasar a una página de destino y hacer referencia al parámetro desde la biblioteca JavaScript (SDK web de Adobe Experience Platform o at.js). No puede ser una página de redirector intermedia.

1. En un sitio de terceros, solo se usan AdBoxes o Flashboxes.

   Dos métodos (acuda al representante de su cuenta para determinar cuál es el más adecuado):

   * Habilitar cookies de origen y de terceros.

     Se requieren cookies de origen y de terceros para los Flashboxes y los elementos creativos dinámicos.

   * Habilitar solo las cookies de terceros.

     Este método solo se aplica en el más que improbable caso de que se usen implementaciones de AdBoxes sin segmentación en el sitio.

## Comportamiento de cookie de origen

La cookie de origen se almacena en clientdomain.com, donde `clientdomain` es su dominio.

La biblioteca JavaScript de genera un `mboxSession ID` y lo almacena en [!DNL Target] cookie. La primera respuesta de mbox contiene la oferta y el JavaScript para almacenar el `mboxPC ID` generado por la aplicación, en la cookie de mbox.

>[!NOTE]
>
>La cookie de origen AMCV_###@AdobeOrg siempre se establece con el ID de visitante de Experience Cloud.

## Comportamiento de cookie de terceros

La cookie de terceros se almacena en clientcode.tt.omtrdc.net y la de origen en clientdomain.com, donde `clientdomain` es su dominio.

La biblioteca JavaScript de genera un `mboxSession ID`. La primera solicitud de ubicación devuelve encabezados de respuesta HTTP que intentan establecer cookies de terceros denominadas `mboxSession` y `mboxPC`, y se devuelve una solicitud de redirección con un parámetro extra (`mboxXDomainCheck=true`).

Si el navegador acepta cookies de terceros, la solicitud de redirección incluye dichas cookies y la oferta se devuelve.

Si el navegador rechaza cookies de terceros, la solicitud de redirección no incluye dichas cookies y se muestra el contenido predeterminado de todas las ubicaciones en la página. Como no hay cookies definidas, el mismo proceso anterior se vuelve a producir en cada solicitud de página.

>[!NOTE]
>
>Se instala la cookie de demdex.net si no están bloqueadas las cookies de terceros.

## Comportamiento de cookies de terceros y de origen

La cookie de terceros se almacena en clientcode.tt.omtrdc.net y la de origen en clientdomain.com, donde `clientdomain` es su dominio.

La biblioteca JavaScript de genera un `mboxSession ID`. La primera solicitud de ubicación devuelve encabezados de respuesta HTTP que intentan establecer cookies de terceros denominadas `mboxSession` y `mboxPC`, y se devuelve una solicitud de redirección con un parámetro extra (`mboxXDomainCheck=true`).

Si el navegador acepta cookies de terceros, la solicitud de redirección incluye dichas cookies y la oferta se devuelve.

Algunos navegadores rechazan las cookies de terceros. Si se bloquea la cookie de terceros, la cookie de origen seguirá funcionando. [!DNL Target] intenta establecer la cookie de terceros y, en caso de no poder, [!DNL Target] solo puede realiza el seguimiento en el dominio específico del cliente. El seguimiento entre dominios no funciona si la cookie de terceros está bloqueada, a menos que la variable `mboxSession` se anexa en el vínculo que cruza los dominios. En dicho caso, se definirá otra cookie de origen que se sincronizará con la cookie de origen del dominio anterior.

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
| disable | Se establece si el tiempo de carga de un visitante supera el tiempo de espera fijado en el archivo de biblioteca JavaScript. De forma predeterminada, tiene una duración de una hora. |

## Impacto en [!DNL Target] para visitantes de Safari debido a cambios en el seguimiento de Apple WebKit

**¿Cómo? [!DNL Target] ¿trabajo de seguimiento?**

| Cookies | Detalles |
|--- |--- |
| Dominios de origen | La implementación estándar para [!DNL Target] clientes. La cookie “mbox” se establece en el dominio del cliente. |
| Seguimiento de terceros | El seguimiento de terceros es importante para los casos de uso de publicidad y segmentación en [!DNL Target] y en [!DNL Adobe Audience Manager] AAM (de la). El seguimiento de terceros requiere técnicas de programación entre sitios. [!DNL Target] utiliza dos cookies, “mboxSession” y “mboxPC”, que se establecen en el dominio `clientcode.tt.omtrd.net`. |
**¿Cuál es el enfoque de Apple?**

De Apple:

“La prevención inteligente del seguimiento es una nueva función de WebKit que reduce el seguimiento entre sitios mediante una mayor limitación de las cookies y otros datos de sitios web”.

“Esto es lo que se denomina seguimiento entre sitios, y la cookie empleada por `example-tracker.com` se denomina cookie de terceros. En nuestras pruebas hemos hallado sitios web populares con más de 70 de estos rastreadores, todos ellos dedicados a recopilar en silencio datos sobre los usuarios.”

| Enfoque | Detalles |
|--- |--- |
| Prevención inteligente del seguimiento | Para obtener más información, consulte [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) en el sitio del motor de navegación web de código abierto WebKit (en inglés). |
| Cookies | Cómo gestiona Safari las cookies:<ul><li>Las cookies de terceros que no están en un dominio al que el usuario accede directamente no se guardan nunca. Este comportamiento no es nuevo. Safari ya no admite las cookies de terceros.</li><li>Las cookies de terceros establecidas en un dominio al que el usuario accede directamente se purgan pasadas 24 horas.</li><li>Las cookies de origen se purgan pasados 30 días si el dominio de origen está clasificado como uno que realiza un seguimiento de los usuarios entre sitios. Esto podría aplicarse a las grandes empresas que envían a los usuarios a distintos dominios en línea. Apple no ha dejado claro cómo se clasifican exactamente estos dominios, o cómo un dominio puede determinar si se han clasificado como usuarios de seguimiento entre sitios.</li></ul> |
| Aprendizaje automático para identificar dominios que abarcan varios sitios | De Apple:<br />Clasificador de aprendizaje automático: se utiliza un modelo de aprendizaje automático para clasificar qué dominios superiores de control privado pueden realizar un seguimiento de los usuarios entre sitios, según las estadísticas recopiladas. De las distintas estadísticas recopiladas, tres vectores resultaron especialmente significativos para la clasificación, basándose en las prácticas de seguimiento actuales: subrecurso bajo número de dominios exclusivos, submarco bajo número de dominios exclusivos y número de dominios exclusivos a los que se redirecciona. Toda la recopilación y clasificación de datos se produce en el dispositivo.<br />Sin embargo, si el usuario interactúa con `example.com` como dominio principal, denominado con frecuencia dominio de origen, la prevención inteligente de seguimiento lo considera una señal de que el usuario está interesado en el sitio web y ajusta temporalmente su comportamiento como se muestra en esta cronología:<br />Si el usuario interactuó con `example.com` las últimas 24 horas, sus cookies están disponibles cuando `example.com` es un tercero. Esta práctica permite situaciones de inicio de sesión del tipo &quot;Iniciar sesión con mi cuenta X en Y&quot;.<ul><li>Los dominios visitados como dominio de nivel superior no se ven afectados. Sitios como OKTA, por ejemplo</li><li>Identifica los dominios que son subdominio o submarco de la página actual en varios dominios exclusivos.</li></ul> |

**¿Cómo está? [!DNL Adobe] ¿afectado?**

| Funcionalidad afectada | Detalles |
|--- |--- |
| Soporte para la no participación | Los cambios de Apple en el seguimiento de WebKit interrumpen el soporte para la no participación.<br />La no participación en Target emplea una cookie en el dominio `clientcode.tt.omtrdc.net`. Para obtener más información, consulte [Privacidad](privacy.md).<br />Target admite dos formas de no participación:<ul><li>Una por cliente (el cliente gestiona el vínculo de no participación).</li><li>Uno mediante [!DNL Adobe] que excluye al usuario de todas las [!DNL Target] para todos los clientes.</li></ul>Ambos métodos utilizan una cookie de terceros. |
| Actividades de Target | Los clientes pueden elegir la   [duración del perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) para sus [!DNL Target] cuentas (hasta 90 días). El problema es que si la duración del perfil de la cuenta supera los 30 días y se purga la cookie de origen porque el dominio del cliente se ha marcado como un seguimiento de usuarios entre sitios, el comportamiento para los visitantes de Safari se ve afectado en las siguientes áreas de Target:<br />**Informes de Target**: Si un usuario de Safari entra en una actividad, regresa pasados 30 días y luego se convierte, ese usuario cuenta como dos visitantes y una conversión.<br />Este comportamiento es el mismo para las actividades que utilizan Analytics como fuente de informes (A4T).<br />**Abono a perfiles y actividades**:<ul><li>Los datos de perfil se borran al caducar la cookie de origen.</li><li>La pertenencia a actividades se borra al caducar la cookie de origen.</li><li> [!DNL Target] no funciona en Safari para cuentas que utilizan una implementación de cookie de terceros, o de cookies de origen y de terceros. Este comportamiento no es nuevo. Safari lleva tiempo sin permitir cookies de terceros.</li></ul><br />**Sugerencias**: Si existe preocupación en cuanto a que el dominio del cliente pueda marcarse como uno que realiza un seguimiento de los visitantes entre sesiones, lo más seguro es establecer en Target la duración del perfil en 30 días o menos. Este límite garantiza que los usuarios reciban un seguimiento similar en Safari y en todos los demás navegadores. |
