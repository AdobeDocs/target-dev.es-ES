---
keywords: mboxCreate, mboxcreate, mbox create, at.js, funciones, función
description: Utilice la función [!UICONTROL mboxCreate()] de la biblioteca JavaScript  [!DNL Adobe Target] at.js para aplicar ofertas al DIV más cercano con el nombre de clase mboxDefault. (at.js 1.x)
title: ¿Cómo se utiliza la función [!UICONTROL mboxCreate()]?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 56%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

Ejecuta una solicitud y aplica la oferta al DIV más cercano con nombre de clase mboxDefault.

>[!NOTE]
>
>Esta función está disponible para las versiones 1 de at.js.Solamente *x*. Esta función quedó obsoleta con el lanzamiento de at.js 2.x. Esta función devuelve el contenido predeterminado si se utiliza con at.js 2.x.

Esta función está integrada en at.js principalmente para facilitar la transición de mbox.js (ahora obsoleto) a at.js. Una alternativa nueva a `[!UICONTROL mboxCreate()]` es `[!UICONTROL adobe.target.getOffer()]`/ `[!UICONTROL adobe.target.applyOffer()]`/ o la directiva Angular.

## Ejemplo

```javascript {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  mboxCreate('mboxName','param1=value1','param2=value2'); 
</script>
```

## Notas

`mboxCreate()` ahora usa el extremo “json” en lugar del extremo “standard” y se activa asincrónicamente. Debido a ello:

* [Depuración](/help/dev/implement/client-side/target-debugging-atjs/target-debugging-atjs.md) es algo diferente.
* Evite el código de oferta que requiere llamadas sincrónicas de bloqueo.

  Por ejemplo, las ofertas que establecen variables de JavaScript utilizadas por código de sitio u otros mboxes que vienen después en la página.

* Asegúrese de tener un `<div class="mboxDefault"></div>` antes de invocar `[!UICONTROL mboxCreate()]`, ya que at.js no lo agregará por usted.

* No se recomiendan funciones `[!UICONTROL mboxCreate()]` vacías que aparecen en la parte superior de la página como mbox global.

  El mbox global creado automáticamente en at.js es una mejor opción porque se activa desde `<head>` y puede devolver contenido más rápido.
