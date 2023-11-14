---
title: ¿Qué es la API de Adobe Recommendations?
description: Esta guía muestra a los desarrolladores la práctica de usar las API de Recommendations de Adobe Target para configurar y administrar catálogos de Recommendations y criterios personalizados, así como el uso de la API de envío para recuperar contenido de Recommendations.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# Información general de API de Adobe Recommendations

Las API relevantes para Recommendations incluyen [API de administrador](../../before-administer/target-api-overview.md) que le permiten:

* Administre su catálogo de productos o contenido recomendables
* Administrar los algoritmos y las actividades de Recommendations

Uso de Target [API de envío](../../implement/delivery-api/overview.md) con Recommendations, también puede:

* Recupere recomendaciones en objetos JSON, HTML o XML para que se puedan mostrar en la web, dispositivos móviles, correo electrónico, Internet de las cosas (IOT) y otros canales.

## Descripción

Esta guía, relativa a las API de Recommendations, muestra a los desarrolladores la práctica práctica de utilizar las API de Recommendations para configurar y administrar catálogos de Recommendations y criterios personalizados, así como el uso de la API de envío para recuperar contenido de Recommendations. Al final, usted será capaz de:

* Configuración y administración de entidades mediante la API de Recommendations
* Configuración y administración de criterios personalizados con la API de Recommendations
* Obtenga información sobre cómo utilizar Recommendations con la API de envío para utilizar los resultados de Recommendations en dispositivos que no son de HTML

## Audiencia

Esta guía está dirigida a desarrolladores que utilicen las API de Target o las API de Recommendations por primera vez.

## Requisitos previos   {#prerequisites}

Las API de administrador de Target requieren lo siguiente [configuración de autenticación de Adobe](../configure-authentication.md). Asegúrese de tener esto configurado antes de utilizar la API de Recommendations.

## Recursos

Tenga en cuenta los siguientes recursos, que son necesarios para comprender esta guía y seguirla correctamente:

| Recurso | Detalles |
| --- | --- |
| Postman | Obtenga la [aplicación de Postman](https://www.postman.com/downloads/) para su sistema operativo. Postman basic es gratuito con la creación de cuentas. Aunque no es necesario para utilizar las API de Adobe Target en general, Postman facilita los flujos de trabajo de las API y Adobe Target proporciona varias colecciones de Postman para ayudarle a ejecutar sus API y aprender cómo funcionan. El resto de esta guía supone conocimientos prácticos de Postman. Para obtener ayuda, consulte la [Documentación de Postman](https://learning.getpostman.com/). |
| Referencias | En el resto de esta guía se da por hecho que está familiarizado con los siguientes recursos:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentación de la API de perfil y administración de Target](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Documentación de API de Recommendations](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
