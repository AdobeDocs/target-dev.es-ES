---
keywords: Navegadores, Requisitos previos, Requisitos, internet explorer, chrome, firefox, safari, android, surface, Navegadores0
description: Conozca qué exploradores de Internet [!DNL Adobe Target] admiten para su interfaz y para la entrega de contenido.
title: ¿Qué exploradores admiten  [!DNL Target] ?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: f194c6de43070443b78c9a69b4233c27d70b8858
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 23%

---

# Navegadores admitidos

La aplicación y la entrega de contenido de [!DNL Adobe Target] se han probado en una amplia gama de navegadores y dispositivos.

Para obtener información más importante acerca de TLS, vea [Cambios en el cifrado de TLS (Seguridad de capa de transporte)](tls-transport-layer-security-encryption.md).

## Interfaz de [!DNL Target] Standard/Premium

La interfaz [!DNL Target] es compatible con los siguientes exploradores y dispositivos:

| Tipo de dispositivo | Versión del navegador |
|--- |--- |
| Windows | <ul><li>Microsoft Edge</li><li>Google Chrome (última versión, última menos 1)</li><li>Mozilla Firefox (última versión, menos 1)</li></ul> |
| Mac | <ul><li>Firefox (último, último menos 1)</li><li>Chrome (última versión, menos 1)</li></ul> |

## Entrega de contenido

La entrega de contenido se ha probado en los siguientes navegadores y dispositivos:

| Tipo de dispositivo | Versión del navegador |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 y 10. Probado en modo de emulación. **Nota**: la entrega de contenido en IE 9 ya no es compatible con at.js 1.3.0 (y versiones posteriores). La entrega de contenido en IE 10, 11 y todas las versiones anteriores ya no es compatible con at.js 2.5.0 (y versiones posteriores).</li><li>Internet Explorer 11. **Nota**: la entrega de contenido en IE 10, 11 y todas las versiones anteriores ya no es compatible con at.js 2.5.0 (y versiones posteriores).</li><li>Microsoft Edge</li><li>Chrome (última versión, menos 1)</li><li>Firefox (último, último menos 1)</li></ul> |
| Mac | <ul><li>Apple Safari (versión más reciente). **Nota**: Para obtener más información sobre cómo administra Safari las cookies de origen y de terceros, consulte [Cookie de Target](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (último, último menos 1)</li><li>Chrome (última versión, menos 1)</li></ul> |
| Móvil o tableta | <ul><li>Apple iOS (última versión)</li><li>Dispositivos y tabletas Android (Android 4 y versiones posteriores)</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

Tenga en cuenta lo siguiente:

* [!DNL Adobe Experience Platform Web SDK] está diseñado para funcionar de manera óptima en las últimas versiones de [!DNL Google Chrome], [!DNL Safari], [!DNL Firefox] y [!DNL Microsoft Edge Chromium]. Es posible que tenga problemas al usar ciertas funciones en versiones anteriores de estos exploradores o en exploradores obsoletos, como [!DNL Internet Explorer].
* Para implementaciones de at.js, [!DNL Target] muestra el contenido predeterminado en versiones anteriores de Internet Explorer y posiblemente en versiones anteriores de los exploradores enumerados anteriormente.
* Internet Explorer trata todos los elementos desconocidos (como los elementos personalizados) como el mismo tipo de elemento. Como resultado, la entrega no funciona con elementos personalizados.
* [!DNL Target] muestra contenido predeterminado en exploradores que no aparecen enumerados anteriormente y en exploradores que usan [modo quirks](https://en.wikipedia.org/wiki/Quirks_mode). at.js requiere un tipo de documento que se muestre en modo estándar, por ejemplo: `<!DOCTYPE html>`.
* [!DNL Adobe] La infraestructura de entrega se está protegiendo para NO admitir dispositivos y exploradores TLS 1.0 a partir del 12 de septiembre de 2018. Consulte [Cambios en el cifrado de TLS (Seguridad de capa de transporte)](../before-implement/tls-transport-layer-security-encryption.md) para entender el impacto general de este cambio.
