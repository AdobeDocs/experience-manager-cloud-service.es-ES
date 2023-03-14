---
title: Configuración y uso de microservicios de recursos
description: Configure y utilice los microservicios de recursos nativos de la nube para procesar recursos a escala.
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Asset Processing
role: Architect,Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 5545cd1739db41dbabf06cff916811123e7e09be
workflow-type: tm+mt
source-wordcount: '2902'
ht-degree: 3%

---

# Uso de microservicios de recursos y perfiles de procesamiento {#get-started-using-asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante aplicaciones nativas de la nube (también denominadas trabajadores). Adobe administra los servicios para un manejo óptimo de diferentes tipos de recursos y opciones de procesamiento.

Los microservicios de recursos le permiten procesar una [amplia gama de tipos de archivos](/help/assets/file-format-support.md) que cubren más formatos listos para usar que los posibles de las versiones anteriores de [!DNL Experience Manager]. Por ejemplo, ahora es posible extraer miniaturas de los formatos PSD y PSB, pero se requerían soluciones de terceros como [!DNL ImageMagick].

El procesamiento de recursos depende de la configuración de **[!UICONTROL Perfiles de procesamiento]**. Experience Manager proporciona una configuración predeterminada básica y permite que los administradores agreguen configuraciones de procesamiento de recursos más específicas. Los administradores crean, mantienen y modifican las configuraciones de flujos de trabajo posteriores al procesamiento, incluida la personalización opcional. La personalización de los flujos de trabajo permite a los desarrolladores ampliar la oferta predeterminada.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Una vista de alto nivel del procesamiento de recursos](assets/asset-microservices-flow.png "Una vista de alto nivel del procesamiento de recursos")

>[!NOTE]
>
>El procesamiento de recursos que se describe aquí reemplaza a `DAM Update Asset` modelo de flujo de trabajo que existe en versiones anteriores de [!DNL Experience Manager]. La mayoría de los pasos estándar relacionados con la generación de representaciones y los metadatos se sustituyen por el procesamiento de microservicios de recursos y los pasos restantes, si los hay, se pueden reemplazar por la configuración del flujo de trabajo posterior al procesamiento.

## Comprender las opciones de procesamiento de recursos {#get-started}

[!DNL Experience Manager] permite los siguientes niveles de procesamiento.

| Opción | Descripción | Casos de uso cubiertos |
|---|---|---|
| [Configuración predeterminada](#default-config) | Está disponible tal cual y no se puede modificar. Esta configuración proporciona una capacidad de generación de representaciones muy básica. | <ul> <li>Miniaturas estándar utilizadas por [!DNL Assets] interfaz de usuario (48, 140 y 319 píxeles) </li> <li> Vista previa grande (representación web: 1280 píxeles) </li><li> Extracción de metadatos y texto.</li></ul> |
| [Configuración personalizada](#standard-config) | Configurado por los administradores mediante la interfaz de usuario de. Proporciona más opciones para la generación de representaciones al ampliar la opción predeterminada. Amplíe la opción predeterminada para proporcionar diferentes formatos y representaciones. | <ul><li>Representación de FPO. </li> <li>Cambiar el formato de archivo y la resolución de las imágenes</li> <li> Aplicar condicionalmente a los tipos de archivo configurados. </li> </ul> |
| [Perfil personalizado](#custom-config) | Configurado por los administradores mediante la interfaz de usuario para utilizar código personalizado mediante aplicaciones personalizadas para llamar a [Servicio de asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). Admite requisitos más complejos en un método nativo y escalable de la nube. | Consulte [casos de uso permitidos](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formatos de archivo compatibles {#supported-file-formats}

Los microservicios de recursos son compatibles con una amplia variedad de formatos de archivo para procesar, generar representaciones o extraer metadatos. Consulte [formatos de archivo compatibles](file-format-support.md) para obtener la lista completa de tipos MIME y la funcionalidad admitida para cada tipo.

## Configuración predeterminada {#default-config}

Algunos valores predeterminados están preconfigurados para garantizar que las representaciones predeterminadas requeridas en Experience Manager estén disponibles. La configuración predeterminada también garantiza que las operaciones de extracción de metadatos y extracción de texto estén disponibles. Los usuarios pueden empezar a cargar o actualizar recursos inmediatamente y el procesamiento básico está disponible de forma predeterminada.

Con la configuración predeterminada, solo se configura el perfil de procesamiento más básico. Este perfil de procesamiento no es visible en la interfaz de usuario y no se puede modificar. Siempre se ejecuta para procesar los recursos cargados. Este perfil de procesamiento predeterminado garantiza que el procesamiento básico requerido por [!DNL Experience Manager] se completa en todos los recursos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configuración estándar {#standard-config}

[!DNL Experience Manager] proporcione funciones para generar representaciones más específicas para formatos comunes según las necesidades del usuario. Un administrador puede crear más [!UICONTROL Perfiles de procesamiento] para facilitar la creación de la representación. A continuación, asigne uno o más perfiles disponibles a carpetas específicas para realizar el procesamiento adicional. Por ejemplo, el procesamiento adicional puede generar representaciones para la web, dispositivos móviles y tabletas. El siguiente vídeo ilustra cómo crear y aplicar [!UICONTROL Perfiles de procesamiento] y cómo acceder a las representaciones creadas.

* **Anchura y altura de representación**: la especificación de anchura y altura de la representación proporciona los tamaños máximos de la imagen de salida generada. Los microservicios de recursos intentan producir la representación más grande posible, cuya anchura y altura no son mayores que la anchura y altura especificadas, respectivamente. Se conserva la relación de aspecto, es decir, la misma que la original. Un valor vacío significa que el procesamiento de recursos supone la dimensión en píxeles del original.

* **Reglas de inclusión de tipo MIME**: Cuando se procesa un recurso con un tipo MIME específico, el tipo MIME se comprueba primero con el valor de tipos MIME excluidos para la especificación de representación. Si coincide con esa lista, esta representación específica no se genera para el recurso (lista de bloqueados). De lo contrario, el tipo MIME se comprueba con el tipo MIME incluido y, si coincide con la lista, se genera la representación (lista de permitidos).

* **Representación especial de FPO**: Al colocar recursos de gran tamaño desde [!DNL Experience Manager] en [!DNL Adobe InDesign] documentos, un profesional creativo espera un tiempo considerable después de que [colocar un recurso](https://helpx.adobe.com/indesign/using/placing-graphics.html). Mientras tanto, se bloquea al usuario el uso de [!DNL InDesign]. Esto interrumpe el flujo creativo y afecta negativamente a la experiencia del usuario. El Adobe permite colocar temporalmente representaciones de pequeño tamaño en [!DNL InDesign] documentos para empezar, que se pueden reemplazar con recursos de resolución completa bajo demanda más adelante. [!DNL Experience Manager] proporciona representaciones que se utilizan solo para ubicación (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño, pero son de la misma proporción de aspecto.

El perfil de procesamiento puede incluir una representación de FPO (solo para ubicación). Consulte [!DNL Adobe Asset Link] [documentación](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) para saber si debe activarlo para el perfil de procesamiento. Para obtener más información, consulte [Documentación completa de Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html).

### Creación de un perfil estándar {#create-standard-profile}

Para crear un perfil de procesamiento estándar, siga estos pasos:

1. Acceso de administradores **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de procesamiento]**. Haga clic en **[!UICONTROL Crear]**.
1. Proporcione un nombre que le ayude a identificar el perfil de forma exclusiva al aplicarlo a una carpeta.
1. Para generar representaciones de FPO, en **[!UICONTROL Imagen]** pestaña, habilitar **[!UICONTROL Crear representación de FPO]**. Entrada a **[!UICONTROL Calidad]** valor entre 1 y 100.
1. Para generar otras representaciones, haga clic en **[!UICONTROL Añadir nuevo]** y proporcione la siguiente información:

   * Nombre de archivo de cada representación.
   * Formato de archivo (PNG, JPEG, GIF o WebP) de cada representación.
   * Anchura y altura en píxeles de cada representación. Si no se especifican los valores, se utiliza el tamaño de píxel completo de la imagen original.
   * Calidad en porcentaje de cada JPEG y representación WebP.
   * Se han incluido y excluido tipos MIME para definir la aplicabilidad de un perfil.

   ![processing-profiles-adding](assets/processing-profiles-image.png)

1. Haga clic en **[!UICONTROL Guardar]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Casos de uso y perfil personalizados {#custom-config}

El [!DNL Asset Compute Service] admite una variedad de casos de uso, como procesamiento predeterminado, procesamiento de formatos específicos del Adobe, como archivos Photoshop, e implementación de procesamiento personalizado o específico de la organización. La personalización del flujo de trabajo de recursos de actualización de DAM requerida en el pasado se gestiona automáticamente o mediante la configuración de perfiles de procesamiento. Si estas opciones de procesamiento no satisfacen las necesidades empresariales, Adobe recomienda desarrollar y utilizar [!DNL Asset Compute Service] para ampliar las funciones predeterminadas. Para obtener una descripción general, consulte [comprender la extensibilidad y cuándo utilizarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>Adobe recomienda utilizar una aplicación personalizada solo cuando no se puedan cumplir los requisitos empresariales con las configuraciones predeterminadas o el perfil estándar.

Puede transformar los formatos de imagen, vídeo, documento y otros archivos en distintas representaciones, incluidas miniaturas, texto extraído y metadatos, y archivos.

Los desarrolladores pueden utilizar el [!DNL Asset Compute Service] hasta [creación de aplicaciones personalizadas](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) para los casos de uso admitidos. [!DNL Experience Manager] Puede llamar a estas aplicaciones personalizadas desde la interfaz de usuario mediante perfiles personalizados que configuran los administradores. [!DNL Asset Compute Service] admite los siguientes casos de uso de invocar servicios externos:

* Uso [!DNL Adobe Photoshop]de [API ImageCutout](https://developer.adobe.com/photoshop/photoshop-api-docs/) y guarde el resultado como representación.
* Llame a sistemas de terceros para actualizar datos como, por ejemplo, un sistema PIM.
* Uso [!DNL Photoshop] API para generar diversas representaciones basadas en la plantilla de Photoshop.
* Uso [API de Adobe Lightroom](https://developer.adobe.com/photoshop/photoshop-api-docs/) para optimizar los recursos ingeridos y guardarlos como representaciones.

>[!NOTE]
>
>No puede editar los metadatos estándar mediante las aplicaciones personalizadas. Solo puede modificar los metadatos personalizados.

### Creación de un perfil personalizado {#create-custom-profile}

Para crear un perfil personalizado, siga estos pasos:

1. Acceso de administradores **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de procesamiento]**. Haga clic en **[!UICONTROL Crear]**.
1. Clic **[!UICONTROL Personalizado]** pestaña. Clic **[!UICONTROL Añadir nuevo]**. Proporcione el nombre de archivo deseado para la representación.
1. Proporcione la siguiente información.

   * Nombre de archivo de cada representación y una extensión de archivo compatible.
   * [Dirección URL de punto final de una aplicación personalizada de App Builder](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html). La aplicación debe pertenecer a la misma organización que la cuenta de Experience Manager.
   * Añadir parámetros de servicio a [pasar información o parámetros adicionales a la aplicación personalizada](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * Se han incluido y excluido tipos MIME para limitar el procesamiento a algunos formatos de archivo específicos.

   Haga clic en **[!UICONTROL Guardar]**.

Las aplicaciones personalizadas no tienen encabezado [Generador de aplicaciones de proyecto](https://developer.adobe.com/app-builder/docs/overview/) aplicaciones. La aplicación personalizada obtiene todos los archivos proporcionados si se configuran con un perfil de procesamiento. La aplicación debe filtrar los archivos.

>[!CAUTION]
>
>Si la aplicación App Builder y [!DNL Experience Manager] Las cuentas de no son de la misma organización, la integración no funciona.

### Ejemplo de perfil personalizado {#custom-profile-example}

Para ilustrar el uso de un perfil personalizado, consideremos un caso de uso para aplicar texto personalizado a las imágenes de la campaña. Puede crear un perfil de procesamiento que aproveche la API de Photoshop para editar las imágenes.

La integración del servicio de asset compute permite al Experience Manager pasar estos parámetros a la aplicación personalizada mediante [!UICONTROL Parámetros de servicio] field. A continuación, la aplicación personalizada llama a la API de Photoshop y pasa estos valores a la API. Por ejemplo, puede pasar el nombre de la fuente, el color, el peso y el tamaño del texto para añadir el texto personalizado a las imágenes de campaña.

<!-- TBD: Check screenshot against the interface. -->

![custom-processing-profile](assets/custom-processing-profile.png)

*Imagen: uso [!UICONTROL Parámetros de servicio] para pasar información añadida a parámetros predefinidos creados en la aplicación personalizada. En este ejemplo, cuando se cargan imágenes de campaña, las imágenes se actualizan con `Jumanji` texto en `Arial-BoldMT` fuente.*

## Uso de perfiles de procesamiento para procesar recursos {#use-profiles}

Cree y aplique perfiles de procesamiento adicionales personalizados a carpetas específicas para que el Experience Manager los procese para los recursos cargados o actualizados en estas carpetas. El perfil de procesamiento estándar integrado y predeterminado siempre se ejecuta, pero no es visible en la interfaz de usuario. Si agrega un perfil personalizado, ambos perfiles se utilizan para procesar los recursos cargados.

Aplique perfiles de procesamiento a las carpetas mediante uno de los métodos siguientes:

* Los administradores pueden seleccionar una definición de perfil de procesamiento en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de procesamiento]** y utilice **[!UICONTROL Aplicar perfil a las carpetas]** acción. Se abre un explorador de contenido que le permite navegar a carpetas específicas, seleccionarlas y confirmar la aplicación del perfil.
* Los usuarios pueden seleccionar una carpeta en la interfaz de usuario de Assets; utilice **[!UICONTROL Propiedades]** acción para abrir la pantalla de propiedades de la carpeta, haga clic en **[!UICONTROL Procesamiento de recursos]** y en la pestaña [!UICONTROL Perfil de procesamiento] , seleccione el perfil de procesamiento adecuado para esa carpeta. Para guardar los cambios, haga clic en **[!UICONTROL Guardar y cerrar]**.
   ![Aplicar perfil de procesamiento a una carpeta desde la pestaña Propiedades del recurso](assets/folder-properties-processing-profile.png)

* Los usuarios pueden seleccionar carpetas o recursos específicos en la interfaz de usuario de Assets para aplicar un perfil de procesamiento y, a continuación, seleccionar ![icono de reprocesamiento de recursos](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL Volver a procesar recursos]** de las opciones disponibles en la parte superior.

>[!TIP]
>
>Solo se puede aplicar un perfil de procesamiento a una carpeta. Para generar más representaciones, agregue más definiciones de representación al perfil de procesamiento existente.

Después de aplicar un perfil de procesamiento a una carpeta, todos los recursos nuevos cargados (o actualizados) en esta o en cualquiera de sus subcarpetas se procesan con el perfil de procesamiento adicional configurado. Este procesamiento se suma al perfil predeterminado estándar.

>[!NOTE]
>
>Un perfil de procesamiento aplicado a una carpeta funciona para todo el árbol, pero se puede sobrescribir con otro perfil aplicado a una subcarpeta. Cuando los recursos se cargan en una carpeta, Experience Manager comprueba las propiedades de la carpeta contenedora para ver si hay un perfil de procesamiento. Si no se aplica ninguno, se comprueba la existencia de un perfil de procesamiento en una carpeta principal de la jerarquía.

Para comprobar que los recursos se procesan, previsualice las representaciones generadas en la [!UICONTROL Representaciones] vista en el carril izquierdo. Abra la previsualización de recursos y abra el carril izquierdo para acceder a **[!UICONTROL Representaciones]** vista. Las representaciones específicas en el perfil de procesamiento, para las que el tipo del recurso específico coincide con las reglas de inclusión de tipo MIME, deben ser visibles y accesibles.

![additional-renditions](assets/renditions-additional-renditions.png)

*Imagen: ejemplo de dos representaciones adicionales generadas por un perfil de procesamiento aplicado a la carpeta principal.*

## Flujos de trabajo de posprocesamiento {#post-processing-workflows}

En una situación en la que se requiera un procesamiento adicional de recursos que no se pueda lograr con los perfiles de procesamiento, se pueden agregar flujos de trabajo posteriores al procesamiento a la configuración. El posprocesamiento le permite agregar un procesamiento completamente personalizado sobre el procesamiento configurable mediante microservicios de recursos.

Flujos de trabajo de posprocesamiento o [Flujo de trabajo de inicio automático](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/auto-start-workflows.html), si está configurado, los ejecuta automáticamente [!DNL Experience Manager] una vez finalizado el procesamiento de los microservicios. No es necesario añadir manualmente iniciadores de flujo de trabajo para almacenar en déclencheur los flujos de trabajo. Los ejemplos incluyen:

* Pasos personalizados del flujo de trabajo para procesar recursos.
* Integraciones para añadir metadatos o propiedades a recursos de sistemas externos como, por ejemplo, información de productos o procesos.
* Procesamiento adicional realizado por servicios externos.

Para añadir una configuración de flujo de trabajo de posprocesamiento a [!DNL Experience Manager], siga estos pasos:

* Cree uno o varios modelos de flujo de trabajo. Estos modelos personalizados se denominan *modelos de flujo de trabajo de posprocesamiento* en esta documentación. Esos son regulares [!DNL Experience Manager] modelos de flujo de trabajo.
* Añada los pasos de flujo de trabajo necesarios a estos modelos. Revise los pasos del flujo de trabajo predeterminado y añada todos los pasos predeterminados necesarios al flujo de trabajo personalizado. Los pasos se ejecutan en los recursos en función de una configuración de modelo de flujo de trabajo. Por ejemplo, si desea que el etiquetado inteligente se produzca automáticamente al cargar el recurso, agregue el paso al modelo de flujo de trabajo de posprocesamiento personalizado.
* Añadir [!UICONTROL Proceso completado de flujo de trabajo de recursos de actualización DAM] paso al final. Añadir este paso garantiza que el Experience Manager sepa cuándo termina el procesamiento y que el recurso se pueda marcar como procesado, es decir, *Nuevo* se muestra en el recurso.
* Cree una configuración para el servicio de flujo de trabajo personalizado que permita configurar la ejecución de un modelo de flujo de trabajo de posprocesamiento por una ruta (ubicación de carpeta) o por una expresión regular.

Para obtener más información sobre qué paso del flujo de trabajo estándar se puede utilizar en el flujo de trabajo de posprocesamiento, consulte [pasos del flujo de trabajo en el flujo de trabajo de posprocesamiento](developer-reference-material-apis.md#post-processing-workflows-steps) en la referencia del desarrollador.

### Creación de modelos de flujo de trabajo de posprocesamiento {#create-post-processing-workflow-models}

Los modelos de flujo de trabajo de posprocesamiento son regulares [!DNL Experience Manager] modelos de flujo de trabajo. Cree diferentes modelos si necesita un procesamiento diferente para diferentes ubicaciones de repositorios o tipos de recursos.

Los pasos de procesamiento se añaden según sea necesario. Puede utilizar tanto los pasos compatibles disponibles como cualquier paso del flujo de trabajo implementado de forma personalizada.

Asegúrese de que el último paso de cada flujo de trabajo de posprocesamiento sea `DAM Update Asset Workflow Completed Process`. El último paso ayuda a garantizar que el Experience Manager sepa cuándo se completa el procesamiento de recursos.

### Configuración de la ejecución del flujo de trabajo posterior al procesamiento {#configure-post-processing-workflow-execution}

Una vez que los microservicios de recursos completen el procesamiento de los recursos cargados, puede definir un flujo de trabajo de posprocesamiento para procesar aún más los recursos. Para configurar el posprocesamiento mediante modelos de flujo de trabajo, puede realizar una de las siguientes acciones:

* [Aplicar un modelo de flujo de trabajo en la carpeta Propiedades](#apply-workflow-model-to-folder).
* [Configurar el servicio Workflow Runner personalizado](#configure-custom-workflow-runner-service).

#### Aplicar un modelo de flujo de trabajo a una carpeta {#apply-workflow-model-to-folder}

Para los casos de uso habituales del posprocesamiento, considere la posibilidad de utilizar el método para aplicar un flujo de trabajo a una carpeta. Para aplicar un modelo de flujo de trabajo en la carpeta [!UICONTROL Propiedades], siga estos pasos:

1. Crear un modelo del flujo de trabajo.
1. Seleccione una carpeta y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas y haga clic en **[!UICONTROL Procesamiento de recursos]** pestaña.
1. En **[!UICONTROL Flujo de trabajo de inicio automático]**, seleccione el flujo de trabajo necesario, proporcione un título para el flujo de trabajo y guarde los cambios.

   ![Aplicar un flujo de trabajo de posprocesamiento a una carpeta de sus propiedades](assets/post-processing-profile-workflow-for-folders.png)

#### Configurar el servicio Workflow Runner personalizado {#configure-custom-workflow-runner-service}

Puede configurar el servicio del ejecutor de flujo de trabajo personalizado para las configuraciones avanzadas que no se pueden completar fácilmente aplicando un flujo de trabajo a una carpeta. Por ejemplo, un flujo de trabajo que utiliza una expresión regular. El ejecutor de flujo de trabajo personalizado Adobe CQ DAM (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) es un servicio OSGi. Proporciona las dos opciones de configuración siguientes:

* Flujos de trabajo de posprocesamiento por ruta (`postProcWorkflowsByPath`): Se pueden enumerar varios modelos de flujo de trabajo en función de diferentes rutas de repositorio. Separe las rutas y los modelos con dos puntos. Se admiten rutas de repositorio simples. Asigne estos elementos a un modelo de flujo de trabajo en `/var` ruta. Por ejemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flujos de trabajo de posprocesamiento por expresión (`postProcWorkflowsByExpression`): Se pueden enumerar varios modelos de flujo de trabajo basados en distintas expresiones regulares. Las expresiones y los modelos deben separarse con dos puntos. La expresión regular debe señalar directamente al nodo Asset y no a una de las representaciones o archivos. Por ejemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

Para obtener información sobre cómo implementar una configuración OSGi, consulte [implementar en [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### Deshabilitar la ejecución del flujo de trabajo posterior al procesamiento

Cuando no sea necesario posprocesar, cree y utilice un modelo de flujo de trabajo &quot;vacío&quot; en __Flujo de trabajo de inicio automático__ selección.

##### Creación del modelo de flujo de trabajo de inicio automático desactivado

1. Navegue hasta __Herramientas > Flujo de trabajo > Modelos__
1. Seleccionar __Crear > Crear modelo__ desde la barra de acciones superior
1. Proporcione un título y un nombre para el nuevo modelo de flujo de trabajo, por ejemplo:
   * Título: Deshabilitar el flujo de trabajo de inicio automático
   * Nombre: disable-auto-start-workflow
1. Seleccionar __Listo__ para crear el modelo de flujo de trabajo
1. __Seleccionar__ y __Editar__ el modelo de flujo de trabajo recién creado
1. En el editor del Modelo de flujo de trabajo, seleccione __Paso 1__ de la definición del modelo y elimínelo
1. Abra el __Panel lateral__ y seleccione __Pasos__
1. Arrastre el __Flujo de trabajo del recurso de actualización DAM completado__ paso a la definición del modelo
1. Seleccione el __Información de página__ botón (junto al __Panel lateral__ alternar) y seleccione __Abrir propiedades__
1. En el __Básico__ pestaña, seleccione __Flujo de trabajo transitorio__
1. Seleccionar __Guardar y cerrar__ desde la barra de acciones superior
1. Seleccionar __Sincronización__ en la barra de acciones superior
1. Cierre el editor del modelo de flujo de trabajo

##### Aplicar el modelo de flujo de trabajo de inicio automático deshabilitado

Siga los pasos descritos en [aplicar un modelo de flujo de trabajo a una carpeta](#apply-workflow-model-to-folder) y configure el __Deshabilitar flujo de trabajo de inicio automático__ como el __Flujo de trabajo de inicio automático__ para carpetas no requieren el posprocesamiento de recursos.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* Tenga en cuenta las necesidades de todos los tipos de representaciones al diseñar flujos de trabajo. Si no prevé la necesidad de una representación en el futuro, elimine su paso de creación del flujo de trabajo. Las representaciones no se pueden eliminar por lotes posteriormente. Las representaciones no deseadas pueden ocupar mucho espacio de almacenamiento después de un uso prolongado de [!DNL Experience Manager]. Para los recursos individuales, puede eliminar las representaciones manualmente desde la interfaz de usuario. Para varios recursos, puede personalizar [!DNL Experience Manager] para eliminar representaciones específicas o eliminar los recursos y cargarlos de nuevo.
* Actualmente, la compatibilidad se limita a generar representaciones. No se admite la generación de nuevos recursos.
* Actualmente, el límite de tamaño de archivo para la extracción de metadatos es de aproximadamente 15 GB. Al cargar recursos muy grandes, a veces la operación de extracción de metadatos falla.

>[!MORELIKETHIS]
>
>* [Introducción al servicio de Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html).
>* [Comprender la extensibilidad y cuándo utilizarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [Creación de aplicaciones personalizadas](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html).
>* [Tipos MIME admitidos para varios casos de uso](/help/assets/file-format-support.md).


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
