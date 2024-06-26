---
title: Recuperación de perfiles
description: Aprenda a utilizar las API de perfil de Adobe Target para recuperar datos de visitantes que utilizar en [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Recuperación de perfiles

A [!DNL Target] El perfil de se puede recuperar de tres formas: mediante una `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` o `thirdPartyId`.

## Uso de un [!DNL Experience Cloud Visitor ID] (ECID)

Puede obtener un perfil basado en el `ECID`. El método HTTP debe ser GET.

La dirección URL es similar al siguiente ejemplo:

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

Reemplazar `<clientCode>` con su [!DNL Target] [!UICONTROL Código de cliente] y `<ECID>` con su [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## Uso de un tntid

[!DNL Target] asigna automáticamente un `tntid` para cada solicitud.

El siguiente ejemplo muestra el formato de solicitud para recuperar un perfil mediante una `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Reemplazar `<your-client-code>` y `your-tnt-id` y activa una solicitud de GET. Esta es una llamada de captura de perfil de ejemplo que utiliza un `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Uso de thirdPartyId

[!DNL Adobe Target] Los perfiles de se pueden aumentar con su propio identificador (por ejemplo: CRM id, `uuid`, número de abono, etc.).

Consulte [Actualización de perfiles](/help/dev/administer/profile-api/profile-api-overview.md) para obtener información sobre cómo adjuntar un `thirdPartyId` a su perfil.

El siguiente ejemplo muestra el formato de solicitud para recuperar un perfil mediante una `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Reemplazar `<your-client-code>` y `your-thirdpartyid` y activa una solicitud de GET. Esta es una llamada de captura de perfil de ejemplo que utiliza un [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Cuando se realice esta llamada, [!DNL Target] intenta localizar el perfil primero en el clúster indicado en la solicitud de edge, o donde quiera que esté ubicado el perfil, y devolver el contenido. El contenido del perfil se devuelve en formato JSON.

## Autenticación

El [!DNL Target Profile API] se puede proteger activando la autenticación desde el [!DNL Target] Interfaz de usuario como se describe aquí. Una vez activada la autenticación, todas las solicitudes de API de perfil deben tener el token de autenticación de perfil establecido en los encabezados de solicitud. El propio token se puede generar utilizando la variable [!DNL Target] para usar los pasos explicados anteriormente en la [Token de autenticación de perfil](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} sección.

## Medición

Estas llamadas no se contabilizan en sus llamadas de mbox.

## Control de errores

En el caso de una llamada a `/thirdPartyId` con un no válido o un caducado `thirdPartyId` especificado:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Si el perfil no se encuentra o ha caducado:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
