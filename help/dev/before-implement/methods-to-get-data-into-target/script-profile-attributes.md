---
keywords: implementar, implementar, configurar, configurar atributos de perfil de secuencia de comandos
description: Obtener datos en  [!DNL Target] mediante atributos de perfil de script.
title: ¿Cómo obtengo datos en  [!DNL Target] usando atributos de perfil de script?
feature: Implementation
exl-id: ba11f1de-e68b-4505-8e3e-cd4d46ef59a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 74%

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
