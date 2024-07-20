---
keywords: apple, ITP, prevención inteligente del seguimiento, experience cloud id, ecid, itp
description: Obtenga información acerca de  [!DNL Adobe Target]  y el impacto de la iniciativa Prevención inteligente del seguimiento (ITP) de Apple, que busca proteger la privacidad de los usuarios de Safari.
title: ¿Cómo administra  [!DNL Target] la compatibilidad con Apple ITP?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 30%

---

# Prevención inteligente del seguimiento de Apple (ITP) 2.x

Prevención inteligente del seguimiento (ITP) es la iniciativa de Apple para proteger la privacidad de los usuarios de Safari. La primera versión de ITP, que fue en 2017, iba orientada al uso de cookies por terceros. De hecho, Apple bloqueó toda la información sobre cookies de terceros, lo cual a su vez causó problemas graves para las empresas de tecnología de anuncios y de marketing, ya que las cookies de terceros se utilizan generalmente para rastrear visitantes y recopilar sus datos. Ahora Apple busca imponer limitaciones y restricciones sobre cómo se utilizan las cookies de origen en Safari.

Estas versiones de ITP incluyen las restricciones siguientes:

| Versión | Detalles |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | Las cookies del lado del cliente restringidas que se colocan en el explorador mediante la API `document.cookie` con una caducidad de siete días.<br />Publicado el 21 de febrero de 2019. |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | Se ha reducido drásticamente la caducidad de siete días a un día.<br />Publicado el miércoles, 24 de abril de 2019. |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | Se eliminaron varias soluciones, como usar localStorage o usar JavaScript `Document.referrer property`.<br />Publicado el 23 de septiembre de 2019.Se ha lanzado la función de defensa de encubrimiento <br />CNAME en ITP en Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14 y iPadOS 14. Todas las cookies creadas por una respuesta HTTP cubierta por CNAME de terceros se configurarán para que caduquen en siete días.<br />Anunciado el 12 de noviembre de 2020. |

## ¿Cuál es el impacto para mí como cliente de [!DNL Target]?

Target proporciona bibliotecas JavaScript para que usted las implemente en sus páginas de modo que [!DNL Target] pueda ofrecer personalización en tiempo real a sus visitantes. Hay tres bibliotecas de JavaScript [!DNL Target] en at.js 1.*x*, at.js 2.*x*, el [!DNL Adobe Experience Cloud Web SDK] que coloca cookies del lado del cliente [!DNL Target] en los navegadores de los visitantes a través de la API `document.cookie`. Como resultado, las cookies de [!DNL Target] se ven afectadas por ITP 2.1, 2.2 y 2.3 de Apple y caducarán pasados siete días (con ITP 2.1) y después de un día (con ITP 2.2 e ITP 2.3).

Apple ITP 2.x afecta a [!DNL Target] en las siguientes áreas:

| Impacto | Detalles |
| --- | --- |
| Aumento potencial del número de visitantes únicos | Debido a que el periodo de caducidad se establece en siete días (con ITP 2.1) y un día (con ITP 2.2 e ITP 2.3), es posible que vea un aumento de visitantes únicos procedentes de exploradores Safari. Si los visitantes vuelven a su dominio después de siete días (ITP 2.1) o un día (ITP 2.2 e ITP 2.3), [!DNL Target] se verá obligado a colocar una nueva cookie [!DNL Target] en su dominio en lugar de la cookie caducada. La nueva cookie [!DNL Target] supone un nuevo visitante único aunque el usuario sea el mismo. |
| Reducción de los periodos retroactivos de las actividades [!DNL Target] | Los perfiles de visitante para las actividades [!DNL Target] pueden tener un período retroactivo reducido para la toma de decisiones. Las cookies [!DNL Target] se aprovechan para identificar a un visitante y almacenar atributos de perfil de usuario para la personalización. Dado que las cookies [!DNL Target] pueden caducar en Safari después de siete días (ITP 2.1) o un día (ITP 2.2 y 2.3), los datos de perfil de usuario vinculados a la cookie [!DNL Target] purgada no se pueden utilizar para la toma de decisiones. |
| Scripts de perfil basados en 3rdPartyID | Debido a que el período de caducidad se establece en siete días (con ITP 2.1) y un día (con ITP 2.2 e ITP 2.3), [los scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html) basados en la cookie 3rdPartyID dejarán de funcionar al expirar. |
| URL de control de calidad/vista previa en dispositivos iOS | Debido a que el período de caducidad se establece en siete días (con ITP 2.1) y un día (con ITP 2.2 e ITP 2.3), [las direcciones URL de control de calidad y vista previa](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) dejarán de funcionar tras la caducidad porque las direcciones URL se basan en la cookie 3rdPartyID. |

## ¿Esto afectará a mi implementación actual de [!DNL Target]?

Si usa la biblioteca de ID de Experience Cloud (ECID) además de la biblioteca de JavaScript [!DNL Target], su implementación se verá afectada de las formas enumeradas en este artículo: [Impacto de Safari ITP 2.1 en clientes de Adobe Experience Cloud y Experience Platform](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
