---
title: Herramienta de migración/Herramientas de modernización de AEM para convertir Forms adaptable basado en componentes de base a formularios basados en componentes principales
description: Aprenda a instalar y utilizar la utilidad de migración/herramientas de modernización de AEM para convertir Forms adaptable basado en componentes de base en formularios basados en componentes principales.
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 8%

---

# Introducción

<span class="preview">: la característica está disponible en el programa de usuarios que la adoptaron por primera vez. Puede enviar un correo electrónico a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa para primeros usuarios y solicitar acceso a esta funcionalidad. </span>

La Utilidad de conversión de Forms, que forma parte del conjunto de aplicaciones [AEM Modernize Tool](https://opensource.adobe.com/aem-modernize-tools/), le ayuda a convertir fácilmente Forms adaptable creado con componentes de base heredados a formularios que aprovechan las capacidades modernas y compatibles de los componentes principales.

## ¿Qué son las herramientas de modernización de AEM?

[Herramientas de modernización de AEM](https://opensource.adobe.com/aem-modernize-tools/) se refiere a un conjunto de utilidades o aplicaciones de software diseñadas para facilitar el proceso de modernización o actualización de proyectos de Adobe Experience Manager (AEM). Estas herramientas suelen ayudar a convertir componentes o funcionalidades antiguas de AEM en alternativas más nuevas, eficientes y compatibles. La utilidad de conversión de Forms se instala en Herramientas de modernización de AEM Forms para convertir formularios adaptables basados en componentes de base a formularios basados en componentes principales.

La utilidad de conversión de Forms convierte los Forms adaptables basados en componentes de base antiguos en formularios basados en componentes principales más recientes. Este proceso de conversión garantiza que los formularios se alineen con los estándares y las capacidades modernas, lo que mejora potencialmente el rendimiento, la compatibilidad y la facilidad de mantenimiento dentro del entorno de AEM.

![Herramientas de modernización de AEM](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
>Se recomienda instalar las herramientas de modernización de AEM en la configuración local de AEM. Migre el Forms adaptable basado en componentes de base a formularios basados en componentes principales. Descargue el formulario junto con sus recursos. A continuación, cargue el formulario y sus recursos en el entorno requerido.

## Consideraciones al utilizar las herramientas de modernización de AEM {#considerations}

* Si las conversiones se realizan correctamente, se eliminarán todas las reglas aplicadas al formulario. Las reglas no se migran automáticamente. Debe volver a crear y aplicar manualmente estas reglas al formulario convertido.
* La configuración de traducción utilizada en el formulario original no se transfiere. Vuelva a configurar la traducción del formulario convertido.
* Si el formulario creado en Foundation Components contiene scripts o reglas de función personalizadas, debe volver a escribirlos para el formulario convertido basado en Core Components.
* Los siguientes componentes de base OOTB aún no son compatibles con los componentes principales y, por lo tanto, se eliminan en el formulario convertido:

   * Bloque de Adobe Sign
   * Gráfico
   * Lista de archivos adjuntos
   * Marcador de nota al pie
   * Opción de imagen
   * Botón Siguiente
   * Botón Anterior
   * Firma manuscrita
   * Paso de resumen
   * Barra de herramientas

## Requisitos previos para utilizar las herramientas de modernización de AEM

* [Configurar el entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md).
* Instale la última versión para habilitar los componentes principales adaptables de Forms para su entorno de AEM Cloud Service.
* Añadir sus usuarios al grupo [!DNL forms-users]. Los miembros del grupo [!DNL forms-users] tienen permisos para crear un formulario adaptable.
* Los usuarios con las siguientes funciones tienen los permisos para instalar las herramientas de modernización de AEM en un entorno de AEM:

   * Función Desarrollador
   * Función de administrador

Para obtener una lista detallada de los grupos de usuarios específicos de formularios, consulte [Grupos y permisos](forms-groups-privileges-tasks.md).

## Instalación y configuración de las herramientas de modernización de AEM

Para instalar y configurar las herramientas de modernización de AEM:

1. [Instalación de las herramientas de modernización de AEM en el entorno local de AEM Forms](#install-aem-modernize-Tools)
1. [Habilitar las herramientas de modernización de AEM para su entorno local de AEM Forms](#enable-aem-modernize-Tools)

### Instalación de las herramientas de modernización de AEM en el entorno local de AEM Forms {#install-aem-modernize-Tools}

Siga estos pasos para instalar las herramientas de modernización de AEM en el entorno local de AEM Forms:

1. Abra el símbolo de comando o el terminal.
1. Inicie el servicio local de AEM Author. Por ejemplo, ejecute el siguiente código desde el para iniciar la instancia de autor local de AEM:

   `java -jar aem-author-p4502.jar`

1. Clone el repositorio [AEM Modernize Tool](https://github.com/adobe/forms-modernizer) en su sistema local.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   Después de ejecutar el comando correctamente, tiene una copia local del repositorio de la herramienta de modernización de AEM disponible en el equipo.

1. Vaya a `[AEM Modernize Tool Repository]` en el sistema local.
1. Ejecute el siguiente comando:

   ```Shell
       mvn clean install 
   ```

![Imagen de instalación correcta](/help/forms/assets/aem-modernize-install-steps.png)

Una vez completada la instalación, las herramientas de modernización de AEM estarán disponibles para su entorno.

![Habilitar la herramienta de migración de AEM](/help/forms/assets/enable-aem-modernizer-tools.png)


### Habilitar las herramientas de modernización de AEM para su entorno local de AEM Forms{#enable-aem-modernize-Tools}

Para habilitar y utilizar las herramientas de modernización de AEM para su entorno de AEM, es importante asignar las reglas para migrar componentes de base a componentes principales:

1. Inicie sesión en la instancia de autor.
1. Navegue hasta `http://[host]:[port]/system/console/configMgr`
1. Busque y edite `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Agregar `Component Rule Paths` como `/apps/forms-modernizer/rules`.
1. Haga clic en **Guardar** para guardar los cambios.

![Regla de componente de modernización de AEM](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Ejecute la utilidad de conversión de formularios para convertir formularios basados en componentes básicos a formularios basados en componentes principales

1. Vaya a **[!UICONTROL Herramientas > Herramientas de modernización AEM > Conversión Forms]**.

   ![Seleccionar herramientas de modernización de AEM](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Seleccione la opción **[!UICONTROL Conversión de Forms]**.

   ![Seleccionar opción de conversión de Forms](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Haga clic en **Crear** para crear un nuevo trabajo.

   ![Trabajo de creación de herramientas de modernización de AEM](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Especifique **[!UICONTROL Nombre de trabajo]**.
1. En la ficha **[!UICONTROL Formulario]**, puede seleccionar una de las siguientes opciones:

   * **Ninguno**: seleccione la opción si no desea crear una copia de los formularios basados en el componente Foundation antes de iniciar la conversión del formulario.
   * **Restaurar**: seleccione la opción para restaurar el formulario al estado en el que se encontraba antes de iniciar la conversión del formulario.
   * **Copiar en Target**: seleccione la opción para crear una copia de los formularios basados en el componente Foundation antes de iniciar la conversión del formulario.

   En nuestro caso, la opción **Copiar a destino** está seleccionada. Si se selecciona la opción **Copiar a destino**, las opciones **[!UICONTROL Ruta de Source]** y **[!UICONTROL Ruta de destino]** se volverán visibles.

1. Especifique el nombre de `source folder` en la **[!UICONTROL ruta de acceso de Source]**.
1. Especifique el nombre de `target folder` en la **[!UICONTROL ruta de destino]**.
1. Seleccione **[!UICONTROL Siguiente]**.
1. Haz clic en **[!UICONTROL Agregar Forms]**. Todos los formularios de `source folder` aparecen en la pantalla.
1. Seleccione el Forms adaptable basado en componentes de base para convertirlo en formularios basados en componentes principales. También puede seleccionar varios formularios.

   ![Formulario de selección de herramientas de modernización de AEM](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Haga clic en **[!UICONTROL Seleccionar]**.
1. Haga clic en **[!UICONTROL Programar trabajo]** para iniciar el proceso de conversión.
1. Haga clic en **[!UICONTROL Convertir]** en el cuadro de diálogo **[!UICONTROL Convertir páginas]**.

   ![Herramientas de modernización de AEM para convertir páginas](/help/forms/assets/aem-modernize-tools-convert-form.png)

   Cuando el estado del proceso se cambie a `success`. Vaya a `target folder` para ver el formulario convertido.

   ![Éxito en la modernización de herramientas de AEM](/help/forms/assets/aem-modernize-tools-success.png)

1. Seleccione el formulario adaptable y seleccione > **[!UICONTROL Propiedades]**. Se abre la página Propiedades del formulario.

   ![Carpeta de destino de herramientas de modernización de AEM](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Seleccione **[!UICONTROL Guardar y cerrar]** para volver a guardar las propiedades del formulario convertido.
   ![Propiedades de formulario adaptable de las herramientas de modernización de AEM](/help/forms/assets/aem-modernize-tools-af-properties.png)

Ahora puede ver que el formulario adaptable creado en los componentes de base se transforma en el formulario adaptable creado en los componentes principales.

## Prácticas recomendadas {#best-practices}

* Asegúrese de que los formularios basados en componentes de base utilicen únicamente los componentes que tengan [componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type) equivalentes disponibles. En los casos en los que se utilizan componentes de base que no tienen un componente principal equivalente, el componente de base no se convierte. Como resultado, no funciona correctamente al crear un formulario
* Asegúrese de que las reglas para convertir los componentes de base en componentes principales tengan formato XML.
