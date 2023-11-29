---
keywords: implementación, implementación, configuración, configuración, actualización de perfil único
description: Introducción de datos en [!DNL Target] uso de la API de actualización de perfil único.
title: ¿Cómo puedo obtener datos en? [!DNL Target] ¿Utiliza la API de actualización de perfil único?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 734bda64915a08f2edba37cbbb66b2de581c2237
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 15%

---

# API de actualización de perfil único

Casi idéntico al [!UICONTROL API de actualización de perfil en lote] in [!DNL Adobe Target], pero se actualiza un perfil de visitante a la vez, en línea en la llamada de API en lugar de con un archivo .csv.

## Formato

El visitante debe identificarse mediante la variable [!DNL Target] `mboxPC` valor o `mbox3rdPartyId` valor. El [!UICONTROL ID de Experience Cloud] (ECID) no es compatible.

## Casos de uso de ejemplo

Desea actualizar el perfil de un único visitante que realiza alguna acción sin conexión. Las acciones pueden incluir llegar a un centro de llamadas, financiar un préstamo, usar una tarjeta de fidelidad en una tienda, acceder a un quiosco, etc.

## Ventajas del método

* No hay ningún límite en la cantidad de atributos del perfil.*
* Los atributos de perfil enviados a través del sitio se pueden actualizar mediante la API y viceversa.

## Advertencias 

* Límite de 1 000 000 (1 millón) de llamadas a la API por período de 24 horas.
* Solo se actualiza el perfil. No se puede crear un perfil para un usuario potencial [!DNL Target] aún no lo ha visto.
* Las actualizaciones suelen producirse en menos de una hora, pero pueden tardar hasta 24 horas en reflejarse.

## Ejemplos de código

Se admiten GET y POST. 

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## Recursos

* [Actualización de perfiles](https://developers.adobetarget.com/api/#updating-profiles)
