---
keywords: implementar, implementación, implementación, adobe launch, launch, race, redirect, experience platform launch, platform launch, etiquetas, adobe platform, implement2
description: Aprenda a implementar la biblioteca  [!DNL Adobe Target] at.js mediante [!DNL Adobe Experience Platform], el método preferido para implementar Target.
title: ¿Cómo puedo implementar  [!DNL Target]  utilizando  [!DNL Adobe Experience Platform]?
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
TQID: https://experienceleague.adobe.com/5dXJlXYYvlu5sskrNED2j55SNmeggtWTb1jLgXRXAEo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 61%

---

# Implementación [!DNL Target] mediante [!DNL Adobe Experience Platform]

Las etiquetas de [!DNL Adobe Experience Platform] son la siguiente generación de funcionalidades de administración de etiquetas de [!DNL Adobe]. Las etiquetas ofrecen a los clientes una forma sencilla de implementar y administrar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente.

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en [!DNL Adobe Experience Platform]. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento] (¿https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?) para obtener una referencia consolidada de los cambios terminológicos.

En la siguiente tabla se enumeran distintos recursos donde puede obtener más información:

| Recurso | Detalles |
|--- |--- |
| [Agregar Adobe Target](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html?lang=es#implement-solutions) | Este tutorial proporciona instrucciones paso a paso para implementar [!DNL Target] en un sitio web con etiquetas en [!DNL Adobe Experience Platform]. Los temas incluyen añadir la biblioteca JavaScript at.js, activar el mbox global, añadir parámetros e integrar con otras soluciones. Este artículo forma parte de un tutorial más amplio que muestra cómo implementar Adobe Experience Platform y otras soluciones de Adobe Experience Cloud. |
| [Guía de inicio rápido](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=es) | Información acerca de la implementación y administración de las etiquetas de análisis, marketing y publicidad necesarias para lograr experiencias de cliente relevantes. |
| Información general de la [extensión de Adobe  [!DNL Target] &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=es) | Información acerca de la implementación de [!DNL Target] mediante [!DNL Adobe Experience Platform]. |

## Ventajas de implementar at.js con la extensión [!DNL Target]

Las siguientes ventajas se aplican únicamente si utiliza etiquetas en [!DNL Adobe Experience Platform] para implementar at.js. Por este motivo, Adobe recomienda encarecidamente que utilice etiquetas en [!DNL Adobe Experience Platform] en lugar de una implementación manual de at.js.

* **Soluciona la condición Race de [!DNL Adobe Analytics] y [!DNL Target]:** Como la llamada a [!DNL Analytics] podría activarse antes de la llamada a [!DNL Target], la llamada [!DNL Target] no se “une” a la llamada de [!DNL Analytics]. Esta secuencia puede generar datos incorrectos. La extensión [!DNL Target] garantiza que la llamada de señalización [!DNL Analytics] espera hasta que la llamada [!DNL Target] se complete, tenga éxito o no. El uso de etiquetas en [!DNL Adobe Experience Platform] resuelve la incoherencia de datos que los clientes pueden experimentar al implementar manualmente.

  >[!NOTE]
  >
  >Utilice la acción Enviar señalización en la extensión [!DNL Adobe Analytics] para que la llamada de [!DNL Analytics] espere a que se realice la llamada de [!DNL Target]. Si llama directamente a `s.t()` o `s.tl()` utilizando código personalizado, las llamadas de [!DNL Analytics] no esperan hasta que se hayan completado las llamadas de [!DNL Target].

* **Evita la gestión de ofertas de redirección incorrectas:** Si tiene [!DNL Target] y [!DNL Analytics] en la página y Target ejecuta una oferta de redirección, puede darse el caso de que el rastreador de [!DNL Analytics] active una solicitud cuando no debería, (ya que el usuario se redirige a una dirección URL diferente). Si implementa [!DNL Target] y [!DNL Analytics] mediante etiquetas en [!DNL Adobe Experience Platform], no tendrá este problema. Utilizando etiquetas en [!DNL Adobe Experience Platform], [!DNL Target] ordena a [!DNL Analytics] que interrumpa la solicitud de señalización de [!DNL Analytics].
