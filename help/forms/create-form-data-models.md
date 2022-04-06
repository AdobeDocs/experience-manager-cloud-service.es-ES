---
title: ¿Cómo se crea el modelo de datos de formulario?
description: La integración de datos de Experience Manager Forms proporciona una interfaz de usuario intuitiva para crear y trabajar con modelos de datos de formulario. Aprenda a crear modelos de datos de formulario con o sin fuentes de datos configuradas.
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 1e2b58015453c194af02fdae62c3735727981da1
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 0%

---

# Crear modelo de datos de formulario {#create-form-data-model}

![Integración de datos](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] la integración de datos proporciona una interfaz de usuario intuitiva para crear y trabajar con modelos de datos de formulario. Un modelo de datos de formulario se basa en fuentes de datos para el intercambio de datos; sin embargo, puede crear un modelo de datos de formulario con o sin un origen de datos. Existen dos métodos para crear un desde el modelo de datos en función de si ha configurado fuentes de datos:

* **Uso de fuentes de datos preconfiguradas**: Si ha configurado las fuentes de datos tal como se describe en [Configuración de fuentes de datos](configure-data-sources.md), puede seleccionarlos al crear un modelo de datos de formulario. Incorpora todos los objetos, propiedades y servicios del modelo de datos de los orígenes de datos seleccionados que se pueden utilizar en el modelo de datos de formulario.

* **Sin fuentes de datos**: Si no ha configurado orígenes de datos para el modelo de datos de formulario, puede crearlos sin orígenes de datos. Puede utilizar el Modelo de datos de formulario para crear Forms adaptable <!--and interactive communication--> y pruébelas utilizando datos de ejemplo. Cuando hay orígenes de datos disponibles, puede enlazar el Modelo de datos de formulario con orígenes de datos, que se refleja automáticamente en el Forms adaptable asociado<!--and interactive communications-->.

>[!NOTE]
>
>Debe ser miembro de ambas **fdm-author** y **forms-user** grupos para poder crear y trabajar con el modelo de datos de formulario. Póngase en contacto con su [!DNL Experience Manager] administrador para convertirse en miembro de los grupos.

## Crear modelo de datos de formulario {#data-sources}

Asegúrese de haber configurado los orígenes de datos que desea utilizar en el Modelo de datos de formulario como se describe en [Configuración de fuentes de datos](configure-data-sources.md). Para crear un Modelo de datos de formulario basado en orígenes de datos configurados, haga lo siguiente:

1. En [!DNL Experience Manager] instancia de autor, vaya a **[!UICONTROL Forms > Integraciones de datos]**.
1. Toque **[!UICONTROL Crear > Modelo de datos de formulario]**.
1. En el cuadro de diálogo Crear modelo de datos de formulario:

   * Especifique un nombre para el modelo de datos del formulario.
   * (**Opcional**) Especifique el título, la descripción y las etiquetas del modelo de datos del formulario.
   * (**Opcional y aplicable solo si se configuran fuentes de datos**) Pulse el icono de visto situado junto a la **[!UICONTROL Configuración de fuente de datos]** y seleccione el nodo de configuración donde residen los servicios en la nube para los orígenes de datos que desea utilizar. Restringe la lista de fuentes de datos disponibles para su selección en la página siguiente a las disponibles en el nodo de configuración seleccionado. Sin embargo, cualquier base de datos JDBC y [!DNL Experience Manager] las fuentes de datos de perfil de usuario se enumeran de forma predeterminada. Si no selecciona un nodo de configuración, se enumeran las fuentes de datos de todos los nodos de configuración.

1. Toque **[!UICONTROL Siguiente]**.

1. (**Aplicable únicamente si se han configurado fuentes de datos**). **[!UICONTROL Seleccionar origen de datos]** lista las fuentes de datos disponibles, si las hay. Seleccione los orígenes de datos que desee utilizar en el modelo de datos de formulario.
1. Toque **[!UICONTROL Crear]** y en el cuadro de diálogo de confirmación, pulse **[!UICONTROL Apertura]** para abrir el editor Modelo de datos de formulario.

   Vamos a revisar los diferentes componentes de la interfaz de usuario del editor del Modelo de datos de formulario.

   ![Modelo de datos de formulario con tres fuentes de datos: un servicio RESTful, [!DNL Experience Manager] perfil de usuario y un RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL Fuentes de datos]** Muestra los orígenes de datos en un modelo de datos de formulario. Expanda un origen de datos para ver los objetos y servicios del modelo de datos.

   B. **[!UICONTROL Actualizar definiciones de fuentes de datos]** Recupera cualquier cambio en las definiciones de orígenes de datos de orígenes de datos configurados y los actualiza en la ficha Fuentes de datos del editor del Modelo de datos de formulario.

   C. **[!UICONTROL Modelo]** Área de contenido en la que aparecen los objetos del modelo de datos añadidos.

   D. **[!UICONTROL Servicios]** Área de contenido en la que aparecen las operaciones o los servicios de fuentes de datos añadidos.

   E. **[!UICONTROL Barra de herramientas]** Herramientas para trabajar con el modelo de datos de formulario. La barra de herramientas muestra más opciones en función del objeto seleccionado en el modelo de datos de formulario.

   F. **[!UICONTROL Agregar selección]** Agrega objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

Para obtener más información sobre el editor del Modelo de datos de formulario y cómo se puede trabajar con él para editar y configurar el modelo de datos de formulario, consulte [Trabajo con el modelo de datos de formulario](work-with-form-data-model.md).

## Actualización de fuentes de datos {#update}

Haga lo siguiente para agregar o actualizar orígenes de datos a un modelo de datos de formulario existente.

1. Vaya a **[!UICONTROL Forms > Integraciones de datos]**, seleccione el Modelo de datos de formulario en el que desea agregar o actualizar orígenes de datos y pulse **[!UICONTROL Propiedades]**.
1. En las propiedades del Modelo de datos de formulario, vaya a **[!UICONTROL Actualizar origen]** pestaña .

   En el **[!UICONTROL Actualizar origen]** pestaña:

   * Toque el icono Examinar en la **[!UICONTROL Configuración según el contexto]** y seleccione un nodo de configuración en el que reside la configuración de nube para la fuente de datos que desea añadir. Si no selecciona ningún nodo, las configuraciones de nube solo residen en la variable `global` los nodos se enumeran al pulsar **[!UICONTROL Agregar fuentes]**.

   * Para agregar una fuente de datos nueva, pulse **[!UICONTROL Agregar fuentes]** y seleccione los orígenes de datos que desea agregar al modelo de datos de formulario. Todas las fuentes de datos configuradas en `global` y se muestra el nodo de configuración seleccionado, si lo hay.

   * Para reemplazar una fuente de datos existente por otra fuente de datos del mismo tipo, pulse el botón **[!UICONTROL Editar]** para la fuente de datos y seleccione en la lista de fuentes de datos disponibles.
   * Para eliminar una fuente de datos existente, pulse la tecla **[!UICONTROL Eliminar]** para la fuente de datos. El icono Eliminar está desactivado si se agrega un objeto de modelo de datos en el origen de datos en el modelo de datos del formulario.

      ![fdm-properties](assets/fdm-properties.png)

1. Toque **[!UICONTROL Guardar y cerrar]** para guardar las actualizaciones.

>[!NOTE]
>
>Una vez que agregue nuevas fuentes de datos o actualice las fuentes de datos existentes en un modelo de datos de formulario, asegúrese de actualizar las referencias de enlace, según corresponda, en Forms adaptable<!--and interactive communications--> que utilizan el modelo de datos de formulario actualizado.

## Configuraciones según el contexto para modos de ejecución específicos {#runmode-specific-context-aware-config}

[!UICONTROL Modelo de datos de formulario] utiliza [Configuraciones según el contexto de Sling](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) para admitir distintos parámetros de fuente de datos para conectarse con orígenes de datos para diferentes [!DNL Experience Manager] ejecutar modos.

When [!UICONTROL Modelo de datos de formulario] utiliza configuraciones de nube para almacenar parámetros, que cuando se registran y se implementan mediante control de código fuente (repositorio GIT de Cloud-Manager) crea una configuración de nube con los mismos parámetros para todos los modos de ejecución (desarrollo, fase y producción). Sin embargo, en los casos de uso en los que sea necesario tener diferentes conjuntos de datos para entornos de prueba y producción, se utilizan parámetros de fuente de datos (por ejemplo, la URL de la fuente de datos) para diferentes [!DNL Experience Manager] ejecutar modos.

Para conseguirlo, debe crear una configuración OSGi que contenga pares de parámetros-valor de la fuente de datos. Esto anula el mismo par de [!UICONTROL Modelo de datos de formulario] configuración de nube en tiempo de ejecución. Como las configuraciones de OSGi admiten estos modos de ejecución de forma predeterminada, puede anular un parámetro de fuente de datos en diferentes valores según el modo de ejecución.

Para habilitar configuraciones de nube específicas de la implementación en [!UICONTROL Modelo de datos de formulario]:

1. Cree una configuración de nube en la instancia de desarrollo local. Para ver los pasos detallados, consulte [Configuración de fuentes de datos](/help/forms/configure-data-sources.md).

1. Almacene la configuración de nube en el sistema de archivos.
   1. Crear paquete con filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Utilice lo mismo `{foldername}` como en el paso 1. Y reemplace `fdm` con `azurestorage` para la configuración de almacenamiento de Azure.
   1. Cree y descargue el paquete. Para obtener más información, consulte [acciones de paquete](/help/implementing/developing/tools/package-manager.md).

1. Integrar la configuración de nube en [!DNL Experience Manager] Proyecto Tipo de archivo.
   1. Descomprima el paquete descargado.
   1. Copiar `jcr_root` carpeta y póngala en su `ui.content` > `src` > `main` > `content`.
   1. Actualizar `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` contener filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Para obtener más información, consulte [módulo ui.content de AEM tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). Cuando este proyecto de tipo de archivo se implementa mediante la canalización de CM, la misma configuración de nube se instala en todos los entornos (o modos de ejecución). Para cambiar el valor de los campos (como la URL) de las configuraciones de nube basadas en el entorno, utilice la configuración OSGi que se describe en el siguiente paso.

1. Cree una configuración de Apache Sling según el contexto. Para crear la configuración OSGi:
   1. **Configure los archivos de configuración de OSGi en [!DNL Experience Manager] Arquetipo de proyecto.**
Creación de archivos de configuración de fábrica OSGi con PID 
`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. Cree un archivo con el mismo nombre en cada carpeta del modo de ejecución donde los valores deban cambiarse por modo de ejecución. Para obtener más información, consulte [Configuración de OSGi para [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **Establezca el json de configuración OSGI.** Para utilizar el proveedor de anulación de configuración según el contexto de Apache Sling:
      1. En la instancia de desarrollo local `/system/console/configMgr`, seleccione la configuración de fábrica de OSGi con el nombre **[!UICONTROL Proveedor de anulación de configuración según el contexto de Apache Sling: Configuración de OSGi]**.
      1. Proporcione una descripción.
      1. Select **[!UICONTROL enabled]**.
      1. En anulaciones, proporcione los campos que deben cambiarse en función del entorno en la sintaxis de anulación de sling. Para obtener más información, consulte [Configuración según el contexto de Apache Sling: Sustituir](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). Por ejemplo, `cloudconfigs/fdm/{configName}/url="newURL"`.
Se pueden agregar varias anulaciones seleccionando **[!UICONTROL +]**.
      1. Seleccione **[!UICONTROL Guardar]**.
      1. Para obtener la configuración OSGi JSON, siga los pasos en [Generación de configuraciones de OSGi mediante el inicio rápido AEM SDK](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. Coloque JSON en los archivos de configuración de fábrica de OSGi creados en el paso anterior.
      1. Cambiar el valor de `newURL` en función del entorno (o modo de ejecución).
      1. Para cambiar el valor secreto en función del modo de ejecución, se puede crear una variable secreta mediante [API de cloud manager](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) y más adelante en la sección [Configuración de OSGi](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
Cuando este proyecto de tipo de archivo se implementa mediante la canalización de CM, override proporciona valores diferentes en entornos diferentes (o modo de ejecución).

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] los usuarios pueden cifrar los valores secretos utilizando la compatibilidad con criptografía (para obtener más información, consulte [compatibilidad con cifrado para propiedades de configuración](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) y colocar texto cifrado en el valor después de [las configuraciones según el contexto están disponibles en el Service Pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. Actualice las definiciones de fuentes de datos mediante la opción para actualizar las definiciones de fuentes de datos en la [Editor del modelo de datos de formulario](#data-sources) para actualizar la caché de FDM a través de la interfaz de usuario de FDM y obtener la configuración más reciente.

## Pasos siguientes {#next-steps}

Ahora tiene un modelo de datos de formulario con orígenes de datos agregados. A continuación, puede editar el Modelo de datos de formulario para agregar y configurar objetos y servicios del modelo de datos, agregar asociaciones entre objetos del modelo de datos, editar propiedades, agregar objetos y propiedades del modelo de datos personalizado, generar datos de ejemplo, etc.

Para obtener más información, consulte [Trabajo con el modelo de datos de formulario](work-with-form-data-model.md).
