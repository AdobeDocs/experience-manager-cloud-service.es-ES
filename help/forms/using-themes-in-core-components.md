---
title: Crear y usar temáticas
description: Puede utilizar temas para estilizar y proporcionar una identidad visual a un formulario adaptable mediante componentes principales. Puede compartir una temática en cualquier número de formularios adaptables.
source-git-commit: 1357b36dc3d14d2ceceb6761cb005b592472890a
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 19%

---


# Temas en Forms adaptable (componentes principales) {#themes-for-af-using-core-components}

Puede crear y aplicar temas para diseñar un formulario adaptable utilizando componentes principales. Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar una temática, el estilo especificado se refleja en los componentes correspondientes. La temática se administra de forma independiente sin hacer referencia a un formulario adaptable.

Cuando [crear un formulario adaptable](/help/forms/creating-adaptive-form.md) con los componentes principales, los temas predeterminados aparecen en la sección **Estilo** pestaña . De forma predeterminada, solo la variable **Lienzo** está disponible.

>[!NOTE]
>
>Un tema del formulario adaptable no debe confundirse con [Plantillas de formulario adaptables.](/help/forms/template-editor.md) Los temas del formulario adaptable solo contienen la información de estilo de un formulario adaptable. Las plantillas de formulario adaptable definen la estructura del formulario y el contenido inicial y contienen un tema para permitir la creación de [Formulario adaptable.](/help/forms/creating-adaptive-form.md)

## Uso del tema del lienzo en Forms adaptable mediante componentes principales {#using-theme-in-adaptive-form}

Los pasos para aplicar el tema a un formulario adaptable son:

1. Inicie sesión en la instancia de autor de AEM Forms.

1. Toque **Adobe Experience Manager** > **Forms** > **Forms y documentos**.

1. Haga clic en **Crear** > **Forms adaptable**. Se abre el asistente para crear formularios adaptables.

1. Seleccione la plantilla de componente principal en la **Fuente** pestaña .

   >[!NOTE]
   >
   > Cuando cree un formulario adaptable con componentes principales, verá el tema Lienzo en la ficha Estilo . Este es el único tema predeterminado disponible en este momento. Pero puede cambiar el tema a su gusto y guardarlo para utilizarlo en el futuro configurando una canalización de front-end.

1. Seleccione el tema del lienzo en la **Estilo** pestaña .
1. Haga clic en **Crear**.

Los temas del formulario adaptable se utilizan como parte de una plantilla de formulario adaptable para definir el estilo al crear un formulario adaptable.

## Personalizar el tema {#customizing-theme}

Para personalizar un tema,

* [configuración de una canalización en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* Configure un usuario con la variable [función de colaborador](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* Debe tener un [conocimientos básicos de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) y repositorios Git Cloud Service.

Para personalizar un tema de lienzo:
1. [Clonar el tema del lienzo](#1-download-canvas-theme-download-canvas-theme)
1. [Comprender la estructura del tema](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [Cambiar el nombre en package.json y package_lock.json](#changename-packagelock-packagelockjson)
1. [Cree la variable ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [Iniciar el servidor proxy local](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [Personalizar el tema](#customize-the-theme-customizing-theme)
1. [Confirmar los cambios](#6-committing-the-changes-committing-the-changes)
1. [Implementación de la canalización](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1. Clonar el tema del lienzo {#download-canvas-theme}

Abra el símbolo del sistema y ejecute el siguiente comando para clonar el tema del lienzo:

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> La ficha Estilo del Asistente para la creación de formularios muestra el mismo nombre de tema que en el archivo package.json.

### 2. Comprender la estructura del tema {#structure-of-canvas-theme}

Un tema de formulario adaptable es un paquete que contiene CSS, JavaScript y recursos estáticos que definen el estilo del formulario y cumplen con la estructura de un tema de formulario adaptable. Un tema de formulario adaptable tiene la siguiente estructura típica de un proyecto front-end:

* `src/components`: Archivos JavaScript y CSS específicos de AEM componentes principales
* `src/resources`: archivos estáticos como iconos, logotipos y fuentes
* `src/site`: Archivos JavaScript y CSS que se aplican a toda la página de AEM Sites
* `src/theme.ts`: El punto de entrada principal de su tema JavaScript y CSS
* `src\theme.scss`: Archivos JavaScript y CSS que se aplican a todo el tema

La variable `src/components` tiene archivos JavaScript y CSS específicos para todos los componentes principales de AEM, como botón, casilla de verificación, contenedor, pie de página, etc. Puede aplicar estilo a un botón o casilla de verificación si edita el archivo CSS específico del componente AEM.

![Edición del tema](/help/forms/assets/theme_structure.png)

Para personalizar el tema, puede iniciar el servidor proxy local para ver las personalizaciones del tema en tiempo real en función del contenido AEM real.

### 3. Cambie el nombre en package.json y package_lock.json de Canvas theme {#changename-packagelock-packagelockjson}

Actualice el nombre y la versión del tema del lienzo en la `package.json` y `package_lock.json` archivos.

>[!NOTE]
>
> Los nombres no deben tener `@aemforms` etiqueta. Debe ser texto simple como nombre proporcionado por el usuario.

![Imagen del tema del lienzo](/help/forms/assets/changename_canvastheme.png)

### 4. Cree el archivo .env en una carpeta de temas {#creating-env-file-theme-folder}

Cree un `.env` en la carpeta del tema y añada los siguientes parámetros:

* **URL de AEM**
AEM_URL=https://[author-instance]

* **AEM nombre del sitio**
AEM_ADAPTIVE_FORM=Form_name

* **AEM puerto proxy**
AEM_PROXY_PORT=7000


![Estructura del tema del lienzo](/help/forms/assets/env-file-canvas-theme.png)

### 5. Iniciar un servidor proxy local {#starting-a-local-proxy-server}

1. Desde la línea de comandos, vaya a la raíz del tema en el equipo local.
1. Ejecutar `npm install` y npm recupera dependencias e instala el proyecto.
1. Ejecute `npm run live` y se inicia el servidor proxy.

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. Toque o haga clic **INICIAR SESIÓN LOCALMENTE (SOLO TAREAS DE ADMINISTRACIÓN)** e inicie sesión con las credenciales del usuario proxy proporcionadas por el administrador de AEM.

   ![Iniciar sesión localmente](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * Cree un usuario local para iniciar sesión localmente. Proporcione la función de colaborador para el diseñador de temas.
   > * Si especifica la dirección URL de AEM como `http://localhost:[port]/` en el `.env` del tema del lienzo, se le redirige directamente al explorador.


1. Una vez que haya iniciado sesión, cambie la dirección URL en el explorador para que apunte a la ruta del contenido de ejemplo que le proporcionó el administrador de AEM.

   * Por ejemplo, si la ruta proporcionada era `/content/formname.html?wcmmode=disabled`, cambie la dirección URL a `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![Contenido de muestra de proxy](/help/forms/assets/sample_af.png)

Vaya a un formulario adaptable para ver el tema Lienzo aplicado a un formulario adaptable.

### 6. Personalizar el tema {#customize-theme}

1. En el editor, abra el archivo `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > Puede aplicar estilo a todos los componentes del formulario adaptable de un sitio directamente editando el `site/_variables.scss` archivo.

1. Edite la variable para la variable `font colour` a `red`.

   ![Editar tema](/help/forms/assets/edit_theme.png)

   **Estilos de los distintos componentes de AEM**

   Puede aplicar estilo a los distintos componentes de un formulario adaptable cambiando su archivo CSS en el editor. Hay diferentes carpetas CSS para cada componente principal del formulario adaptable en la carpeta Tema del lienzo.

   ![Componente principal](/help/forms/assets/theme-component.png)

   Para especificar estilos para un componente específico en el editor de temas, puede editar el CSS en una carpeta de temas. Por ejemplo, si desea cambiar el color del borde de un campo de cuadro de texto, abra el archivo CSS en el editor y cambie su color del borde.

   ![Editar CSS de cuadro de texto](/help/forms/assets/edit_color_textbox.png)

1. Al guardar el archivo, el servidor proxy reconoce el cambio a través de la línea `[Browsersync] File event [change]`.

   ![Sincronización de exploradores proxy](/help/forms/assets/browser_sync.png)

1. Al volver al explorador del servidor proxy local, el cambio es visible inmediatamente.

   ![cambiar tema AF](/help/forms/assets/edit_theme_af.png)

El diseñador de temas obtiene una vista previa de los cambios en el servidor proxy local y personaliza el tema según los requisitos de diferentes componentes de AEM.

Antes de confirmar los cambios en el repositorio de AEM Git, debe acceder a su [Información del repositorio de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 7. Confirmar los cambios {#committing-the-changes}

Después de realizar cambios en el tema y probarlo con un servidor proxy local, confirme los cambios en el repositorio Git de su Cloud Service de AEM Forms. Hace que el tema personalizado esté disponible en el entorno de su Cloud Service de Forms para que lo utilicen los autores de Adaptive Forms.

Antes de confirmar los cambios en el repositorio Git de su Cloud Service de AEM Forms, necesita un clon del repositorio en su equipo local. Para clonar el repositorio:

1. Cree un nuevo repositorio de temas haciendo clic en el **[!UICONTROL Repositorios]** .

   ![crear nuevo repositorio de temas](/help/forms/assets/createrepo_canvastheme.png)

1. Haga clic en **[!UICONTROL Agregar repositorio]** y especifique el **Nombre del repositorio** en el **Agregar repositorio** para abrir el Navegador. Haga clic en **[!UICONTROL Guardar]**.

   ![Agregar repositorio de tema del lienzo](/help/forms/assets/addcanvasthemerepo.png)

1. Haga clic en **[!UICONTROL Copiar URL del repositorio]** para copiar la URL del repositorio creado.

   ![URL del tema del lienzo](/help/forms/assets/copyurl_canvastheme.png)

1. Abra el símbolo del sistema y clone el repositorio de nube creado anteriormente.

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. Mueva los archivos del repositorio de temas que está editando al repositorio de la nube con un comando similar a
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
Por ejemplo, utilice este comando 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. En el directorio del repositorio de la nube, confirme los archivos de tema a los que se movió con los siguientes comandos.

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. Las personalizaciones se insertan en el repositorio de Git.

   ![Cambios confirmados](/help/forms/assets/cmd_git_push.png)

Sus personalizaciones ahora se almacenan de forma segura en el repositorio de Git.


### 8. Ejecute la canalización de front-end {#deploy-pipeline}

1. Cree la canalización front-end para implementar el tema personalizado. Más información [configuración de una canalización de front-line para implementar un tema personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. Ejecute la canalización de front-end creada para implementar la carpeta de temas personalizada en la sección **[!UICONTROL Estilo]** ficha de un asistente para la creación de formularios adaptables.

>[!NOTE]
>
>En el futuro, si realiza alguna modificación en la carpeta Canvas theme , debe volver a ejecutar la canalización anterior. Por lo tanto, es necesario recordar el nombre de la canalización.

## Ejemplo para personalizar el tema {#example-to-customize-a-theme}

1. Inicie sesión en la instancia de autor de AEM Forms.
1. Abra un formulario adaptable creado con componentes principales.
1. Inicie el servidor proxy local mediante el símbolo del sistema y haga clic en **INICIAR SESIÓN LOCALMENTE (SOLO TAREAS DE ADMINISTRACIÓN)**.
1. Una vez que haya iniciado sesión, se le redirigirá al explorador y verá el tema aplicado.
1. Descargue el [Tema del lienzo](https://github.com/adobe/aem-forms-theme-canvas) y extraiga la carpeta zip descargada.
1. Abra la carpeta zip extraída en su editor preferido.
1. Cree un `.env` en la carpeta del tema y añada parámetros: **URL de AEM**, **AEM_ADAPTIVE_FORM** y **AEM_PROXY_PORT**.
1. Abra el archivo CSS del cuadro de texto en la carpeta de temas del lienzo y cambie el color del borde por ejemplo `red` coloree y guarde los cambios.
1. Vuelva a abrir el explorador y verá que los cambios se reflejan inmediatamente en un formulario adaptable.
1. Mueva la carpeta de temas del lienzo a su repositorio clonado.
1. Confirme los cambios y ejecute la canalización de front-end.

Una vez ejecutada la canalización, el tema está disponible en la pestaña Style .

## Prácticas recomendadas {#best-practices}

* **Evitar recursos de otro tema**

   Al editar una temática, puede examinar y agregar recursos (como imágenes) de otras temáticas. Por ejemplo, quiere editar el fondo de una página. Al seleccionar **[!UICONTROL Página]** ![edit-button](assets/edit-button.png) > **[!UICONTROL Fondo]** > **[!UICONTROL Agregar]** > **[!UICONTROL Imagen]**, verá un cuadro de diálogo que le permite examinar y agregar imágenes en otras temáticas.

   Puede tener problemas con la temática actual si se agrega un recurso desde otra y esta se mueve o se elimina. Se recomienda evitar explorar y agregar recursos de otras temáticas.

* **Cambio de la anchura de diseño del panel contenedor**

   No se recomienda cambiar la anchura del diseño del panel contenedor. Cuando se especifica la anchura de un panel contenedor, este se vuelve estático y no se adapta a distintas pantallas.

* **Uso del editor de formularios o del editor de temas para trabajar con encabezado y pie de página**

   Utilice el editor de temáticas si desea aplicar estilo al encabezado y al pie de página mediante opciones de estilo como estilo de fuente, fondo y transparencia. 
Si desea proporcionar información como un logotipo, el nombre de la empresa en el encabezado e información de copyright en el pie de página, utilice las opciones del editor de formularios.
