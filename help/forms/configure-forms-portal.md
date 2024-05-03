---
title: ¿Cómo crear un portal de Forms en una página de Experience Manager Sites?
description: Obtenga información sobre cómo crear un portal de Forms y utilizar componentes principales listos para usar en una página de AEM Sites.
feature: Adaptive Forms, Foundation Components
exl-id: 13cfe3ba-2e85-46bf-a029-2673de69c626
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 98%

---

# Portal Agregar Formularios adaptables a una página de AEM Sites {#publish-forms-on-portal}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/creating-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/introduction-publishing-forms.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

En un escenario típico de implementación de portal centrado en formularios, el desarrollo de los formularios y el de portales son dos actividades separadas. Mientras los diseñadores de formularios diseñan y almacenan formularios en un repositorio, los desarrolladores web crean una aplicación web para enumerar formularios y administrar su envío. Los formularios se copian en el nivel web, ya que no hay ninguna comunicación entre el repositorio de formularios y la aplicación web.

Estos escenarios suelen dar lugar a problemas de administración y retrasos en la producción. Por ejemplo, si hay una versión más reciente de un formulario disponible en el repositorio, debe reemplazar el formulario en el nivel web, modificar la aplicación web y volver a implementar el formulario en el sitio público. La reimplementación de la aplicación web puede causar cierto tiempo de inactividad en el servidor. Normalmente, el tiempo de inactividad del servidor es una actividad planificada y, por lo tanto, los cambios no se pueden insertar instantáneamente en el sitio público.

AEM Forms proporciona componentes del portal que reducen los gastos generales de administración y los retrasos en la producción. Los componentes equipan a los desarrolladores web para crear y personalizar un portal de Forms en sitios web creados con Adobe Experience Manager (AEM).

Los componentes del portal de Forms le permiten agregar las siguientes funciones:

* Enumerar formularios en diseños personalizados. Se proporcionan los diseños Vista de lista y Vista de tarjeta. Puede crear sus propios diseños personalizados.
* Permite mostrar metadatos y acciones personalizados al enumerarlos.
* Enumerar los formularios publicados por la interfaz de usuario de AEM Forms en la instancia Publicación en la que se utilizan los componentes del portal de Forms.
* Permite que los usuarios finales procesen formularios en formato HTML y PDF.
* Habilita la búsqueda de formularios en función del título y la descripción.
* Utiliza CSS personalizada para personalizar la apariencia del portal.
* Crea vínculos a formularios.
* Muestra borradores y envíos relacionados con formularios adaptables que haya creado el usuario.

## Componentes de una página del portal de Forms {#forms-portal-components}

AEM Forms proporciona los siguientes componentes listos para usar del portal:

* Buscar y listar: este componente le permite mostrar una lista de formularios del repositorio de formularios en la página del portal y proporciona opciones de configuración para mostrar una lista de formularios basados en criterios específicos.

* Borradores y envíos: Mientras que el componente Buscar y listar muestra los formularios que publica el autor de Forms, el componente Borradores y envíos muestra los formularios guardados como borrador para completarlos posteriormente y enviarlos. Este componente proporciona una experiencia personalizada a cualquier usuario que haya iniciado sesión.

* Vínculo: este componente permite crear un vínculo a un formulario en cualquier parte de la página.

Puede [importar los componentes listos para usar del portal de Forms](#import-forms-portal-components-aem-archetype) desde el proyecto AEM Archetype. Después de la importación, realice las siguientes configuraciones:

* [Configure un almacenamiento externo](#configure-azure-storage-adaptive-forms)

* [Habilite los componentes del portal de Forms](#enable-forms-portal-components)

* [Configure los componentes del portal de Forms](#configure-forms-portal-components)

## Importar componentes del portal de Forms {#import-forms-portal-components-aem-archetype}

Para importar componentes listos para usar del portal de Forms en AEM Forms as a Cloud Service, haga lo siguiente:

1. **Clone el repositorio Git de Cloud Manager en su instancia de desarrollo local:** Su repositorio Git de Cloud Manager contiene un proyecto de AEM predeterminado. Se basa en [AEM Archetype](https://github.com/adobe/aem-project-archetype/). Clone su Repositorio Git de Cloud Manager mediante la administración de cuentas Git de autoservicio desde la interfaz de usuario de Cloud Manager para llevar el proyecto a su entorno de desarrollo local. Para obtener más información sobre el acceso al repositorio, consulte [Acceder a repositorios](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html?lang=es).

1. **Cree un proyecto [!DNL Experience Manager Forms] as a [Cloud Service]:** Cree un proyecto [!DNL Experience Manager Forms] as a [Cloud Service] basado en [AEM Archetype 27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) o posterior. El arquetipo ayuda a los desarrolladores a empezar a desarrollar fácilmente para [!DNL AEM Forms] as a Cloud Service. También incluye algunas temáticas de muestra y plantillas para ayudarle a empezar rápidamente.

   Para crear un proyecto [!DNL Experience Manager Forms] as a Cloud Service, abra el símbolo del sistema y ejecute el siguiente comando. Para incluir [!DNL Forms] configuraciones, temáticas y plantillas específicos, establezca `includeForms=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Además, cambie `appTitle`, `appId`y `groupId`, en el comando anterior para reflejar su entorno.

   Una vez que el proyecto esté listo, actualice la `<core.forms.components.version>x.y.z</core.forms.components.version>` propiedad en el nivel superior `pom.xml` del proyecto Arquetipo para reflejar la última versión de [core-forms-components](https://github.com/adobe/aem-core-forms-components) en su `AEM Archetype` proyecto.

1. **Implemente el proyecto en su entorno de desarrollo local:** Puede utilizar el siguiente comando para implementar en el entorno de desarrollo local

   `mvn -PautoInstallPackage clean install`

   Para obtener la lista completa de comandos, consulte [Creación e instalación](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=es#building-and-installing)

1. [Implemente el código en su entorno de  [!DNL AEM Forms] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es#embeddeds).


## Configuración del almacenamiento de Azure para formularios adaptables {#configure-azure-storage-adaptive-forms}

La integración de datos de [[!DNL Experience Manager Forms] ](data-integration.md) proporciona [!DNL Azure]la configuración de almacenamiento para integrar formularios con [!DNL Azure] servicios de almacenamiento. El modelo de datos de formulario (FDM) se puede utilizar para crear Forms adaptable que interactúe con [!DNL Azure] para activar flujos de trabajo empresariales.

### Crear configuración de almacenamiento de Azure {#create-azure-storage-configuration}

Antes de ejecutar estos pasos, asegúrese de que tiene una cuenta de almacenamiento de Azure y una clave de acceso para autorizar el acceso [!DNL Azure]a ella.

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Almacenamiento de Azure]**.
1. Seleccione una carpeta para crear la configuración y seleccione **[!UICONTROL Crear]**.
1. Especifique un título para la configuración en el campo **[!UICONTROL Título]**.
1. Especifique el nombre de la cuenta de [!DNL Azure] Storage en el campo **[!UICONTROL Cuenta de Azure Storage]**.

### Configuración del conector de almacenamiento unificado para el portal de Forms {#configure-usc-forms-portal}

Para configurar el conector de almacenamiento unificado para flujos de trabajo de AEM, haga lo siguiente:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Formularios]** > **[!UICONTROL Conector de almacenamiento unificado]**.
1. En el **[!UICONTROL portal de Forms]**, seleccione **[!UICONTROL Azure]** de la lista desplegable **[!UICONTROL Almacenamiento]**.
1. Especifique la ruta de configuración [para la configuración del almacenamiento de Azure](#create-azure-storage-configuration) en el campo **[!UICONTROL Ruta de configuración del almacenamiento]**.
1. Seleccione **[!UICONTROL Publicar]** y, a continuación, seleccione **[!UICONTROL Guardar]** para guardar la configuración.

## Habilitar componentes del portal de Forms {#enable-forms-portal-components}

Para utilizar cualquier componente principal (incluidos los componentes de portal predeterminados) en un sitio de Adobe Experience Manager (AEM), debe crear un componente proxy y habilitarlo para su sitio. Para crear un componente proxy y habilitar los componentes del portal, consulte [Utilizar componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=es#create-proxy-components).

Una vez habilitado un componente del portal, puede utilizarlo en la instancia Autor de la página del sitio.

## Agregar y configurar componentes del portal de Forms {#configure-forms-portal-components}

Puede crear y personalizar el portal de Forms en sitios web creados mediante AEM si agrega y configura los componentes del portal. Asegúrese de que los componentes [estén habilitados](#enable-forms-portal-components) antes de utilizarlos en el portal de Forms.

Para agregar un componente, arrástrelo y suéltelo desde el panel Componentes al contenedor del diseño de la página, o bien, seleccione el icono Agregar en el contenedor de diseño y agregue el componente desde el cuadro de diálogo [!UICONTROL Insertar nuevo componente].

### Configurar Borradores y envíos {#configure-drafts-submissions-component}

El componente Borradores y envíos muestra los formularios guardados como borrador para completarlos posteriormente y enviarlos. Para configurarlo, seleccione el componente y, a continuación, seleccione el icono ![Configurar](assets/configure_icon.png). En el cuadro de diálogo [!UICONTROL Borradores y envíos], especifique el título para indicar la lista del formulario como formulario borrador o enviado. Seleccione también si el componente debe enumerar los formularios borrador o enviados en formato de tarjeta o lista.

![Icono Borradores](assets/drafts-component.png)

![Icono Envíos](assets/submission-listing.png)

### Configurar el componente Buscar y listar {#configure-search-lister-component}

El componente Buscar y listar se utiliza para enumerar los formularios adaptables en una página e implementar la búsqueda en los formularios enumerados.

![Icono Buscar y listar](assets/search-and-lister-component.png)

Para configurarlo, seleccione el componente y, a continuación, seleccione el icono ![Configurar](assets/configure_icon.png). El cuadro de diálogo [!UICONTROL Buscar y listar] se abre.

1. En la pestaña [!UICONTROL Mostrar], configure lo siguiente:
   * En **[!UICONTROL Título]**, especifique el título del componente Buscar y listar. Un título indicativo permite a los usuarios realizar una búsqueda rápida en toda la lista de formularios.
   * En la lista **[!UICONTROL Diseño]**, seleccione el diseño para representar los formularios en formato de tarjeta o lista.
   * Seleccione **[!UICONTROL Ocultar búsqueda]** y **[!UICONTROL Ocultar orden]** para ocultar la búsqueda y ordenar por características.
   * En **[!UICONTROL Información de objeto]**, proporcione la información de objeto que aparece al pasar el ratón por encima del componente.
1. En la pestaña [!UICONTROL Carpeta de activos] especifique la ubicación desde la que se extraen los formularios se enumeran en la página. Puede configurar varias ubicaciones de carpetas.
1. En la pestaña [!UICONTROL Resultados] configure el número máximo de formularios que se mostrarán por página. El valor predeterminado es de ocho formularios por página.

### Configurar el componente Vínculo {#configure-link-component}

El componente Vínculo le permite proporcionar vínculos a un formulario adaptable en la página. Para configurarlo, seleccione el componente y, a continuación, seleccione el icono ![Configurar](assets/configure_icon.png). Se abrirá el cuadro de diálogo [!UICONTROL Editar el componente Vínculo].

1. En la pestaña [!UICONTROL Mostrar], proporcione el pie de ilustración del vínculo y la información del objeto para facilitar la identificación de los formularios representados por el vínculo.
1. En la pestaña [!UICONTROL Información del activo], especifique la ruta del repositorio donde se almacena el activo.
1. En la pestaña [!UICONTROL Parámetros de consulta], especifique los parámetros adicionales en el formato de par clave-valor. Cuando se hace clic en el vínculo, estos parámetros adicionales se pasan junto con el formulario.

## Configurar el envío asincrónico de formularios con Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

Puede enviar un formulario adaptable solo cuando todos los destinatarios hayan completado la ceremonia de firma. Para configurar la configuración mediante Adobe Sign, haga lo siguiente.

1. En la instancia Autor, abra un formulario adaptable en el modo de edición.
1. En el panel izquierdo, seleccione el icono Propiedades y expanda la opción **[!UICONTROL FIRMA ELECTRÓNICA]**.
1. Seleccione **[!UICONTROL Habilitar Adobe Sign]**. Se mostrarán varias opciones de configuración.
1. En la sección [!UICONTROL Enviar el formulario], seleccione la opción **[!UICONTROL después de que cada destinatario complete la ceremonia de firma]** para configurar la acción Enviar formulario, donde el formulario se enviará por primera vez a todos los destinatarios para que lo firmen. Una vez que todos los destinatarios hayan firmado el formulario, solo entonces se enviará.

## Guardar formularios adaptables como borradores {#save-adaptive-forms-as-drafts}

Los formularios se pueden guardar como borradores para completarlos más adelante. Existen dos formas de guardar un formulario como borrador:

* Crear una regla “Guardar formulario” en un componente de formulario, por ejemplo, un botón. Al hacer clic en el botón, los activadores de la regla y el formulario se guardarán como borrador.
* Habilite la característica de guardado automático, que guarda el formulario según el evento especificado o después de un intervalo de tiempo configurado.

### Crear reglas para guardar un formulario adaptable como borrador {#rule-to-save-adaptive-form-as-draft}

Para crear una regla “Guardar formulario”; en un componente de formulario, por ejemplo, un botón, haga lo siguiente:

1. En la instancia Autor, abra un formulario adaptable en modo de edición.
1. En el panel izquierdo, seleccione el icono ![Componentes](assets/components_icon.png) y arrastre el componente [!UICONTROL Botón] al formulario.
1. Seleccione el componente [!UICONTROL Botón] y, a continuación, seleccione el icono ![Configurar](assets/configure_icon.png).
1. Seleccione el icono [!UICONTROL Editar reglas] para abrir el Editor de reglas.
1. Seleccione **[!UICONTROL Crear]** para configurar y crear la regla.
1. En la sección [!UICONTROL Cuándo], seleccione “se haga clic” y en la sección [!UICONTROL Entonces] seleccione la opción “Guardar formulario”.
1. Seleccione **[!UICONTROL Listo]** para guardar la regla.

### Habilitar el guardado automático {#enable-auto-save}

Puede configurar la característica de guardado automático para un formulario adaptable de la siguiente manera:

1. En la instancia Autor, abra un formulario adaptable en modo de edición.
1. En el panel izquierdo, seleccione el icono ![Propiedades](assets/configure_icon.png) y expanda la opción [!UICONTROL GUARDAR AUTOMÁTICAMENTE].
1. Seleccione la casilla de verificación **[!UICONTROL Habilitar]** para habilitar el guardado automático del formulario. Puede configurar lo siguiente:
* De forma predeterminada, [!UICONTROL Evento de formulario adaptable] se establece en “true”, lo que significa que el formulario se guardará automáticamente después de cada evento.
* En [!UICONTROL Activador], establezca activar el guardado automático en función de la ocurrencia de un evento o después de un intervalo de tiempo específico.

## Consulte también {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->