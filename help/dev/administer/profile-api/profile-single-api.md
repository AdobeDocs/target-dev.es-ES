---
title: API de actualización de perfil único de Adobe Target
description: Aprenda a utilizar [!DNL Adobe Target] [!UICONTROL API de actualización de perfil único] para enviar los datos de perfil de un solo visitante a [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 81bff85a9d1fe28ca267c471a470da95568fd06d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# [!DNL Adobe Target Single Profile Update API]

El [!DNL Adobe Target] [!UICONTROL API de actualización de perfil único] permite enviar una actualización de perfil para un solo usuario. El [!UICONTROL API de actualización de perfil único] es casi idéntico al de [!UICONTROL API de actualización de perfil en lote], pero se actualiza un perfil de visitante a la vez, en línea con la llamada de API en lugar de con un archivo .cvs.

El [!UICONTROL API de actualización de perfil único] y se utiliza generalmente cuando debe producirse una actualización en relación con una transacción que se produce en un canal que no se ha implementado [!DNL Target]. Por ejemplo, desea actualizar el perfil de un único visitante que realiza alguna acción sin conexión. Las acciones pueden incluir llegar a un centro de llamadas, financiar un préstamo, usar una tarjeta de fidelidad en una tienda, acceder a un quiosco, etc.

Ventajas de la [!UICONTROL API de actualización de perfil único] incluir:

* No hay ningún límite en la cantidad de atributos del perfil.
* Los atributos de perfil enviados a través del sitio se pueden actualizar mediante la API y viceversa.

## Advertencias 

* El [!UICONTROL API de actualización de perfil único] se limita a realizar 1 millón de actualizaciones en cualquier periodo móvil de 24 horas.
* Las actualizaciones suelen producirse en menos de una hora, pero pueden tardar hasta 24 horas en reflejarse.

  Si debe enviar más actualizaciones o requerir que las actualizaciones se procesen en intervalos de tiempo más cortos, considere la posibilidad de enviar actualizaciones de perfil transaccionales a través de la actualización del lado del cliente (opción preferida) o a través de la variable [!DNL Adobe Target] del lado del servidor [API de envío](/help/dev/implement/delivery-api/overview.md).

## Formato

Especifique los parámetros de perfil en el formato `profile.paramName=value`.

Para actualizar el perfil de un `pcId`, use:

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

Para actualizar el perfil de un `mbox3rdPartyId`, use:

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

El [!UICONTROL API de actualización de perfil único] es solo para actualizaciones. Si no se encuentra nada, no se crea ningún perfil.

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