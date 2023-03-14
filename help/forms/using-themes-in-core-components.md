---
title: Crear y usar temáticas
description: Puede utilizar temáticas para estilizar y proporcionar una identidad visual a un formulario adaptable mediante componentes principales. Puede compartir una temática en cualquier número de formularios adaptables.
source-git-commit: ca61b72fd442cf50319861d5d8e6d23343056358
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 19%

---


# Temáticas en Forms adaptable (componentes principales) {#themes-for-af-using-core-components}

Puede crear y aplicar temáticas para diseñar un formulario adaptable mediante componentes principales. Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar una temática, el estilo especificado se refleja en los componentes correspondientes. La temática se administra de forma independiente sin hacer referencia a un formulario adaptable.

Cuando usted [crear un formulario adaptable](/help/forms/creating-adaptive-form.md) Al utilizar los componentes principales, las temáticas predeterminadas aparecen en la **Estilo** pestaña. De forma predeterminada, solo la variable **Lienzo** tema está disponible.

>[!NOTE]
>
>Una temática de formulario adaptable no debe confundirse con [Plantillas de formulario adaptable.](/help/forms/template-editor.md) Las temáticas de formularios adaptables solo contienen la información de estilo de un formulario adaptable. Las plantillas de formulario adaptable definen la estructura del formulario y el contenido inicial, y contienen una temática para permitir la creación de nuevas plantillas [Formulario adaptable.](/help/forms/creating-adaptive-form.md)

## Uso de la temática Lienzo en Forms adaptable mediante componentes principales {#using-theme-in-adaptive-form}

Los pasos para aplicar una temática a un formulario adaptable son los siguientes:

1. Inicie sesión en la instancia de autor de AEM Forms.

1. Tocar **Adobe Experience Manager** > **Forms** > **Forms y documentos**.

1. Clic **Crear** > **Forms adaptable**. Se abre el asistente para crear formularios adaptables.

1. Seleccione la plantilla del componente principal en la **Origen** pestaña.

   >[!NOTE]
   >
   > Cuando cree un formulario adaptable con componentes principales, verá la temática Lienzo en la pestaña Estilo. Este es el único tema predeterminado disponible en este momento. Pero puede cambiar el tema a su gusto y guardarlo para usarlo en el futuro configurando una canalización de front-end.

1. Seleccione la temática Lienzo en la **Estilo** pestaña.
1. Haga clic en **Crear**.

Las temáticas de formularios adaptables se utilizan como parte de una plantilla de formulario adaptable para definir el estilo al crear un formulario adaptable.

## Personalizar la temática {#customizing-theme}

Para personalizar una temática,

* [Configuración de una canalización en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* Configure un usuario con [rol de colaborador](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* Usted debe tener un [conocimientos básicos de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) y repositorios Git de Cloud Service.

Para personalizar una temática de lienzo:
1. [Clonar la temática Lienzo](#1-download-canvas-theme-download-canvas-theme)
1. [Comprender la estructura del tema](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [Cambie el nombre en package.json y package_lock.json](#changename-packagelock-packagelockjson)
1. [Cree el ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [Iniciar el servidor proxy local](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [Personalizar la temática](#customize-the-theme-customizing-theme)
1. [Confirmar los cambios](#6-committing-the-changes-committing-the-changes)
1. [Implementación de la canalización](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1. Clonar el tema Lienzo {#download-canvas-theme}

Abra el símbolo del sistema y ejecute el siguiente comando para clonar el tema del lienzo:

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> La pestaña Estilo del Asistente para la creación de formularios muestra el mismo nombre de tema que en el archivo package.json.

### 2. Comprender la estructura del tema {#structure-of-canvas-theme}

Una temática de formulario adaptable es un paquete que contiene CSS, JavaScript y recursos estáticos que definen el estilo del formulario y cumplen la estructura de una temática de formulario adaptable. Una temática de formulario adaptable tiene la siguiente estructura típica de un proyecto front-end:

* `src/components`AEM : Archivos JavaScript y CSS específicos de los componentes principales de la
* `src/resources`: archivos estáticos como iconos, logotipos y fuentes
* `src/site`: Archivos JavaScript y CSS que se aplican a toda la página de AEM Sites
* `src/theme.ts`: el punto de entrada principal del tema de JavaScript y CSS
* `src\theme.scss`: archivos JavaScript y CSS que se aplican a toda la temática

El `src/components` AEM tiene archivos JavaScript y CSS específicos para todos los componentes principales, como botón, casilla de verificación, contenedor, pie de página, etc., de la lista de carpetas. AEM Puede aplicar estilo a un botón o una casilla de verificación si edita el archivo CSS específico del componente de.

![Edición del tema](/help/forms/assets/theme_structure.png)

AEM Para personalizar la temática, puede iniciar el servidor proxy local para ver las personalizaciones de la temática en tiempo real en función del contenido real de la.

### 3. Cambie el nombre en package.json y package_lock.json del tema Lienzo {#changename-packagelock-packagelockjson}

Actualice el nombre y la versión de la temática Lienzo en la `package.json` y `package_lock.json` archivos.

>[!NOTE]
>
> Los nombres no deben tener `@aemforms` etiqueta. Debe ser un texto simple como un nombre proporcionado por el usuario.

![Tema de lienzo](/help/forms/assets/changename_canvastheme.png)

### 4. Cree el archivo .env en una carpeta de temas {#creating-env-file-theme-folder}

Crear un `.env` en la carpeta theme y agregue los siguientes parámetros:

* **AEM url de la**
AEM_URL=https://[instancia de autor]

* **AEM nombre del sitio de**
AEM_ADAPTIVE_FORM=Nombre_formulario

* **AEM puerto de proxy de**
AEM PROXY_PORT=7000_PROXY_PROXY


![Estructura del tema del lienzo](/help/forms/assets/env-file-canvas-theme.png)

### 5. Iniciar un servidor proxy local {#starting-a-local-proxy-server}

1. Desde la línea de comandos, vaya a la raíz del tema en el equipo local.
1. Ejecutar `npm install` y npm recupera dependencias e instala el proyecto.
1. Ejecute `npm run live` y se inicia el servidor proxy.

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. Haga clic o pulse **INICIAR SESIÓN LOCALMENTE (SOLO TAREAS DE ADMINISTRACIÓN)** AEM e inicie sesión con las credenciales de usuario de proxy proporcionadas por el administrador de la.

   ![Iniciar sesión localmente](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * Cree un usuario local para iniciar sesión localmente. Proporcione la función de colaborador para el diseñador de temáticas.
   > * AEM Si especifica la dirección URL como `http://localhost:[port]/` en el `.env` de la temática Lienzo, se le redirigirá directamente al explorador.


1. Una vez que haya iniciado sesión, cambie la dirección URL en el explorador para que apunte a la ruta del contenido de ejemplo que le proporcionó el administrador de AEM.

   * Por ejemplo, si la ruta proporcionada era `/content/formname.html?wcmmode=disabled`, cambie la dirección URL a `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![Contenido de muestra de proxy](/help/forms/assets/sample_af.png)

Vaya a un formulario adaptable para ver la temática de lienzo aplicada a un formulario adaptable.

### 6. Personalización del tema {#customize-theme}

1. En el editor, abra el archivo `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > Puede aplicar estilo a todos los componentes de formulario adaptable en un sitio directamente editando la variable `site/_variables.scss` archivo.

1. Edite la variable para el `font colour` hasta `red`.

   ![Editar tema](/help/forms/assets/edit_theme.png)

   **AEM Aplicar estilo a los diferentes componentes de la**

   Puede aplicar estilo a los diferentes componentes de un formulario adaptable cambiando su archivo CSS en el editor. Hay diferentes carpetas CSS para cada componente principal del formulario adaptable en la carpeta Temática del lienzo.

   ![Componente principal](/help/forms/assets/theme-component.png)

   Para especificar estilos para un componente específico en el editor de temáticas, puede editar el CSS en una carpeta de temáticas. Por ejemplo, si desea cambiar el color del borde de un campo de cuadro de texto, abra el archivo CSS en el editor y cambie el color del borde.

   ![Editar CSS de cuadro de texto](/help/forms/assets/edit_color_textbox.png)

1. Al guardar el archivo, el servidor proxy reconoce el cambio mediante la línea `[Browsersync] File event [change]`.

   ![Sincronización de exploradores proxy](/help/forms/assets/browser_sync.png)

1. Al volver al explorador del servidor proxy local, el cambio es visible de inmediato.

   ![cambiar tema de AF](/help/forms/assets/edit_theme_af.png)

AEM El diseñador de temáticas obtiene una vista previa de los cambios en el servidor proxy local y personaliza la temática según los requisitos de los distintos componentes de la.

AEM Antes de confirmar los cambios en el repositorio de Git de la, debe acceder a su [Información del repositorio Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 7. Confirmar los cambios {#committing-the-changes}

Después de realizar cambios en la temática y probarla con un servidor proxy local, confirme los cambios en el repositorio de Git de su Cloud Service de AEM Forms. Hace que el tema personalizado esté disponible en el entorno de Cloud Service de Forms para que lo utilicen los autores de Forms adaptables.

Antes de confirmar los cambios en el repositorio Git de su Cloud Service de AEM Forms, necesita un clon del repositorio en el equipo local. Para clonar el repositorio:

1. Cree un nuevo repositorio de temáticas haciendo clic en **[!UICONTROL Repositorios]** opción.

   ![crear nuevo repositorio de temas](/help/forms/assets/createrepo_canvastheme.png)

1. Clic **[!UICONTROL Añadir repositorio]** y especifique el **Nombre del repositorio** en el **Añadir repositorio** Cuadro de diálogo. Haga clic en **[!UICONTROL Guardar]**.

   ![Agregar repositorio de tema de lienzo](/help/forms/assets/addcanvasthemerepo.png)

1. Clic **[!UICONTROL Copiar URL del repositorio]** para copiar la URL del repositorio creado.

   ![URL de tema de lienzo](/help/forms/assets/copyurl_canvastheme.png)

1. Abra el símbolo del sistema y clone el repositorio de la nube creado anteriormente.

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. Mueva los archivos del repositorio de temáticas que está editando al repositorio de la nube con un comando similar a
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
Por ejemplo, utilice este comando 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. En el directorio del repositorio de la nube, confirme los archivos de tema que ha movido a con los siguientes comandos.

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. Las personalizaciones se insertan en el repositorio de Git.

   ![Cambios confirmados](/help/forms/assets/cmd_git_push.png)

Sus personalizaciones ahora se almacenan de forma segura en el repositorio de Git.


### 8. Ejecutar la canalización de front-end {#deploy-pipeline}

1. Cree la canalización front-end para implementar el tema personalizado. Aprender [cómo configurar una canalización de primera línea para implementar un tema personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. Ejecute la canalización de front-end creada para implementar la carpeta de temas personalizada en **[!UICONTROL Estilo]** de un asistente de creación de formularios adaptables.

>[!NOTE]
>
>En el futuro, si realiza modificaciones en la carpeta de temas del lienzo, debe volver a ejecutar la canalización anterior. Por lo tanto, es necesario recordar el nombre de la canalización.

## Ejemplo para personalizar la temática {#example-to-customize-a-theme}

1. Inicie sesión en la instancia de autor de AEM Forms.
1. Abra un formulario adaptable creado con componentes principales.
1. Inicie el servidor proxy local mediante el símbolo del sistema y haga clic en **INICIAR SESIÓN LOCALMENTE (SOLO TAREAS DE ADMINISTRACIÓN)**.
1. Una vez que haya iniciado sesión, se le redirigirá al explorador y verá el tema aplicado.
1. Descargue la [Tema de lienzo](https://github.com/adobe/aem-forms-theme-canvas) y extraiga la carpeta zip descargada.
1. Abra la carpeta zip extraída en su editor preferido.
1. Crear un `.env` en la carpeta de la temática y agregue parámetros: **AEM URL de**, **AEM FORMULARIO_ADAPTABLE_** y **AEM PUERTO_PROXY_**.
1. Abra el archivo CSS del cuadro de texto en la carpeta Temática del lienzo y cambie el color del borde a `red` coloree y guarde los cambios.
1. Vuelva a abrir el explorador y verá que los cambios se reflejan inmediatamente en un formulario adaptable.
1. Mueva la carpeta de temas de lienzo al repositorio clonado.
1. Confirme los cambios y ejecute la canalización front-end.

Una vez ejecutada la canalización, la temática estará disponible en la pestaña Estilo.

## Prácticas recomendadas {#best-practices}

* **Evitar recursos de otra temática**

   Al editar una temática, puede examinar y agregar recursos (como imágenes) de otras temáticas. Por ejemplo, quiere editar el fondo de una página. Al seleccionar **[!UICONTROL Página]** ![edit-button](assets/edit-button.png) > **[!UICONTROL Fondo]** > **[!UICONTROL Agregar]** > **[!UICONTROL Imagen]**, verá un cuadro de diálogo que le permite examinar y agregar imágenes en otras temáticas.

   Puede tener problemas con la temática actual si se agrega un recurso desde otra y esta se mueve o se elimina. Se recomienda evitar explorar y agregar recursos de otras temáticas.

* **Cambio de la anchura de diseño del panel contenedor**

   No se recomienda cambiar la anchura del diseño del panel contenedor. Cuando se especifica la anchura de un panel contenedor, este se vuelve estático y no se adapta a distintas pantallas.

* **Usar el editor de formularios o el editor de temáticas para trabajar con encabezado y pie de página**

   Utilice el editor de temáticas si desea aplicar estilo al encabezado y al pie de página mediante opciones de estilo como estilo de fuente, fondo y transparencia. 
Si desea proporcionar información como un logotipo, el nombre de la empresa en el encabezado e información de copyright en el pie de página, utilice las opciones del editor de formularios.
