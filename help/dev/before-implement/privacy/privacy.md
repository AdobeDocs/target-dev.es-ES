---
keywords: privacidad, dirección ip, segmentación geográfica, exclusión, exclusión, exclusión, privacidad de datos, regulaciones gubernamentales, regulaciones, rgpd, ccpa, privacidad, información de identificación personal, PII
description: Descubra cómo [!DNL Adobe Target] cumple con las leyes aplicables sobre privacidad de datos, incluida la recopilación y administración de direcciones IP, PII e instrucciones de exclusión.
title: ¿Cómo gestiona Target los problemas de privacidad, incluida la PII?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 58%

---

# Privacidad

[!DNL Adobe Target] ha habilitado procesos y configuraciones que permiten [!DNL Target] utilizar en cumplimiento con las leyes aplicables sobre privacidad de datos.

## Recopilación de direcciones IP e información de identificación personal (PII)

La dirección IP de un visitante del sitio web se transmite a un centro de procesamiento de datos (DPC) de Adobe. Según la configuración de red del visitante, la dirección IP no representa necesariamente la dirección IP del equipo del visitante. Por ejemplo, la dirección IP puede ser una dirección IP externa de un cortafuegos de traducción de direcciones de red (NAT), un proxy HTTP o una puerta de enlace de Internet.

>[!IMPORTANT]
>
>[!DNL Target] no almacena ninguna dirección IP del usuario ni ningún tipo de información de identificación personal (PII). Solo usan direcciones IP [!DNL Target] durante la sesión (en memoria, nunca persistió).

## Sustitución del último octeto de direcciones IP

Adobe ha desarrollado una configuración de &quot;privacidad mediante diseño&quot; que los usuarios pueden habilitar para el Adobe [!DNL Target]. Cuando está activada, Adobe [!DNL Target] oculta inmediatamente el último octeto (la última parte) de la dirección IP en el momento en que se recopila la dirección IP. Esta anonimización se realiza antes de cualquier procesamiento de la dirección IP, incluso antes de una consulta geográfica opcional de la dirección IP.

Cuando se habilita esta función, la dirección IP se convierte en lo suficientemente anónima para que ya no pueda identificarse como información personal. Como resultado, [!DNL Target] puede utilizarse en cumplimiento de las leyes de privacidad de datos en países que no permiten la recopilación de información personal. Es muy probable que la obtención de información por nivel de ciudad vea significativamente afectada por la confusión de la dirección IP. La obtención de información por nivel de región y país solo debería verse ligeramente afectada.

Las siguientes configuraciones están disponibles en la variable [!DNL Target] IU navegando a **[!UICONTROL Administration]** > **[!UICONTROL Implementación]**:

* [!UICONTROL Ofuscación del último octeto]: [!DNL Target] oculta el último octeto de la dirección IP.
* [!UICONTROL Confusión de IP completa]: [!DNL Target] oculta la dirección IP completa.
* [!UICONTROL Ninguno]: [!DNL Target] no oculta ninguna parte de la dirección IP.

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target] recibe la dirección IP completa y la oculta (si se establece en Último octeto o IP completa) según se ha especificado. [!DNL Target] a continuación, guarda la dirección IP ocultada en la memoria sólo durante la sesión actual.

## Segmentación geográfica

Si habilita la sustitución del último octeto de la dirección IP, los valores restantes de la dirección IP pueden analizarse mediante los informes de [!DNL Target]. Si el último octeto de la dirección IP no se ha disimulado, entonces se podrá analizar toda la dirección IP en [!DNL Target]. Puede usar la característica Segmentación geográfica para determinar la ubicación del visitante por zona geográfica. Los datos de segmentación geográfica se detallan solamente hasta el nivel de ciudad o de código postal, y no a nivel individual.

Si las direcciones IP se ocultan por completo, la segmentación geográfica y el direccionamiento geográfico no estarán disponibles.

## Vínculo de no participación

Puede añadir un vínculo de no participación a sus sitios para permitir que los visitantes renuncien a los recuentos y la publicación de contenido.

1. Añada el vínculo siguiente a su sitio:

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (Condicional) Si utiliza CNAME, el vínculo debe contener la variable &quot;client=`clientcode` por ejemplo:
   `https://my.cname.domain/optout?client=clientcode`.

1. Reemplace `clientcode` por su código de cliente de y añada el texto o la imagen que se vinculará a la dirección URL de no participación.

Los visitantes que hagan clic en este vínculo no se incluirán en ninguna petición de mbox llamada desde sus sesiones de navegación hasta que eliminen sus cookies o hasta pasados dos años, lo que ocurra primero. Esto funciona estableciendo una cookie para el visitante llamada `disableClient` en el dominio `clientcode.tt.omtrdc.net`.

Aunque utilice una implementación de cookies de origen, la posibilidad de exclusión proporcionada se establece mediante una cookie de terceros. Si el cliente solo utiliza una cookie de origen, [!DNL Target] comprueba si hay una cookie de exclusión configurada.

## Reglamentos de protección de datos y privacidad

Consulte [Reglamentos de protección de datos y privacidad](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) para obtener Información sobre el Reglamento General de Protección de Datos (RGPD) de la Unión Europea, la Ley de privacidad del consumidor de California (CCPA) y otros requisitos de privacidad internacionales, y cómo estos reglamentos afectan a su organización y a [!DNL Target].

## Recopilación de datos sobre el uso de las funciones

Los datos de uso de funciones individuales se recopilan con fines de Adobe interno para identificar si [!DNL Target] Las funciones de están funcionando según lo previsto o para identificar las funciones que se están infrautilizando. Se recopilan varias mediciones de latencia para ayudar a resolver los problemas de rendimiento. Los datos personales no se recopilan.

Puede excluirse de los datos de uso de informes en nuestros SDK configurando `telemetryEnabled` como false en las opciones de inicialización del cliente. Para obtener más información, consulte [telemetryEnabled en targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).
