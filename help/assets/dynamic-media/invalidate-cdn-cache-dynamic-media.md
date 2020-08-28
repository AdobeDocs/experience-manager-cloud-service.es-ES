---
title: Invalidación de la caché de CDN mediante Dynamic Media
description: La invalidación del contenido en caché de CDN (Red de Envío de contenido) permite actualizar rápidamente los recursos que se entregan mediante Dynamic Media, en lugar de esperar a que caduque la caché.
translation-type: tm+mt
source-git-commit: 42788d6a64c5bca7bddd563cb26634db80b2e75d
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 1%

---


# Invalidación de la caché de CDN mediante Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Los recursos de Dynamic Media se almacenan en caché en la red de Envío de contenido (CDN) para un envío rápido a sus clientes. Sin embargo, cuando actualice estos recursos, es posible que desee que los cambios surtan efecto inmediatamente en el sitio web. La depuración o invalidación de la caché de CDN permite actualizar rápidamente los recursos que se envían mediante Dynamic Media. En lugar de esperar a que la caché caduque con un valor TTL (tiempo de vida) (el valor predeterminado es 10 horas), puede enviar una solicitud desde la interfaz de usuario de Dynamic Media para que la caché caduque en cuestión de minutos.

>[!IMPORTANT]
>
>Los pasos siguientes solo se aplican a Dynamic Media en AEM como Cloud Service. Esta función también requiere que utilice la CDN integrada con AEM Dynamic Media; no se admite ningún otro CDN personalizado. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Consulte también Descripción general [del almacenamiento en caché en Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar la caché de CDN mediante Dynamic Media**

*Parte 1: Creación de una plantilla de invalidación de CDN*

1. En AEM como Cloud Service, toque **[!UICONTROL Herramientas > Recursos > Plantilla de invalidación de CDN.]**

<!--
    ![CDN Validation feature](/help/assets/assets-dm/cdn-invalidation-template.png)
-->

1. En la página Plantilla **[!UICONTROL de invalidación de]** CDN, realice una de las siguientes opciones según el escenario:

   | Escenario | Opción |
   | --- | --- |
   | Ya he creado una plantilla de invalidación de CDN en el pasado mediante Dynamic Media Classic. | El campo de texto **[!UICONTROL Crear plantilla]** se rellena previamente con los datos de la plantilla. En ese caso, puede editar la plantilla o continuar con el paso siguiente. |
   | Necesito crear una plantilla. ¿En qué puedo entrar? | En el campo de texto **[!UICONTROL Crear plantilla]** , introduzca una URL de imagen (incluidos los ajustes preestablecidos o modificadores de imagen) que haga referencia `<ID>`, en lugar de un ID de imagen específico como en el ejemplo siguiente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Si la plantilla contiene solo `<ID>`, Dynamic Media rellena `https://<publishserver_name>/is/image/<company_name>/<ID>` donde `<publishserver_name>` es el nombre del servidor de publicación definido en Configuración general en Dynamic Media Classic; el `<company_name>` es el nombre de la raíz de compañía asociada a esta instancia de AEM y `<ID>` es el recurso seleccionado a través del selector de recursos que se va a invalidar.<br>Cualquier anuncio de modificadores/ajustes preestablecidos `<ID>` se copia tal cual en la definición de URL.<br>Solo las imágenes (es decir, `/is/image`) pueden formarse automáticamente en función de la plantilla.<br>Por ejemplo, `/is/content/`la adición de recursos como vídeos o archivos PDF mediante el selector de recursos no genera automáticamente direcciones URL. En su lugar, debe especificar estos recursos en la plantilla Invalidación de CDN o puede agregar manualmente la URL a dichos recursos en la *parte 2: Configuración de las opciones* de Invalidación de CDN.<br>**Ejemplos:**<br> en este primer ejemplo, la plantilla de invalidación contiene `<ID>` junto con la URL del recurso que tiene `/is/content`. Por ejemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forma la dirección URL basada en esto, siendo `<ID>` los recursos seleccionados mediante el selector de recursos que desea invalidar.<br>En este segundo ejemplo, la plantilla de invalidación contiene la dirección URL completa del recurso utilizado en las propiedades web con `/is/content` (no depende del selector de recursos). Por ejemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` donde backpack es el ID del recurso.<br>Los formatos de recurso compatibles con Dynamic Media pueden invalidarse. Los tipos de archivo de recurso que *no son* compatibles con la invalidación de CDN son Postscript, Encapsulated Postscript, Adobe Illustrator, Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word y Formato de texto enriquecido.<br>Cuando cree la plantilla, pero asegúrese de prestar atención a la sintaxis y a los errores ortográficos; Dynamic Media no realiza ninguna validación de plantilla.<br>Tenga en cuenta que debe especificar direcciones URL para los recortes inteligentes de imagen en esta plantilla de invalidación de CDN o en el campo de texto **[!UICONTROL Añadir URL]** de la *parte 2: Configuración de las opciones* de Invalidación de CDN.<br>**Importante:** Cada entrada de una plantilla de invalidación de CDN debe estar en su propia línea.<br>El siguiente ejemplo de plantilla se muestra únicamente con fines ilustrativos. |

   ![Plantilla de invalidación de CDN: Crear](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. En la esquina superior derecha de la página Plantilla de invalidación de CDN, toque **[!UICONTROL Guardar]** y, a continuación, **[!UICONTROL Aceptar]**.

   *Parte 2: Configuración de las opciones de invalidación de CDN*

1. En AEM como Cloud Service, toque **[!UICONTROL Herramientas > Recursos > Invalidación de CDN.]**

   ![Función de validación de CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. En la página **[!UICONTROL Invalidación]** de CDN: **[!UICONTROL Añadir detalles]** , seleccione los recursos para invalidación de CDN.

   ![Invalidación de CDN: Añadir detalles](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Si decide dejar sin marcar las opciones **[!UICONTROL Invalidar los ajustes preestablecidos de imagen asociados al recurso en CDN]** *e* Invalidar basándose en plantilla **** , la dirección URL base de los recursos seleccionados se formará para su invalidación. Debe utilizar esta disposición de opciones solo para imágenes.


   | Opción | Descripción |
   | --- | --- |
   | **[!UICONTROL Anular los ajustes preestablecidos de imagen asociados a activos en la CDN]** | (Opcional) Al marcar esta opción, los recursos seleccionados y todas las URL de ajustes preestablecidos de imagen asociadas se forman automáticamente para la invalidación de caché.<br>Los recursos y sus URL predefinidas asociadas se forman automáticamente para invalidar. Esta opción solo funciona para recursos de imagen. |
   | **[!UICONTROL Invalidación basada en plantilla]** | (Opcional) Seleccione esta opción para utilizar solo la plantilla definida para la formación de URL. |
   | **[!UICONTROL Añadir recursos]** | Utilice el Selector de recursos para seleccionar los recursos que desea invalidar. Puede seleccionar recursos publicados o no publicados.<br>El almacenamiento en caché en CDN se basa en URL, no en recursos. Por lo tanto, es necesario que tenga en cuenta las direcciones URL completas que se encuentran en el sitio web. Después de determinar esas direcciones URL, puede agregarlas a la plantilla. A continuación, puede seleccionar y agregar esos recursos e invalidar las direcciones URL en un solo paso. <br>Utilice esta opción junto con **[!UICONTROL Invalidar los ajustes preestablecidos de imagen asociados al recurso en CDN]** o **[!UICONTROL Invalidación basada en plantilla]**, o ambos. |
   | **[!UICONTROL Añadir URL]** | Agregue o pegue manualmente rutas de URL completas a recursos de Dynamic Media cuya caché de CDN desee invalidar. Utilice esta opción si no ha creado una plantilla de invalidación de CDN en la ***parte 1: Trabajar con la plantilla*** de invalidación de CDN y tener sólo unos pocos recursos para invalidar.<br>**Importante:** Cada dirección URL que agregue debe estar en su propia línea.<br>Puede invalidar hasta 1000 direcciones URL a la vez. Si el número de direcciones URL en el campo de texto **[!UICONTROL Añadir URL]** es bueno a 1000, no podrá tocar **[!UICONTROL Siguiente]**. En estos casos, debe tocar **[!UICONTROL X]** a la derecha de un recurso seleccionado o una URL agregada manualmente para eliminarlo de la lista de invalidación.<br>Tenga en cuenta que debe especificar direcciones URL para los recortes inteligentes de imagen en la plantilla Invalidación de CDN o en este campo de texto **[!UICONTROL Añadir URL]** . |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next]**.
1. En la página **[!UICONTROL Invalidación]** de CDN: **[!UICONTROL Confirmar]** , en el cuadro lista de **[!UICONTROL URL]** , verá una lista de una o varias URL generadas a partir de la plantilla de invalidación de CDN que creó anteriormente y de los recursos que acaba de agregar.

   Por ejemplo, con la plantilla de invalidación de CDN creada anteriormente, supongamos que ha agregado un único recurso denominado `spinset`. Al tocar **[!UICONTROL Herramientas > Recursos > Invalidación]** de CDN, se generan las siguientes cinco direcciones URL en la interfaz de usuario Invalidación de **[!UICONTROL CDN: Confirmar]** :

   ![Invalidación de CDN: Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Si es necesario, toque **X** a la derecha de una dirección URL si desea eliminarla del proceso de invalidación.

1. Cerca de la esquina superior derecha de la página, toque **[!UICONTROL Enviar]** para iniciar el proceso de invalidación de CDN.

## Resolución de problemas de errores de invalidación de CDN

En todos los casos, el lote completo se procesa para invalidación o se produce un error en todo el lote.

| Error | Explicación |
| --- | --- |
| *No se pudieron recuperar las direcciones URL de los recursos seleccionados.* | Se produce si se cumple cualquiera de los siguientes escenarios:<br>- No se encuentra una configuración de Dynamic Media.<br>- Existe una excepción al recuperar un usuario de servicio a través del cual se lee la configuración de Dynamic Media.<br>- Falta el servidor de publicación o la raíz de compañía que se utiliza para formar las direcciones URL en la configuración de Dynamic Media. |
| *Algunas direcciones URL no están definidas correctamente. Corrija y vuelva a enviarlo.* | Se produce si la API de invalidación de caché CDN de IPS devuelve un error en el que la dirección URL hace referencia a una compañía diferente o si la dirección URL no es válida según la validación realizada por la API cdnCacheInvalidation de IPS. |
| *No se pudo invalidar la caché de CDN.* | Se produce si la solicitud de invalidación de caché de CDN falla por cualquier otro motivo. |
| *No se especificó ninguna dirección URL para invalidarla.* | Se produce si no hay direcciones URL presentes en la página **[!UICONTROL Invalidación de]** CDN: Confirmar y toca **[!UICONTROL Enviar]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
