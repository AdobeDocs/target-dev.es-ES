---
keywords: implementar, implementar, configurar, configurar atributos de perfil de secuencia de comandos
description: Obtener datos en  [!DNL Target] mediante atributos de perfil de script.
title: ¿Cómo obtengo datos en  [!DNL Target] usando atributos de perfil de script?
feature: Implementation
exl-id: ba11f1de-e68b-4505-8e3e-cd4d46ef59a2
TQID: https://experienceleague.adobe.com/bRsl4ipgw0OeuVD0d69wmnHmrVvcGt9o0KmkhrEECZQ
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 292
ht-degree: 71%

---

# Atributos de perfil en script

Los atributos de perfil de script son pares de nombre/valor definidos en la solución [!DNL Adobe Target]. El valor se determina a partir de la ejecución de un fragmento JavaScript en el servidor de Target por llamada de servidor.

Los usuarios escriben pequeños fragmentos de código que se ejecutan mediante una llamada de mbox y antes de que el visitante se evalúe por audiencia y abono a la actividad.

## Formato

Los atributos de perfil en script se crean en la sección Audiencias de Target. Cualquier nombre de atributo es válido y el valor es el resultado de una función de JavaScript escrita por el usuario [!DNL Target]. Al nombre de atributo se le añade automáticamente el prefijo “user. &quot; en [!DNL Target] para distinguirlos de los atributos de perfil en página.

El fragmento de código se escribe en lenguaje Rhino JS y puede hacer referencia a tokens y a otros valores.

## Casos de uso de ejemplo

* **Abandono del carrito**: cuando el visitante llega hasta el carrito de compra, el script de perfil se establece en 1. Si el visitante hace una conversión, se restablece en 0. Si el valor es igual a 1, el visitante tiene un artículo en el carrito.
* **Recuento de visitas**: en cada nueva visita el recuento aumenta 1 punto para hacer el seguimiento de la frecuencia con la que un visitante regresa al sitio.

## Ventajas del método

No requiere actualizaciones de código.

Se ejecuta antes de la toma de decisiones de audiencia y abono a la actividad, por lo que estos atributos de script de perfil pueden afectar al abono en una sola llamada de servidor.

Puede ser muy potente. Se pueden ejecutar hasta 2000 instrucciones por script.

## Advertencias

Se requieren conocimientos de JavaScript.

La orden de ejecución de los scripts de perfil no está garantizada, por lo que no pueden depender los unos en los otros.

La depuración puede ser difícil.

## Ejemplos de código

Los scripts de perfil son bastante flexibles:

```
user.purchase_recency: var dayInMillis = 3600 * 24 * 1000; if (mbox.name == 'orderThankyouPage') {  user.setLocal('lastPurchaseTime', new Date().getTime()); } var lastPurchaseTime = user.getLocal('lastPurchaseTime'); if (lastPurchaseTime) {  return ((new Date()).getTime()-lastPurchaseTime)/dayInMillis; }
```

### Vínculos a información relevante

[Atributos de script de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html#concept_8C07AEAB0A144FECA8B4FEB091AED4D2)
