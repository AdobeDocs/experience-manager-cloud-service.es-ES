---
title: AEM Herramienta de utilidad de migración/Herramientas de modernización de la para convertir Forms adaptable basado en componentes de base a formularios basados en componentes principales
description: AEM Aprenda a instalar y utilizar la utilidad de migración/herramientas de modernización de la para convertir Forms adaptable basado en componentes de base en formularios basados en componentes principales.
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 7%

---

# Introducción

<span class="preview">: la característica está disponible en el programa de usuarios que la adoptaron por primera vez. Puede enviar un correo electrónico a aem-forms-ea@adobe.com desde su ID oficial para unirse al programa de usuarios pioneros y solicitar acceso a esta funcionalidad. </span>

La utilidad de conversión de Forms AEM, que forma parte del conjunto de herramientas de modernización [&#128279;](https://opensource.adobe.com/aem-modernize-tools/), le ayuda a convertir fácilmente Forms adaptable creado con componentes básicos heredados en formularios que aprovechan las capacidades modernas y compatibles de los componentes principales.

## AEM ¿Qué son las herramientas de modernización de?

AEM [Herramientas de modernización](https://opensource.adobe.com/aem-modernize-tools/) se refiere a un conjunto de utilidades o aplicaciones de software diseñadas para facilitar el proceso de modernización o actualización de proyectos de Adobe Experience Manager AEM (). AEM Normalmente, estas herramientas ayudan a convertir componentes o funcionalidades antiguas dentro de la aplicación a alternativas más nuevas, eficientes y compatibles. La utilidad de conversión de Forms AEM Forms se instala en Herramientas de modernización de la para convertir formularios adaptables basados en componentes de base a formularios basados en componentes principales.

La utilidad de conversión de Forms convierte los Forms adaptables basados en componentes de base antiguos en formularios basados en componentes principales más recientes. AEM Este proceso de conversión garantiza que los formularios se alineen con los estándares y las capacidades modernas, lo que mejora potencialmente el rendimiento, la compatibilidad y la facilidad de mantenimiento dentro del entorno de la.

AEM ![Herramientas de modernización de](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
>AEM AEM Se recomienda instalar las herramientas de modernización de la local. Migre el Forms adaptable basado en componentes de base a formularios basados en componentes principales. Descargue el formulario junto con sus recursos. A continuación, cargue el formulario y sus recursos en el entorno requerido.

## AEM Consideraciones al utilizar las herramientas de modernización de la {#considerations}

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

## AEM Requisitos previos para utilizar las herramientas de modernización de

* [Configurar el entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md).
* [Habilite los componentes principales de Forms adaptable para su entorno](/help/forms/enable-adaptive-forms-core-components.md).
* Agregue los usuarios al grupo [!DNL forms-users]. Los miembros del grupo [!DNL forms-users] tienen permisos para crear un formulario adaptable.
* AEM AEM Los usuarios con las siguientes funciones tienen los permisos para instalar las herramientas de modernización de dentro de un entorno de trabajo:

   * Función Desarrollador
   * Función de administrador

Para obtener una lista detallada de los grupos de usuarios específicos de formularios, consulte [Grupos y permisos](forms-groups-privileges-tasks.md).

## AEM Instalación y configuración de herramientas de modernización de

AEM Para instalar y configurar las herramientas de modernización de la:

1. [AEM Instalación de herramientas de modernización de la en el entorno local de AEM Forms](#install-aem-modernize-Tools)
1. [AEM Habilite las herramientas de modernización de recursos para su entorno local de AEM Forms](#enable-aem-modernize-Tools)

### AEM Instalación de herramientas de modernización de la en el entorno local de AEM Forms {#install-aem-modernize-Tools}

AEM Siga estos pasos para instalar las herramientas de modernización de la en el entorno local de AEM Forms:

1. Abra el símbolo de comando o el terminal.
1. AEM Inicie el servicio local de creación de. AEM Por ejemplo, ejecute el siguiente código desde el para iniciar la instancia local de autor de la:

   `java -jar aem-author-p4502.jar`

1. AEM Clona el repositorio [Herramienta de modernización de](https://github.com/adobe/forms-modernizer) en tu sistema local.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   AEM Después de ejecutar el comando correctamente, tiene disponible en su equipo una copia local del repositorio de la herramienta de modernización de la.

1. Vaya a `[AEM Modernize Tool Repository]` en el sistema local.
1. Ejecute el siguiente comando:

   ```Shell
       mvn clean install 
   ```

![Imagen de instalación correcta](/help/forms/assets/aem-modernize-install-steps.png)

AEM Después de la instalación correcta, las herramientas de modernización de la estarán disponibles para su entorno.

AEM ![Habilitar herramienta de utilidad de migración de datos](/help/forms/assets/enable-aem-modernizer-tools.png)


### AEM Habilite las herramientas de modernización de recursos para su entorno local de AEM Forms{#enable-aem-modernize-Tools}

AEM AEM Para habilitar y utilizar las herramientas de modernización de la para su entorno de trabajo, es importante asignar las reglas para migrar componentes de base a componentes principales:

1. Inicie sesión en la instancia de autor.
1. Navegue hasta `http://[host]:[port]/system/console/configMgr`
1. Busque y edite `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Agregar `Component Rule Paths` como `/apps/forms-modernizer/rules`.
1. Haga clic en **Guardar** para guardar los cambios.

AEM ![Actualizar Regla De Componente](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Ejecute la utilidad de conversión de formularios para convertir formularios basados en componentes básicos a formularios basados en componentes principales

1. AEM Vaya a **[!UICONTROL Herramientas > Herramientas de modernización de la > Conversión de Forms]**.

   AEM ![Seleccionar Herramientas De Modernización De La](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Seleccione la opción **[!UICONTROL Conversión de Forms]**.

   ![Seleccionar opción de conversión de Forms](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Haga clic en **Crear** para crear un nuevo trabajo.

   AEM ![Actualizar herramientas Crear trabajo](/help/forms/assets/aem-modernize-tools-create-job.png)

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

   AEM ![Actualizar herramientas Seleccionar formulario](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Haga clic en **[!UICONTROL Seleccionar]**.
1. Haga clic en **[!UICONTROL Programar trabajo]** para iniciar el proceso de conversión.
1. Haga clic en **[!UICONTROL Convertir]** en el cuadro de diálogo **[!UICONTROL Convertir páginas]**.

   AEM ![Actualizar herramientas Convertir páginas](/help/forms/assets/aem-modernize-tools-convert-form.png)

   Cuando el estado del proceso se cambie a `success`. Vaya a `target folder` para ver el formulario convertido.

   AEM ![Éxito en la modernización de herramientas de](/help/forms/assets/aem-modernize-tools-success.png)

1. Seleccione el formulario adaptable y seleccione > **[!UICONTROL Propiedades]**. Se abre la página Propiedades del formulario.

   AEM ![Carpeta De Destino De Herramientas De Modernización De](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Seleccione **[!UICONTROL Guardar y cerrar]** para volver a guardar las propiedades del formulario convertido.
   AEM ![Propiedades del formulario adaptable de las herramientas de modernización de](/help/forms/assets/aem-modernize-tools-af-properties.png)

Ahora puede ver que el formulario adaptable creado en los componentes de base se transforma en el formulario adaptable creado en los componentes principales.

## Prácticas recomendadas {#best-practices}

* Asegúrese de que los formularios basados en componentes de base utilicen únicamente los componentes que tengan [componentes principales](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type) equivalentes disponibles. En los casos en los que se utilizan componentes de base que no tienen un componente principal equivalente, el componente de base no se convierte. Como resultado, no funciona correctamente al crear un formulario
* Asegúrese de que las reglas para convertir los componentes de base en componentes principales tengan formato XML.
