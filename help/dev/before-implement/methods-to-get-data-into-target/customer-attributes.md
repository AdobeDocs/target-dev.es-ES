---
keywords: implementar, implementar, configurar, configurar, atributos del cliente
description: Obtener datos en  [!DNL Target] usando atributos del cliente.
title: ¿Cómo puedo obtener datos en  [!DNL Target] usando los atributos del cliente?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 14%

---

# Atributos del cliente

Los atributos del cliente le permiten cargar datos de perfil del visitante a [!DNL Adobe Experience Cloud] a través de FTP. Una vez cargados, use los datos en [!DNL Adobe Analytics] y [!DNL Adobe Target].

Los clientes de Target Standard pueden aplicar cinco atributos, [!DNL Target Premium] clientes pueden aplicar 200 atributos.

## Formato

Se ha cargado un archivo .csv con [!DNL Experience Cloud] ID (ECID) y pares de nombre/valor de atributo a través de FTP o manualmente en la interfaz de usuario de Experience Cloud.

## Casos de uso de ejemplo

Su CRM u otro sistema interno almacena información valiosa que desea compartir con [!DNL Adobe Experience Cloud], incluidos [!DNL Target] y [!DNL Analytics].

## Ventajas del método

Al cargar los datos del cliente, se crea una entrada de perfil para ese visitante en Target, aunque [!DNL Target] aún no haya visto al visitante.

Los mismos datos están disponibles automáticamente en [!DNL Target] y [!DNL Analytics].

FTP puede ser un método de implementación más sencillo que la API.

## Advertencias

Los clientes de Target Standard pueden aplicar cinco atributos, [!DNL Target Premium] clientes pueden aplicar 200 atributos

Los valores solo se pueden actualizar a través de Atributos del cliente, no en la página.

Se requiere la implementación del Experience Cloud ID (ECID).

## Ejemplos de código

Encontrará información detallada en [Crear un origen de atributos del cliente y cargar el archivo de datos](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).

### Vínculos a información relevante

[Cree un origen de atributo de cliente y cargue el archivo de datos](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).
