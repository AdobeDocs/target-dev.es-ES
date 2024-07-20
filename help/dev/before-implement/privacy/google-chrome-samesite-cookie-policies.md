---
keywords: google, samesite, cookies, chrome 80, ietf
description: Descubra cómo [!DNL Adobe Target] gestiona el estándar SameSite IETF introducido con Google Chrome versión 80 y lo que necesita hacer para cumplir con estas políticas.
title: ¿Cómo administra  [!DNL Target]  las políticas de cookies de SameSite de Google?
feature: Privacy & Security
exl-id: 58a83def-9625-4d44-914f-203509c6c434
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1973'
ht-degree: 68%

---

# Políticas de cookies de Google Chrome SameSite

Google empezó a imponer nuevas políticas de cookies de forma predeterminada a los usuarios a partir de Chrome 80, que se publicó a principios de 2020. En este artículo se explica todo lo que necesita saber sobre las nuevas directivas de cookies de SameSite, cómo [!DNL Adobe Target] admite estas directivas y cómo puede usar [!DNL Target] para cumplir con las nuevas directivas de cookies de SameSite de Google Chrome.

A partir de Chrome 80, los desarrolladores web deben especificar explícitamente qué cookies pueden funcionar en distintos sitios web. Este es el primero de muchos anuncios que Google planea hacer para mejorar la privacidad y seguridad en la web.

Dado el hecho de que Facebook ha estado en el primer puesto con respecto a la privacidad y la seguridad, otras empresas importantes como Apple, y ahora Google, han sido rápidos a la hora de crear nuevas identidades como defensores de la privacidad y la seguridad. Apple lideró a estas empresas anunciando primero cambios en sus políticas de cookies a principios de este año a través de ITP 2.1 y recientemente, ITP 2.2. En ITP 2.1, Apple bloquea completamente las cookies de terceros y mantiene las cookies creadas en el explorador durante solo siete días. En ITP 2.2, las cookies se conservan solo durante un día. El anuncio de Google no es ni de lejos tan agresivo como el de Apple, pero es el primer paso hacia el mismo objetivo final. Para obtener más información sobre las políticas de Apple, consulte [Prevención inteligente del seguimiento de Apple (ITP) 2.x](/help/dev/before-implement/privacy/apple-itp-2x.md).

## ¿Qué son las cookies y cómo se utilizan?

Antes de profundizar en los cambios de Google en sus políticas de cookies, hablemos de qué son las cookies y cómo se utilizan. En pocas palabras, las cookies son pequeños archivos de texto almacenados en el explorador web que se utilizan para recordar atributos de usuario.

Las cookies son importantes porque mejoran la experiencia del usuario a medida que navega por la web. Por ejemplo, si está realizando compras en un sitio web de comercio electrónico y agrega algo al carro de compras pero no inicia sesión ni realiza compras en esa visita, las cookies recuerdan sus artículos y los mantienen en el carro de compras para la próxima visita. O imagine que se vió obligado a volver a introducir su nombre de usuario y contraseña cada vez que visita su sitio web de medios sociales favorito. Las cookies también resuelven ese problema, ya que almacenan información que ayuda a los sitios a identificar quién es. Este tipo de cookies se denominan cookies de origen porque las crea y utiliza el sitio web que visitó.

También existen cookies de terceros. Para entenderlos mejor, veamos este ejemplo:

Digamos que una hipotética empresa de medios sociales llamada &quot;Amigos&quot; proporciona un botón Compartir que otros sitios implementan para permitir que los usuarios de Amigos compartan el contenido del sitio en la fuente de Amigos. Ahora, un usuario lee un artículo de noticias en un sitio web de noticias que está usando el botón Compartir y hace clic en él para publicar automáticamente en su cuenta de Amigos.

Para que esto suceda, el explorador recupera el botón Compartir de Amigos de `platform.friends.com` cuando se carga el artículo de noticias. Dentro de este proceso, el explorador adjunta las cookies de Amigos, que contienen las credenciales de inicio de sesión del usuario, a la solicitud a los servidores de Amigos. Esto permite a Amigos publicar el artículo en su fuente en nombre del usuario sin que este tenga que iniciar sesión.

Todo esto es posible mediante el uso de cookies de terceros. En este caso, la cookie de terceros se guarda en el explorador para `platform.friends.com`, de modo que `platform.friends.com` pueda realizar la publicación en la aplicación de Amigos en nombre del usuario.

Si se imagina por un momento cómo lograr este caso de uso sin cookies de terceros, el usuario tendría que seguir muchos pasos manuales. En primer lugar, el usuario tendría que copiar el enlace al artículo. En segundo lugar, el usuario tendría que iniciar sesión en la aplicación de Amigos por separado. A continuación, el usuario haría clic en el botón Crear publicación. Después, el usuario copiará y pegará el vínculo en el campo de texto y, finalmente, hará clic en Publicar. Como puede ver, las cookies de terceros ayudan enormemente a los usuarios, ya que los pasos manuales se pueden reducir drásticamente.

De forma más general, las cookies de terceros permiten que los datos se almacenen en el explorador de un usuario sin que este tenga que visitar explícitamente un sitio web.

## Cuestiones de seguridad

Aunque las cookies mejoran la experiencia del usuario y la ayudan a la publicidad, también pueden introducir vulnerabilidades de seguridad, como los ataques de falsificación de solicitudes entre sitios (CSRF). Por ejemplo, si un usuario inicia sesión en un sitio bancario para pagar cuentas de tarjeta de crédito y abandona el sitio sin cerrar la sesión y luego navega a un sitio malicioso en la misma sesión, puede ocurrir un ataque de CSRF. El sitio malintencionado puede incluir código que realiza una solicitud al sitio bancario que se ejecuta cuando se carga la página. Debido a que el usuario sigue estando autenticado en el sitio bancario, la cookie de sesión se puede utilizar para iniciar un ataque CSRF para iniciar un evento de transferencia de fondos desde la cuenta bancaria del usuario. Esto se debe a que, cada vez que visita un sitio, todas las cookies se adjuntan en la solicitud HTTP. Y debido a estas preocupaciones de seguridad, Google ahora está tratando de mitigarlas.

## ¿Cómo usa [!DNL Target] las cookies?

Dicho esto, veamos cómo [!DNL Target] usa cookies. Para que pueda usar [!DNL Target], debe instalar la biblioteca JavaScript de [!DNL Target] en su sitio. Esto le permite colocar una cookie de origen en el explorador del usuario que visita el sitio. A medida que el usuario interactúa con el sitio web, puede pasar los datos de comportamiento e interés del usuario a [!DNL Target] a través de la biblioteca de JavaScript. La biblioteca de JavaScript [!DNL Target] usa cookies de origen para extraer información de identificación sobre el usuario y asignarla a los datos de comportamiento e interés del usuario. Estos datos los utiliza [!DNL Target] para llevar a cabo las actividades de personalización.

Target también utiliza cookies de terceros (a veces). Si es propietario de varios sitios web que residen en dominios diferentes y desea rastrear el recorrido del usuario en dichos sitios web, puede utilizar cookies de terceros aprovechando el seguimiento entre dominios. Al habilitar el seguimiento entre dominios en la biblioteca JavaScript de [!DNL Target], su cuenta empezará a usar cookies de terceros. Cuando un usuario va de un dominio a otro, el explorador se comunica con el servidor back-end de Target y, en este proceso, se crea una cookie de terceros y se coloca en el explorador del usuario. A través de la cookie de terceros que se encuentra en el explorador del usuario, [!DNL Target] puede ofrecer una experiencia coherente en distintos dominios para un único usuario.

## Nueva fórmula de cookies de Google

Para proporcionar garantías sobre cuándo se envían cookies entre sitios para que los usuarios estén protegidos, Google tiene previsto añadir compatibilidad con un estándar IETF denominado SameSite, que requiere que los desarrolladores web administren cookies con el componente de atributo SameSite en el encabezado Set-Cookie.

Existen tres valores diferentes que se pueden pasar al atributo SameSite: Estricto, Laxo o Ninguno.

| Valor | Descripción |
| --- | --- |
| Estricto | Solo se puede acceder a las cookies con este ajuste al visitar el dominio en el que se estableció inicialmente. En otras palabras: Estricto bloquea completamente el uso de la cookie entre sitios. Esta opción es perfecta para las aplicaciones que requieren mucha seguridad, como bancos. |
| Laxo | Las cookies con esta configuración se envían solo en solicitudes del mismo sitio o navegación de nivel superior con solicitudes HTTP que no sean idempotentes, como `HTTP GET`, por ejemplo. Por lo tanto, esta opción se usaría si la cookie puede ser utilizada por terceros, pero con una ventaja de seguridad añadida que impide que los usuarios sean víctimas de ataques de CSRF. |
| Ninguna | Las cookies con este ajuste funcionan de la misma manera que las cookies funcionan hoy en día. |

Con esto en mente, Chrome 80 (y posteriores) introduce dos ajustes independientes para los usuarios: “SameSite con cookies predeterminadas” y “Las cookies sin SameSite debe ser seguras”. Esta configuración está habilitada de forma predeterminada en Chrome 80.

![Cuadro de diálogo de SameSite](../assets/samesite.png)

* **SameSite con cookies predeterminadas**: cuando se establece, todas las cookies que no especifiquen el atributo SameSite se verán obligadas a usar `SameSite = Lax` automáticamente.
* **Las cookies sin SameSite deben ser seguras**: cuando se configura, las cookies sin el atributo SameSite o con `SameSite = None` deben ser seguras. Seguras en este contexto significa que todas las solicitudes del explorador deben seguir el protocolo HTTPS. Las cookies que no respetan este requisito son rechazadas. Todos los sitios web deben utilizar HTTPS para cumplir este requisito.

## [!DNL Target] sigue las prácticas recomendadas de seguridad de Google

En Adobe, siempre queremos admitir las prácticas recomendadas más recientes del sector en materia de seguridad y privacidad. Nos complace anunciar que [!DNL Target] es compatible con la nueva configuración de seguridad de Google.

Para la configuración “SameSite con cookies predeterminadas”, [!DNL Target] seguirá ofreciendo personalización sin ningún impacto ni intervención por su parte. [!DNL Target] usa cookies de origen y seguirá funcionando correctamente, ya que Google Chrome aplica el indicador `SameSite = Lax`.

Para la opción &quot;Las cookies sin SameSite deben ser seguras&quot;, si no elige la función de seguimiento entre dominios en Target, las cookies de origen de [!DNL Target] seguirán funcionando.

Sin embargo, cuando decide utilizar el seguimiento entre dominios para usar [!DNL Target] en varios dominios, Chrome requiere que se usen indicadores `SameSite = None` y Secure para las cookies de terceros. Esto significa que debe asegurarse de que sus sitios utilicen el protocolo HTTPS. Las bibliotecas del lado cliente en [!DNL Target] utilizarán automáticamente el protocolo HTTPS y adjuntarán los indicadores `SameSite = None` y Secure en las cookies de terceros en [!DNL Target] para garantizar que todas las actividades sigan funcionando.

## ¿Qué es necesario hacer?

Para comprender lo que debe hacer para que [!DNL Target] siga funcionando para usuarios de Google Chrome 80 (y posteriores), consulte la siguiente tabla, en la que verá las siguientes columnas:

* **Biblioteca JavaScript de Target**: Si utiliza at.js 1.*x* o at.js 2.*x* en sus sitios.
* **SameSite con cookies predeterminadas = Habilitado**: Si los usuarios tienen “SameSite con cookies predeterminadas” habilitado, ¿cómo le afectará a usted? ¿Hay algo que necesite hacer para que [!DNL Target] siga funcionando?
* **Las cookies sin SameSite deben ser seguras = Habilitado**: Si los usuarios tienen “Cookies sin SameSite debe ser seguras” habilitado, ¿cómo le afectará a usted? ¿Hay algo que necesite hacer para que [!DNL Target] siga funcionando?

| Biblioteca JavaScript de Target | SameSite con cookies predeterminadas = Habilitado | Las cookies sin SameSite debe ser seguras = Habilitado |
| --- | --- | --- |
| at.js 1.*x* con cookie de origen. | Sin impacto. | Sin impacto si no usa el seguimiento entre dominios. |
| at.js 1.*x* con seguimiento entre dominios habilitado. | Sin impacto. | Debe habilitar el protocolo HTTPS para su sitio.<br />Target usa una cookie de terceros para rastrear usuarios y Google requiere que las cookies de terceros tengan `SameSite = None` y el indicador Secure. El indicador Secure requiere que sus sitios utilicen el protocolo HTTPS. |
| at.js 2.*x*  | Sin impacto. | Sin impacto. |

## ¿Qué debe hacer [!DNL Target]?

Entonces, ¿qué hemos de hacer en nuestra plataforma para ayudarle a cumplir con las nuevas políticas de cookies de Google Chrome 80+ SameSite?

| Biblioteca JavaScript de Target | SameSite con cookies predeterminadas = Habilitado | Las cookies sin SameSite debe ser seguras = Habilitado |
| --- | --- | --- |
| at.js 1.*x* con cookie de origen. | Sin impacto. | Sin impacto si no usa el seguimiento entre dominios. |
| at.js 1.*x* con seguimiento entre dominios habilitado. | Sin impacto. | at.js 1.*x* con seguimiento entre dominios habilitado. |
| at.js 2.*x*  | Sin impacto. | Sin impacto. |

## ¿Cuál es el impacto si no pasa a utilizar el protocolo HTTPS?

El único caso de uso que le afectará es si utiliza la función de seguimiento entre dominios en [!DNL Target] a través de at.js 1.*x*. Sin pasar a HTTPS, que es un requisito de Google, verá un pico en los visitantes únicos en sus dominios, ya que Google eliminará la cookie de terceros que usamos. Además, debido a que se eliminará la cookie de terceros, [!DNL Target] no podrá proporcionar una experiencia coherente y personalizada para ese usuario a medida que este navega de un dominio a otro. La cookie de terceros se utiliza principalmente para identificar a un único usuario que navega entre sus dominios.

## Conclusión

A medida que el sector realiza avances para crear una web más segura para los consumidores, Adobe está absolutamente comprometido a ayudar a nuestros clientes a ofrecer experiencias personalizadas de una manera que garantice la seguridad y la privacidad para los usuarios finales. Todo lo que debe hacer es seguir las prácticas recomendadas mencionadas anteriormente y aprovechar [!DNL Target] para cumplir con las nuevas directivas de cookies de SameSite de Google Chrome.
