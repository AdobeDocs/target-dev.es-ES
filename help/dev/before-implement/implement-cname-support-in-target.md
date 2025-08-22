---
keywords: client care, cname, programa certificado, nombre canónico, cookies, certificado, amc, adobe managed certificate, digicert, validación de control de dominio, dcv, client care2
description: Trabaje con [!UICONTROL Adobe Client Care] para implementar la compatibilidad con CNAME (nombre canónico) en  [!DNL Adobe Target] para controlar los problemas de bloqueo de anuncios.
title: ¿Cómo utilizo CNAME en Target?
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
source-git-commit: 353597cbbd3478e9598bd42303619440b3b478fd
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 0%

---

# CNAME y Target

Instrucciones para trabajar con [!DNL Adobe Client Care] a fin de implementar el soporte de CNAME (nombre canónico) en [!DNL Adobe Target]. Utilice CNAME para gestionar los problemas de bloqueo de anuncios o las políticas de cookies relacionadas con ITP (Prevención inteligente del seguimiento). Con CNAME, las llamadas se realizan a un dominio propiedad del cliente en lugar de a un dominio propiedad de Adobe.

## Solicitar compatibilidad con CNAME en Target

1. Determine la lista de nombres de host que necesita para su certificado SSL (consulte las preguntas frecuentes a continuación).

1. Para cada nombre de host, cree un registro CNAME en su DNS que apunte a su nombre de host [!DNL Target] normal `clientcode.tt.omtrdc.net`.

   Por ejemplo, si el código de cliente es &quot;cnamecustomer&quot; y el nombre de host propuesto es `target.example.com`, el registro CNAME de DNS tendrá un aspecto similar al siguiente:

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```

   >[!WARNING]
   >
   >La autoridad de certificación de Adobe, DigiCert, no puede emitir un certificado hasta que se complete este paso. Por lo tanto, Adobe no puede cumplir su solicitud de implementación CNAME hasta que se complete este paso.

1. [Rellene este formulario](assets/FPC_Request_Form.xlsx) e inclúyalo cuando [abra un ticket de Adobe Client Care solicitando asistencia de CNAME](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C):

   * [!DNL Adobe Target] código de cliente:
   * Nombres de host de certificado SSL (ejemplo: `target.example.com target.example.org`):
   * Comprador de certificados SSL (se recomienda encarecidamente Adobe, consulte las preguntas frecuentes): Adobe/cliente
   * Si el cliente está comprando el certificado, también conocido como &quot;Traer su propio certificado&quot; (BYOC), rellene estos detalles adicionales:
      * Organización del certificado (ejemplo: Empresa de ejemplo Inc):
      * Unidad organizativa del certificado (opcional, ejemplo: Marketing):
      * País del certificado (ejemplo: EE. UU.):
      * Estado o región del certificado (ejemplo: California):
      * Ciudad del certificado (ejemplo: San José):

1. Si Adobe compra el certificado, Adobe trabaja con DigiCert para adquirir e implementar el certificado en los servidores de producción de Adobe.

   Si el cliente está comprando el certificado (BYOC), Adobe Client Care le envía la solicitud de firma de certificado (CSR). Utilice el CSR cuando compre el certificado a través de la autoridad de certificación que elija. Una vez emitido el certificado, envíe una copia del mismo y de los certificados intermedios a Adobe Client Care para su implementación.

   Adobe Client Care le notifica cuando su implementación está lista.

1. Actualice la `serverDomain`documentación[ de ](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain) al nuevo nombre de host CNAME y establezca `overrideMboxEdgeServer` en `false` [documentación](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver) en su configuración de at.js.

## Preguntas frecuentes

La siguiente información responde a las preguntas más frecuentes sobre la solicitud y la implementación de la compatibilidad con CNAME en Target:

### ¿Puedo proporcionar mi propio certificado (Traer su propio certificado o BYOC)?

Puede proporcionar su propio certificado. Sin embargo, Adobe no recomienda esta práctica. La administración del ciclo de vida del certificado SSL es más sencilla tanto para Adobe como para usted si Adobe compra y controla el certificado. Los certificados SSL deben renovarse cada año. Por lo tanto, Adobe Client Care debe ponerse en contacto con usted cada año para obtener un nuevo certificado de forma oportuna. Algunos clientes pueden tener dificultades para producir un certificado renovado de manera oportuna. La implementación de [!DNL Target] se pone en peligro cuando caduca el certificado porque los exploradores rechazan las conexiones.

>[!WARNING]
>
>Si solicita una implementación CNAME de [!DNL Target] que traiga su propio certificado, usted es responsable de proporcionar certificados renovados a Adobe Client Care cada año. Si permite que el certificado CNAME caduque antes de que Adobe pueda implementar un certificado renovado, se producirá una interrupción en la implementación de [!DNL Target] específica.

### ¿Cuánto falta para que caduque mi nuevo certificado SSL?

Todos los certificados adquiridos por Adobe son válidos durante un año. Consulte el artículo de [DigiCert sobre certificados de 1 año](https://www.digicert.com/blog/position-on-1-year-certificates) para obtener más información.

### ¿Qué nombres de host debo elegir? ¿Cuántos nombres de host por dominio debo elegir?

Las implementaciones de CNAME de Target solo requieren un nombre de host por dominio en el certificado SSL y en el DNS del cliente. Adobe recomienda un nombre de host por dominio. Algunos clientes requieren más nombres de host por dominio para sus propios fines (como probar en el ensayo), lo cual es compatible.

La mayoría de los clientes elige un nombre de host como `target.example.com`. Adobe recomienda seguir esta práctica, pero la opción es, en última instancia, suya. No solicite un nombre de host de un registro DNS existente. Al hacerlo, se genera un conflicto y se retrasa el tiempo de resolución de la solicitud CNAME [!DNL Target].

### Ya tengo una implementación CNAME para Adobe Analytics, ¿puedo utilizar el mismo certificado o nombre de host?

No, [!DNL Target] requiere un nombre de host y un certificado independientes.

### ¿Se ve afectada mi implementación actual de [!DNL Target] por ITP 2.x?

Apple Intelligent Tracking Prevention (ITP) versión 2.3 ha introducido su función de mitigación de ocultación CNAME, que puede detectar implementaciones CNAME de [!DNL Target] y reduce la caducidad de la cookie a siete días. Actualmente [!DNL Target] no cuenta con una solución alternativa para la mitigación de encubrimiento CNAME de ITP. Para obtener más información sobre ITP, consulte [Prevención inteligente del seguimiento de Apple (ITP) 2.x](../before-implement/privacy/apple-itp-2x.md).

### ¿Qué tipo de interrupciones de servicio puedo esperar cuando se implementa mi implementación CNAME?

No hay interrupciones en el servicio cuando se implementa el certificado (incluidas las renovaciones de certificados).

Sin embargo, después de cambiar el nombre de host en el código de implementación de [!DNL Target] (`serverDomain` en at.js) por el nuevo nombre de host CNAME (`target.example.com`), los exploradores web tratan a los visitantes que regresan como nuevos visitantes. Los datos de perfil de los visitantes que regresan se pierden porque no se puede obtener acceso a la cookie anterior con el nombre de host anterior (`clientcode.tt.omtrdc.net`). No se puede acceder a la cookie anterior debido a los modelos de seguridad del explorador. Esta interrupción se produce únicamente en la transición inicial al nuevo CNAME. Las renovaciones de certificados no tienen el mismo efecto porque el nombre de host no cambia.

### ¿Qué tipo de clave y algoritmo de firma de certificado se utiliza para mi implementación CNAME?

De forma predeterminada, todos los certificados son RSA SHA-256 y las claves son RSA de 2048 bits. Los tamaños de clave superiores a 2048 bits deben solicitarse explícitamente a través de [!UICONTROL Customer Care].

### ¿Cómo puedo validar que mi implementación CNAME está lista para el tráfico?

Utilice el siguiente conjunto de comandos (en el terminal de línea de comandos de macOS o Linux, utilizando bash y curl >=7.49):

1. Copie y pegue esta función bash en su terminal, o pegue la función en su archivo de script de inicio bash (normalmente `~/.bash_profile` o `~/.bashrc`) para que la función esté disponible entre sesiones de terminal:

   ```bash {line-numbers="true"}
    function adobeTargetCnameValidation {
   
     local hostname="$1"
   
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
   
     local service="Adobe Target CNAME implementation"
     local edges="41 42 44 45 46 47 48"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local poolDomain="pool.data.adobedc.net"
     local shards=5
     local shardsFoundCount=0
     local shardsFound=""
     local shardsFoundOutput=""
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslShopperUrl="https://www.sslshopper.com/ssl-checker.html#hostname=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2)"
     local curlVersionRequired=7.49
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local cnameExists=""
     local endToEndTestSucceeded=""
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local currShard="${region}-${poolDomain}"
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currShard:443" "$url" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         shardsFound+=" $currShard"
   
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundCount=$((shardsFoundCount+1))
           shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currShard] $miniRule\n"
         else
           shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currShard] $miniRule\n"
         fi
   
         shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
   
         if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
         fi
       fi
     done
   
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
   
     local dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
     if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
       echo "$success $hostname passes DNS CNAME validation"
       cnameExists=true
     else
       echo -n "$failure $hostname FAILED DNS CNAME validation -- "
       if [ -n "$dnsOutput" ]; then
         echo -e "$dnsOutput is not in the subdomain $edgeDomain"
       else
         echo "required DNS CNAME record pointing to <target-client-code>.$edgeDomain not found"
       fi
     fi
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:${region}-pool.data.adobedc.net:443" "https://$hostname$curlEndpoint" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           echo -en "$success $hostname passes TLS and HTTP response validation for region $region"
           if [ -n "$cnameExists" ]; then
             echo
           else
             echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
               "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
           fi
           endToEndTestSucceeded=true
         else
           echo -n "$failure $hostname FAILED HTTP response validation for region $region --" \
             "unexpected response from $url -- "
           if [ -n "$cnameExists" ]; then
             echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
           else
             echo "the required DNS CNAME record is missing, see above"
           fi
         fi
       else
         echo -n "$failure $hostname FAILED TLS validation for region $region -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
             "protocols, see curl output below and optionally SSL Shopper ($sslShopperUrl):"
           echo ""
           echo "$horizontalRule"
           echo "$curlResult" | sed 's/^/    /g'
           echo "$horizontalRule"
           echo ""
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     done
   
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
   
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, see SSL Shopper:"
         echo ""
         echo "    $info  $sslShopperUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       echo ""
     fi
   
     echo
     echo "$horizontalRule"
     echo
   }
   ```

1. Pegue este comando (reemplazando `target.example.com` con su nombre de host):

   ```adobeTargetCnameValidation target.example.com```

Si la implementación está lista, verá el resultado como se muestra a continuación. Lo importante es que todas las líneas de estado de validación muestren `✅` en lugar de `🚫`. Cada recurso compartido CNAME de Edge de Target debe mostrar `CN=target.example.com`, que coincide con el nombre de host principal del certificado solicitado (los nombres de host de SAN adicionales del certificado no se imprimen en esta salida).

    +++ Ver detalles
    
    &quot;bash {line-numbers=&quot;true&quot;}
    $ adobeTargetCnameValidation
    target.example.com============================================================ validación de implementación CNAME de Adobe Target para hostname target.example.com:
    ✅ target.example.com pasa la validación de CNAME de DNS
    ✅ target.example.com pasa la validación de respuesta TLS y HTTP para region IRL1
    ✅ target.example.com pasa y la validación de respuesta HTTP para la región IND1
    ✅ target.example.com pasa la validación de respuesta TLS y HTTP para la región SIN
    ✅ target.example.com pasa la validación de respuesta TLS y HTTP para la región OR
    ✅ target.example.com pasa la validación de respuesta TLS y HTTP para la región SYD
    ✅ target.example.com pasa la validación de respuesta TLS y HTTP para la región VA
    ✅ target.example.com pasa la validación de respuesta TLS y HTTP para la región TYO
    ✅ target.example.com pasa la validación de partición para los siguientes 7 fragmentos de Edge:===== ✅ target.example.com [fragmento de Edge: IRL1-pool.data.adobedc.net] =====
     fecha de caducidad: feb. fecha 14&rbrace;* 20 23:59:59 2026 GMT
    * emisor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    * asunto: C=US; ST=California; L=San José; O=Adobe Systems Incorporated; CN=target.example.com===== ✅ target.example.com [edge shard: IND1-pool.data.adobedc.net] =====
    * fecha de caducidad: 20/Feb/23/20&rbrace;59/2026 GMT:59:* emisor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    * asunto: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== 
     target.example.com [Edge Shard: SIN-pool.data.adobedc.net] =====✅* fecha de caducidad: 20 de febrero de 23
    59 2026 GMT:59:* emisor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    * asunto: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== &lbrace;2target.example.com OR-pool.data.adobedc.net&rbrack; =====
    * fecha de caducidad: 20 de febrero de 23✅59 2026 GMT
    * emisor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1:59:* asunto: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== 
     [edge shard: SYD-pool.data.adobedc.net] =====
    * fecha de caducidad: 20 de febrero de 23✅59 2026 GMT
    * emisor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1:59:* asunto: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== 
     target.example.com [edge shard: VA-pool.data.adobedc.net] =====
    * fecha de caducidad: 20 de febrero de 23✅59 2026 GMT
    * emisor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1:59:* asunto: C=US; ST=California; L=San Jose; Incorporated CN=target.example.com===== 
     target.example.com target.example.com [edge shard: TYO-pool.data.adobedc.net] =====
    * fecha de caducidad: 20 de febrero de 23✅59 2026 GMT
    * emisor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1:59:* asunto: C=US; ST=California; L=San José O=Adobe Systems Incorporated; CN=target.example.com========================================================== Para obtener más información sobre la validación de TLS/SSL, consulte Comprador de SSL.    
     https://www.sslshopper.com/ssl-checker.html#hostname=target.example.com Para comprobar la propagación de DNS en todo el mundo, consulte whatsmydns.net:    
     registros A de DNS:     Registro CNAME DNS de https://whatsmydns.net/#A/target.example.com🔎: https://whatsmydns.net/#CNAME/target.example.com🔎&quot;
    +++🔎
    
    
    

>[!NOTE]
>
>Si este comando de validación falla en la validación de DNS pero ya ha realizado los cambios de DNS necesarios, es posible que tenga que esperar a que las actualizaciones de DNS se propaguen completamente. Los registros DNS tienen un [TTL (tiempo de vida)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) asociado que dicta el tiempo de caducidad de la caché para las respuestas DNS de esos registros. Como resultado, es posible que tenga que esperar al menos el tiempo que sus TTL. Puede usar el comando `dig target.example.com` o [G Suite Toolbox](https://toolbox.googleapps.com/apps/dig/#CNAME) para buscar los TTL específicos. Para comprobar la propagación de DNS por todo el mundo, vea [whatsmydns.net](https://whatsmydns.net/#CNAME).

### ¿Cómo utilizo un vínculo de no participación con CNAME?

Si utiliza CNAME, el vínculo de no participación debe contener el parámetro &quot;client=`clientcode`&quot;, por ejemplo:
`https://my.cname.domain/optout?client=clientcode`.

Reemplace `clientcode` por su código de cliente y luego agregue el texto o la imagen que se vinculará a la [URL de exclusión](privacy/privacy.md).

## Limitaciones conocidas

* El modo de control de calidad no se fija cuando tiene CNAME y at.js 1.x porque se basa en una cookie de terceros. La solución consiste en agregar los parámetros de vista previa a cada dirección URL a la que vaya. El modo de control de calidad es fijo cuando tiene CNAME y at.js 2.x.
* Al utilizar CNAME, es más probable que aumente el tamaño del encabezado de la cookie para [!DNL Target] llamadas. Adobe recomienda mantener el tamaño de la cookie por debajo de 8 KB.
