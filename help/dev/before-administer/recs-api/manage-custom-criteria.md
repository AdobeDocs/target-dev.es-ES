---
title: Cómo administrar los criterios personalizados
description: Pasos necesarios para utilizar las API de Adobe Target para administrar, crear, enumerar, editar, obtener y eliminar criterios de Recommendations de Adobe Target.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 51a67a49-a92d-4377-9a9f-27116e011ab1
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Administrar criterios personalizados

A veces, los algoritmos proporcionados por Recommendations no pueden mostrar elementos concretos que desea promocionar. En tal situación, los criterios personalizados proporcionan una forma de proporcionar un conjunto específico de elementos recomendados para un elemento o categoría clave determinada.

Para crear criterios personalizados, defina e importe la asignación deseada entre el elemento o la categoría clave y los elementos recomendados. Este proceso se describe en la [documentación de criterios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html). Como se indica en esa documentación, puede crear, editar y eliminar criterios personalizados a través de la interfaz de usuario (IU) de Target. Sin embargo, Target también proporciona un conjunto de API de criterios personalizados que permiten una administración más detallada de los criterios personalizados.

>[!WARNING]
>
>Para los criterios personalizados, realice todas las acciones (crear, editar, eliminar) para un criterio personalizado determinado mediante las API o, de lo contrario, realice todas las acciones (crear, editar, eliminar) mediante la IU. La administración de los criterios personalizados mediante una combinación de la interfaz de usuario y la API puede generar información conflictiva o resultados inesperados. Por ejemplo, al crear un criterio personalizado en la interfaz de usuario y, a continuación, editarlo mediante API, no se reflejarán las actualizaciones en la interfaz de usuario, aunque se actualizará en el servidor, tal y como puede verse mediante la API.

## Crear criterios personalizados

Para crear criterios personalizados con la API [Crear criterios personalizados](https://developer.adobe.com/target/administer/recommendations-api/#operation/createCriteriaCustom), la sintaxis es:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Los criterios personalizados creados con la API Crear criterio personalizado, tal como se describe en este ejercicio, aparecerán en la interfaz de usuario, donde persistirán. No podrá editarlos ni eliminarlos de la interfaz de usuario. Puede editarlos o eliminarlos **mediante la API**, pero de cualquier forma seguirán apareciendo en la interfaz de usuario de Target. Para mantener la opción de editar o eliminar de la interfaz de usuario, cree los criterios personalizados usando la interfaz de usuario para [la documentación](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html), en lugar de usar la API Crear criterios personalizados.

Solo continúe con los siguientes pasos después de haber leído la advertencia anterior y de sentirse cómodo con la creación de nuevos criterios personalizados que no se puedan eliminar posteriormente de la interfaz de usuario.

1. Compruebe que `TENANT_ID` y `API_KEY` de **[!UICONTROL Create custom criteria]** hacen referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para compararla.

   ![CrearCriteriosPersonalizados1](assets/CreateCustomCriteria1.png)

1. Agregue su **cuerpo** como **archivo sin procesar** JSON que define la ubicación del archivo CSV de criterios personalizados. Use el ejemplo proporcionado en la documentación [Crear API de criterios personalizados](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom) como plantilla, proporcionando sus `environmentId` y otros valores según sea necesario. Para este ejemplo, utilizamos LAST_PURCHASED como clave.

   ![CrearCriteriosPersonalizados2](assets/CreateCustomCriteria2.png)

1. Envíe la solicitud y observe la respuesta, que contiene los detalles de los criterios personalizados que acaba de crear.

   ![CrearCriteriosPersonalizados3](assets/CreateCustomCriteria3.png)

1. Para comprobar que se han creado los criterios personalizados, vaya a Adobe Target hasta **[!UICONTROL Recommendations > Criteria]** y busque los criterios por su nombre, o use **[!UICONTROL List Custom Criteria API]** en el paso siguiente.

   ![CrearCriteriosPersonalizados4](assets/CreateCustomCriteria4.png)

En este caso, se produce un error. Investiguemos el error examinando más de cerca los criterios personalizados, usando el **[!UICONTROL List Custom Criteria API]**.

## Enumerar criterios personalizados

Para recuperar una lista de todos los criterios personalizados junto con los detalles de cada uno, use la [API de lista de criterios personalizados](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom). La sintaxis es:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Compruebe `TENANT_ID` y `API_KEY` como antes y envíe la solicitud. En la respuesta, observe el ID de criterios personalizados, así como los detalles relativos al mensaje de error anotado anteriormente.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

En este caso, el error se produjo porque la información del servidor es incorrecta, lo que significa que Target no puede acceder al archivo CSV que contiene la definición de criterios personalizados. Vamos a editar los criterios personalizados para corregir esto.

## Editar criterios personalizados

Para cambiar los detalles de una definición de criterio personalizada, use [Editar API de criterio personalizado](https://developer.adobe.com/target/administer/recommendations-api/#operation/updateCriteriaCustom). La sintaxis es:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Compruebe `TENANT_ID` y `API_KEY`, como antes.
   ![EditarCriteriosPersonalizados1](assets/EditCustomCriteria1.png)

1. Especifique el ID de criterio de los criterios personalizados (únicos) que desea editar.
   ![EditarCriteriosPersonalizados2](assets/EditCustomCriteria2.png)

1. En el cuerpo, proporcione el JSON actualizado con la información correcta del servidor. (Para este paso, especifique el acceso FTP a un servidor al que pueda acceder).
   ![EditarCriteriosPersonalizados3](assets/EditCustomCriteria3.png)

1. Envíe la solicitud y anote la respuesta.
   ![EditarCriteriosPersonalizados4](assets/EditCustomCriteria4.png)

Vamos a comprobar el éxito de los criterios personalizados actualizados utilizando **[!UICONTROL Get Custom Criteria API]**.

## Obtener criterios personalizados

Para ver los detalles de criterios personalizados de un criterio personalizado específico, use [Obtener API de criterios personalizados](https://developer.adobe.com/target/administer/recommendations-api/#operation/getCriteriaCustom). La sintaxis es:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique el ID de criterio de los criterios personalizados cuyos detalles desee obtener. Envíe la solicitud y revise la respuesta.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Verifique si se ha realizado correctamente. (En nuestro caso, compruebe que no haya más errores de FTP).
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Opcional) Compruebe que la actualización se refleja con precisión en la interfaz de usuario.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Eliminar criterios personalizados

Si utiliza el identificador de criterios mencionado anteriormente, elimine los criterios personalizados mediante la [API Eliminar criterios personalizados](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteCriteriaCustom). La sintaxis es:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique el ID de criterio de los criterios personalizados (únicos) que desea eliminar. Haga clic en **[!UICONTROL Send]**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Compruebe que los criterios se han eliminado utilizando Obtener criterios personalizados.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
En este caso, el error 404 esperado indica que no se pueden encontrar los criterios eliminados.

>[!NOTE]
>
>Como recordatorio, los criterios no se eliminarán de la IU de Target aunque se hayan eliminado, ya que se crearon con la API Crear criterio personalizado.

¡Felicidades! Ahora puede crear, mostrar en lista, editar, eliminar y obtener detalles sobre criterios personalizados con la API de Recommendations. En la siguiente sección, utilice la API de envío de Target para recuperar recomendaciones.

&lt;!— [Siguiente: &quot;Recuperar Recommendations con la API de envío del lado del servidor&quot; >](fetch-recs-server-side-delivery-api.md) —>
