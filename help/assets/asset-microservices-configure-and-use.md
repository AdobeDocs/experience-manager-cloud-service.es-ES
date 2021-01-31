---
title: Configuración y uso de microservicios de recursos
description: Configure y utilice los microservicios de recursos nativos de la nube para procesar los recursos a escala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 57ae02b90d1e78e8a940b65d195bc2077feec2d2
workflow-type: tm+mt
source-wordcount: '2576'
ht-degree: 1%

---


# Utilizar microservicios de recursos y perfiles de procesamiento {#get-started-using-asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante aplicaciones nativas de la nube (también denominadas trabajadores). Adobe gestiona los servicios para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento.

Los microservicios de recursos le permiten procesar una [amplia gama de tipos de archivos](/help/assets/file-format-support.md) que cubren más formatos predeterminados que los posibles con versiones anteriores de [!DNL Experience Manager]. Por ejemplo, ahora es posible la extracción en miniatura de los formatos PSD y PSB que anteriormente requerían soluciones de terceros como ImageMagick.

El procesamiento de recursos depende de la configuración de **[!UICONTROL Perfiles de procesamiento]**. Experience Manager proporciona una configuración predeterminada básica y permite a los administradores agregar una configuración de procesamiento de recursos más específica. Los administradores crean, mantienen y modifican las configuraciones de los flujos de trabajo posteriores al procesamiento, incluida la personalización opcional. La personalización de los flujos de trabajo permite a los desarrolladores ampliar la oferta predeterminada.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Una vista de alto nivel del ](assets/asset-microservices-flow.png "procesamiento de recursosUna vista de alto nivel del procesamiento de recursos")

>[!NOTE]
>
>El procesamiento de recursos descrito aquí reemplaza el modelo de flujo de trabajo `DAM Update Asset` que existe en las versiones anteriores de [!DNL Experience Manager]. La mayoría de los pasos de generación de representación estándar y relacionados con los metadatos se sustituyen por el procesamiento de los microservicios de recursos y los pasos restantes, si los hay, se pueden reemplazar por la configuración del flujo de trabajo posterior al procesamiento.

## Comprender las opciones de procesamiento de recursos {#get-started}

Experience Manager permite los siguientes niveles de procesamiento.

| Opción | Descripción | Casos de uso cubiertos |
|---|---|---|
| [Configuración predeterminada](#default-config) | Está disponible tal cual y no se puede modificar. Esta configuración proporciona una capacidad de generación de representaciones muy básica. | <ul> <li>Miniaturas estándar utilizadas por la interfaz de usuario [!DNL Assets] (48, 140 y 319 píxeles) </li> <li> Previsualización grande (representación web: 1280 píxeles) </li><li> Metadatos y extracción de texto.</li></ul> |
| [Configuración personalizada](#standard-config) | Configurado por los administradores mediante la interfaz de usuario. Proporciona más opciones para la generación de representaciones ampliando la opción predeterminada. Amplíe la opción lista para usar para proporcionar diferentes formatos y representaciones. | <ul><li>Representación de FPO. </li> <li>Cambiar el formato de archivo y la resolución de las imágenes</li> <li> Se aplica condicionalmente a los tipos de archivo configurados. </li> </ul> |
| [Perfil personalizado](#custom-config) | Configurados por los administradores mediante la interfaz de usuario para utilizar código personalizado a través de aplicaciones personalizadas para llamar al [servicio de Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). Admite requisitos más complejos en un método escalable y nativo de la nube. | Consulte [casos de uso permitidos](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formatos de archivo compatibles {#supported-file-formats}

Los microservicios de recursos admiten una amplia variedad de formatos de archivo para procesar, generar representaciones o extraer metadatos. Consulte [formatos de archivo admitidos](file-format-support.md) para obtener la lista completa de los tipos MIME y la funcionalidad admitida para cada tipo.

## Configuración predeterminada {#default-config}

Algunos valores predeterminados están preconfigurados para garantizar que las representaciones predeterminadas necesarias en Experience Manager están disponibles. La configuración predeterminada también garantiza que las operaciones de extracción de metadatos y extracción de texto estén disponibles. Los usuarios pueden cargar o actualizar los recursos de forma inmediata con inicio y el procesamiento básico está disponible de forma predeterminada.

Con la configuración predeterminada, solo se configura el perfil de procesamiento más básico. Este perfil de procesamiento no está visible en la interfaz de usuario y no se puede modificar. Siempre se ejecuta para procesar los recursos cargados. Este perfil de procesamiento predeterminado garantiza que el procesamiento básico requerido por [!DNL Experience Manager] se complete en todos los recursos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configuración estándar {#standard-config}

[!DNL Experience Manager] ofrece capacidades para generar representaciones más específicas para formatos comunes según las necesidades del usuario. Un administrador puede crear [!UICONTROL Perfiles de procesamiento] adicionales para facilitar la creación de dichas representaciones. A continuación, los usuarios asignan una o varias de las perfiles disponibles a carpetas específicas para realizar el procesamiento adicional. Por ejemplo, el procesamiento adicional puede generar representaciones para web, móvil y tablet. El siguiente vídeo muestra cómo crear y aplicar [!UICONTROL Perfiles de procesamiento] y cómo acceder a las representaciones creadas.

* **Ancho y altura** de representación: La especificación de anchura y altura de representación proporciona los tamaños máximos de la imagen de salida generada. Los microservicios de recursos intentan producir la representación más grande posible, cuya anchura y altura no superan la anchura y la altura especificadas, respectivamente. Se conserva la relación de aspecto, que es la misma que la original. Un valor vacío significa que el procesamiento de recursos asume la dimensión de píxeles del original.

* **Reglas** de inclusión de tipo MIME: Cuando se procesa un recurso con un tipo MIME específico, se comprueba primero el tipo MIME con el valor de tipos MIME excluidos para la especificación de representación. Si coincide con esa lista, esta representación específica no se genera para el recurso (lista de bloqueados). De lo contrario, el tipo MIME se compara con el tipo MIME incluido y, si coincide con la lista, se genera la representación (lista de permitidos).

* **Representación** especial de FPO: Al colocar recursos de gran tamaño  [!DNL Experience Manager] en  [!DNL Adobe InDesign] documentos, un profesional creativo espera mucho tiempo después de  [colocar un recurso](https://helpx.adobe.com/indesign/using/placing-graphics.html). Mientras tanto, el usuario no puede utilizar [!DNL InDesign]. Esto interrumpe el flujo creativo y afecta negativamente a la experiencia del usuario. Adobe permite colocar temporalmente representaciones de pequeño tamaño en documentos [!DNL InDesign] para empezar, que se pueden reemplazar con recursos de resolución completa bajo demanda más adelante. [!DNL Experience Manager] proporciona representaciones que se utilizan únicamente para la colocación (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño pero tienen la misma proporción de aspecto.

El perfil de procesamiento puede incluir una representación FPO (solo para ubicación). Consulte [!DNL Adobe Asset Link] [documentación](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) para saber si necesita activarla para su perfil de procesamiento. Para obtener más información, consulte la [documentación completa de Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html).

### Crear un perfil estándar {#create-standard-profile}

Para crear un perfil de procesamiento estándar, siga estos pasos:

1. Los administradores acceden a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de procesamiento]**. Haga clic en **[!UICONTROL Crear]**.
1. Proporcione un nombre que le ayude a identificar de forma exclusiva el perfil al aplicarlo a una carpeta.
1. Para generar representaciones de FPO, en la ficha **[!UICONTROL Standard]**, habilite **[!UICONTROL Crear representación de FPO]**. Introduzca un valor **[!UICONTROL Quality]** entre 1 y 100.
1. Para generar otras representaciones, haga clic en **[!UICONTROL Añadir nuevo]** y proporcione la siguiente información:

   * Nombre de archivo de cada representación.
   * Formato de archivo (PNG, JPEG, GIF o WebP) de cada representación.
   * Anchura y altura en píxeles de cada representación. Si no se especifican los valores, se utiliza el tamaño de píxel completo de la imagen original.
   * Calidad en porcentaje de cada representación JPEG y WebP.
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

El [!DNL Asset Compute Service] admite una variedad de casos de uso como el procesamiento predeterminado, el procesamiento de formatos específicos de Adobe como archivos Photoshop y la implementación de procesamiento personalizado o específico de la organización. La personalización del flujo de trabajo de recursos de actualización de DAM necesaria en el pasado se gestiona automáticamente o mediante la configuración de perfiles de procesamiento. Si estas opciones de procesamiento no satisfacen las necesidades comerciales, Adobe recomienda desarrollar y utilizar [!DNL Asset Compute Service] para ampliar las capacidades predeterminadas. Para obtener información general, consulte [comprender la extensibilidad y cuándo utilizarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>Adobe recomienda utilizar una aplicación personalizada únicamente cuando los requisitos comerciales no se puedan cumplir con las configuraciones predeterminadas o con el perfil estándar.

Puede transformar formatos de imagen, vídeo, documento y otros archivos en distintas representaciones, incluidas miniaturas, texto extraído y metadatos, y archivos.

Los desarrolladores pueden utilizar [!DNL Asset Compute Service] para [crear aplicaciones personalizadas](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) para los casos de uso admitidos. [!DNL Experience Manager] Puede llamar a estas aplicaciones personalizadas desde la interfaz de usuario mediante perfiles personalizados que los administradores configuran. [!DNL Asset Compute Service] admite los siguientes casos de uso de invocar servicios externos:

* Utilice la [!DNL Adobe Photoshop] [API de ImageCutout](https://github.com/AdobeDocs/photoshop-api-docs-pre-release#imagecutout) y guarde el resultado como representación.
* Llame a sistemas de terceros para actualizar los datos, por ejemplo, un sistema PIM.
* Utilice la API [!DNL Photoshop] para generar diversas representaciones basadas en la plantilla de Photoshop.
* Utilice [API de Lightroom de Adobe](https://github.com/AdobeDocs/lightroom-api-docs#supported-features) para optimizar los recursos ingestados y guardarlos como representaciones.

>[!NOTE]
>
>No se pueden editar los metadatos estándar con las aplicaciones personalizadas. Solo puede modificar metadatos personalizados.

### Crear un perfil personalizado {#create-custom-profile}

Para crear un perfil personalizado, siga estos pasos:

1. Los administradores acceden a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de procesamiento]**. Haga clic en **[!UICONTROL Crear]**.
1. Haga clic en la ficha **[!UICONTROL Personalizado]**. Haga clic en **[!UICONTROL Añadir nuevo]**. Proporcione el nombre de archivo que desee para la representación.
1. Proporcione la siguiente información.

   * Nombre de archivo de cada representación y extensión de archivo admitida.
   * [URL de punto final de una aplicación](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html) personalizada de Firefly. La aplicación debe pertenecer a la misma organización que la cuenta de Experience Manager.
   * Añada Parámetros de servicio para [pasar información o parámetros adicionales a la aplicación personalizada](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * Se han incluido y excluido tipos MIME para limitar el procesamiento a unos pocos formatos de archivo específicos.

   Haga clic en **[!UICONTROL Guardar]**.

Las aplicaciones personalizadas son aplicaciones [Project Firefly](https://github.com/AdobeDocs/project-firefly) sin encabezado. La aplicación personalizada obtiene todos los archivos proporcionados si están configurados con un perfil de procesamiento. La aplicación debe filtrar los archivos.

>[!CAUTION]
>
>Si la aplicación Firefly y la cuenta [!DNL Experience Manager] no pertenecen a la misma organización, la integración no funcionará.

### Un ejemplo de un perfil personalizado {#custom-profile-example}

Para ilustrar el uso personalizado del perfil, consideremos un caso de uso para aplicar texto personalizado a las imágenes de campaña. Puede crear un perfil de procesamiento que aproveche la API de Photoshop para editar las imágenes.

La integración del servicio de asset compute permite al Experience Manager pasar estos parámetros a la aplicación personalizada mediante el campo [!UICONTROL Parámetros de servicio]. La aplicación personalizada llama a la API de Photoshop y pasa estos valores a la API. Por ejemplo, puede pasar el nombre de la fuente, el color del texto, el peso del texto y el tamaño del texto para agregar el texto personalizado a las imágenes de campaña.

<!-- TBD: Check screenshot against the interface. -->

![custom-processing-perfil](assets/custom-processing-profile.png)

*Figura: Utilice  [!UICONTROL Service ] Parametersfield para pasar información agregada a los parámetros predefinidos integrados en la aplicación personalizada. En este ejemplo, cuando se cargan imágenes de campaña, las imágenes se actualizan con `Jumanji` texto en `Arial-BoldMT` font.*

## Utilice perfiles de procesamiento para procesar los recursos {#use-profiles}

Cree y aplique los perfiles de procesamiento personalizados adicionales a carpetas específicas para que el Experience Manager pueda procesarlos para los recursos cargados o actualizados en estas carpetas. El perfil de procesamiento estándar predeterminado e integrado siempre se ejecuta, pero no es visible en la interfaz de usuario. Si agrega un perfil personalizado, se utilizan ambos perfiles para procesar los recursos cargados.

Aplique perfiles de procesamiento a las carpetas mediante uno de los siguientes métodos:

* Los administradores pueden seleccionar una definición de perfil de procesamiento en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de procesamiento]** y utilizar la acción **[!UICONTROL Aplicar Perfil a las carpetas]**. Abre un navegador de contenido que le permite desplazarse a carpetas específicas, seleccionarlas y confirmar la aplicación del perfil.
* Los usuarios pueden seleccionar una carpeta en la interfaz de usuario de Recursos, utilizar la acción **[!UICONTROL Propiedades]** para abrir la pantalla de propiedades de la carpeta, hacer clic en la ficha **[!UICONTROL Perfiles de procesamiento]** y, en la lista emergente, seleccionar el perfil de procesamiento correspondiente para esa carpeta. Para guardar los cambios, haga clic en **[!UICONTROL Guardar y cerrar]**.
   ![Aplicar perfil de procesamiento a una carpeta desde la ficha Propiedades del recurso](assets/folder-properties-processing-profile.png)

>[!TIP]
>
>Solo se puede aplicar un perfil de procesamiento a una carpeta. Para generar más representaciones, agregue más definiciones de representación al perfil de procesamiento existente.

Después de aplicar un perfil de procesamiento a una carpeta, todos los recursos nuevos cargados (o actualizados) en esta carpeta o en cualquiera de sus subcarpetas se procesan con el perfil de procesamiento adicional configurado. Este procesamiento se suma al perfil predeterminado estándar.

>[!NOTE]
>
>Un perfil de procesamiento aplicado a una carpeta funciona para todo el árbol, pero se puede sobrescribir con otro perfil aplicado a una subcarpeta. Cuando se cargan recursos en una carpeta, el Experience Manager comprueba si hay un perfil de procesamiento en las propiedades de la carpeta contenedora. Si no se aplica ninguno, se comprueba la existencia de un perfil de procesamiento en una carpeta principal de la jerarquía.

Para comprobar que los recursos se procesan, previsualización las representaciones generadas en la vista [!UICONTROL Representaciones] en el carril izquierdo. Abra la previsualización de recursos y abra el carril izquierdo para acceder a la vista **[!UICONTROL Representaciones]**. Las representaciones específicas del perfil de procesamiento, para las que el tipo de recurso específico coincide con las reglas de inclusión de tipo MIME, deben ser visibles y accesibles.

![representaciones adicionales](assets/renditions-additional-renditions.png)

*Figura: Ejemplo de dos representaciones adicionales generadas por un perfil de procesamiento aplicado a la carpeta principal.*

## Flujos de trabajo posteriores al procesamiento {#post-processing-workflows}

En una situación en la que se requiere un procesamiento adicional de los recursos que no se puede lograr con los perfiles de procesamiento, se pueden agregar flujos de trabajo adicionales posteriores al procesamiento a la configuración. Esto permite agregar un procesamiento totalmente personalizado además del procesamiento configurable mediante microservicios de recursos.

Los flujos de trabajo posteriores al procesamiento, si se configuran, son ejecutados automáticamente por [!DNL Experience Manager] una vez finalizado el procesamiento de los microservicios. No es necesario agregar iniciadores de flujo de trabajo manualmente para déclencheur de los flujos de trabajo. Los ejemplos incluyen:

* Pasos personalizados del flujo de trabajo para procesar recursos.
* Integraciones para agregar metadatos o propiedades a recursos de sistemas externos, por ejemplo, información de productos o procesos.
* Procesamiento adicional realizado por servicios externos.

Para agregar una configuración de flujo de trabajo posterior al procesamiento a [!DNL Experience Manager], siga estos pasos:

* Cree uno o varios modelos de flujo de trabajo. Estos modelos personalizados se conocen como *modelos de flujo de trabajo posteriores al procesamiento* en esta documentación. Son modelos de flujo de trabajo [!DNL Experience Manager] normales.
* Añada los pasos necesarios del flujo de trabajo a estos modelos. Revise los pasos del flujo de trabajo predeterminado y agregue todos los pasos predeterminados necesarios al flujo de trabajo personalizado. Los pasos se ejecutan en los recursos según una configuración de modelo de flujo de trabajo. Por ejemplo, si desea que el etiquetado inteligente se produzca automáticamente tras la carga de recursos, agregue el paso al modelo de flujo de trabajo personalizado posterior al procesamiento.
* Añada el paso [!UICONTROL Flujo de trabajo completado de recursos de actualización de DAM] al final. Añadir este paso garantiza que el Experience Manager sepa cuándo finaliza el procesamiento y el recurso se puede marcar como procesado, es decir, *New* se muestra en el recurso.
* Cree una configuración para el servicio de ejecución de flujo de trabajo personalizado que permita configurar la ejecución de un modelo de flujo de trabajo posterior al procesamiento mediante una ruta (ubicación de carpeta) o una expresión normal.

### Crear modelos de flujo de trabajo posteriores al procesamiento {#create-post-processing-workflow-models}

Los modelos de flujo de trabajo posteriores al procesamiento son modelos de flujo de trabajo [!DNL Experience Manager] normales. Cree distintos modelos si necesita un procesamiento diferente para distintas ubicaciones de repositorio o tipos de recursos.

Los pasos de procesamiento deben agregarse en función de las necesidades. Puede utilizar los pasos admitidos disponibles, así como cualquier paso de flujo de trabajo personalizado.

Asegúrese de que el último paso de cada flujos de trabajo posterior al procesamiento sea `DAM Update Asset Workflow Completed Process`. El último paso ayuda a garantizar que el Experience Manager sepa cuándo se completa el procesamiento de recursos.

### Configurar la ejecución del flujo de trabajo posterior al procesamiento {#configure-post-processing-workflow-execution}

Para configurar los modelos de flujo de trabajo posteriores al procesamiento que se van a ejecutar para los recursos cargados o actualizados en el sistema una vez finalizado el procesamiento de los microservicios de recursos, es necesario configurar el servicio de ejecución de flujo de trabajo personalizado.

El Ejecutor de flujo de trabajo personalizado de Adobe CQ DAM (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) es un servicio OSGi y proporciona dos opciones de configuración:

* Flujos de trabajo posteriores al procesamiento por ruta (`postProcWorkflowsByPath`): Se pueden enumerar varios modelos de flujo de trabajo, basados en diferentes rutas de repositorio. Las rutas y los modelos deben separarse con dos puntos. Se admiten rutas de repositorio simples que deben asignarse a un modelo de flujo de trabajo en la ruta `/var`. Por ejemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flujos de trabajo posteriores al procesamiento por expresión (`postProcWorkflowsByExpression`): Se pueden enumerar varios modelos de flujo de trabajo, basados en diferentes expresiones regulares. Las expresiones y los modelos deben separarse con dos puntos. La expresión regular debe apuntar directamente al nodo Recurso y no a una de las representaciones o archivos. Por ejemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>La configuración del Ejecutor de flujo de trabajo personalizado es una configuración de un servicio OSGi. Consulte [implementación en Experience Manager](/help/implementing/deploying/overview.md) para obtener información sobre cómo implementar una configuración OSGi.
>La consola web OSGi, a diferencia de las implementaciones de servicios locales y administrados de [!DNL Experience Manager], no está disponible directamente en las implementaciones de servicios en la nube.

Para obtener más información sobre qué paso de flujo de trabajo estándar se puede utilizar en el flujo de trabajo posterior al procesamiento, consulte [pasos de flujo de trabajo en el flujo de trabajo posterior al procesamiento](developer-reference-material-apis.md#post-processing-workflows-steps) en la referencia del desarrollador.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* Tenga en cuenta sus necesidades para todos los tipos de representaciones al diseñar flujos de trabajo. Si no prevé la necesidad de una representación en el futuro, elimine el paso de creación del flujo de trabajo. Las representaciones no se pueden eliminar de forma masiva posteriormente. Las representaciones no deseadas pueden ocupar mucho espacio en almacenamiento después de un uso prolongado de [!DNL Experience Manager]. Para recursos individuales, puede quitar las representaciones manualmente de la interfaz de usuario. Para varios recursos, puede personalizar [!DNL Experience Manager] para eliminar representaciones específicas o eliminar los recursos y volver a cargarlos.
* Actualmente, la compatibilidad está limitada a la generación de representaciones. No se admite la generación de recursos nuevos.
* Actualmente, el límite de tamaño de archivo para la extracción de metadatos es de aproximadamente 10 GB. Al cargar recursos muy grandes, a veces falla la operación de extracción de metadatos.

>[!MORELIKETHIS]
>
>* [Introducción al servicio](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html) de Asset compute.
>* [Comprenda la extensibilidad y cuándo utilizarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [Cómo crear aplicaciones](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) personalizadas.
>* [Tipos MIME admitidos para varios casos](/help/assets/file-format-support.md) de uso.


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
