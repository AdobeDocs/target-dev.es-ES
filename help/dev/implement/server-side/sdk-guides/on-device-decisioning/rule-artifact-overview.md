---
title: Comprender el artefacto de la regla de toma de decisiones en el dispositivo
description: Aprenda a utilizar el artefacto de regla, que es una representación JSON de sus actividades  [!DNL Adobe Target] [!UICONTROL on-device decisioning].
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Resumen de artefactos de regla

El artefacto de regla es una representación JSON de sus actividades [!DNL Adobe Target] [!UICONTROL on-device decisioning]. Se genera por [!DNL Adobe Target] y se propaga a la CDN de Akamai para garantizar que haya un artefacto de regla disponible lo más cerca posible de los usuarios finales. Contiene metadatos que garantizan la ejecución y el envío precisos de sus actividades, a la vez que permiten el análisis en tiempo real mediante el seguimiento de eventos. Los SDK de [!DNL Adobe Target] se pueden configurar de forma que permitan la administración automática del artefacto de regla, mediante el cual se puede descargar o actualizar según un intervalo de tiempo especificado por el usuario. Además, también puede mantener su propia copia local del artefacto de regla usando un sistema de almacenamiento en caché de memoria distribuida como [Memcached](https://memcached.org/) para inicializar el SDK [!DNL Adobe Target], de modo que los servidores sin estado puedan servir solicitudes inmediatamente. Para obtener más información sobre estas opciones, consulte las siguientes guías:

* [Descargar, almacenar y actualizar el artefacto de regla automáticamente mediante el SDK  [!DNL Adobe Target] SDK](rule-artifact-sdk.md)
* [Descarga, almacenamiento y actualización del artefacto de regla a través de la carga útil JSON](rule-artifact-json.md)

## Ejemplo de artefacto de regla

Haga clic aquí para ver un ejemplo del [artefacto de regla](rule-artifact-example.md).

## Visualización del artefacto de regla para el cliente

Al habilitar los seguimientos, se generará información adicional de [!DNL Adobe Target] con respecto al artefacto de regla, específicamente la dirección URL.

1. Vaya a la IU de Target.

   &lt;!— Insert image-target-ui-1.png —>
   ![imagen alt](assets/asset-rule-artifact-1.png)

1. Vaya a **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** y haga clic en **[!UICONTROL Generate New Authorization Token]**.

   &lt;!— Insert image-target-ui-2.png —>
   ![imagen alt](assets/asset-rule-artifact-2.png)

1. Copie el token de autorización recién generado en el portapapeles y agréguelo a la solicitud de Target.

   ```javascript {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: '88f1a924-6bc5-4836-8560-2f9c86aeb36b'
     },
     execute: {
       mboxes: [{
         address: getAddress(req),
         name: "node-sdk-mbox"
       }]
   }};
   ```

1. Obtenga el seguimiento de destino a través del terminal para ver los detalles del artefacto. Se puede acceder a la dirección URL a través de la variable `artifactLocation`.

   ```
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.bin",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
        "clientCode": "your-client-code",
      "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```
