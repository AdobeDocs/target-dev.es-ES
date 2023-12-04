---
title: API de perfiles de Adobe Target
description: Aprenda a utilizar las API de perfil de Adobe Target para enviar datos sobre visitantes a [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: 289299a52e5611c0da341f313aa4a447fcf3666a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] descripción general

[!DNL Adobe Target] crea y mantiene un perfil para cada usuario individual. Este perfil se almacena en el [!DNL Target] edge cluster y se actualiza en tiempo real después de cada visita.

## Perfiles [!DNL Postman] colección

[!DNL Postman] es una aplicación que facilita la activación de llamadas de API. Esta [!DNL Postman] La colección contiene todas las [!DNL Profile API] llamadas. Clic [Ejecutar en Postman](https://www.getpostman.com/collections/ec7376f9028977ccaa99){target=_blank} para importar la colección de API de perfil.

## Documentación de API de perfiles heredados.

La documentación heredada de la API de perfiles se puede encontrar aquí: [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}

## Estructura de un [!DNL Target] perfil

Un perfil de Target consta de los siguientes objetos:

| Objeto | Detalles |
| --- | --- |
| `clientcode` | El [!DNL Target] código de cliente al que está asociado el perfil. |
| `visitorId` | El identificador del perfil. Puede ser un `tntid`, `thirdpartyid`, o `marketingcloudvisitorid`. |
| `modifiedAt` | La marca de tiempo de la última actualización del perfil. |
| `profileAttributes` | Lista de todos los atributos de perfil almacenados como pares clave-valor en ese perfil individual. |

### Estructura del perfil de muestra

```
{
    "client": "<your-tenant-name>",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}
```
