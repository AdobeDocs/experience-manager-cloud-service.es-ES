---
title: Invalidación de la caché de la red de distribución de contenido mediante Dynamic Media
description: Obtenga información sobre cómo invalidar el contenido en caché de la CDN (red de distribución de contenido) para permitirle actualizar rápidamente los recursos que entrega Dynamic Media, en lugar de esperar a que la caché caduque.
contentOwner: Rick Brough
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 1%

---

# Invalidación de la caché de CDN mediante Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

La CDN (red de distribución de contenido) almacena en caché los recursos de Dynamic Media para una entrega rápida a sus clientes. Sin embargo, cuando realice actualizaciones en esos recursos, desea que los cambios surtan efecto inmediatamente en el sitio web. La depuración o invalidación de la caché de la CDN permite actualizar rápidamente los recursos que envía Dynamic Media. Ya no tiene que esperar a que la caché caduque con un valor TTL (Tiempo de vida) (el valor predeterminado es de diez horas). En su lugar, puede enviar una solicitud desde la interfaz de usuario de Dynamic Media para que la caché caduque en cuestión de minutos.

>[!NOTE]
>
>Esta función requiere que utilice la CDN agrupada en Adobe que viene con Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

Si ha habilitado [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md) en su cuenta y está usando la CDN agrupada en Adobe, puede purgar todas las direcciones URL con diferentes cadenas de consulta purgando la dirección URL base única.

Por ejemplo, al invalidar `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`, también se invalidan las siguientes direcciones URL:

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* y demás.

Sin embargo, esta invalidación no es el caso de los dominios genéricos que no admiten imágenes inteligentes, como `s7d1.scene7.com`. Estos dominios necesitan la dirección URL completa para que la invalidación funcione correctamente.

**Para invalidar la caché de la CDN mediante Dynamic Media:**

*Parte 1 de 2: Creación de una plantilla de invalidación de CDN*

1. En Adobe Experience Manager as a Cloud Service, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Plantilla de invalidación de CDN]**.

   ![Característica de validación de CDN](/help/assets/assets-dm/cdn-invalidation-template.png)

1. En la página **[!UICONTROL Plantilla de invalidación de CDN]**, realice una de las siguientes opciones según su escenario:

   | Escenario | Opción |
   | --- | --- |
   | Ya he creado una plantilla de invalidación de CDN en el pasado mediante Dynamic Media Classic. | El campo de texto **[!UICONTROL Crear plantilla]** está rellenado previamente con los datos de la plantilla. En este caso, puede editar la plantilla o continuar con el siguiente paso. |
   | Tengo que crear una plantilla. ¿En qué puedo participar? | En el campo de texto **[!UICONTROL Crear plantilla]**, escriba una URL de imagen (incluidos los ajustes preestablecidos o modificadores de imagen) que haga referencia a `<ID>`, en lugar de un ID de imagen específico como en el siguiente ejemplo:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Si la plantilla contiene solo `<ID>`, Dynamic Media rellena `https://<publishserver_name>/is/image/<company_name>/<ID>`, donde `<publishserver_name>` es el nombre de su servidor de Publish que se define en Configuración general en Dynamic Media Classic. `<company_name>` es el nombre de la raíz de la compañía asociada con esta instancia de Experience Manager y `<ID>` son los recursos seleccionados a través del selector de recursos que se van a invalidar.<br>Todos los ajustes preestablecidos o modificadores que siguen a `<ID>` se copian tal cual en la definición de la dirección URL.<br>Solo las imágenes (es decir, `/is/image`) se pueden formar automáticamente según la plantilla.<br>Para `/is/content/`, agregar recursos como vídeos o PDF mediante el selector de recursos no genera automáticamente direcciones URL. En su lugar, debe especificar dichos recursos en la plantilla de invalidación de CDN o puede agregar manualmente la dirección URL a dichos recursos en *Parte 2 de 2: Configurar las opciones de invalidación de CDN*.<br>**Ejemplos:**<br> En este primer ejemplo, la plantilla de invalidación contiene `<ID>` junto con la dirección URL del recurso que tiene `/is/content`. Por ejemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forma la dirección URL en función de esta ruta, donde `<ID>` son los recursos seleccionados mediante el selector de recursos que desea invalidar.<br>En este segundo ejemplo, la plantilla de invalidación contiene la dirección URL completa del recurso utilizado en las propiedades web con `/is/content` (no depende del selector de recursos). Por ejemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` donde la mochila es el ID del recurso.<br>Los formatos de recursos compatibles con Dynamic Media pueden invalidarse. Los tipos de archivos de recursos *no* admitidos para la invalidación de la CDN son PostScript®, PostScript® encapsulada, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word y formato de texto enriquecido.<br><br>· Cuando cree la plantilla, pero asegúrese de prestar mucha atención a la sintaxis y a los errores tipográficos; Dynamic Media no realiza ninguna validación de plantilla.<br>· La plantilla de invalidación de CDN puede guardar texto de hasta 2500 caracteres.<br>· Especifique las direcciones URL para los recortes inteligentes de imagen en esta plantilla de invalidación de CDN o en el campo de texto **[!UICONTROL Agregar dirección URL]** en *Parte 2: Configurar las opciones de invalidación de CDN.*<br>· Cada entrada de una plantilla de invalidación de CDN debe estar en su propia línea.<br>· El siguiente ejemplo de plantilla de invalidación de CDN es solo para fines de demostración. |

   ![Plantilla de invalidación de CDN - Crear](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >La plantilla de invalidación de CDN puede guardar texto de hasta 2500 caracteres.

1. En la esquina superior derecha de la página **[!UICONTROL Plantilla de invalidación de CDN]**, seleccione **[!UICONTROL Guardar]** y, a continuación, seleccione **[!UICONTROL Aceptar]**.<br>
   *Parte 2 de 2: Estableciendo opciones de invalidación de CDN*
   <br>

1. En el as a Cloud Service del Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidación de CDN]**.

   ![Característica de validación de CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. En la página **[!UICONTROL Invalidación de CDN]** - **[!UICONTROL Agregar detalles]**, seleccione los recursos para la invalidación de CDN.

   ![Invalidación de CDN - Agregar detalles](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Si decide dejar sin marcar las opciones **[!UICONTROL Invalidar ajustes preestablecidos de imagen asociados al recurso en CDN]** *y* **[!UICONTROL Invalidar según la plantilla]**, se formará la URL base de los recursos seleccionados para su invalidación. Utilice esta disposición de opciones solo para imágenes.


   | Opción | Descripción |
   | --- | --- |
   | **[!UICONTROL Invalidar ajustes preestablecidos de imagen asociados a recursos en CDN]** | (Opcional) Al marcar esta opción, los recursos seleccionados y todas sus URL de ajustes preestablecidos de imagen asociadas se forman automáticamente para invalidar la caché.<br>Assets y sus direcciones URL predefinidas asociadas se forman automáticamente para su invalidación. Esta opción solo funciona para recursos de imagen. |
   | **[!UICONTROL Invalidación basada en plantilla]** | (Opcional) Marque esta opción para utilizar solo la plantilla definida para la formación de URL. |
   | **[!UICONTROL Agregar Assets]** | Utilice el Selector de recursos para seleccionar los recursos que desea invalidar. Puede seleccionar recursos publicados o no publicados.<br>El almacenamiento en caché en la CDN se basa en URL, no en recursos. Por lo tanto, es necesario conocer las direcciones URL completas que se encuentran en el sitio web. Después de determinar esas direcciones URL, puede agregarlas a la plantilla. A continuación, puede seleccionar y añadir esos recursos e invalidar las direcciones URL en un solo paso. <br>Utilice esta opción con **[!UICONTROL Invalidar ajustes preestablecidos de imagen asociados a recursos en CDN]**, **[!UICONTROL Invalidación basada en plantilla]** o ambos. |
   | **[!UICONTROL Agregar URL]** | Agregue o pegue manualmente rutas URL completas a los recursos de Dynamic Media cuya caché de CDN desee invalidar. Utilice esta opción si no ha creado una plantilla de invalidación de CDN en ***Parte 1 de 2: Creación de una plantilla de invalidación de CDN*** y sólo tiene unos pocos recursos que invalidar.<br>**Importante:** Cada dirección URL que agregue debe estar en su propia línea.<br>Puede invalidar hasta 1000 direcciones URL a la vez. Si el número de direcciones URL en el campo de texto **[!UICONTROL Agregar dirección URL]** es mayor que 1000, no podrá seleccionar **[!UICONTROL Siguiente]**. En estos casos, debe seleccionar **[!UICONTROL X]** a la derecha del recurso seleccionado o agregar manualmente una URL para eliminarlo de la lista de invalidación.<br>Especifique direcciones URL para los cultivos inteligentes de imagen en la plantilla de invalidación de la CDN o en este campo de texto **[!UICONTROL Agregar dirección URL]**. |

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Siguiente]**.
1. En la página **[!UICONTROL Invalidación de CDN]** - **[!UICONTROL Confirmar]**, en el cuadro de lista **[!UICONTROL URL]**, verá una lista de una o más URL generadas a partir de la plantilla de invalidación de CDN que creó anteriormente y de los recursos que acaba de agregar.

   Por ejemplo, si utiliza el ejemplo de la plantilla de invalidación de CDN que se mostró en los pasos anteriores, suponga que agregó un solo recurso denominado `spinset`. Si va a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidación de CDN]**, se generarán las siguientes cinco direcciones URL en la interfaz de usuario **[!UICONTROL Invalidación de CDN: Confirmar]**:

   ![Invalidación de CDN: confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Si es necesario, seleccione **X** a la derecha de una dirección URL para eliminarla del proceso de invalidación.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Enviar]** para comenzar el proceso de invalidación de la CDN.

## Solucionar errores de invalidación de CDN

En todos los casos, se procesa todo el lote para su invalidación o se produce un error en todo el lote.

| Error | Explicación |
| --- | --- |
| *Error al recuperar las direcciones URL de los recursos seleccionados.* | Se produce si se cumple cualquiera de los siguientes escenarios:<br>- No se encuentra una configuración de Dynamic Media.<br>: hay una excepción al recuperar un usuario de servicio a través del cual se lee la configuración de Dynamic Media.<br>: falta el servidor de publicación o la raíz de la empresa utilizada para formar las direcciones URL en la configuración de Dynamic Media. |
| *Algunas direcciones URL no se han definido correctamente. Corregir y volver a enviar.* | Se produce si la API de invalidación de caché de la CDN de IPS devuelve un error. El error indica que la dirección URL hace referencia a una empresa diferente o que la dirección URL no es válida según la validación realizada por la API cdnCacheInvalidation de IPS. |
| *No se pudo invalidar la caché de CDN.* | Se produce si la solicitud de invalidación de la caché de la CDN falla por cualquier otro motivo. |
| *No se ha ingresado ninguna dirección URL para invalidar.* | Se produce si no hay direcciones URL presentes en la página **[!UICONTROL Invalidación de CDN]** - **[!UICONTROL Confirmar]** y selecciona **[!UICONTROL Enviar]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. While you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
