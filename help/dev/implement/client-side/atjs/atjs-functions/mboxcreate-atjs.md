---
keywords: mboxCreate, mboxcreate, mbox create, at.js, funciones, función
description: Utilice la función [!UICONTROL mboxCreate()] para que la biblioteca JavaScript  [!DNL Adobe Target] at.js aplique ofertas al DIV más cercano con el nombre de clase mboxDefault. (at.js 1.x)
title: ¿Cómo se usa la función [!UICONTROL mboxCreate()]?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
TQID: https://experienceleague.adobe.com/hCEKL9RPtqIbMVEouzObjU6dc7TKl1hBtKZ1jEdicRE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a1af9d2c909d9b3d506dd4875d1bd75149dbf636
workflow-type: tm+mt
source-wordcount: 216
ht-degree: 40%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

Ejecuta una solicitud y aplica la oferta al DIV más cercano con nombre de clase mboxDefault.

>[!NOTE]
>
>Esta función solo está disponible para las versiones 1.0 *de at.js.* Esta función quedó obsoleta con el lanzamiento de at.js 2.x. Esta función devuelve el contenido predeterminado si se utiliza con at.js 2.x.

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



