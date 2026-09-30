---
title: ¿Qué es la API de Adobe Recommendations?
description: Esta guía muestra a los desarrolladores la práctica de usar las API de Recommendations de Adobe Target para configurar y administrar los catálogos de Recommendations y los criterios personalizados, así como el uso de la API de envío para recuperar contenido de Recommendations.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail:
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
TQID: 'https://experienceleague.adobe.com/-bWsxWNZK7LXp0VvKZmsZc68jXcit57v7Wki9hR3wH4'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
    internal-label: Administration and configuration
  - id: f69bc5f1-ebdb-4306-a281-f2e77daf734c
    internal-label: Activities and tests
subfeature_v2:
  - id: ed58f4a1-16eb-4c8c-b505-be9da766a9ec
    internal-label: Recommendations
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
    internal-label: Overview
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%
---
# Información general de API de Adobe Recommendations

Las API relevantes para Recommendations incluyen [API de administrador](../../before-administer/target-api-overview.md) que le permiten lo siguiente:

* Administre su catálogo de productos o contenido recomendables
* Administrar los algoritmos y las actividades de Recommendations

Si usa la [API de envío](../../implement/delivery-api/overview.md) de Target con Recommendations, también puede:

* Recupere recomendaciones en objetos JSON, HTML o XML para que se puedan mostrar en la web, dispositivos móviles, correo electrónico, Internet de las cosas (IOT) y otros canales.

## Descripción

Esta guía, relativa a las API de Recommendations, guía a los desarrolladores a través de la práctica con las API de Recommendations para configurar y administrar catálogos de Recommendations y criterios personalizados, así como el uso de la API de envío para recuperar contenido de Recommendations. Al final, usted será capaz de:

* Configuración y administración de entidades mediante la API de Recommendations
* Configuración y administración de criterios personalizados con la API de Recommendations
* Obtenga información sobre cómo utilizar Recommendations con la API de envío para utilizar los resultados de Recommendations en dispositivos que no son de HTML

## Público

Esta guía está dirigida a desarrolladores que utilicen las API de Target o las API de Recommendations por primera vez.

## Requisitos previos {#prerequisites}

Las API de administración de Target requieren [configuración de autenticación de Adobe](../configure-authentication.md). Asegúrese de tener esto configurado antes de utilizar la API de Recommendations.

## Recursos

Tenga en cuenta los siguientes recursos, que son necesarios para comprender esta guía y seguirla correctamente:

| Recurso | Detalles |
| --- | --- |
| Postman | Obtén la [aplicación de Postman](https://www.postman.com/downloads/) para tu sistema operativo. Postman basic es gratuito con la creación de cuentas. Aunque no es necesario para utilizar las API de Adobe Target en general, Postman facilita los flujos de trabajo de las API y Adobe Target proporciona varias colecciones de Postman para ayudarle a ejecutar sus API y aprender cómo funcionan. El resto de esta guía supone conocimientos prácticos de Postman. Para obtener ayuda, consulte la [documentación de Postman](https://learning.getpostman.com/). |
| Referencias: | En el resto de esta guía se da por hecho que está familiarizado con los siguientes recursos:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentación de la API de perfil y administrador de Target](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Documentación de la API de Recommendations](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
