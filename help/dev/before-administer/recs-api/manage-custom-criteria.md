---
title: Cómo administrar los criterios personalizados
description: Pasos necesarios para utilizar las API de Adobe Target para administrar, crear, enumerar, editar, obtener y eliminar criterios de Recommendations de Adobe Target.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 51a67a49-a92d-4377-9a9f-27116e011ab1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 1%

---

# Administrar criterios personalizados

A veces, los algoritmos proporcionados por Recommendations no pueden mostrar elementos concretos que desea promocionar. En tal situación, los criterios personalizados proporcionan una forma de proporcionar un conjunto específico de elementos recomendados para un elemento o categoría clave determinada.

Para crear criterios personalizados, defina e importe la asignación deseada entre el elemento o la categoría clave y los elementos recomendados. Este proceso se describe en la [documentación de criterios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html). Como se indica en esa documentación, puede crear, editar y eliminar criterios personalizados a través de la interfaz de usuario (IU) de Target. Sin embargo, Target también proporciona un conjunto de API de criterios personalizados que permiten una administración más detallada de los criterios personalizados.

>[!WARNING]
>
>Para los criterios personalizados, realice todas las acciones (crear, editar, eliminar) para un criterio personalizado determinado mediante las API o, de lo contrario, realice todas las acciones (crear, editar, eliminar) mediante la IU. La administración de los criterios personalizados mediante una combinación de la interfaz de usuario y la API puede generar información conflictiva o resultados inesperados. Por ejemplo, al crear un criterio personalizado en la interfaz de usuario y, a continuación, editarlo mediante API, no se reflejarán las actualizaciones en la interfaz de usuario, aunque se actualizará en el servidor, tal y como puede verse mediante la API.

## Crear criterios personalizados

Para crear criterios personalizados con [Crear API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom), la sintaxis es:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Los criterios personalizados creados con la API Crear criterio personalizado, tal como se describe en este ejercicio, aparecerán en la interfaz de usuario, donde persistirán. No podrá editarlos ni eliminarlos de la interfaz de usuario. Puede editarlos o eliminarlos **mediante API**, pero de cualquier forma, seguirán apareciendo en la interfaz de usuario de Target. Para mantener la opción de editar o eliminar de la interfaz de usuario, cree los criterios personalizados con la interfaz de usuario de [la documentación](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html), en lugar de usar la API Crear criterio personalizado.

Solo continúe con los siguientes pasos después de haber leído la advertencia anterior y de sentirse cómodo con la creación de nuevos criterios personalizados que no se puedan eliminar posteriormente de la interfaz de usuario.

1. Verificar `TENANT_ID` y `API_KEY` para **[!UICONTROL Crear criterios personalizados]** haga referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para compararla.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

1. Añada su **Cuerpo** as **crudo** JSON que define la ubicación del archivo CSV de criterios personalizados. Utilice el ejemplo proporcionado en la variable [Crear API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) documentación como plantilla, proporcionando su `environmentId` y otros valores según sea necesario. Para este ejemplo, utilizamos LAST_PURCHASED como clave.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

1. Envíe la solicitud y observe la respuesta, que contiene los detalles de los criterios personalizados que acaba de crear.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

1. Para comprobar que se ha creado su criterio personalizado, vaya a Adobe Target a **[!UICONTROL Recommendations > Criterios]** y busque los criterios por nombre, o use el **[!UICONTROL API de lista de criterios personalizados]** en el paso siguiente.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

En este caso, se produce un error. Vamos a investigar el error examinando más de cerca los criterios personalizados, utilizando el **[!UICONTROL API de lista de criterios personalizados]**.

## Enumerar criterios personalizados

Para recuperar una lista de todos los criterios personalizados junto con los detalles de cada uno, utilice el [API de lista de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). La sintaxis es:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Verificar `TENANT_ID` y `API_KEY` como antes y envíe la solicitud. En la respuesta, observe el ID de criterios personalizados, así como los detalles relativos al mensaje de error anotado anteriormente.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

En este caso, el error se produjo porque la información del servidor es incorrecta, lo que significa que Target no puede acceder al archivo CSV que contiene la definición de criterios personalizados. Vamos a editar los criterios personalizados para corregir esto.

## Editar criterios personalizados

Para cambiar los detalles de una definición de criterio personalizada, utilice la variable [Editar API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom). La sintaxis es:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verificar `TENANT_ID` y `API_KEY`, como antes.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Especifique el ID de criterio de los criterios personalizados (únicos) que desea editar.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. En el cuerpo, proporcione el JSON actualizado con la información correcta del servidor. (Para este paso, especifique el acceso FTP a un servidor al que pueda acceder).
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Envíe la solicitud y anote la respuesta.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Vamos a verificar el éxito de los criterios personalizados actualizados utilizando **[!UICONTROL Obtener API de criterios personalizados]**.

## Obtener criterios personalizados

Para ver los detalles de criterios personalizados de un criterio personalizado específico, use [Obtener API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). La sintaxis es:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique el ID de criterio de los criterios personalizados cuyos detalles desee obtener. Envíe la solicitud y revise la respuesta.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Verifique si se ha realizado correctamente. (En nuestro caso, compruebe que no haya más errores de FTP).
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Opcional) Compruebe que la actualización se refleja con precisión en la interfaz de usuario.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Eliminar criterios personalizados

Con el ID de criterios mencionado anteriormente, elimine los criterios personalizados con el [Eliminar API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom). La sintaxis es:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique el ID de criterio de los criterios personalizados (únicos) que desea eliminar. Haga clic en **[!UICONTROL Enviar]**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Compruebe que los criterios se han eliminado utilizando Obtener criterios personalizados.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
En este caso, el error 404 esperado indica que no se pueden encontrar los criterios eliminados.

>[!NOTE]
>
>Como recordatorio, los criterios no se eliminarán de la IU de Target aunque se hayan eliminado, ya que se crearon con la API Crear criterio personalizado.

¡Felicidades! Ahora puede crear, mostrar en lista, editar, eliminar y obtener detalles sobre criterios personalizados con la API de Recommendations. En la siguiente sección, utilice la API de envío de Target para recuperar recomendaciones.

&lt;!— [Siguiente: &quot;Buscar Recommendations con la API de envío del lado del servidor&quot; >](fetch-recs-server-side-delivery-api.md) —>
