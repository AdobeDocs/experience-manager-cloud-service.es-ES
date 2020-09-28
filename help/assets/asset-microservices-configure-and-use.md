---
title: Configuración y uso de microservicios de recursos
description: Configure y utilice los microservicios de recursos nativos de la nube para procesar los recursos a escala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '2527'
ht-degree: 1%

---


# Use asset microservices and processing profiles {#get-started-using-asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante aplicaciones nativas de la nube (también denominadas trabajadores). Adobe gestiona los servicios para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento.

Los microservicios de recursos le permiten procesar una [amplia gama de tipos](/help/assets/file-format-support.md) de archivos que cubren más formatos listos para usar que los que son posibles con versiones anteriores de [!DNL Experience Manager]. Por ejemplo, ahora es posible la extracción en miniatura de los formatos PSD y PSB que anteriormente requerían soluciones de terceros como ImageMagick.

El procesamiento de recursos depende de la configuración de los Perfiles **[!UICONTROL de procesamiento]**. Experience Manager proporciona una configuración predeterminada básica y permite a los administradores agregar una configuración de procesamiento de recursos más específica. Los administradores crean, mantienen y modifican las configuraciones de los flujos de trabajo posteriores al procesamiento, incluida la personalización opcional. La personalización de los flujos de trabajo permite a los desarrolladores ampliar la oferta predeterminada.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Una vista de alto nivel del](assets/asset-microservices-flow.png "procesamiento de recursosUna vista de alto nivel del procesamiento de recursos")

>[!NOTE]
>
>El procesamiento de recursos descrito aquí reemplaza el modelo de `DAM Update Asset` flujo de trabajo que existe en las versiones anteriores de [!DNL Experience Manager]. La mayoría de los pasos de generación de representación estándar y relacionados con los metadatos se sustituyen por el procesamiento de los microservicios de recursos y los pasos restantes, si los hay, se pueden reemplazar por la configuración del flujo de trabajo posterior al procesamiento.

## Comprender las opciones de procesamiento de recursos {#get-started}

Experience Manager permite los siguientes niveles de procesamiento.

| Opción | Descripción | Casos de uso cubiertos |
|---|---|---|
| [Configuración predeterminada](#default-config) | Está disponible tal cual y no se puede modificar. Esta configuración proporciona una capacidad de generación de representaciones muy básica. | <ul> <li>Miniaturas estándar utilizadas por la interfaz [!DNL Assets] de usuario (48, 140 y 319 píxeles) </li> <li> Previsualización grande (representación web - 1280 px) </li><li> Metadatos y extracción de texto.</li></ul> |
| [Configuración personalizada](#standard-config) | Configurado por los administradores mediante la interfaz de usuario. Proporciona más opciones para la generación de representaciones ampliando la opción predeterminada. Amplíe la opción lista para usar para proporcionar diferentes formatos y representaciones. | <ul><li>Representación de FPO. </li> <li>Cambiar el formato de archivo y la resolución de las imágenes</li> <li> Se aplica condicionalmente a los tipos de archivo configurados. </li> </ul> |
| [Perfil personalizado](#custom-config) | Configurado por los administradores a través de la interfaz de usuario para utilizar código personalizado a través de aplicaciones personalizadas para llamar al servicio [de cómputo de](https://docs.adobe.com/content/help/en/asset-compute/using/introduction.html)recursos. Admite requisitos más complejos en un método escalable y nativo de la nube. | Consulte casos [de uso](#custom-config)permitidos. |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formatos de archivo compatibles {#supported-file-formats}

Los microservicios de recursos admiten una amplia variedad de formatos de archivo para procesar, generar representaciones o extraer metadatos. Consulte los formatos [de archivo](file-format-support.md) admitidos para ver la lista completa de los tipos MIME y la funcionalidad admitida para cada tipo.

## Configuración predeterminada {#default-config}

Algunos valores predeterminados están preconfigurados para garantizar que las representaciones predeterminadas necesarias en Experience Manager están disponibles. La configuración predeterminada también garantiza que las operaciones de extracción de metadatos y extracción de texto estén disponibles. Los usuarios pueden cargar o actualizar los recursos de forma inmediata con inicio y el procesamiento básico está disponible de forma predeterminada.

Con la configuración predeterminada, solo se configura el perfil de procesamiento más básico. Este perfil de procesamiento no está visible en la interfaz de usuario y no se puede modificar. Siempre se ejecuta para procesar los recursos cargados. Este perfil de procesamiento predeterminado garantiza que el procesamiento básico requerido por [!DNL Experience Manager] se complete en todos los recursos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configuración estándar {#standard-config}

[!DNL Experience Manager] ofrece capacidades para generar representaciones más específicas para formatos comunes según las necesidades del usuario. Un administrador puede crear Perfiles [!UICONTROL de] procesamiento adicionales para facilitar la creación de dichas representaciones. A continuación, los usuarios asignan una o varias de las perfiles disponibles a carpetas específicas para realizar el procesamiento adicional. Por ejemplo, el procesamiento adicional puede generar representaciones para web, móvil y tablet. El siguiente vídeo muestra cómo crear y aplicar Perfiles  de procesamiento y cómo acceder a las representaciones creadas.

* **Ancho y altura** de representación: La especificación de anchura y altura de representación proporciona los tamaños máximos de la imagen de salida generada. Los microservicios de recursos intentan producir la representación más grande posible, cuya anchura y altura no superan la anchura y la altura especificadas, respectivamente. Se conserva la relación de aspecto, que es la misma que la original. Un valor vacío significa que el procesamiento de recursos asume la dimensión de píxeles del original.

* **Reglas** de inclusión de tipo MIME: Cuando se procesa un recurso con un tipo MIME específico, se comprueba primero el tipo MIME con el valor de tipos MIME excluidos para la especificación de representación. Si coincide con esa lista, esta representación específica no se genera para el recurso (lista de bloqueados). De lo contrario, el tipo MIME se compara con el tipo MIME incluido y, si coincide con la lista, se genera la representación (lista de permitidos).

* **Representación** especial de FPO: Al colocar recursos de gran tamaño desde [!DNL Experience Manager] en [!DNL Adobe InDesign] documentos, un profesional creativo espera mucho tiempo después de [colocar un recurso](https://helpx.adobe.com/indesign/using/placing-graphics.html). Mientras tanto, se bloquea el uso del usuario [!DNL InDesign]. Esto interrumpe el flujo creativo y afecta negativamente a la experiencia del usuario. Adobe permite colocar temporalmente representaciones de pequeño tamaño en [!DNL InDesign] documentos para empezar, que se pueden reemplazar posteriormente con recursos de resolución completa a petición. [!DNL Experience Manager] proporciona representaciones que se utilizan únicamente para la colocación (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño pero tienen la misma proporción de aspecto.

El perfil de procesamiento puede incluir una representación FPO (solo para ubicación). Consulte [!DNL Adobe Asset Link] la documentación [](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) para saber si necesita activarla para su perfil de procesamiento. Para obtener más información, consulte la documentación [completa de Vínculo de recursos de](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)Adobe.

### Crear perfil estándar {#create-standard-profile}

Para crear un perfil de procesamiento estándar, siga estos pasos:

1. Los administradores acceden a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Perfiles **** de procesamiento. Haga clic en **[!UICONTROL Crear]**.
1. Proporcione un nombre que le ayude a identificar de forma exclusiva el perfil al aplicarlo a una carpeta.
1. Para generar representaciones de FPO, en la ficha **[!UICONTROL Estándar]** , active **[!UICONTROL Crear representación]** de FPO. Introduzca un valor de **[!UICONTROL calidad]** entre 1 y 100.
1. Para generar otras representaciones, haga clic en **[!UICONTROL Añadir nuevo]** y proporcione la siguiente información:

   * Nombre de archivo de cada representación.
   * Formato de archivo (PNG, JPEG o GIF) de cada representación.
   * Anchura y altura en píxeles de cada representación. Si no se especifican los valores, se utiliza el tamaño de píxel completo de la imagen original.
   * Calidad en porcentaje de cada representación JPEG.
   * Se han incluido y excluido tipos MIME para definir la aplicabilidad de un perfil.

   ![proceso-perfiles-adición](assets/processing-profiles-image.png)

1. Haga clic en **[!UICONTROL Guardar]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Casos de uso y perfil personalizados {#custom-config}

El [!DNL Asset Compute Service] admite una variedad de casos de uso, como el procesamiento predeterminado, el procesamiento de formatos específicos de Adobe como archivos Photoshop y la implementación de un procesamiento personalizado o específico de la organización. La personalización del flujo de trabajo de recursos de actualización de DAM necesaria en el pasado se gestiona automáticamente o mediante la configuración de perfiles de procesamiento. Si estas opciones de procesamiento no satisfacen las necesidades comerciales, Adobe recomienda desarrollar y utilizar [!DNL Asset Compute Service] para ampliar las capacidades predeterminadas. Para obtener información general, consulte [Comprender la extensibilidad y cuándo utilizarla](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>Adobe recomienda utilizar una aplicación personalizada únicamente cuando los requisitos comerciales no se puedan cumplir con las configuraciones predeterminadas o con el perfil estándar.

Puede transformar formatos de imagen, vídeo, documento y otros archivos en distintas representaciones, incluidas miniaturas, texto extraído y metadatos, y archivos.

Los desarrolladores pueden usar el [!DNL Asset Compute Service] para [crear aplicaciones](https://docs.adobe.com/content/help/en/asset-compute/using/extend/develop-custom-application.html) personalizadas que se adapten a los casos de uso admitidos. [!DNL Experience Manager] Puede llamar a estas aplicaciones personalizadas desde la interfaz de usuario mediante perfiles personalizados que los administradores configuran. [!DNL Asset Compute Service] admite los siguientes casos de uso de invocar servicios externos:

* Utilice [!DNL Adobe Photoshop]la [API](https://github.com/AdobeDocs/photoshop-api-docs-pre-release#imagecutout) ImageCutout de Adobe y guarde el resultado como representación.
* Llame a sistemas de terceros para actualizar los datos, por ejemplo, un sistema PIM.
* Utilice [!DNL Photoshop] la API para generar diversas representaciones basadas en la plantilla de Photoshop.
* Utilice la API [de Lightroom de](https://github.com/AdobeDocs/lightroom-api-docs#supported-features) Adobe para optimizar los recursos ingestados y guardarlos como representaciones.

>[!NOTE]
>
>No se pueden editar los metadatos estándar con las aplicaciones personalizadas. Solo puede modificar metadatos personalizados.

### Crear un perfil personalizado {#create-custom-profile}

Para crear un perfil personalizado, siga estos pasos:

1. Los administradores acceden a **[!UICONTROL Herramientas > Recursos > Perfiles]** de procesamiento. Haga clic en **[!UICONTROL Crear]**.
1. Haga clic en la ficha **[!UICONTROL Personalizado]** . Haga clic en **[!UICONTROL Añadir nuevo]**. Proporcione el nombre de archivo que desee para la representación.
1. Proporcione la siguiente información.

   * Nombre de archivo de cada representación y extensión de archivo admitida.
   * [URL de punto final de una aplicación](https://docs.adobe.com/content/help/en/asset-compute/using/extend/deploy-custom-application.html)personalizada de Firefly. La aplicación debe pertenecer a la misma organización que la cuenta de Experience Manager.
   * Añada Parámetros de servicio para [pasar información o parámetros adicionales a la aplicación](https://docs.adobe.com/content/help/en/asset-compute/using/extend/develop-custom-application.html#pass-custom-parameters)personalizada.
   * Se han incluido y excluido tipos MIME para limitar el procesamiento a unos pocos formatos de archivo específicos.

   Haga clic en **[!UICONTROL Guardar]**.

Las aplicaciones personalizadas son aplicaciones [de Project Firefly](https://github.com/AdobeDocs/project-firefly) sin encabezado. La aplicación personalizada obtiene todos los archivos proporcionados si están configurados con un perfil de procesamiento. La aplicación debe filtrar los archivos.

>[!CAUTION]
>
>Si la aplicación y la cuenta de Firefly no son de la misma organización, la integración no funcionará. [!DNL Experience Manager]

### Ejemplo de un perfil personalizado {#custom-profile-example}

Para ilustrar el uso personalizado del perfil, consideremos un caso de uso para aplicar texto personalizado a las imágenes de campaña. Puede crear un perfil de procesamiento que aproveche la API de Photoshop para editar las imágenes.

La integración del servicio de cómputo de recursos permite al Experience Manager pasar estos parámetros a la aplicación personalizada mediante el campo Parámetros  de servicio. La aplicación personalizada llama a la API de Photoshop y pasa estos valores a la API. Por ejemplo, puede pasar el nombre de la fuente, el color del texto, el peso del texto y el tamaño del texto para agregar el texto personalizado a las imágenes de campaña.

![custom-processing-perfil](assets/custom-processing-profile.png)

*Figura: Utilice el campo Parámetrosde servicio para pasar información agregada a los parámetros predefinidos generados en la aplicación personalizada. En este ejemplo, cuando se cargan imágenes de campaña, las imágenes se actualizan con`Jumanji`texto en la`Arial-BoldMT`fuente.*

## Uso de perfiles de procesamiento para procesar recursos {#use-profiles}

Cree y aplique los perfiles de procesamiento personalizados adicionales a carpetas específicas para que el Experience Manager pueda procesarlos para los recursos cargados o actualizados en estas carpetas. El perfil de procesamiento estándar predeterminado e integrado siempre se ejecuta, pero no es visible en la interfaz de usuario. Si agrega un perfil personalizado, se utilizan ambos perfiles para procesar los recursos cargados.

Aplique perfiles de procesamiento a las carpetas mediante uno de los siguientes métodos:

* Los administradores pueden seleccionar una definición de perfil de procesamiento en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Perfiles **** de procesamiento y utilizar la acción **[!UICONTROL Aplicar Perfil a carpetas]** . Abre un navegador de contenido que le permite desplazarse a carpetas específicas, seleccionarlas y confirmar la aplicación del perfil.
* Users can select a folder in the Assets user interface, use **[!UICONTROL Properties]** action to open folder properties screen, click on the **[!UICONTROL Processing Profiles]** tab, and in the popup list, select the appropriate processing profile for that folder. Para guardar los cambios, haga clic en **[!UICONTROL Guardar y cerrar]**.
   ![Aplicar perfil de procesamiento a una carpeta desde la ficha Propiedades del recurso](assets/folder-properties-processing-profile.png)

>[!TIP]
>
>Solo se puede aplicar un perfil de procesamiento a una carpeta. Para generar más representaciones, agregue más definiciones de representación al perfil de procesamiento existente.

Después de aplicar un perfil de procesamiento a una carpeta, todos los recursos nuevos cargados (o actualizados) en esta carpeta o en cualquiera de sus subcarpetas se procesan con el perfil de procesamiento adicional configurado. Este procesamiento se suma al perfil predeterminado estándar.

>[!NOTE]
>
>Un perfil de procesamiento aplicado a una carpeta funciona para todo el árbol, pero se puede sobrescribir con otro perfil aplicado a una subcarpeta. Cuando se cargan recursos en una carpeta, el Experience Manager comprueba si hay un perfil de procesamiento en las propiedades de la carpeta contenedora. Si no se aplica ninguno, se comprueba la existencia de un perfil de procesamiento en una carpeta principal de la jerarquía.

Para comprobar que los recursos se procesan, previsualización las representaciones generadas en la vista [!UICONTROL Representaciones] del carril izquierdo. Abra la previsualización de recursos y abra el carril izquierdo para acceder a la vista **[!UICONTROL Representaciones]** . Las representaciones específicas del perfil de procesamiento, para las que el tipo de recurso específico coincide con las reglas de inclusión de tipo MIME, deben ser visibles y accesibles.

![representaciones adicionales](assets/renditions-additional-renditions.png)

*Figura: Ejemplo de dos representaciones adicionales generadas por un perfil de procesamiento aplicado a la carpeta principal.*

## Flujos de trabajo posteriores al procesamiento {#post-processing-workflows}

En el caso de que sea necesario un procesamiento adicional de los recursos que no se pueda lograr con los perfiles de procesamiento, se pueden agregar flujos de trabajo adicionales posteriores al procesamiento a la configuración. Esto permite agregar un procesamiento totalmente personalizado además del procesamiento configurable mediante microservicios de recursos.

Los flujos de trabajo posteriores al procesamiento, si se configuran, son ejecutados automáticamente por AEM una vez finalizado el procesamiento de los microservicios. No es necesario agregar los iniciadores de flujo de trabajo manualmente para activarlos. Los ejemplos incluyen:

* Pasos personalizados del flujo de trabajo para procesar recursos.
* Integraciones para agregar metadatos o propiedades a recursos de sistemas externos, por ejemplo, información de productos o procesos.
* Procesamiento adicional realizado por servicios externos.

Añadir una configuración de flujo de trabajo posterior al procesamiento en Experience Manager consta de los siguientes pasos:

* Cree uno o varios modelos de flujo de trabajo. Los documentos lo mencionan como modelos *de flujo de trabajo de* postprocesamiento, pero son modelos de flujo de trabajo de Experience Manager habituales.
* Añada pasos específicos del flujo de trabajo a estos modelos. Los pasos se ejecutan en los recursos según una configuración de modelo de flujo de trabajo.
* Añadir paso de proceso [!UICONTROL completado de actualización de recursos de] DAM al final. Añadir este paso garantiza que el Experience Manager sabe cuándo finaliza el procesamiento y el recurso se puede marcar como procesado, es decir, *Nuevo* se muestra en el recurso.
* Cree una configuración para el servicio de ejecución de flujo de trabajo personalizado que permita configurar la ejecución de un modelo de flujo de trabajo posterior al procesamiento mediante una ruta (ubicación de carpeta) o una expresión normal.

### Crear modelos de flujo de trabajo posteriores al procesamiento {#create-post-processing-workflow-models}

Los modelos de flujo de trabajo de postprocesamiento son modelos AEM de flujo de trabajo habituales. Cree distintos modelos si necesita un procesamiento diferente para distintas ubicaciones de repositorio o tipos de recursos.

Los pasos de procesamiento deben agregarse en función de las necesidades. Puede utilizar los pasos admitidos disponibles, así como cualquier paso de flujo de trabajo personalizado.

Asegúrese de que el último paso de cada flujos de trabajo posterior al procesamiento sea `DAM Update Asset Workflow Completed Process`. El último paso ayuda a garantizar que el Experience Manager sepa cuándo se completa el procesamiento de recursos.

### Configurar la ejecución del flujo de trabajo posterior al procesamiento {#configure-post-processing-workflow-execution}

Para configurar los modelos de flujo de trabajo posteriores al procesamiento que se van a ejecutar para los recursos cargados o actualizados en el sistema una vez finalizado el procesamiento de los microservicios de recursos, es necesario configurar el servicio de ejecución de flujo de trabajo personalizado.

El servicio Ejecutor de flujo de trabajo personalizado (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) es un servicio OSGi y proporciona dos opciones de configuración:

* Flujos de trabajo posteriores al procesamiento por ruta (`postProcWorkflowsByPath`): Se pueden enumerar varios modelos de flujo de trabajo, basados en diferentes rutas de repositorio. Las rutas y los modelos deben separarse con dos puntos. Se admiten rutas de repositorio simples que deben asignarse a un modelo de flujo de trabajo en la `/var` ruta. Por ejemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flujos de trabajo posteriores al procesamiento por expresión (`postProcWorkflowsByExpression`): Se pueden enumerar varios modelos de flujo de trabajo, basados en diferentes expresiones regulares. Las expresiones y los modelos deben separarse con dos puntos. La expresión regular debe apuntar directamente al nodo Recurso y no a una de las representaciones o archivos. Por ejemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>La configuración del Ejecutor de flujo de trabajo personalizado es una configuración de un servicio OSGi. Consulte [Implementación en Experience Manager](/help/implementing/deploying/overview.md) para obtener información sobre cómo implementar una configuración OSGi.
>La consola web OSGi, a diferencia de las implementaciones de servicios locales y gestionados de AEM, no está disponible directamente en las implementaciones de servicios en la nube.

Para obtener más información sobre qué paso de flujo de trabajo estándar se puede utilizar en el flujo de trabajo posterior al procesamiento, consulte los pasos de [flujo de trabajo en el flujo de trabajo](developer-reference-material-apis.md#post-processing-workflows-steps) posterior al procesamiento en la referencia del desarrollador.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* Tenga en cuenta sus necesidades para todos los tipos de representaciones al diseñar flujos de trabajo. Si no prevé la necesidad de una representación en el futuro, elimine el paso de creación del flujo de trabajo. Las representaciones no se pueden eliminar de forma masiva posteriormente. Las representaciones no deseadas pueden ocupar mucho espacio en almacenamiento después de un uso prolongado de [!DNL Experience Manager]. Para recursos individuales, puede quitar las representaciones manualmente de la interfaz de usuario. En el caso de varios recursos, puede personalizar [!DNL Experience Manager] para eliminar representaciones específicas o eliminar los recursos y cargarlos de nuevo.
* Actualmente, la compatibilidad está limitada a la generación de representaciones. No se admite la generación de recursos nuevos.

>[!MORELIKETHIS]
>
>* [Introducción al servicio](https://docs.adobe.com/content/help/en/asset-compute/using/introduction.html)de cómputo de recursos.
>* [Comprenda la extensibilidad y cuándo utilizarla](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html).
>* [Cómo crear aplicaciones](https://docs.adobe.com/content/help/en/asset-compute/using/extend/develop-custom-application.html)personalizadas.
>* [Tipos MIME admitidos para varios casos](/help/assets/file-format-support.md)de uso.


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
