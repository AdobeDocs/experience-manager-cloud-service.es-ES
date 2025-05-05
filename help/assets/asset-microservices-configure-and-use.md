---
title: Configuración y uso de microservicios de recursos
description: Configure y utilice los microservicios de recursos nativos de la nube para procesar recursos a escala.
contentOwner: AG
feature: Asset Compute Microservices, Asset Processing, Asset Management
role: Architect, Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '2937'
ht-degree: 4%

---

# Uso de microservicios de recursos y perfiles de procesamiento {#get-started-using-asset-microservices}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante aplicaciones nativas de la nube (también denominadas trabajadores). Adobe administra los servicios para un manejo óptimo de diferentes tipos de recursos y opciones de procesamiento.

Los microservicios de recursos le permiten procesar una [amplia gama de tipos de archivos](/help/assets/file-format-support.md) que abarcan más formatos listos para usar que los que son posibles con versiones anteriores de [!DNL Experience Manager]. Por ejemplo, ahora es posible extraer miniaturas de los formatos PSD y PSB, pero se requerían soluciones de terceros como [!DNL ImageMagick].

El procesamiento de recursos depende de la configuración de **[!UICONTROL Perfiles de procesamiento]**. Experience Manager proporciona una configuración predeterminada básica y permite a los administradores añadir configuraciones de procesamiento de recursos más específicas. Los administradores crean, mantienen y modifican las configuraciones de flujos de trabajo posteriores al procesamiento, incluida la personalización opcional. La personalización de los flujos de trabajo permite a los desarrolladores ampliar la oferta predeterminada.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Vista de alto nivel del procesamiento de recursos](assets/asset-microservices-flow.png "Vista de alto nivel del procesamiento de recursos")

>[!NOTE]
>
>El procesamiento de recursos que se describe aquí reemplaza el modelo de flujo de trabajo `DAM Update Asset` que existe en las versiones anteriores de [!DNL Experience Manager]. El procesamiento de los microservicios de recursos reemplaza la mayoría de los pasos estándar relacionados con la generación de representaciones y los metadatos, y la configuración del flujo de trabajo posterior al procesamiento puede reemplazar los pasos restantes, si los hay.

## Comprender las opciones de procesamiento de recursos {#get-started}

[!DNL Experience Manager] permite los siguientes niveles de procesamiento.

| Opción | Descripción | Casos de uso cubiertos |
|---|---|---|
| [Configuración predeterminada](#default-config) | Está disponible tal cual y no se puede modificar. Esta configuración proporciona una capacidad básica de generación de representaciones. | <ul> <li>Miniaturas estándar utilizadas por la interfaz de usuario [!DNL Assets] (48, 140 y 319 píxeles) </li> <li> Vista previa grande (representación web: 1280 píxeles) </li><li> Extracción de metadatos y texto.</li></ul> |
| [Configuración personalizada](#standard-config) | Configurado por los administradores mediante la interfaz de usuario de. Se proporcionan más opciones para la generación de representaciones ampliando la opción predeterminada. Amplíe la opción predeterminada para proporcionar diferentes formatos y representaciones. | <ul><li>Representación de FPO (solo para ubicación). </li> <li>Cambiar el formato de archivo y la resolución de las imágenes</li> <li> Aplicar condicionalmente a los tipos de archivo configurados. </li> </ul> |
| [Perfil personalizado](#custom-config) | Configurado por los administradores a través de la interfaz de usuario para usar código personalizado mediante aplicaciones personalizadas y llamar al servicio [Asset Compute](https://experienceleague.adobe.com/es/docs/asset-compute/using/introduction). Admite requisitos más complejos en un método nativo y escalable de la nube. | Ver [casos de uso permitidos](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formatos de archivo compatibles {#supported-file-formats}

Los microservicios de recursos son compatibles con una amplia variedad de formatos de archivo para procesar, generar representaciones o extraer metadatos. Consulte [formatos de archivo compatibles](file-format-support.md) para obtener una lista completa de los tipos MIME y la funcionalidad admitida para cada tipo.

## Configuración predeterminada {#default-config}

Algunos valores predeterminados están preconfigurados para garantizar que las representaciones predeterminadas requeridas en Experience Manager estén disponibles. La configuración predeterminada también garantiza que las operaciones de extracción de metadatos y extracción de texto estén disponibles. Los usuarios pueden empezar a cargar o actualizar recursos inmediatamente y el procesamiento básico está disponible de forma predeterminada.

Con la configuración predeterminada, solo se configura el perfil de procesamiento más básico. Este perfil de procesamiento no es visible en la interfaz de usuario y no se puede modificar. Siempre se ejecuta para procesar los recursos cargados. Este perfil de procesamiento predeterminado garantiza que el procesamiento básico requerido por [!DNL Experience Manager] se complete en todos los recursos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configuración estándar {#standard-config}

[!DNL Experience Manager] proporciona capacidades para generar representaciones más específicas de formatos comunes según las necesidades del usuario. Un administrador puede crear [!UICONTROL Perfiles de procesamiento] adicionales para facilitar la creación de representaciones. A continuación, asigne uno o más perfiles disponibles a carpetas específicas para realizar el procesamiento adicional. Por ejemplo, el procesamiento adicional puede generar representaciones para la web, dispositivos móviles y tabletas. El siguiente vídeo ilustra cómo crear y aplicar [!UICONTROL Perfiles de procesamiento] y cómo acceder a las representaciones creadas.

* **Anchura y altura de representación**: La especificación de la anchura y altura de representación proporciona los tamaños máximos de la imagen de salida generada. Los microservicios de recursos intentan producir la representación más grande posible, cuya anchura y altura no son mayores que la anchura y altura especificadas, respectivamente. Se conserva la relación de aspecto, es decir, la misma que la original. Un valor vacío significa que el procesamiento de recursos supone la dimensión en píxeles del original.

* **Reglas de inclusión de tipo MIME**: Cuando se procesa un recurso con un tipo MIME específico, el tipo MIME se comprueba primero con el valor de tipos MIME excluidos para la especificación de representación. Si coincide con esa lista, esta representación específica no se genera para el recurso (lista de bloqueados). De lo contrario, el tipo MIME se comprueba con el tipo MIME incluido y, si coincide con la lista, se genera la representación (lista de permitidos).

* **Representación especial de FPO**: al colocar recursos de gran tamaño de [!DNL Experience Manager] en [!DNL Adobe InDesign] documentos, un profesional creativo espera un tiempo considerable después de [colocar un recurso](https://helpx.adobe.com/es/indesign/using/placing-graphics.html). Mientras tanto, se ha bloqueado al usuario el uso de [!DNL InDesign]. Esto interrumpe el flujo creativo y afecta negativamente a la experiencia del usuario. Adobe permite colocar de forma temporal representaciones de pequeño tamaño en [!DNL InDesign] documentos, para empezar, que se pueden reemplazar con recursos de resolución completa bajo demanda más adelante. [!DNL Experience Manager] proporciona representaciones que solo se utilizan para la ubicación. Estas representaciones de FPO tienen un tamaño de archivo pequeño, pero son de la misma proporción de aspecto.

El perfil de procesamiento puede incluir una representación de FPO (solo para ubicación). Consulte la [!DNL Adobe Asset Link] [documentación](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) para saber si necesita activarla para su perfil de procesamiento. Para obtener más información, consulte la [documentación completa de Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html).

### Creación de un perfil estándar {#create-standard-profile}

1. Los administradores tienen acceso a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de procesamiento]**. Haga clic en **[!UICONTROL Crear]**.
1. Proporcione un nombre que le ayude a identificar el perfil de forma exclusiva al aplicarlo a una carpeta.
1. Para generar representaciones FPO, en la ficha **[!UICONTROL Imagen]**, habilite **[!UICONTROL Crear representación FPO]**. Escriba un valor **[!UICONTROL Quality]** entre 1 y 100.
1. Para generar otras representaciones, haga clic en **[!UICONTROL Agregar nuevo]** y proporcione la siguiente información:

   * Nombre de archivo de cada representación.
   * El formato de archivo (PNG, JPEG, GIF o WebP) de cada representación.
   * Anchura y altura en píxeles de cada representación. Si no se especifican los valores, se utiliza el tamaño de píxel completo de la imagen original.
   * Calidad en porcentaje de cada representación de JPEG y WebP.
   * Se han incluido y excluido tipos MIME para definir la aplicabilidad de un perfil.

   ![perfiles de procesamiento-agregando](assets/processing-profiles-image.png)

1. Haga clic en **[!UICONTROL Guardar]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Casos de uso y perfil personalizados {#custom-config}

[!DNL Asset Compute Service] admite una variedad de casos de uso, incluido el procesamiento predeterminado y el procesamiento de formatos específicos de Adobe como archivos Photoshop. También permite implementar un procesamiento personalizado o específico de la organización. La personalización del flujo de trabajo de recursos de actualización de DAM requerida en el pasado se gestiona automáticamente o mediante la configuración de perfiles de procesamiento. Si estas opciones de procesamiento no satisfacen sus necesidades comerciales, Adobe recomienda desarrollar y utilizar [!DNL Asset Compute Service] para ampliar las capacidades predeterminadas. Para obtener una descripción general, consulte [comprender la extensibilidad y cuándo utilizarla](https://experienceleague.adobe.com/es/docs/asset-compute/using/extend/understand-extensibility).

>[!NOTE]
>
>Adobe recomienda utilizar una aplicación personalizada solo cuando no se puedan cumplir los requisitos empresariales con las configuraciones predeterminadas o el perfil estándar.

Puede transformar los formatos de imagen, vídeo, documento y otros archivos en distintas representaciones, incluidas miniaturas, texto extraído y metadatos, y archivos.

Los desarrolladores pueden usar [!DNL Asset Compute Service] para [crear aplicaciones personalizadas](https://experienceleague.adobe.com/es/docs/asset-compute/using/extend/develop-custom-application) para los casos de uso admitidos. [!DNL Experience Manager] puede llamar a estas aplicaciones personalizadas desde la interfaz de usuario mediante perfiles personalizados que configuran los administradores. [!DNL Asset Compute Service] admite los siguientes casos de uso de invocación a servicios externos:

* Use la [API de ImageCutout](https://developer.adobe.com/photoshop/photoshop-api-docs/) de [!DNL Adobe Photoshop] y guarde el resultado como una representación.
* Llame a sistemas de terceros para realizar cambios, por ejemplo, un sistema PIM.
* Utilice la API [!DNL Photoshop] para generar diversas representaciones basadas en la plantilla de Photoshop.
* Use la [API de Adobe Lightroom](https://developer.adobe.com/photoshop/photoshop-api-docs/) para optimizar los recursos ingeridos y guardarlos como representaciones.

>[!NOTE]
>
>No puede editar los metadatos estándar mediante las aplicaciones personalizadas. Solo puede modificar los metadatos personalizados.

### Creación de un perfil personalizado {#create-custom-profile}

1. Los administradores tienen acceso a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de procesamiento]** > **[!UICONTROL Crear]**.
1. En la página Perfil de procesamiento, haga clic en la ficha **[!UICONTROL Personalizado]** y, a continuación, haga clic en **[!UICONTROL Agregar nuevo]**.
1. En el campo de texto Nombre, escriba el nombre de archivo deseado de la representación y, a continuación, proporcione la siguiente información.

   * Nombre de archivo de cada representación y una extensión de archivo compatible.
   * [URL de extremo de una aplicación personalizada de App Builder](https://experienceleague.adobe.com/es/docs/asset-compute/using/extend/deploy-custom-application). La aplicación debe pertenecer a la misma organización que la cuenta de Experience Manager.
   * Agregue parámetros de servicio a [pase información o parámetros adicionales a la aplicación personalizada](https://experienceleague.adobe.com/es/docs/asset-compute/using/extend/develop-custom-application#extend).
   * Se han incluido y excluido tipos MIME para limitar el procesamiento a algunos formatos de archivo específicos.

1. Junto a la esquina superior derecha de la página, haga clic en **[!UICONTROL Guardar]**.

Las aplicaciones personalizadas son aplicaciones [Project App Builder](https://developer.adobe.com/app-builder/docs/overview/) sin encabezado. La aplicación personalizada obtiene todos los archivos proporcionados si están configurados con un perfil de procesamiento. La aplicación debe filtrar los archivos.

>[!CAUTION]
>
>Si la aplicación App Builder y la cuenta [!DNL Experience Manager] no pertenecen a la misma organización, la integración no funciona.

### Ejemplo de perfil personalizado {#custom-profile-example}

Para ilustrar el uso de un perfil personalizado, consideremos un caso de uso para aplicar texto personalizado a las imágenes de la campaña. Puede crear un perfil de procesamiento que utilice la API de Photoshop para editar las imágenes.

La integración del servicio Asset Compute permite a Experience Manager pasar estos parámetros a la aplicación personalizada mediante el campo [!UICONTROL Parámetros de servicio]. A continuación, la aplicación personalizada llama a la API de Photoshop y pasa estos valores a la API. Por ejemplo, puede pasar el nombre de la fuente, el color, el peso y el tamaño del texto para añadir el texto personalizado a las imágenes de campaña.

<!-- TBD: Check screenshot against the interface. -->

![perfil de procesamiento personalizado](assets/custom-processing-profile.png)

*Figura: Utilice el campo [!UICONTROL Parámetros de servicio] para pasar información agregada a los parámetros predefinidos generados en la aplicación personalizada. En este ejemplo, cuando se cargan imágenes de campaña, las imágenes se actualizan con el texto `Jumanji` en la fuente `Arial-BoldMT`.*

## Uso de perfiles de procesamiento para procesar recursos {#use-profiles}

Cree y aplique perfiles de procesamiento personalizados adicionales a carpetas específicas. Este flujo de trabajo permite a Experience Manager procesar los recursos que se cargan o actualizan en estas carpetas. El perfil de procesamiento estándar integrado y predeterminado siempre se ejecuta, pero no es visible en la interfaz de usuario. Si agrega un perfil personalizado, ambos perfiles se utilizan para procesar los recursos cargados.

Aplique perfiles de procesamiento a las carpetas mediante uno de los métodos siguientes:

* Los administradores pueden seleccionar una definición de perfil de procesamiento en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de procesamiento]** y usar la acción **[!UICONTROL Aplicar perfil a las carpetas]**. Se abre un explorador de contenido que le permite desplazarse a carpetas específicas, seleccionarlas y confirmar la aplicación del perfil.
* Los usuarios pueden seleccionar una carpeta en la interfaz de usuario de Assets y usar la acción **[!UICONTROL Propiedades]** para abrir la pantalla de propiedades de la carpeta. En la ficha **[!UICONTROL Procesamiento de recursos]**, pueden seleccionar el perfil de procesamiento adecuado para esa carpeta en la lista [!UICONTROL Perfil de procesamiento]. Para guardar los cambios, haga clic en **[!UICONTROL Guardar y cerrar]**.
  ![Aplicar perfil de procesamiento a una carpeta desde la ficha Propiedades del recurso](assets/folder-properties-processing-profile.png)

* Los usuarios pueden seleccionar carpetas o recursos específicos en la interfaz de usuario de Assets para aplicar un perfil de procesamiento y, a continuación, seleccionar la opción ![icono de reprocesamiento de recursos](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL Reprocesar Assets]** de las opciones disponibles en la parte superior.

>[!TIP]
>
>Solo se puede aplicar un perfil de procesamiento a una carpeta. Para generar más representaciones, agregue más definiciones de representación al perfil de procesamiento existente.

Después de aplicar un perfil de procesamiento a una carpeta, todos los recursos nuevos cargados (o actualizados) en esta o en cualquiera de sus subcarpetas se procesan con el perfil de procesamiento adicional configurado. Este procesamiento se suma al perfil predeterminado estándar.

>[!NOTE]
>
>Un perfil de procesamiento aplicado a una carpeta funciona para todo el árbol, pero se puede sobrescribir con otro perfil aplicado a una subcarpeta. Cuando los recursos se cargan en una carpeta, Experience Manager comprueba las propiedades de la carpeta contenedora para ver si hay un perfil de procesamiento. Si no se aplica ninguno, se comprueba la existencia de un perfil de procesamiento en una carpeta principal de la jerarquía.

Para comprobar que los recursos se procesan, obtenga una vista previa de las representaciones generadas en la vista [!UICONTROL Representaciones] del carril izquierdo. Abra la vista previa del recurso y el carril izquierdo para acceder a la vista **[!UICONTROL Representaciones]**. Las representaciones específicas en el perfil de procesamiento, para las que el tipo del recurso específico coincide con las reglas de inclusión de tipo MIME, deben ser visibles y accesibles.

![representaciones adicionales](assets/renditions-additional-renditions.png)

*Imagen: ejemplo de dos representaciones adicionales generadas por un perfil de procesamiento aplicado a la carpeta principal.*

## Flujos de trabajo de posprocesamiento {#post-processing-workflows}

En el caso de que se requiera un procesamiento adicional de recursos que no se pueda lograr con los perfiles de procesamiento, se pueden agregar a la configuración flujos de trabajo posteriores al procesamiento. El posprocesamiento le permite agregar un procesamiento completamente personalizado sobre el procesamiento configurable mediante microservicios de recursos.

Una vez finalizado el procesamiento de los microservicios, [!DNL Experience Manager] ejecuta automáticamente flujos de trabajo posteriores al procesamiento o [flujos de trabajo de inicio automático](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/configuring/auto-start-workflows), si están configurados. No es necesario añadir manualmente iniciadores de flujo de trabajo para almacenar en déclencheur los flujos de trabajo. Los ejemplos incluyen:

* Pasos personalizados del flujo de trabajo para procesar recursos.
* Integraciones para añadir metadatos o propiedades a recursos de sistemas externos como, por ejemplo, información de productos o procesos.
* Los servicios externos realizan el procesamiento adicional.

Para agregar una configuración de flujo de trabajo de procesamiento posterior a [!DNL Experience Manager], siga estos pasos:

* Cree uno o varios modelos de flujo de trabajo. Estos modelos personalizados se denominan *modelos de flujo de trabajo de posprocesamiento* en esta documentación. Son modelos de flujo de trabajo de [!DNL Experience Manager] normales.
* Añada los pasos de flujo de trabajo necesarios a estos modelos. Revise los pasos del flujo de trabajo predeterminado y añada todos los pasos predeterminados necesarios al flujo de trabajo personalizado. Los pasos se ejecutan en los recursos en función de una configuración de modelo de flujo de trabajo. Por ejemplo, si desea que el etiquetado inteligente se produzca automáticamente al cargar el recurso, agregue el paso al modelo de flujo de trabajo de posprocesamiento personalizado.
* Agregue el paso [!UICONTROL Proceso completado del flujo de trabajo del recurso de actualización DAM] al final. Añadir este paso garantiza que Experience Manager sepa cuándo termina el procesamiento y que el recurso se pueda marcar como procesado. Es decir, *Nuevo* se muestra en el recurso.
* Cree una configuración para el servicio de flujo de trabajo personalizado Runner que le permita configurar la ejecución de un modelo de flujo de trabajo de posprocesamiento por una ruta (ubicación de carpeta) o por una expresión regular.

Para obtener más información sobre qué paso de flujo de trabajo estándar se puede utilizar en el flujo de trabajo de posprocesamiento, consulte [Pasos del flujo de trabajo en el flujo de trabajo de posprocesamiento](developer-reference-material-apis.md#post-processing-workflows-steps) en la referencia para desarrolladores.

### Creación de modelos de flujo de trabajo de posprocesamiento {#create-post-processing-workflow-models}

Los modelos de flujo de trabajo de posprocesamiento son [!DNL Experience Manager] modelos de flujo de trabajo normales. Cree diferentes modelos si necesita un procesamiento diferente para diferentes ubicaciones de repositorios o tipos de recursos.

Los pasos de procesamiento se añaden según sea necesario. Puede utilizar tanto los pasos admitidos disponibles como los pasos personalizados implementados del flujo de trabajo.

Asegúrese de que el último paso de cada flujo de trabajo posterior al procesamiento sea `DAM Update Asset Workflow Completed Process`. El paso final garantiza que Experience Manager reconozca cuándo se ha completado el procesamiento de los recursos.

### Configuración de la ejecución del flujo de trabajo posterior al procesamiento {#configure-post-processing-workflow-execution}

Una vez que los microservicios de recursos hayan completado el procesamiento de los recursos cargados, puede definir un flujo de trabajo de posprocesamiento para procesar los recursos más detalladamente. Para configurar el posprocesamiento mediante modelos de flujo de trabajo, puede realizar una de las siguientes acciones:

* [Aplicar un modelo de flujo de trabajo en la carpeta Propiedades](#apply-workflow-model-to-folder).
* [Configurar el servicio Workflow Runner personalizado](#configure-custom-workflow-runner-service).

#### Aplicar un modelo de flujo de trabajo a una carpeta {#apply-workflow-model-to-folder}

Para los casos de uso habituales del posprocesamiento, considere la posibilidad de utilizar el método para aplicar un flujo de trabajo a una carpeta. Para aplicar un modelo de flujo de trabajo en la carpeta [!UICONTROL Properties], siga estos pasos:

1. Cree un modelo del flujo de trabajo.
1. Seleccione una carpeta, haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas y luego haga clic en la ficha **[!UICONTROL Procesamiento de Assets]**.
1. En **[!UICONTROL Flujo de trabajo de inicio automático]**, seleccione el flujo de trabajo necesario, proporcione un título para el flujo de trabajo y, a continuación, guarde los cambios.

   ![Aplicar un flujo de trabajo de posprocesamiento a una carpeta de sus propiedades](assets/post-processing-profile-workflow-for-folders.png)

#### Configurar el servicio de Workflow Runner personalizado {#configure-custom-workflow-runner-service}

Puede configurar el servicio de ejecutor de flujo de trabajo personalizado para las configuraciones avanzadas que no se pueden completar fácilmente aplicando un flujo de trabajo a una carpeta. Por ejemplo, un flujo de trabajo que utiliza una expresión regular. El ejecutor de flujo de trabajo personalizado de Adobe CQ DAM (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) es un servicio OSGi. Proporciona las dos opciones de configuración siguientes:

* Flujos de trabajo de posprocesamiento por ruta (`postProcWorkflowsByPath`): se pueden enumerar varios modelos de flujo de trabajo, según diferentes rutas de repositorio. Separe las rutas y los modelos con dos puntos. Se admiten rutas de repositorio simples. Asignarlos a un modelo de flujo de trabajo en la ruta `/var`. Por ejemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flujos de trabajo de posprocesamiento por expresión (`postProcWorkflowsByExpression`): se pueden enumerar varios modelos de flujo de trabajo según distintas expresiones regulares. Separe las expresiones y los modelos con dos puntos. Señale la expresión regular para que apunte directamente al nodo Recurso y no a una de las representaciones o archivos. Por ejemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

Para saber cómo implementar una configuración OSGi, consulte [implementar en [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### Deshabilitar la ejecución del flujo de trabajo posterior al procesamiento

Cuando no sea necesario posprocesar, cree y utilice un modelo de flujo de trabajo &quot;vacío&quot; en la selección **Flujo de trabajo de inicio automático**.

##### Creación del modelo de flujo de trabajo de inicio automático desactivado

1. Navegue hasta **Herramientas** > **Flujo de trabajo** > **Modelos**.
1. Haga clic en **Crear** > **Crear modelo** en la barra de acciones superior.
1. Proporcione un título y un nombre para el nuevo modelo de flujo de trabajo, por ejemplo:
   * Título: Deshabilitar el flujo de trabajo de inicio automático
   * Nombre: disable-auto-start-workflow
1. Haga clic en **Listo** para crear el modelo de flujo de trabajo.
1. Seleccione y edite el modelo de flujo de trabajo creado
1. En el editor del modelo de flujo de trabajo, haga clic en **Paso 1** de la definición del modelo y elimínelo.
1. En el panel lateral, haga clic en **Pasos**.
1. Arrastre el paso **Flujo de trabajo de recursos de actualización DAM completado** a la definición del modelo.
1. Haga clic en **Información de la página** (junto al botón de alternancia **Panel lateral**) y luego haga clic en **Abrir propiedades**.
1. En la pestaña Básico, haga clic en **Flujo de trabajo transitorio**.
1. En la barra de acciones superior, haz clic en **Guardar y cerrar**.
1. En la barra de acciones superior, haz clic en **Sincronizar**.
1. Cierre el editor del modelo de flujo de trabajo.

##### Aplicar el modelo de flujo de trabajo de inicio automático deshabilitado

Siga los pasos descritos en [aplicar un modelo de flujo de trabajo a una carpeta](#apply-workflow-model-to-folder) y establezca **Deshabilitar flujo de trabajo de inicio automático** como **Flujo de trabajo de inicio automático** para las carpetas que no requieran el procesamiento posterior de recursos.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* Tenga en cuenta las necesidades de todos los tipos de representaciones al diseñar flujos de trabajo. Si no prevé la necesidad de una representación en el futuro, elimine su paso de creación del flujo de trabajo. Las representaciones no se pueden eliminar por lotes posteriormente. Las representaciones no deseadas pueden ocupar una gran cantidad de espacio de almacenamiento después de un uso prolongado de [!DNL Experience Manager]. Para los recursos individuales, puede eliminar las representaciones manualmente desde la interfaz de usuario. Para varios recursos, puede personalizar [!DNL Experience Manager] para eliminar representaciones específicas o eliminar los recursos y cargarlos de nuevo.
* Actualmente, la compatibilidad se limita a generar representaciones. No se admite la generación de nuevos recursos.
* Actualmente, el límite de tamaño de archivo para la extracción de metadatos es de aproximadamente 15 GB. Al cargar recursos muy grandes, a veces se produce un error en la operación de extracción de metadatos.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Introducción al servicio Asset Compute](https://experienceleague.adobe.com/es/docs/asset-compute/using/introduction).
>* [Comprenda la extensibilidad y cuándo utilizarla](https://experienceleague.adobe.com/es/docs/asset-compute/using/extend/understand-extensibility).
>* [Cómo crear aplicaciones personalizadas](https://experienceleague.adobe.com/es/docs/asset-compute/using/extend/develop-custom-application).
>* [Tipos MIME admitidos para varios casos de uso](/help/assets/file-format-support.md).

<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
