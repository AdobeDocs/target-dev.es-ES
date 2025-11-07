---
keywords: rgpd, ue, unión europea, privacidad, preguntas frecuentes, ley de privacidad del consumidor de california, ccpa, privacidad, protección de datos, exclusión, exclusión, gobierno, regulación, rgpr5, rgpd6, rgpd7, rgpd8, rgpd9, eu0, eu1, eu2, eu3, eu4, eu5
description: Obtenga información sobre Target y el Reglamento General de Protección de Datos (RGPD) de la Unión Europea, la Ley de Privacidad del Consumidor de California (CCPA) y otros requisitos de privacidad.
title: ¿Cómo gestiona Target las normas de privacidad y protección de datos?
feature: Privacy & Security
exl-id: 40bac3c5-8e6f-4a90-ac0c-eddce1dbe6c0
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '2329'
ht-degree: 62%

---

# Reglamentos de protección de datos y privacidad

Información sobre el Reglamento General de Protección de Datos (RGPD) de la Unión Europea, la Ley de Privacidad del Consumidor de California (CCPA) y otros requisitos de privacidad internacionales. Descubra cómo afectan estas regulaciones a su organización y a Adobe Target.

## Información general sobre el Reglamento General de Protección de Datos (RGPD) 

El 25 de mayo de 2018, entró en vigor el RGPD de la Unión Europea. Para obtener más información sobre qué significa esto para usted, consulte [RGPD y su empresa](https://business.adobe.com/es/privacy/general-data-protection-regulation.html).

Cuando proporciona software y servicios a una empresa, Adobe actúa como procesador de datos de cualquier dato personal que procese y almacene como parte de la provisión de dichos servicios. Como procesador de datos, Adobe procesa los datos personales de acuerdo con los permisos e instrucciones que su empresa proporcione (y que pueden establecerse, por ejemplo, en el acuerdo entre su empresa y Adobe).

Como responsable del tratamiento de datos, determinará qué datos personales Adobe trata y almacena en su nombre. Si usa soluciones de Adobe Experience Cloud, Adobe podría alojar datos personales en su nombre según las soluciones que use y la información que decida enviar a su cuenta de Adobe Experience Cloud. Si desea ver una lista detallada de ejemplos, consulte [Privacidad de Adobe Experience Cloud](https://www.adobe.com/es/privacy/experience-cloud.html#collect).

Adobe Experience Cloud proporciona API preparadas para RGPD para Controladores de datos que les permite completar las tareas siguientes:

* Acceder a información del interesado almacenada dentro de Target
* Eliminar información del interesado almacenada dentro de Target

Para obtener más información, consulte:

* [Información general de Adobe Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=es)
* [Guía de API de Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/api/overview.html?lang=es)
* [Descripción general de la IU de Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=es)

## Información general sobre la Ley de privacidad del consumidor de California (CCPA)

La Ley de privacidad del consumidor de California (CCPA) segura a los consumidores californianos nuevos derechos relacionados con su información personal e impone responsabilidades de protección de datos a determinadas entidades que realizan negocios en California. La CCPA entró en vigor el 1 de enero de 2020.

La ley asegura varios derechos clave para los californianos, incluidos los derechos a:

* Solicitar información (acceso a datos)
* Excluirse de la venta de información personal (un derecho con una definición muy amplia para evitar que se comparta información con terceros)
* Eliminar información personal
* Saber que la información personal se está revelando o vendiendo

Si estuvo al tanto de la ley de privacidad de Europa (RGPD) del año pasado, algunos de estos derechos le resultarán familiares y podrá aprovechar gran parte del trabajo realizado.

>[!NOTE]
>
>El acceso a los datos y su eliminación, tal como se aplican a la CCPA, siguen el mismo proceso que para el RGPD.

## Inclusión de Adobe Target y Adobe Experience Platform

Target proporciona soporte de funcionalidad opcional a través de etiquetas en Adobe Experience Platform para ayudar a respaldar su estrategia de gestión de consentimiento. La funcionalidad de inclusión permite a los clientes controlar cómo y cuándo se inicia la etiqueta de Target. También hay una opción a través de Adobe Experience Platform para aprobar previamente la etiqueta de Target. Para habilitar la capacidad de usar la inclusión en la biblioteca de Target at.js, debe usar `targetGlobalSettings` y agregar la configuración `optinEnabled=true`. En Adobe Experience Platform, seleccione &quot;habilitar&quot; en la lista desplegable Inclusión del RGPD en la vista de instalación de extensión. Consulte [Implementar Target mediante Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) para obtener más información.

El siguiente fragmento de código muestra cómo habilitar la configuración `optinEnabled=true`:

```
window.targetGlobalSettings = {
  optinEnabled: true
};
```

>[!NOTE]
>
>La funcionalidad Opt-in es compatible con la versión 1.7.0 de at.js y con at.js 2.1.0 o posteriores. Opt-in no es compatible con la versión 2.0.0 y 2.0.1 de at.js.

El uso de Adobe Experience Platform es el enfoque recomendado para administrar inclusiones. Existe un control granular adicional en Adobe Experience Platform para ocultar elementos seleccionados de su página antes de la activación de Target que son útiles para su estrategia de consentimiento.

Hay tres escenarios a considerar cuando se usa la inclusión:

1. **La etiqueta de Target se aprobó previamente mediante Adobe Experience Platform (o el sujeto de datos aprobó previamente Target):** La etiqueta de Target no se retiene para el consentimiento y funciona como se espera.
1. **La etiqueta de Target NO está aprobada previamente y `bodyHidingEnabled` es FALSO:** la etiqueta de Target se activa solo después de que se haya obtenido el consentimiento del cliente. Antes de recopilar el consentimiento, solo está disponible el contenido predeterminado. Después de recibir el consentimiento, se llama a Target y el contenido personalizado está disponible para el sujeto de los datos (visitante). Debido a que solo el contenido predeterminado está disponible antes del consentimiento, es importante usar una estrategia adecuada, como una página de inicio que cubra cualquier parte de la página o contenido que pueda ser personalizado. Este proceso asegura que la experiencia se mantenga consistente para el sujeto de los datos (visitante).
1. **La etiqueta de Target NO está aprobada previamente y `bodyHidingEnabled` es VERDADERO:** la etiqueta de Target se activa solo después de que se haya obtenido el consentimiento del cliente. Antes de recopilar el consentimiento, solo está disponible el contenido predeterminado. Sin embargo, debido a que `bodyHidingEnabled` se establece en verdadero, `bodyHiddenStyle` dicta qué contenido de la página está oculto hasta que se dispara la etiqueta de Target (o el sujeto de los datos rechaza la opción de inclusión, en cuyo caso se muestre el contenido por defecto). De forma predeterminada, `bodyHiddenStyle` se establece en `body { opacity:0;}`, que oculta la etiqueta de cuerpo HTML. A continuación encontrará la configuración de página recomendada por Adobe para que todo el cuerpo de la página, excepto el cuadro de diálogo del administrador de consentimiento, se oculte al colocar el contenido de la página en un contenedor y el cuadro de diálogo del administrador de consentimiento en un contenedor separado. Estos ajustes configuran Target de modo que ocultan solo el contenedor de contenido de la página. Consulte [Resumen de Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=es&).

   La configuración de página recomendada para el escenario 3 es:

   ```
   <html> 
   <head> 
   //visitor, at.js 
   </head> 
   
   <body> 
   <div id = "consentManagerDialog"> 
   
   //consent manager html dialog goes here 
   </div> 
   
   <div id="pageContent"> 
   // page content goes here 
   </div> 
   
   </body> 
   </html> 
   ```

   Suponiendo el `bodyHiddenStyle` de:

   ```
   #pageContent { opacity:0;}
   ```

## Preguntas frecuentes sobre legislación de protección de datos y privacidad

Preguntas frecuentes sobre el Reglamento General de Protección de Datos (RGPD) de la Unión Europea, la Ley de privacidad del consumidor de California (CCPA) y otros requisitos de privacidad internacionales específicos de Target.

### ¿Cuál es la política de Adobe para estas regulaciones?

Adobe ya cumple o está implementando sus obligaciones como procesador de datos. Adobe tiene una base sólida de controles de privacidad y seguridad certificados y realizó mejoras de producto con antelación al plazo de mayo de 2018. Los clientes empresariales tienen la responsabilidad de implementar estas mejoras, como así también actualizar cualquier política y procedimiento necesarios.

### ¿Debe mi empresa, como responsable del tratamiento de datos, enviar una solicitud de RGPD o de CCPA para cada solución de Adobe Experience Cloud que utilice?

No, Adobe ofrece una solución única para que los responsables de datos cumplan los requisitos del RGPD y de la CCPA. Los responsables del tratamiento de datos no necesitan ir directamente a cada una de las soluciones.

Todas las solicitudes de RGPD y CCPA entre soluciones de Experience Cloud, incluido Target, se realizan a través de una API central de Adobe denominada actualmente API del RGPD. La API completa la solicitud para el conjunto de soluciones de Experience Cloud del responsable de datos.

### ¿Qué información Adobe permite que nuestros clientes eliminen en respuesta a una solicitud del sujeto/usuario?

La información relacionada con un visitante individual dentro de Target está contenida dentro del perfil del visitante de Target. Target permite que los clientes eliminen todos los datos asociados con un ID en su perfil del visitante. Para obtener ejemplos de los datos de perfil que Target almacena, consulte [Perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=es).

Los datos agregados o anonimizados (por ejemplo, datos de informe) que no identifican a una persona en particular, o datos que no están relacionados con una persona específica (por ejemplo, datos de contenido) están fuera del alcance de una solicitud de eliminación de usuario.

De forma predeterminada, los perfiles del visitante de Target inactivos durante 90 días se eliminan sin necesidad de realizar acción alguna.

### ¿Qué ID se admiten para ayudar a los clientes a realizar una solicitud de eliminación y acceso de RGPD o de CCPA para Target?

Target admite los siguientes tipos de ID para localizar un perfil de cliente:

| ID de usuario | Tipo de ID de espacio de nombres | ID de espacio de nombres | Definición |
|--- |--- |--- |--- |
| Experience Cloud ID (ECID) | Standard | 4 | Adobe Experience Cloud ID, anteriormente conocido como ID de visitante o Experience Cloud ID. Puede usar la API de JavaScript para ubicar este ID (consulte los detalles más abajo). |
| ID de TnT/ID de cookie (TNTID) | Standard | 9 | Identificador de Target establecido como cookie en el explorador del visitante. Puede usar la API de JavaScript para ubicar este ID (consulte los detalles más abajo). |
| ID de terceros/ID de CRM (THIRDPARTYID) | Específico de Target | N/A | Si proporciona a Target su administración de la relación con los clientes u otra información de identificador único para sus clientes. |

>[!NOTE]
>
>Aunque Target admite cookies de dominio cruzado de origen y de terceros, solo se recomiendan las cookies de Target de origen para RGPD y CCPA.

### ¿Cómo gestiona Target la administración de consentimiento?

RGPD y CCPA no afectan al momento en el que se requiere consentimiento, sino que cambia el modo en que se consigue. La estrategia de consentimiento de cada cliente depende de su forma de recopilar y utilizar los datos, así como de su política de privacidad. La administración de consentimiento no es compatible y no debería lograrse mediante Target para RGPD y CCPA.

Adobe no ofrece actualmente una solución de administración de consentimiento, pero hay diversas herramientas en desarrollo en el mercado para satisfacer algunos de los nuevos requisitos. Para obtener más información sobre herramientas de privacidad en general, incluidos los administradores de consentimiento, consulte el [2017 Privacy Tech Vendor Report](https://iapp.org/media/pdf/resource_center/Tech-Vendor-Directory-1.4.1-electronic.pdf) disponible en el sitio web de la *International Association of Privacy Professionals (iapp)*.

Target proporciona soporte de funcionalidad opcional a través de Adobe Experience Platform para ayudar a su estrategia de administración de consentimiento. La funcionalidad de inclusión permite a los clientes controlar cómo y cuándo se inicia la etiqueta de Target. También hay una opción a través de Adobe Experience Platform para aprobar previamente la etiqueta de Target. El uso de Adobe Experience Platform es el enfoque recomendado para administrar inclusiones. Existe un control granular adicional en Adobe Experience Platform para ocultar elementos seleccionados de su página antes de la activación de Target que pueden ser útiles para su estrategia de consentimiento.

Para obtener más información sobre el RGPD, la CCPA y Adobe Experience Platform, consulte [La biblioteca JavaScript de privacidad de Adobe y RGPD](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=es&). Además, consulte la *inclusión de Adobe Target y Adobe Experience Platform* en la sección superior.

### ¿Envía `AdobePrivacy.js` información a la API del RGPD?

AdobePrivacy.js *no* envía esta información a la API. Debe hacerlo el cliente. Esta biblioteca proporciona únicamente los ID almacenados en el navegador para ese visitante concreto.

### ¿Qué elimina `removeIdentities`?

`removeIdentities` *elimina únicamente* esas identidades del navegador, y solo depende de si la solución de Adobe lo ha implementado.

Por ejemplo, Target elimina las cookies que almacenan sus ID, pero Adobe Audience Manager (AAM) no elimina el ID demdex, que se almacena en una cookie de terceros.

### ¿Qué información debe incluirse en una solicitud de RGPD o CCPA de Target?

Además de los requisitos de Privacy Service central, un mensaje de RGPD o de CCPA válido para Target contiene lo siguiente:

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            "namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            "namespace":"TNTID", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"THIRDPARTYID", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
}
```

### ¿Qué tipos de respuesta puedo esperar de Target a través de la API del RGPD? 

| Estado de la solicitud | Mensaje de respuesta de Target | Escenario |
|--- |--- |--- |
| Procesamiento | Procesamiento | Target ha recibido la solicitud de RGPD o de CCPA y la está procesando. |
| Completado | No aplicable: el contexto de la empresa no es aplicable | El ID de IMS de la solicitud de RGPD o de CCPA no está asignado a ningún cliente de Target.<br />Algunas empresas tienen varios ID de IMS. Envíe el ID de IMS donde se proporciona Target. |
| Completado | No aplicable: no se encontró el contexto del usuario | El ID proporcionado en la solicitud de RGPD o de CCPA para el visitante o sujeto de datos específico no está presente en el almacén de perfiles de Target.<br />Este resultado también devuelve si intenta enviar un tipo de ID de área de nombres no compatible con Target (consulte más atrás cuáles son los ID compatibles). |
| Error | Mensaje de error (los detalles dependen del tipo de error) | Error al recuperar o eliminar el perfil objeto de los datos solicitados.<br />Error al cargar en Azure la solicitud de acceso. |

### ¿Qué respuesta Target envía a la API de RGPD para una solicitud de acceso?

Las respuestas a solicitudes de datos de acceso contienen un resumen del perfil de Target para el visitante en cuestión. Esta devolución se envía a la API de RGPD de Experience Cloud, que a su vez envía una respuesta a los Responsables de datos.

Una respuesta de API de acceso para Target de muestra tendrá un aspecto similar al siguiente:

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            ~"namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            ~"namespace":"tntId", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"thirdPartyId", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
} 
```

| Campo | Descripción |
|--- |--- |
| jobId | Indica el ID del trabajo del RGPD o de la CCPA a partir de la API del RGPD central. |
| imsOrgID | Proporciona un identificador único para su empresa. |
| namespace | También conocido como la fuente de datos. Consulte “¿Cuáles son los ID compatibles para ayudar a los clientes a realizar una solicitud de acceso y eliminación de RGPD o de CCPA para Target?” en este tema. |
| type | El tipo de ID para el cual solicitó acceso de datos del RGPD o de la CCPA. Target acepta varios tipos de ID, algunos de los cuales son estándares y algunos son específicos de Target. Consulte “¿Cuáles son los ID compatibles para ayudar a los clientes a realizar una solicitud de acceso y eliminación de RGPD o de CCPA para Target?” en este tema. |
| value | El ID de la fuente de datos/espacio de nombres. Consulte “¿Cuáles son los ID compatibles para ayudar a los clientes a realizar una solicitud de acceso y eliminación de RGPD o de CCPA para Target?” para valores aceptados. |
| integration code | Los códigos de integración son nombres descriptivos para las fuentes de datos y ayudarle a seguir sus fuentes de datos con más facilidad que con los ID de fuentes de datos. |

Cuando se proporcionan varios valores para identificar perfiles, cada identificador válido tiene un archivo de perfil. Uno o más archivos de perfil se envían al RGPD central de Azure Blob mediante la API central del RGPD, con el formato de una respuesta JSON de perfil de Target.

Un JSON de perfil de Target podría tener un aspecto similar al siguiente ejemplo:

```
{"profileAttributes": 
 
"Sample_Parameter":{"value":"Gold Loyalty Status","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"user.ReturnTimeOfDay":{"value":"44.0","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"firstSessionStart":{"value":"1523497450602","modifiedAt":"2018-04-11T21:44:10.000-04:00"}, 
 
"user.sessionCountScript":{"value":"1","modifiedAt":"2018-04-11T21:44:14.000-04:00"} 
   } 
} 
```

La siguiente tabla contiene descripción de los campos JSON de perfil ilustrativos:

| Campo | Descripción |
|--- |--- |
| Sample_Parameter | El responsable del tratamiento de datos carga o proporciona directamente gran cantidad de información en el perfil de Target. En este ejemplo, se cargó un parámetro en el perfil de Target con la API de actualización de perfil. Para obtener más información, consulte [Métodos para obtener datos en Target](/help/dev/before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md). |
| user.ReturnTimeOfDay | Este campo estándar incluye la hora del día correspondiente a la visita de retorno más reciente de un usuario. |
| firstSessionStart | Este campo estándar incluye la hora del día en que comenzó la primera sesión del usuario. |
| user.sessionCountScript | El responsable del tratamiento de datos carga o proporciona directamente gran cantidad de información en el perfil de Target. En este ejemplo, un script de perfil está incrementando el número de sesiones que este visitante realizó en el sitio del responsable del tratamiento de datos. Para obtener más información, consulte [Atributos de script de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=es). |

>[!NOTE]
>
>Este ejemplo de código es una versión abreviada de un JSON de perfil de Target para ilustrarlo. Muchos de los campos del perfil de Target no son estándares. El resultado obtenido depende de la información que contenga ese perfil del visitante específico.

### ¿Admite Target la ocultación de la IP? 

Target admite la ocultación de la IP si se decide utilizar dicha ocultación como parte de la estrategia de implementación del RGPD o de la CCPA. Para obtener más información, consulte [Privacidad](privacy.md#replacement-of-last-octet-of-ip-addresses).

### ¿Debo hacer algo para evitar que mis datos se compartan o vendan a terceros?

Target no permite que los clientes compartan o vendan datos directamente desde Target a terceros, por lo que no hay exclusión de la venta para Target.
