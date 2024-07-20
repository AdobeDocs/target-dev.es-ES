---
title: Recuperación de perfiles
description: Aprenda a utilizar las API de perfil de Adobe Target para recuperar datos de visitantes que se usarán en  [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Recuperación de perfiles

Un perfil [!DNL Target] se puede obtener de tres maneras: usando un `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` o `thirdPartyId`.

## Usando un [!DNL Experience Cloud Visitor ID] (ECID)

Puede obtener un perfil basado en `ECID`. El método HTTP debe ser GET.

La dirección URL es similar al siguiente ejemplo:

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

Reemplazar `<clientCode>` por [!DNL Target] [!UICONTROL Client Code] y `<ECID>` por [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## Uso de un tntid

[!DNL Target] asigna automáticamente un(a) `tntid` para cada solicitud.

El ejemplo siguiente muestra el formato de solicitud para recuperar un perfil mediante un `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Reemplace `<your-client-code>` y `your-tnt-id` y active una solicitud de GET. Esta es una llamada de captura de perfil de ejemplo que usa un `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Uso de thirdPartyId

[!DNL Adobe Target] perfiles se pueden aumentar con su propio identificador (por ejemplo: ID de CRM, `uuid`, número de pertenencia, etc.).

Consulta [Actualizar perfiles](/help/dev/administer/profile-api/profile-api-overview.md) para saber cómo adjuntar un(a) `thirdPartyId` a tu perfil.

El ejemplo siguiente muestra el formato de solicitud para recuperar un perfil mediante un `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Reemplace `<your-client-code>` y `your-thirdpartyid` y active una solicitud de GET. Esta es una llamada de captura de perfil de ejemplo que usa un [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Cuando se realiza esta llamada, [!DNL Target] intenta ubicar el perfil primero en el clúster indicado en la solicitud de Edge, o en cualquier lugar donde se encuentre el perfil y devuelve el contenido. El contenido del perfil se devuelve en formato JSON.

## Autenticación

[!DNL Target Profile API] se puede proteger activando la autenticación desde la interfaz de usuario de [!DNL Target] como se describe aquí. Una vez activada la autenticación, todas las solicitudes de API de perfil deben tener el token de autenticación de perfil establecido en los encabezados de solicitud. El token en sí se puede generar usando la interfaz de usuario [!DNL Target] o los pasos explicados anteriormente en la sección [Token de autenticación de perfil](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank}.

## Medición

Estas llamadas no se contabilizan en sus llamadas de mbox.

## Control de errores

En el caso de una llamada a `/thirdPartyId` con un `thirdPartyId` no válido o caducado especificado:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Si el perfil no se encuentra o ha caducado:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
