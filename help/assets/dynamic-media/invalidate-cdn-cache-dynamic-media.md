---
title: Invalidación de la caché de CDN mediante Dynamic Media
description: La invalidación del contenido en caché de CDN (Red de Envío de contenido) permite actualizar rápidamente los recursos que se entregan mediante Dynamic Media, en lugar de esperar a que caduque la caché.
translation-type: tm+mt
source-git-commit: aae3dcb0f44ef8e8d1401274fbf1fd47ea718b09
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---


# Invalidación de la caché de CDN mediante Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Los recursos de Dynamic Media se almacenan en caché en la red de Envío de contenido (CDN) para un envío rápido a sus clientes. Sin embargo, cuando actualice estos recursos, es posible que desee que los cambios surtan efecto inmediatamente en el sitio web. La depuración o invalidación de la caché de CDN permite actualizar rápidamente los recursos que se envían mediante Dynamic Media. En lugar de esperar a que la caché caduque con un valor TTL (tiempo de vida) (el valor predeterminado es 10 horas), puede enviar una solicitud desde la interfaz de usuario de Dynamic Media para que la caché caduque en cuestión de minutos.

>[!IMPORTANT]
>
>Los pasos siguientes solo se aplican a Dynamic Media en AEM como Cloud Service. También debe utilizar la CDN predeterminada que se incluye con AEM Dynamic Media. Esta función no admite ningún otro CDN personalizado. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Consulte también Descripción general [del almacenamiento en caché en Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar la caché de CDN mediante Dynamic Media**

*Parte 1: Creación de una plantilla de invalidación de CDN*

1. En AEM como Cloud Service, toque **[!UICONTROL Herramientas > Recursos > Plantilla de invalidación de CDN.]**

   ![Función de validación de CDN](/help/assets/assets-dm/cdn-invalidation-template.png)

1. En la página Plantilla **[!UICONTROL de invalidación de]** CDN, realice una de las siguientes opciones según el escenario:

   | Escenario | Opción |
   | --- | --- |
   | Ya he creado una plantilla de invalidación de CDN en el pasado mediante Dynamic Media Classic. | El campo de texto **[!UICONTROL Crear plantilla]** se rellena previamente con los datos de la plantilla. En ese caso, puede editar la plantilla o continuar con el paso siguiente. |
   | Necesito crear una plantilla. ¿En qué puedo entrar? | En el campo de texto **[!UICONTROL Crear plantilla]** , introduzca una URL de imagen (incluidos los ajustes preestablecidos o modificadores de imagen) que haga referencia a `<ID>`, en lugar de un ID de imagen específico como en el ejemplo siguiente:<br><br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br><br>Si la plantilla solo contiene `<ID>`, Dynamic Media rellena `https://<publishserver_name>/is/image` donde `<publishserver_name>` es el nombre del servidor de publicación y `ID` es el recurso seleccionado para invalidar.<br><br>Solo las imágenes (es decir, `/is/image`) pueden formarse automáticamente en función de la plantilla. Por ejemplo, `/is/content/`la adición de recursos como vídeos o archivos PDF mediante el selector de recursos no genera automáticamente direcciones URL. En su lugar, debe especificar estos recursos en la plantilla Invalidación de CDN o puede agregar manualmente la URL a dichos recursos en la *parte 2: Configuración de las opciones* de Invalidación de CDN.<br>Los formatos de recurso compatibles con Dynamic Media pueden invalidarse. Recursos como PowerPoint o archivos de texto sin formato no son recursos admitidos para la invalidación de CDN.<br>Cuando cree la plantilla, pero asegúrese de prestar atención a la sintaxis y a los errores ortográficos; Dynamic Media no realiza ninguna validación de plantilla.<br>El siguiente ejemplo de plantilla se muestra únicamente con fines ilustrativos. |

   ![Plantilla de invalidación de CDN: Crear](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. En la esquina superior derecha de la página Plantilla de invalidación de CDN, toque **[!UICONTROL Guardar]** y, a continuación, **[!UICONTROL Aceptar]**.<br>

   ***Parte 2: Configuración de las opciones de invalidación de CDN***
<br>

1. En AEM como Cloud Service, toque **[!UICONTROL Herramientas > Recursos > Invalidación de CDN.]**

   ![Función de validación de CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. En la página **[!UICONTROL Invalidación]** de CDN: **[!UICONTROL Añadir detalles]** , seleccione los recursos para invalidación de CDN.

   ![Invalidación de CDN: Añadir detalles](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Si decide dejar sin marcar las opciones **[!UICONTROL Invalidar los ajustes preestablecidos de imagen asociados al recurso en CDN]** *e* Invalidar basándose en plantilla **** , la dirección URL base de los recursos seleccionados se formará para su invalidación. Debe utilizar esta disposición de opciones solo para imágenes.


   | Opción | Descripción |
   | --- | --- |
   | **[!UICONTROL Anular los ajustes preestablecidos de imagen asociados a activos en la CDN]** | (Opcional) Al marcar esta opción, puede seleccionar uno o varios recursos de Dynamic Media (independientemente del tipo MIME) y sus ajustes preestablecidos de imagen asociados para la invalidación de caché.<br>Los recursos y sus URL predefinidas asociadas se forman automáticamente para invalidar. Esta opción solo funciona para<br>los recursos de imagenAunque puede seleccionar una o varias carpetas que contengan recursos, Adobe no recomienda este método. En su lugar, debe seleccionar archivos de recursos individuales. |
   | **[!UICONTROL Invalidación basada en plantilla]** | (Opcional) Seleccione esta opción para utilizar solo la plantilla definida para la formación de URL. |
   | **[!UICONTROL Añadir recursos]** | Utilice el Selector de recursos para seleccionar los recursos que desea invalidar. Puede seleccionar recursos publicados o no publicados.<br>Puede obtener una lista en blanco al agregar recursos. Dynamic Media utiliza la plantilla de invalidación de CDN para crear automáticamente una URL que invalide la CDN. Si no se ha creado ninguna plantilla de invalidación de CDN, se obtiene una lista en blanco.<br>El almacenamiento en caché en CDN se basa en URL, no en recursos. Por lo tanto, es necesario que tenga en cuenta las direcciones URL completas que se encuentran en el sitio web. Después de determinar esas direcciones URL, puede agregarlas a la plantilla.A continuación, puede seleccionar y agregar esos recursos e invalidar las direcciones URL en un solo paso. La otra opción que tiene es agregar direcciones URL a la lista de invalidación de CDN. Si prefiere este método, no es necesario seleccionar y agregar recursos antes de tocar **[!UICONTROL Siguiente]** y luego **[!UICONTROL Enviar]** para invalidar.<br>Utilice esta opción junto con **[!UICONTROL Invalidar los ajustes preestablecidos de imagen asociados al recurso en CDN]** o **[!UICONTROL Invalidación basada en plantilla]**, o ambos. |
   | **[!UICONTROL Añadir URL]** | Agregue o pegue manualmente rutas de URL completas a recursos de Dynamic Media cuya caché de CDN desee invalidar. Utilice esta opción si no ha creado una plantilla de invalidación de CDN en la ***parte 1: Trabajar con la plantilla*** de invalidación de CDN y tener sólo unos pocos recursos para invalidar.<br> |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next]**.
1. En la página **[!UICONTROL Invalidación]** de CDN: **[!UICONTROL Confirmar]** , en el cuadro lista de **[!UICONTROL URL]** , verá una lista de una o varias URL generadas a partir de la plantilla de invalidación de CDN que creó anteriormente y de los recursos que acaba de agregar.

   Por ejemplo, con la plantilla de invalidación de CDN creada anteriormente, supongamos que ha agregado un único recurso denominado `spinset`. Al tocar **[!UICONTROL Herramientas > Recursos > Invalidación]** de CDN, se generan las siguientes cinco direcciones URL en la interfaz de usuario Invalidación de **[!UICONTROL CDN: Confirmar]** :

   ![Invalidación de CDN: Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Si es necesario, toque la **X** a la derecha de una URL para eliminarla del proceso de invalidación. Puede tener hasta 1000 direcciones URL en un momento dado.

1. Cerca de la esquina superior derecha de la página, toque **[!UICONTROL Enviar]** para iniciar el proceso de invalidación de CDN.

## Resolución de problemas de errores de invalidación de CDN

* Esta función permite invalidar hasta 1000 direcciones URL a la vez. Un número bueno de 1000 da como resultado un error que puede resolver eliminando direcciones URL en la página Invalidación de **[!UICONTROL CDN - Confirmar]** .
* En todos los casos, el lote completo se procesa para invalidación o se produce un error en todo el lote.

| Error | Explicación |
| --- | --- |
| *No se pudieron recuperar las direcciones URL de los recursos seleccionados.* | Se produce si se cumple cualquiera de los siguientes escenarios:<br>- No se encuentra una configuración de Dynamic Media.<br>- Existe una excepción al recuperar un usuario de servicio a través del cual se lee la configuración de Dynamic Media.<br>- Falta el servidor de publicación o la raíz de compañía que se utiliza para formar las direcciones URL en la configuración de Dynamic Media. |
| *Algunas direcciones URL no están definidas correctamente. Corrija y vuelva a enviarlo.* | Se produce si la API de invalidación de caché CDN de IPS devuelve un error en el que la dirección URL hace referencia a una compañía diferente o si la dirección URL no es válida según la validación realizada por la API cdnCacheInvalidation de IPS. |
| *No se pudo invalidar la caché de CDN.* | Se produce si la solicitud de invalidación de caché de CDN falla por cualquier otro motivo. |
| *No se especificó ninguna dirección URL para invalidarla.* | Se produce si no hay direcciones URL presentes en la página **[!UICONTROL Invalidación de]** CDN: Confirmar y toca **[!UICONTROL Enviar]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->