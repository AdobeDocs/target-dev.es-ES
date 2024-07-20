---
keywords: registerExtension, registerextension, registrar extensión, at.js, funciones, función, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, timeout, registerExtension2
description: Utilice la función [!UICONTROL registerExtension()] para la biblioteca JavaScript  [!DNL Adobe Target] at.js para registrar una extensión específica. (at.js 1.x)
title: ¿Cómo se utiliza la función [!UICONTROL registerExtension()]?
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 69%

---

# [!UICONTROL registerExtension()] - at.js 1.x

Ofrece una forma estándar de registrar una extensión determinada.

>[!NOTE]
>
>Esta función está disponible para las versiones 1 de at.js.Solamente *x*. Esta función quedó obsoleta con el lanzamiento de at.js 2.*x*. Esta función devuelve el contenido predeterminado si se utiliza con at.js 2.x.

El parámetro de opciones es obligatorio y tiene la siguiente estructura:

| Clave | Tipo | Requerido | Descripción |
|--- |--- |--- |--- |
| name | Cadena | Sí | Nombre de la extensión. |
| módulos | Matriz[Cadena] | Sí | Una matriz de cadenas que representan los nombres de los módulos solicitados. |
| registrarse | Función | Sí | Una función que se usa para inicializar y compilar la extensión. Esta función recibe argumentos basados en la matriz de módulos. |

Notas:

* Si no se proporciona uno de los parámetros, se genera una excepción.
* Si la matriz de módulos está vacía, se genera una excepción.

Para obtener más información y ejemplos sobre cómo usar `[!UICONTROL registerExtension]`, consulte la página [Extensiones atjs de Adobe Experience Cloud Target](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) en GitHub.

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
