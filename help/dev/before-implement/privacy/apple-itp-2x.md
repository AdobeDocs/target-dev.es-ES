---
keywords: apple, ITP, prevención inteligente del seguimiento, experience cloud id, ecid, itp
description: Obtenga información acerca de  [!DNL Adobe Target]  y el impacto de la iniciativa Prevención inteligente del seguimiento (ITP) de Apple, que busca proteger la privacidad de los usuarios de Safari.
title: ¿Cómo administra  [!DNL Target] la compatibilidad con Apple ITP?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
TQID: https://experienceleague.adobe.com/AvrlwiLa-soHwrGT1QMa8KgsiIwfwKaF-0LBxMjb8cs
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 681
ht-degree: 28%

---

# Prevención inteligente del seguimiento de Apple (ITP) 2.x

Prevención inteligente del seguimiento (ITP) es la iniciativa de Apple para proteger la privacidad de los usuarios de Safari. La primera versión de ITP, que fue en 2017, iba orientada al uso de cookies por terceros. De hecho, Apple bloqueó toda la información sobre cookies de terceros, lo cual a su vez causó problemas graves para las empresas de tecnología de anuncios y de marketing, ya que las cookies de terceros se utilizan generalmente para rastrear visitantes y recopilar sus datos. Ahora Apple busca imponer limitaciones y restricciones sobre cómo se utilizan las cookies de origen en Safari.

Estas versiones de ITP incluyen las restricciones siguientes:

| Versión | Detalles |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | Las cookies limitadas del cliente que se colocan en el explorador mediante la API `document.cookie` con una caducidad de siete días.<br />Publicado el 21 de febrero de 2019. |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | Se ha reducido drásticamente la caducidad de siete días a un día.<br />Publicado el miércoles, 24 de abril de 2019. |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | Se han eliminado varias soluciones, como usar localStorage o usar JavaScript `Document.referrer property`.<br />Publicada el 23 de septiembre de 2019.<br />Se ha lanzado la función de defensa de ocultamiento CNAME para ITP en Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14 y iPadOS 14. Todas las cookies creadas por una respuesta HTTP cubierta por CNAME de terceros se configurarán para que caduquen en siete días.<br />Anunciado el 12 de noviembre de 2020. |

## ¿Cuál es el impacto para mí como cliente de [!DNL Target]?

Target proporciona bibliotecas JavaScript para que usted las implemente en sus páginas de modo que [!DNL Target] pueda ofrecer personalización en tiempo real a sus visitantes. Hay tres bibliotecas JavaScript [!DNL Target] at.js 1.*x*, at.js 2.*x*, las [!DNL Adobe Experience Cloud Web SDK] que colocan cookies [!DNL Target] del lado del cliente en los exploradores de los visitantes a través de la API `document.cookie`. Como resultado, las cookies de [!DNL Target] se ven afectadas por ITP 2.1, 2.2 y 2.3 de Apple y caducarán pasados siete días (con ITP 2.1) y después de un día (con ITP 2.2 e ITP 2.3).

Apple ITP 2.x afecta a [!DNL Target] en las siguientes áreas:

| Impacto | Detalles |
| --- | --- |
| Aumento potencial del número de visitantes únicos | Debido a que el periodo de caducidad se establece en siete días (con ITP 2.1) y un día (con ITP 2.2 e ITP 2.3), es posible que vea un aumento de visitantes únicos procedentes de exploradores Safari. Si los visitantes vuelven a su dominio después de siete días (ITP 2.1) o un día (ITP 2.2 e ITP 2.3), [!DNL Target] se verá obligado a colocar una nueva cookie [!DNL Target] en su dominio en lugar de la cookie caducada. La nueva cookie [!DNL Target] supone un nuevo visitante único aunque el usuario sea el mismo. |
| Reducción de los periodos retroactivos de las actividades [!DNL Target] | Los perfiles de visitante para las actividades [!DNL Target] pueden tener un período retroactivo reducido para la toma de decisiones. Las cookies [!DNL Target] se aprovechan para identificar a un visitante y almacenar atributos de perfil de usuario para la personalización. Dado que las cookies [!DNL Target] pueden caducar en Safari después de siete días (ITP 2.1) o un día (ITP 2.2 y 2.3), los datos de perfil de usuario vinculados a la cookie [!DNL Target] purgada no se pueden utilizar para la toma de decisiones. |
| Scripts de perfil basados en 3rdPartyID | Debido a que el período de caducidad se establece en siete días (con ITP 2.1) y un día (con ITP 2.2 e ITP 2.3), [los scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=es) basados en la cookie 3rdPartyID dejarán de funcionar al expirar. |
| URL de control de calidad/vista previa en dispositivos iOS | Debido a que el período de caducidad se establece en siete días (con ITP 2.1) y un día (con ITP 2.2 e ITP 2.3), [las direcciones URL de control de calidad y vista previa](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=es) dejarán de funcionar tras la caducidad porque las direcciones URL se basan en la cookie 3rdPartyID. |

## ¿Esto afectará a mi implementación actual de [!DNL Target]?

Si usa la biblioteca Experience Cloud ID (ECID) además de la biblioteca JavaScript [!DNL Target], su implementación se verá afectada de las formas enumeradas en este artículo: [Impacto de Safari ITP 2.1 en clientes de Adobe Experience Cloud y Experience Platform](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
