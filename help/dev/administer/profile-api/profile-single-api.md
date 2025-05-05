---
title: API de actualización de perfil único de Adobe Target
description: Aprenda a usar [!DNL Adobe Target] [!UICONTROL Single Profile Update API] para enviar los datos de perfil de un solo visitante a [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# [!DNL Adobe Target Single Profile Update API]

El [!DNL Adobe Target] [!UICONTROL Single Profile Update API] le permite enviar una actualización de perfil para un solo usuario. [!UICONTROL Single Profile Update API] es casi idéntico a [!UICONTROL Bulk Profile Update API], pero se actualiza un perfil de visitante a la vez, en línea con la llamada de API en lugar de con un archivo .cvs.

El [!UICONTROL Single Profile Update API] y se usan generalmente cuando se debe producir una actualización en relación con una transacción que se produce en un canal que no ha implementado [!DNL Target]. Por ejemplo, desea actualizar el perfil de un único visitante que realiza alguna acción sin conexión. Las acciones pueden incluir llegar a un centro de llamadas, financiar un préstamo, usar una tarjeta de fidelidad en una tienda, acceder a un quiosco, etc.

Los beneficios de [!UICONTROL Single Profile Update API] incluyen:

* No hay ningún límite en la cantidad de atributos del perfil.
* Los atributos de perfil enviados a través del sitio se pueden actualizar mediante la API y viceversa.

## Advertencias 

* [!UICONTROL Single Profile Update API] se limita a realizar 1 millón de actualizaciones en cualquier período de 24 horas consecutivo.
* Las actualizaciones suelen producirse en menos de una hora, pero pueden tardar hasta 24 horas en reflejarse.

  Si debe enviar más actualizaciones o requerir que las actualizaciones se procesen en lapsos de tiempo más cortos, considere la posibilidad de enviar actualizaciones de perfil transaccionales a través de la actualización del lado del cliente (opción preferida) o a través de la [API de entrega](/help/dev/implement/delivery-api/overview.md) del lado del servidor [!DNL Adobe Target].

* [!UICONTROL Single Profile Update API] es una API de servidor a servidor y no está diseñada para funcionar dentro de una página web. Para actualizar un perfil de visitante desde tu página web, puedes usar la función [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) o la [API de entrega](/help/dev/implement/delivery-api/overview.md).

## Formato

Especifique los parámetros de perfil en el formato `profile.paramName=value`.

Para actualizar el perfil de un(a) `pcId`, use:

``` ```
https://&lt;your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``` ```

Para actualizar el perfil de un(a) `mbox3rdPartyId`, use:

``` ```
shell http://&lt;your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``` ```

[!UICONTROL Single Profile Update API] es solo para actualizaciones. Si no se encuentra nada, no se crea ningún perfil.

## Notas

* Los parámetros y valores deben estar codificados en URL mediante UTF-8.
* El formato del parámetro es `profile.paramName`.
* No todos los valores de parámetro deben existir para todos los pcIds y mbox3rdPartyIds.
* Los parámetros y valores distinguen entre mayúsculas y minúsculas.
* Se admiten tanto el GET como el POST.
* Las limitaciones de tamaño actuales para el límite son de 8 KB para el GET y de 60 KB para el POST.

## Respuesta

Una respuesta de ejemplo para las solicitudes anteriores tiene este aspecto:

`trueRequest successfully submitted`

Esta respuesta indica que la respuesta se ha enviado y se procesará pronto.
