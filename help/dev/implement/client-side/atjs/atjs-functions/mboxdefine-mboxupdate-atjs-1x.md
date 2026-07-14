---
keywords: mboxDefine, mboxdefine, mbox define, mboxUpdate, mboxupdate, actualización de mbox, at.js, funciones, función, mboxDefine0
description: Use las funciones [!UICONTROL mboxDefine()] y [!UICONTROL mboxUpdate()] para la biblioteca JavaScript  [!DNL Adobe Target] at.js para definir o actualizar un mbox. (at.js 1.x)
title: ¿Cómo utilizo las funciones [!UICONTROL mboxDefine()] y [!UICONTROL mboxUpdate()]?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
TQID: https://experienceleague.adobe.com/Fn-Ej8jk2AMEn79tOtRoP9GQc36Ugy6FtXyn6x7jkmA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a1af9d2c909d9b3d506dd4875d1bd75149dbf636
workflow-type: tm+mt
source-wordcount: 208
ht-degree: 46%

---

# [!UICONTROL mboxDefine()] y [!UICONTROL mboxUpdate()] - at.js 1.x

Defina y actualice un mbox en [!DNL Adobe Target].

>[!NOTE]
>
>Estas funciones solo están disponibles para las versiones 1.*x* de at.js. Estas funciones quedaron obsoletas con el lanzamiento de at.js 2.*x*. Estas funciones devuelven contenido predeterminado si se utilizan con at.js 2.*x*.

`[!UICONTROL mboxDefine()]` y `[!UICONTROL mboxCreate()]` están vinculados a elementos HTML DIV donde la oferta debería mostrarse. Estos elementos DIV HTML deberían tener la clase `mboxDefault`. Si los elementos HTML no tendrán esta clase adjunta, usted podría ver un notable parpadeo.

## mboxDefine

Crea una asignación interna entre un nombre de mbox y nodeId, pero no excluye la solicitud. Se usa en conjunto con `[!UICONTROL mboxUpdate()]`. Integrado en at.js principalmente para facilitar la transición de mbox.js (ahora obsoleto) a at.js.

## mboxUpdate

Ejecuta la solicitud y aplica la oferta al elemento identificado por el `nodeId` en `mboxDefine()`. También se puede usar para actualizar un mbox iniciado por `[!UICONTROL mboxCreate]`. Integrado en at.js principalmente para facilitar la transición de mbox.js (ahora obsoleto) a at.js. `mboxDefine()`/ `mboxUpdate()` se puede reemplazar mediante [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) y [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) utilizando el selector de opción.

## Ejemplo

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```



