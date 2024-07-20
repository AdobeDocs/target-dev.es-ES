---
keywords: correo electrónico, AdBox, correo electrónico, AdBox de imagen
description: Aprenda a usar [!DNL Adobe Target]  para probar dinámicamente imágenes en correos electrónicos e incluso cambiar esas imágenes sobre la marcha cuando alguien abra el correo electrónico.
title: ¿Cómo pruebo un AdBox de imagen de correo electrónico?
feature: Implement Email
exl-id: 4512741a-567f-41bb-9721-3e1c4f5302e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 79%

---

# Comprobación de un AdBox de imagen de correo electrónico

Pruebe de forma dinámica imágenes en correos electrónicos e incluso puede cambiar dichas imágenes automáticamente cuando el destinatario recibe el correo.

Se pueden usar redirectores en los correos electrónicos para rastrear los clics y controlar dinámicamente la página de aterrizaje a la que llegan los usuarios.

La comprobación de imágenes de correo electrónico se lleva a cabo usando versiones de AdBoxes modificadas. Dado que los clientes de correo electrónico no permiten que se configuren cookies, se deberá generar un identificador único por cada correo electrónico. Este número se anexa a la dirección URL del AdBox y a todos los redirectores que se usen en el correo electrónico para rastrear los clics en él.

>[!NOTE]
>
>Aunque [!DNL Target] técnicamente puede ofrecer optimización de imágenes en el momento de la apertura, cada cliente de correo electrónico administra el almacenamiento en caché de forma diferente, por lo que los resultados pueden variar. Independientemente del proveedor de servicios de correo electrónico que se utilice, el cliente de correo con el que el usuario final abra el mensaje (la aplicación Gmail, Outlook, Hotmail, etc.) determina si la imagen se recupera en el momento de la apertura. Por ejemplo, Gmail almacena en caché prácticamente todo, de modo que la imagen que el usuario final vea dependerá de cuándo decida Gmail realizar una llamada y guardar la imagen en caché.

**Código de ejemplo de un AdBox de imagen de correo electrónico:**

```
<img src="https://{clientcode}.tt.omtrdc.net/m2/​{clientcode}/ubox/​image?
mbox={email_header}&
mboxDefault=​{http%3A%2F%2Fwww.domain.com%2Fheader.jpg}&
mboxXDomain=disabled&
mboxSession={123456}&
mboxPC={123456}" border=:"0"/>
```

Donde los siguientes valores son específicos del usuario:

| Valor | Descripción |
|--- |--- |
| clientcode | El código de cliente de su compañía: Lo encontrará en at.js como `clientCode='yourclientcode'`. Todo esto se escribe en minúsculas y no contiene caracteres especiales. |
| imagen | El tipo de oferta. Siempre es “image” para las publicidades gráficas y “page” para los redirectores. |
| email_header | El nombre del AdBox. |
| `mboxDefault=http%3A%2F%2Fwww.domain.com%2Fheader.jpg` | Requerido. Reemplace la URL con el contenido predeterminado apropiado para su adbox. Debe ser una referencia absoluta y debe estar codificado en la dirección URL. |
| `mboxXDomain=disabled` | Indica a [!DNL Target] que no intente establecer una cookie. |
| `mboxSession=123456` y `mboxPC=123456` | Dos valores requeridos por [!DNL Target] para combinar el perfil de este usuario con el perfil existente para su sitio. 123456 es el identificador único generado por el correo electrónico. Inserte dinámicamente este valor en cada AdBox y dirección URL de redirector. Este número debe ser único de cada correo electrónico enviado a cada persona. Si se envía un correo electrónico semanalmente a 1000 personas, será necesario generar 1000 identificadores únicos.<br />El identificador único por correo electrónico se debe asignar a mboxSession y a mboxPC en cada AdBox y dirección URL de redirector. El formato recomendado para este identificador es timestamp-NNNNN donde NNNNN es un número aleatorio de cinco dígitos, pero cualquier formato alfanumérico funcionará. Algunos servicios de correo electrónico masivo y todos los lenguajes de programación pueden generar este identificador único. |
