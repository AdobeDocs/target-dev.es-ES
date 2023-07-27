---
keywords: Implementación, mbox.js no javascript, redirector, costes por clic, ingresos por clic
description: Aprenda a utilizar los redirectores en implementaciones de correo electrónico, de forma similar a cómo utiliza un mbox en su [!DNL Adobe Target] actividades.
title: ¿Cómo trabajo con los redirectores?
feature: Implement Email
exl-id: 072368ff-9f17-4709-ac2d-c9e1f0d888bb
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 69%

---

# Trabajar con redirectores

Use un redirector de forma similar a como se usa un mbox en las pruebas.

Los redirectores se crean con una dirección URL de redirector especial que carga un mbox de redirector en su cuenta. Use este redirector de forma similar a como se usa un mbox en las pruebas. Envíe la dirección URL del redirector a la red de publicidad como vínculo de destino de la publicidad.

Use el redirector para   hacer lo siguiente:

* Rastrear los clics de los anuncios en pantalla en su sitio
* Crear un único informe centralizado para rastrear los clics efectuados en los anuncios en pantalla de las redes de publicidad múltiple
* Modificar los destinos de los anuncios en pantalla

  Por ejemplo, el mismo titular aterriza en la página principal, la página de categorías y la página de productos.

* Averigüe cuál es la página de aterrizaje que produce el mayor número de conversiones

Para obtener ayuda para decidir la configuración adecuada, consulte   [Implementaciones no basadas en JavaScript](/help/dev/implement/email/overview.md).

## Creación de un redirector

Antes de poder usar un redirector, debe crearlo.

1. Determine las variaciones de destino de la publicidad, incluido el destino predeterminado.
1. Cree la dirección URL del redirector.

   ```
   https://<your_testandtarget_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox
   /​page?mbox=redirectorlink_456
   &mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm
   ```

   * Donde `yourclientcode` es el código de cliente de la empresa. El código de cliente de su compañía está por completo en minúscula y carece de caracteres especiales.

     El código de cliente se encuentra disponible en la parte superior de la **[!UICONTROL Administration]** > **[!UICONTROL Implementación]** página de la [!DNL Target] interfaz.

   * `redirectorlink_456` es el nombre del mbox de redirector que aparecerá en la cuenta para usarlo en campañas y pruebas.

     Aunque se muestran como cualquier otro mbox en la cuenta, los redirectores funcionan de manera distinta a otros mboxes. Asigne un nombre al redirector que permita distinguirlo fácilmente de los mboxes estándar en la cuenta.  Se recomienda comenzar el nombre del mbox con “redirectorlink”.

   * Donde `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm` es el destino predeterminado.

     Debe tener codificación de dirección URL y ser una referencia absoluta. Puede usar el complemento [Referencia de codificación de URL de HTML](https://www.w3schools.com/tags/ref_urlencode.asp) para codificar rápidamente las direcciones URL.

   >[!WARNING]
   >
   >Tenga en cuenta que con el redirector puede estar expuesto a un riesgo de vulnerabilidad de redireccionamiento abierto. Para evitar el uso no autorizado de vínculos de redirector por parte de terceros, Adobe recomienda utilizar &quot;hosts autorizados&quot; para la lista de permitidos de los dominios de URL de redireccionamiento predeterminados. [!DNL Target] usa hosts para la lista de permitidos de dominios a los que desea permitir redirecciones. Para obtener más información, consulte [Creación de listas de permitidos que especifiquen hosts con autorización para enviar llamadas de mbox a  [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) en *Hosts*.

1. Valide el redirector.
   1. *Práctica recomendada de seguridad*: Asegúrese de que el dominio utilizado en el redirector esté incluido en la lista de permitidos, como se ha indicado anteriormente. Si utiliza un dominio que no está incluido en la lista de permitidos, el Adobe bloqueará cualquier llamada a ese dominio para evitar que agentes malintencionados utilicen el redirector para redirigir a dominios potencialmente malintencionados.
   2. Inserte la dirección URL del redirector en un navegador y actualícelo.
   3. Inicie sesión en la cuenta, actualice la lista de mboxes y confirme que el nuevo redirector aparece enumerado en la cuenta.
1. Si va a comprobar diferentes destinos para un anuncio, cree [Ofertas de redireccionamiento](https://experienceleague.adobe.com/docs/target/using/experiences/vec/redirect-offer.html) para cada versión.
1. Cree la campaña.

   Consulte [Implementaciones no basadas en JavaScript](/help/dev/implement/email/overview.md) para saber cuál es la configuración apropiada para alcanzar sus metas.
1. Lleve a cabo un control de calidad en la campaña.

   Cree una página ficticia con un `<a href>` que contenga la dirección URL del redirector. Ejemplo:

   ```
   <a href=https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=
   
   redirectorlink_456&mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2F​usualdestination%2Ehtm>
   ```

1. Confirme que todas las experiencias, el contenido predeterminado y los informes se comportan del modo esperado en todos los tipos de navegador y en cualquier entorno.

   >[!NOTE]
   >
   >Los redirectores no son compatibles con las vistas previas de ofertas o con la exploración en busca de mboxes. Obtenga una vista previa de las experiencias directamente en un navegador. Además, `mboxDebug` no funciona con los redirectores.

1. Envíe la dirección URL completa del redirector a la red de anuncios en pantalla como destino de la publicidad.

## Uso de un redirector para pasar los costes por clic y los ingresos por clic

Información acerca de cómo utilizar un redirector para pasar los costes por clic y los ingresos por clic.

### Paso de los costes por clic

Use un redirector para pasar los costes por clic.

>[!NOTE]
>
>La práctica recomendada es determinar el valor de coste mediante **[!UICONTROL Puntuación por visita]** métrica de compromiso.

Añada `&mboxPageValue=-value` a la dirección URL. Observe el valor negativo.

Ejemplo: para un costo por clic de 0,10 céntimos:

```
https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=redirectorlink_456
&mboxPageValue=-0.1&mboxDefault=​https://www.yourcompany.com/usualdestination.htm
```

### Paso de los ingresos por clic  

Use un redirector para pasar los ingresos por clic.

>[!NOTE]
>
>La práctica recomendada es determinar el valor de los ingresos mediante la variable **[!UICONTROL Puntuación por visita]** métrica de compromiso.

Añada `&mboxPageValue=value` a la dirección URL.

Ejemplo: para unos ingresos por clic de 0,10 céntimos:

```
https://<​your_clientcode>​​​​.tt​​.omtrdc​.net/​​m2/​yourclientcode/​ubox/​​​page?mbox=redirectorlink_456
&mboxPageValue=0.1​&mbox​Default=​​http%3A%2F%2Fwww%2E​yourcompany%2Ecom​%2Fusualdestination%2Ehtm
```
