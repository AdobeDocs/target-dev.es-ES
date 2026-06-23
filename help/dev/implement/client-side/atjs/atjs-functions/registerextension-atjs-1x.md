---
keywords: registerExtension, registerextension, registrar extensión, at.js, funciones, función, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, timeout, registerExtension2
description: Utilice la función [!UICONTROL registerExtension()] para la biblioteca JavaScript  [!DNL Adobe Target] at.js para registrar una extensión específica. (at.js 1.x)
title: ¿Cómo utilizo la función [!UICONTROL registerExtension()]?
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
TQID: https://experienceleague.adobe.com/qTWubp0dNesN-8vsooz8pdbjfSw1W1ktm-0bG6YRzJw
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
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 62%

---

# [!UICONTROL registerExtension()] - at.js 1.x

Ofrece una forma estándar de registrar una extensión determinada.

>[!NOTE]
>
>Esta función solo está disponible para las versiones 1.0 *de at.js.* Esta función quedó obsoleta con el lanzamiento de at.js 2.*x*. Esta función devuelve el contenido predeterminado si se utiliza con at.js 2.x.

El parámetro de opciones es obligatorio y tiene la siguiente estructura:

| Clave | Tipo | Requerido | Descripción |
|--- |--- |--- |--- |
| name | Cadena | Sí | Nombre de la extensión. |
| módulos | Matriz[Cadena] | Sí | Una matriz de cadenas que representan los nombres de los módulos solicitados. |
| registrarse | Función | Sí | Una función que se usa para inicializar y compilar la extensión. Esta función recibe argumentos basados en la matriz de módulos. |

Notas:

* Si no se proporciona uno de los parámetros, se genera una excepción.
* Si la matriz de módulos está vacía, se genera una excepción.

Para obtener más información y ejemplos sobre cómo usar `[!UICONTROL registerExtension]`, consulte la página [Extensiones atjs de Target de Adobe Experience Cloud](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) en GitHub.

## Métodos del módulo de configuración

| Clave | Tipo | Descripción |
|--- |--- |--- |
| clientCode | Cadena | Código de cliente |
| serverDomain | Cadena | Dominio de servidor Edge |
| globalMboxName | Cadena | [!DNL Target] nombre de mbox global |
| globalMboxAutoCreate | Booleano | Indica si la creación automática está habilitada o no |
| timeout | Número | Tiempo de espera de la solicitud |

## Métodos del módulo del registrador

| Clave | Tipo | Descripción |
|--- |--- |--- |
| log | Función | Registra la lista variable de argumentos en la consola del navegador (si existe). Solo se activa cuando `mboxDebug=true` se pasa a la dirección URL. |
| error | Función | Registra la lista variable de argumentos en la consola del navegador. Solo se activa cuando hay errores graves, como tiempo de espera de la red, nodos HTML que no se encuentran, etc. |

