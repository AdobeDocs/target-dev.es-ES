---
title: API de actualización de perfil único de Adobe Target
description: Aprenda a usar la  [!DNL Adobe Target] [!UICONTROL API de actualización de perfil único] para enviar los datos de perfil de un solo visitante a [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
TQID: https://experienceleague.adobe.com/HEjGkrgixufe9wQvaPAljSlZRSaF-idgwKYWs3cuoJ0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 6fac79420aef0a73c109b2c19f363266c1f8027a
workflow-type: tm+mt
source-wordcount: 396
ht-degree: 4%

---

# [!DNL Adobe Target Single Profile Update API]

La [!DNL Adobe Target] [!UICONTROL API de actualización de perfil único] le permite enviar una actualización de perfil para un solo usuario. La [!UICONTROL API de actualización de perfil único] es casi idéntica a la [!UICONTROL API de actualización de perfil en lote], pero se actualiza un perfil de visitante a la vez, en línea con la llamada de API en lugar de con un archivo .cvs.

La API [!UICONTROL Actualización de perfil único] y se suelen usar cuando se debe producir una actualización en relación con una transacción que se produce en un canal que no ha implementado [!DNL Target]. Por ejemplo, desea actualizar el perfil de un único visitante que realiza alguna acción sin conexión. Las acciones pueden incluir llegar a un centro de llamadas, financiar un préstamo, usar una tarjeta de fidelidad en una tienda, acceder a un quiosco, etc.

Los beneficios de la [!UICONTROL API de actualización de perfil único] incluyen:

* No hay ningún límite en la cantidad de atributos del perfil.
* Los atributos de perfil enviados a través del sitio se pueden actualizar mediante la API y viceversa.

## Advertencias

* La [!UICONTROL API de actualización de perfil único] se limita a realizar 1 millón de actualizaciones en cualquier período de 24 horas.
* Las actualizaciones suelen producirse en menos de una hora, pero pueden tardar hasta 24 horas en reflejarse.

  Si debe enviar más actualizaciones o requerir que las actualizaciones se procesen en lapsos de tiempo más cortos, considere la posibilidad de enviar actualizaciones de perfil transaccionales a través de la actualización del lado del cliente (opción preferida) o a través de la [API de entrega](/help/dev/implement/delivery-api/overview.md) del lado del servidor [!DNL Adobe Target].

* La [!UICONTROL API de actualización de perfil único] es una API de servidor a servidor y no está diseñada para funcionar dentro de una página web. Para actualizar un perfil de visitante desde tu página web, puedes usar la función [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) o la [API de entrega](/help/dev/implement/delivery-api/overview.md).

## Formato

Especifique los parámetros de perfil en el formato `profile.paramName=value`.

Para actualizar el perfil de un(a) `pcId`, use:

```
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
```

Para actualizar el perfil de un(a) `mbox3rdPartyId`, use:

```
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
```

La [!UICONTROL API de actualización de perfil único] es solo para actualizaciones. Si no se encuentra nada, no se crea ningún perfil.

## Notas

* Los parámetros y valores deben estar codificados en URL mediante UTF-8.
* El formato del parámetro es `profile.paramName`.
* No todos los valores de parámetro deben existir para todos los pcIds y mbox3rdPartyIds.
* Los parámetros y valores distinguen entre mayúsculas y minúsculas.
* Se admiten GET y POST.
* Las limitaciones de tamaño actuales para limit son de 8 KB para GET y 60 KB para POST.

## Respuesta

Una respuesta de ejemplo para las solicitudes anteriores tiene este aspecto:

`trueRequest successfully submitted`

Esta respuesta indica que la respuesta se ha enviado y se procesará pronto.
