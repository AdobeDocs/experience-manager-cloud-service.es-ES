---
title: Utilidad de migración para convertir Forms adaptable basado en componentes de base en formularios basados en componentes principales
description: Aprenda a instalar y utilizar la utilidad de migración para convertir el Forms adaptable basado en componentes de base en formularios basados en componentes principales.
Keywords: Migration Utility tool, Convert Adaptive Forms based on foundation components to core component based forms, Convert Foundation forms to Core components forms, Using Modernizer tool to convert Foundation Components to Core components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 4%

---


# Introducción

Puede utilizar la utilidad de migración para convertir el Forms adaptable basado en componentes básicos a formularios principales basados en componentes. Puede usar el complemento [AEM Herramienta Modernizar de](https://opensource.adobe.com/aem-modernize-tools/) como herramienta de utilidad de migración. El [AEM Herramientas de modernización de](https://opensource.adobe.com/aem-modernize-tools/) proporciona un conjunto de utilidades utilizadas para convertir el Forms adaptable basado en componentes de base a las capacidades modernas y compatibles de los componentes principales.

## AEM ¿Qué son las herramientas de modernización de?

[AEM Herramientas de modernización de](https://opensource.adobe.com/aem-modernize-tools/) hace referencia a un conjunto de utilidades o aplicaciones de software diseñadas para facilitar el proceso de modernización o actualización de proyectos de Adobe Experience Manager AEM (). AEM Estas herramientas suelen ayudar a convertir componentes o funcionalidades antiguos dentro de la aplicación a alternativas más nuevas, eficientes y compatibles.

AEM Herramientas de modernización convierte Forms adaptable basado en componentes de base antiguos en formularios basados en componentes principales más nuevos. AEM Este proceso de conversión garantiza que los formularios se alineen con los estándares y las capacidades modernas, lo que mejora potencialmente el rendimiento, la compatibilidad y la facilidad de mantenimiento dentro del entorno de la.

![AEM Herramientas de modernización de](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
> AEM AEM Se recomienda instalar las herramientas de modernización de la local. Migre los formularios basados en la base a los formularios basados en componentes principales. Descargue el formulario junto con sus recursos. A continuación, cargue el formulario y sus recursos en el entorno requerido.

## AEM Requisitos previos para utilizar las herramientas de modernización de

* [Configurar un entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md)
* [Habilite los componentes principales de Forms adaptable para su entorno.](/help/forms/enable-adaptive-forms-core-components.md)

* Añada los usuarios a [!DNL forms-users] grupo. Los miembros del grupo [!DNL forms-users] tienen permisos para crear un formulario adaptable.

* AEM AEM Los usuarios con las siguientes funciones tienen los permisos para instalar las herramientas de modernización de dentro de un entorno de trabajo:
   * Función Desarrollador
   * Función de administrador Para obtener una lista detallada de los grupos de usuarios específicos de los formularios, consulte [Grupos y permisos](forms-groups-privileges-tasks.md).

## AEM Instalación y configuración de herramientas de modernización de

AEM Pasos para instalar y configurar las herramientas de Modernización de la:

1. [AEM Instalación de herramientas de modernización de la en el entorno local de AEM Forms](#install-aem-modernize-tools)
2. [AEM Habilite las herramientas de modernización de recursos para su entorno local de AEM Forms](#enable-aem-modernize-tools)

### AEM Instalación de herramientas de modernización de la en el entorno local de AEM Forms {#install-aem-modernize-tools}

AEM Siga estos pasos para instalar las herramientas de modernización de la en el entorno local de AEM Forms:

1. AEM Inicie el servicio local de creación de ejecutando lo siguiente desde la línea de comandos:

   `java -jar aem-author-p4502.jar`

   >[!NOTE]
   >
   > Proporcione la contraseña de administrador como `admin`. Cualquier contraseña de administrador es aceptable, pero se recomienda utilizar la predeterminada para el desarrollo local con el fin de reducir la necesidad de volver a configurar.

1. Clonar el [AEM Herramientas de modernización de](https://git.corp.adobe.com/livecycle/forms-modernizer/tree/convertForms) repositorio en el sistema local.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tools]
   ```
   Reemplace el [AEM Ruta del repositorio Git de las herramientas de modernización de la] AEM con la dirección URL real del repositorio de Git correspondiente de las herramientas de modernización de la.
AEM Después de ejecutar el comando correctamente, tiene una copia local del repositorio de herramientas de modernización de la disponible en el equipo.

1. Vaya a`[AEM Modernize Tools Repository]`  en su sistema local.
1. Ejecute el siguiente comando:

   ```Shell
       mvn clean install 
   ```
![Imagen de instalación correcta](/help/forms/assets/aem-modernize-install-steps.png)

AEM Después de la instalación correcta, las herramientas de modernización de la estarán disponibles para su entorno.

![AEM Activar herramientas de modernización de la](/help/forms/assets/enable-aem-modernizer-tools.png)


### AEM Habilite las herramientas de modernización de recursos para su entorno local de AEM Forms{#enable-aem-modernize-tools}

AEM AEM Para habilitar y utilizar las herramientas de modernización de la para su entorno de trabajo, es importante asignar las reglas para migrar componentes de base a componentes principales:

1. Inicie sesión en la instancia de autor.
1. Navegue hasta `http://[host]:[port]/system/console/configMgr`
1. Busque y edite el `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Añada el `Component Rule Paths` as `/apps/forms-modernizer/rules`.
1. Clic **Guardar** para guardar los cambios.

![AEM Regla de componente de modernización](/help/forms/assets/aem-modernize-tools-component-rule.png)

## AEM Ejecute Herramientas de modernización para convertir formularios basados en componentes de base en formularios basados en componentes principales

1. Ir a **[!UICONTROL AEM Herramientas > Actualizar herramientas > Conversión de Forms]**.

   ![AEM Seleccionar herramientas de modernización](/help/forms/assets/aem-modernize-tools-select.png)

1. Seleccione el **[!UICONTROL Conversión de Forms]** opción.

   ![Seleccione la opción Conversión de Forms](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Clic **Crear** para crear un nuevo trabajo.

   ![AEM Herramientas de modernización Crear trabajo](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Especifique el **[!UICONTROL Nombre de trabajo]**.
1. En el **[!UICONTROL Form]** , puede seleccionar una de las siguientes opciones:
   * **Ninguno** : seleccione esta opción si no es necesario administrar el formulario.
   * **Restaurar** : seleccione esta opción para restaurar el formulario al estado anterior a la última conversión.
   * **Copiar en destino**: seleccione esta opción para copiar el formulario antes de realizar la conversión.
En nuestro caso, la variable **Copiar en destino** La opción está seleccionada. Si la variable **Copiar en destino** está seleccionada, la opción **[!UICONTROL Ruta de origen]** y **[!UICONTROL Ruta de destino]** opciones se vuelven visibles.

1. Especifique el `source folder` nombre en el **[!UICONTROL Ruta de origen]**.
1. Especifique el `target folder` nombre en el **[!UICONTROL Ruta de destino]**.
1. Seleccione **[!UICONTROL Siguiente]**.
1. Haga clic en **[!UICONTROL Añadir Forms]**. Todos los formularios del `source folder` aparece en la pantalla.
1. Seleccione el formulario basado en componentes de base para convertirlo en un formulario basado en componentes principales. También puede seleccionar varios formularios.

   ![AEM Herramientas Seleccionar formulario](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Clic **[!UICONTROL Seleccionar]**.
1. Clic **[!UICONTROL Programar trabajo]** para iniciar el proceso de conversión.
1. Clic **[!UICONTROL Convertir]** desde el **[!UICONTROL Convertir páginas]** Cuadro de diálogo.

   ![AEM Herramientas Convertir páginas](/help/forms/assets/aem-modernize-tools-convert-form.png)

   Cuando el estado del proceso se cambie a `success`. Vaya a `target folder` para ver el formulario convertido.

   ![AEM Éxito de modernización de herramientas](/help/forms/assets/aem-modernize-tools-success.png)

1. Seleccione el formulario adaptable y seleccione > **[!UICONTROL Propiedades]**. Se abre la página Propiedades del formulario.
   ![AEM Carpeta de destino de herramientas de modernización](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Seleccionar **[!UICONTROL Guardar y cerrar]** para volver a guardar las propiedades del formulario convertido.
   ![AEM Propiedades del formulario adaptable de las herramientas de modernización](/help/forms/assets/aem-modernize-tools-af-properties.png)

Ahora puede ver que el formulario adaptable creado sobre los componentes de base se transforma en el formulario adaptable creado sobre los componentes principales.

## Consideraciones al utilizar la herramienta Utilidad de migración {#considerations}

* Si el formulario creado a partir de componentes de base contiene reglas de función personalizadas, debe reescribir estas reglas para el formulario convertido en función de los componentes principales.
* El formulario convertido no incluye ninguna regla en el editor de reglas, lo que requiere la reescritura de reglas para el formulario convertido.
* Debe volver a crear el trabajo de traducción para el formulario convertido.

## Prácticas recomendadas {#best-practices}

* El formulario creado en los componentes de base incluye solo los componentes que se encuentran en los componentes principales basados en componentes.
* Asegúrese de que las reglas tengan formato XML.


