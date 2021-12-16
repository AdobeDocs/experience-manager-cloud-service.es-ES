---
title: ¿Cómo se crea un portal de Forms en una página de Experience Manager Sites?
description: Obtenga información sobre cómo crear un portal de Forms y utilizar componentes principales listos para usar en una página de AEM Sites.
source-git-commit: 4c42abfe2cc1b11aefb2b298e883406ca5c17fd2
workflow-type: tm+mt
source-wordcount: '1753'
ht-degree: 1%

---


# Enumerar Forms adaptable en un portal {#publish-forms-on-portal}

En un escenario típico de implementación de portal centrado en formularios, el desarrollo de formularios y el desarrollo de portales son dos actividades separadas. Mientras los diseñadores de formularios diseñan y almacenan formularios en un repositorio, los desarrolladores web crean una aplicación web para enumerar formularios y gestionar el envío de formularios. Forms se copia en el nivel web, ya que no hay comunicación entre el repositorio de formularios y la aplicación web.

Estos escenarios suelen dar lugar a problemas de gestión y retrasos en la producción. Por ejemplo, si hay una versión más reciente de un formulario disponible en el repositorio, debe reemplazar el formulario en el nivel web, modificar la aplicación web y volver a implementar el formulario en el sitio público. La reimplementación de la aplicación web puede causar cierto tiempo de inactividad en el servidor. Normalmente, el tiempo de inactividad del servidor es una actividad planificada y, por lo tanto, los cambios no se pueden insertar instantáneamente en el sitio público.

AEM Forms proporciona componentes del portal que reducen los gastos generales de administración y los retrasos en la producción. Los componentes equipan a los desarrolladores web para crear y personalizar un portal de Forms en sitios web creados con Adobe Experience Manager (AEM).

Los componentes de Form Portal le permiten añadir las siguientes funciones:

* Enumerar formularios en diseños personalizados. De forma predeterminada, se proporcionan los diseños Vista de lista y Vista de tarjeta . Puede crear sus propios diseños personalizados.
* Permite mostrar metadatos personalizados y acciones personalizadas al enumerarlos.
* Enumere los formularios publicados por la interfaz de usuario de AEM Forms en la instancia de publicación en la que se utilizan los componentes de Forms Portal.
* Permita que los usuarios finales procesen formularios en formato HTML y PDF.
* Habilite la búsqueda de formularios en función del título y la descripción.
* Utilice CSS personalizada para personalizar el aspecto del portal.
* Cree vínculos a formularios.
* Enumera borradores y envíos relacionados con Forms adaptable creados por el usuario final.

## Componentes de una página del portal de Forms {#forms-portal-components}

AEM Forms proporciona los siguientes componentes de portal predeterminados:

* Buscar y listar: Este componente le permite enumerar formularios del repositorio de formularios en la página del portal y proporciona opciones de configuración para enumerar formularios basados en criterios específicos.

* Borradores y envíos: Mientras que el componente Buscar y listar muestra los formularios que publica el autor de Forms, el componente Borradores y envíos muestra los formularios guardados como borrador para completarlos posteriormente y enviarlos. Este componente proporciona una experiencia personalizada a cualquier usuario que haya iniciado sesión.

* Vínculo: Este componente le permite crear un vínculo a un formulario en cualquier parte de la página.

Puede [importación de los componentes listos para usar del portal de Forms](#import-forms-portal-components-aem-archetype) del tipo de archivo del proyecto de AEM. Después de la importación, realice las siguientes configuraciones:
* [Configuración de un almacenamiento externo](#configure-azure-storage-adaptive-forms)
* [Activación de los componentes de Forms Portal](#enable-forms-portal-components)
* [Configuración de los componentes de Forms Portal](#configure-forms-portal-components)

## Importar componentes del portal de Forms {#import-forms-portal-components-aem-archetype}

Para importar componentes listos para usar de Forms Portal en AEM Forms as a Cloud Service, realice los siguientes pasos:

1. **Clonar repositorio Git de Cloud Manager en la instancia de desarrollo local:**  El repositorio Git de Cloud Manager contiene un proyecto de AEM predeterminado. Se basa en [Tipo de archivo AEM](https://github.com/adobe/aem-project-archetype/). Clona el repositorio Git de Cloud Manager mediante la administración de cuentas Git de autoservicio de la interfaz de usuario de Cloud Manager para llevar el proyecto a su entorno de desarrollo local. Para obtener más información sobre el acceso al repositorio, consulte [Acceso a repositorios](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

1. **Crear [!DNL Experience Manager Forms] como [Cloud Service] proyecto:** Crear [!DNL Experience Manager Forms] como [Cloud Service] proyecto basado en [AEM Tipo de archivo 27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) o posterior. El arquetipo ayuda a los desarrolladores a empezar a desarrollarse fácilmente para [!DNL AEM Forms] as a Cloud Service. También incluye algunos temas de muestra y plantillas para ayudarle a empezar rápidamente.

   Para crear [!DNL Experience Manager Forms] proyecto as a Cloud Service, abra el símbolo del sistema y ejecute el siguiente comando. Para incluir [!DNL Forms] configuraciones, temas y plantillas específicos, establezca `includeForms=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Además, cambie `appTitle`, `appId`y `groupId`, en el comando anterior para reflejar su entorno.

1. **Implemente el proyecto en su entorno de desarrollo local:** Puede utilizar el siguiente comando para implementar en el entorno de desarrollo local

   `mvn -PautoInstallPackage clean install`

   Para obtener la lista completa de comandos, consulte [Creación e instalación](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Incluir los artefactos del componente principal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds) y la dependencia como se indica a continuación:

   ```shell
   <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>{TBD}</artifactId>
               <type>content-package</type>
               <version>{TBD}</version>
   </dependency>
   ```

1. [Implemente el código en su [!DNL AEM Forms] Entorno as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds).


## Configuración del almacenamiento de Azure para Forms adaptable {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Integración de datos](data-integration.md) proporciona [!DNL Azure] configuración de almacenamiento para integrar formularios con [!DNL Azure] servicios de almacenamiento. El Modelo de datos de formulario se puede utilizar para crear un Forms adaptable que interactúe con [!DNL Azure] para habilitar los flujos de trabajo empresariales.

### Crear configuración de almacenamiento de Azure {#create-azure-storage-configuration}

Antes de ejecutar estos pasos, asegúrese de que dispone de un [!DNL Azure] cuenta de almacenamiento y clave de acceso para autorizar el acceso a [!DNL Azure] cuenta de almacenamiento.

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Almacenamiento de Azure]**.
1. Seleccione una carpeta para crear la configuración y pulse **[!UICONTROL Crear]**.
1. Especifique un título para la configuración en la **[!UICONTROL Título]** campo .
1. Especifique el nombre del [!DNL Azure] cuenta de almacenamiento en la variable **[!UICONTROL Cuenta de almacenamiento de Azure]** campo .

### Configuración del conector de almacenamiento unificado para Forms Portal {#configure-usc-forms-portal}

Realice los siguientes pasos para configurar el conector de almacenamiento unificado para AEM flujos de trabajo:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de almacenamiento unificado]**.
1. En el **[!UICONTROL Portal de Forms]** , seleccione **[!UICONTROL Azure]** de la variable **[!UICONTROL Almacenamiento]** lista desplegable.
1. Especifique la variable [ruta de configuración para la configuración de almacenamiento de Azure](#create-azure-storage-configuration) en el **[!UICONTROL Ruta de configuración de almacenamiento]** campo .
1. Toque **[!UICONTROL Publicación]** y, a continuación, toque **[!UICONTROL Guardar]** para guardar la configuración.

## Habilitar componentes de Forms Portal {#enable-forms-portal-components}

Para utilizar cualquier componente principal (incluidos los componentes de portal predeterminados) en un sitio de Adobe Experience Manager (AEM), debe crear un componente proxy y habilitarlo para su sitio. Para crear un componente proxy y activar los componentes del portal, consulte [Uso de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components).

Una vez habilitado un componente de portal, puede utilizarlo en la instancia de autor de la página de sitios.

## Añadir y configurar componentes del portal de Forms {#configure-forms-portal-components}

Puede crear y personalizar Forms Portal en sitios web creados mediante AEM añadiendo y configurando los componentes del portal. Asegúrese de que la variable [los componentes están activados](#enable-forms-portal-components) antes de utilizarlos en el portal de Forms.

Para agregar un componente, arrástrelo y suéltelo desde el panel Componentes al contenedor de diseño de la página, o bien, pulse el icono Agregar en el contenedor de diseño y agregue el componente desde el panel Componentes [!UICONTROL Insertar nuevo componente] diálogo.

### Configurar Borradores y envíos {#configure-drafts-submissions-component}

El componente Borradores y envíos muestra los formularios guardados como borrador para completarlos posteriormente y enviarlos. Para configurar, pulse el componente y, a continuación, pulse el botón ![Icono Configurar](assets/configure_icon.png). En el [!UICONTROL Borradores y presentaciones] , especifique el título para indicar la lista del formulario como formulario borrador o enviado. Seleccione también si el componente debe enumerar los formularios borrador o enviados en formato de tarjeta o lista.

![Icono Borradores](assets/drafts-component.png)

![Icono de envíos](assets/submission-listing.png)

### Configurar el componente Búsqueda y listado {#configure-search-lister-component}

El componente Búsqueda y lista se utiliza para enumerar los formularios adaptables en una página e implementar la búsqueda en los formularios enumerados.

![Icono Buscar y listar](assets/search-and-lister-component.png)

Para configurar, pulse el componente y, a continuación, pulse el botón ![Icono Configurar](assets/configure_icon.png). La variable [!UICONTROL Buscar y listar] se abre.

1. En el [!UICONTROL Mostrar] , configure lo siguiente:
   * En **[!UICONTROL Título]**, especifique el título del componente Búsqueda y lista . Un título indicativo permite a los usuarios realizar una búsqueda rápida en toda la lista de formularios.
   * En el **[!UICONTROL Diseño]** , seleccione la presentación para representar los formularios en formato de tarjeta o lista.
   * Select **[!UICONTROL Ocultar búsqueda]** y **[!UICONTROL Ocultar ordenación]** para ocultar la búsqueda y ordenar por características.
   * En **[!UICONTROL Información de objeto]**, proporcione la información de objeto que aparece al pasar el ratón por encima del componente.
1. En el [!UICONTROL Carpeta de recursos] especifique la ubicación desde la que se extraen los formularios y aparezca en la página. Puede configurar varias ubicaciones de carpetas.
1. En el [!UICONTROL Resultados] configure el número máximo de formularios que se mostrarán por página. El valor predeterminado es de ocho formularios por página.

### Configurar componente de vínculo {#configure-link-component}

El componente de vínculo le permite proporcionar vínculos a un formulario adaptable en la página. Para configurar, pulse el componente y, a continuación, pulse el botón ![Icono Configurar](assets/configure_icon.png). La variable [!UICONTROL Editar componente de vínculo] se abre.

1. En el [!UICONTROL Mostrar] , proporcione el rótulo del vínculo y la información del objeto para facilitar la identificación de los formularios representados por el vínculo.
1. En el [!UICONTROL Información del recurso] , especifique la ruta del repositorio donde se almacena el recurso.
1. En el [!UICONTROL Parámetros de consulta] , especifique los parámetros adicionales en el formato de par clave-valor. Cuando se hace clic en el vínculo, estos parámetros adicionales se pasan junto con el formulario.

## Configuración del envío asincrónico de formularios con Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

Puede configurar para enviar un formulario adaptable solo cuando todos los destinatarios hayan completado la ceremonia de firma. Siga los pasos a continuación para configurar la configuración mediante Adobe Sign.

1. En la instancia de autor, abra un formulario adaptable en el modo de edición.
1. En el panel izquierdo, pulse el icono Propiedades y expanda el **[!UICONTROL SEÑALIZACIÓN ELECTRÓNICA]** .
1. Select **[!UICONTROL Habilitar Adobe Sign]**. Se muestran varias opciones de configuración.
1. En el [!UICONTROL Enviar el formulario] seleccione **[!UICONTROL después de que cada destinatario complete la ceremonia de firma]** para configurar la acción Enviar formulario, donde el formulario se envía por primera vez a todos los destinatarios para que lo firmen. Una vez que todos los destinatarios han firmado el formulario, solo entonces se envía.

## Guardar Forms adaptable como borradores {#save-adaptive-forms-as-drafts}

Los formularios se pueden guardar como Borradores para completarlos más adelante. Existen dos formas de guardar un formulario como borrador:
* Cree una regla &quot;Guardar formulario&quot; en un componente de formulario, por ejemplo un botón. Al hacer clic en el botón , los déclencheur de regla y el formulario se guardan como borrador.
* Habilite la función de guardado automático, que guarda el formulario según el evento especificado o después de un intervalo de tiempo configurado.

### Crear reglas para guardar un formulario adaptable como borrador {#rule-to-save-adaptive-form-as-draft}

Para crear una regla &quot;Guardar formulario&quot; en un componente de formulario, por ejemplo un botón, siga los pasos a continuación:

1. En la instancia de autor, abra un formulario adaptable en modo de edición.
1. En el panel izquierdo, pulse ![Icono de componentes](assets/components_icon.png) y arrastre el [!UICONTROL Botón] al formulario.
1. Toque . [!UICONTROL Botón] y, a continuación, toque el ![Icono Configurar](assets/configure_icon.png).
1. Toque . [!UICONTROL Editar reglas] para abrir el Editor de reglas.
1. Toque **[!UICONTROL Crear]** para configurar y crear la regla.
1. En el [!UICONTROL When] , seleccione &quot;se hace clic&quot; y en la [!UICONTROL Entonces] seleccione las opciones &quot;Guardar formulario&quot;.
1. Toque **[!UICONTROL Listo]** para guardar la regla.

### Habilitar el guardado automático {#enable-auto-save}

Puede configurar la función de guardado automático para un formulario adaptable de la siguiente manera:

1. En la instancia de autor, abra un formulario adaptable en modo de edición.
1. En el panel izquierdo, pulse el botón ![Icono Propiedades](assets/configure_icon.png) y expanda el [!UICONTROL GUARDAR AUTOMÁTICAMENTE] .
1. Seleccione el **[!UICONTROL Habilitar]** para habilitar el guardado automático del formulario. Puede configurar lo siguiente:
* De forma predeterminada, la variable [!UICONTROL Evento de formulario adaptable] se establece en &quot;true&quot;, lo que significa que el formulario se guarda automáticamente después de cada suceso.
* En [!UICONTROL Déclencheur], configure en déclencheur el guardado automático en función de la aparición de un evento o después de un intervalo de tiempo específico.
