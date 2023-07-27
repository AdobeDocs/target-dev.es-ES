---
keywords: adobe.target.trackEvent, trackEvent, trackevent, rastrear evento, at.js, funciones, función, preventDefault, preventdefault, prevent default, adobe.target.trackEvent
description: Utilice el [!UICONTROL adobe.target.trackEvent()] para la función [!DNL Adobe Target] Biblioteca JavaScript de at.js para activar una solicitud para informar sobre las acciones del usuario, como los clics y las conversiones en el sitio.
title: ¿Cómo utilizo el [!UICONTROL adobe.target.trackEvent()] ¿Función?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 59%

---

# [!UICONTROL adobe.target.trackEvent(options)]

Esta función activa una solicitud para informar sobre las acciones de los usuarios, como clics y conversiones. No proporciona ninguna actividad en la respuesta.

Después, estas llamadas de mbox de seguimiento de eventos se pueden usar para definir métricas en las actividades. Para obtener más información, consulte [Métricas de éxito](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) y [Conversiones de seguimiento](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

He aquí los detalles de API:

| Clave | Tipo | Requerido | Descripción |
|--- |--- |--- |--- |
| mbox | Cadena | Sí | Nombre de mbox<P>**Nota**: Si un [!UICONTROL trackEvent()] se activa con un nombre de mbox que ya se ha activado en la página, el SDID de [!UICONTROL trackEvent()] se restablece y será diferente al [!DNL Target] llama a en la página. Sin embargo, al activar un [!UICONTROL trackEvent()] llamada de con un nombre de mbox diferente mantiene el [!UICONTROL trackEvent()] SDID de la llamada coherente con el [!UICONTROL Solicitud de carga de página]/[!UICONTROL triggerView()] llama a en la página. |
| selector | Cadena | No | Los selectores de CSS utilizados para encontrar los elementos HTML. Los detectores de eventos se adjuntarán a los elementos encontrados. |
| type | Cadena | No | Representa un tipo de evento registrado. Puede ser tanto eventos HTML conocidos como: click, mousedown, etc. como también eventos HTML personalizados. |
| preventDefault | Booleano | No | Indica si usar `[!UICONTROL event.preventDefault()]` en la llamada de retorno de la escucha de eventos. Toma el valor predeterminado de falso.<P>**Nota**: Solo `[!UICONTROL form[submit]]` y `a[click]` son compatibles. No se admiten otros escenarios debido a la complejidad y a la gran cantidad de escenarios por admitir. |
| params | Objeto | No | Parámetros de mbox. Un objeto de pares de clave-valor que tiene la siguiente estructura:<P>`{ "param1": "value1", "param2": "value2"}` |
| timeout | Número | No | Tiempo de espera en milisegundos.<P>Si no se especifica, se utiliza el valor predeterminado:<P>`...timeoutInSeconds: 0.15...}` |
| success | Función | No | Una función de llamada de retorno utilizada para indicar que se ha informado el evento. |
| error | Función | No | Una función de llamada de retorno utilizada para indicar que no se ha podido informar el evento. |

## Ejemplo

```javascript {line-numbers="true"}
<a href="https://asite.com">click me!</a> 
```

código javaScript plus para asignar `trackEvent`:

```javascript {line-numbers="true"}
<script> 
$('a').click(function(event){ 
  adobe.target.trackEvent({'mbox':'homePageHero'}) 
}); 
</script> 
```

O bien:

```javascript {line-numbers="true"}
adobe.target.trackEvent({ 
    "mbox": "clicked-cta", 
    "params": { 
        "param1": "value1" 
    } 
});
```

>[!WARNING]
>
>Si no se establecen los campos obligatorios, no se ejecuta ninguna solicitud y se genera un error.
