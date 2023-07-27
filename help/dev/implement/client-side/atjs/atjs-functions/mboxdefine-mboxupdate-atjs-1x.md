---
keywords: mboxDefine, mboxdefine, mbox define, mboxUpdate, mboxupdate, actualización de mbox, at.js, funciones, función, mboxDefine0
description: Utilice el [!UICONTROL mboxDefine()] y [!UICONTROL mboxUpdate()] funciones para el [!DNL Adobe Target] Biblioteca JavaScript de at.js para definir o actualizar un mbox. (at.js 1.x)
title: ¿Cómo utilizo el [!UICONTROL mboxDefine()] Y [!UICONTROL mboxUpdate()] ¿Funciones?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 52%

---

# [!UICONTROL mboxDefine()] y [!UICONTROL mboxUpdate()] - at.js 1.x

Definición y actualización de un mbox en [!DNL Adobe Target].

>[!NOTE]
>
>Estas funciones están disponibles para las versiones 1 de at.js.Solamente *x*. Estas funciones quedaron obsoletas con el lanzamiento de at.js 2.*x*. Estas funciones devuelven contenido predeterminado si se utilizan con at.js 2.*x*.

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
