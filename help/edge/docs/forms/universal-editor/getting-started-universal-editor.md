---
title: Introducción a Edge Delivery Services para AEM Forms con el editor universal
description: Aprenda a crear y publicar formularios de alto rendimiento con Edge Delivery Services con la creación de WYSIWYG en el editor universal.
feature: Edge Delivery Services
role: Admin, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2608'
ht-degree: 100%

---


# Introducción a Edge Delivery Services para AEM Forms con el editor universal

| Método de creación | Guía |
|---------------------------------|-----------------------------------------------------------------------|
| **Editor universal (WYSIWYG)** | Este artículo |
| **Creación basada en documentos** | [Tutorial basado en documentos](/help/edge/docs/forms/tutorial.md) |

Edge Delivery Services para AEM Forms combina la entrega web de alto rendimiento con la creación de WYSIWYG en el editor universal. Esta guía explica cómo crear, personalizar y publicar formularios de carga rápida.

## Objetivos

Al final de este tutorial, podrá hacer lo siguiente:

- Configurar un repositorio de GitHub con el bloque de formularios adaptables.
- Crear un sitio de AEM integrado con Edge Delivery Services.
- Generar y publicar formularios con el editor universal.
- Configurar su entorno de desarrollo local

## Elegir la ruta

Seleccione el enfoque que coincida con su escenario:

![Guía de decisión para elegir la ruta](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*Figura: Guía visual para ayudarlo a elegir la ruta de implementación correcta*

| **Ruta A: nuevo proyecto** | **Ruta B: proyecto existente** |
|----------------------------------------|-------------------------------------------|
| Comenzar con una plantilla preconfigurada | Añadir formularios al proyecto actual de AEM |
| **Lo mejor para:** nuevas implementaciones | **Lo mejor para:** AEM Sites existente |
| **Lo que obtiene:** bloque de formularios preconfigurado | **Lo que obtienes:** formularios añadidos al sitio existente |
| **Pasos:** Plantilla → Configuración → Formularios | **Pasos:** Integración → Configuración → Formularios |
| [Empezar con la ruta A](#path-a-create-new-project-with-forms) | [Empezar con la ruta B](#path-b-add-forms-to-existing-project) |

## Requisitos previos

Para garantizar una experiencia agradable y sin problemas con Edge Delivery Services para AEM Forms mediante el editor universal, revise y confirme los siguientes requisitos previos antes de continuar:

### Requisitos de acceso

- **Cuenta de GitHub**: debe tener una cuenta de GitHub con permisos para crear nuevos repositorios. Esto es esencial para administrar el código fuente del proyecto y colaborar con el equipo.
- **Acceso de creación de AEM as a Cloud Service**: asegúrese de que tenga acceso de nivel de autor a su entorno de AEM as a Cloud Service. Este acceso es necesario para crear, editar y publicar formularios.

### Requisitos técnicos

- **Familiaridad con Git**: debería sentirse cómodo realizando operaciones básicas de Git, como clonar repositorios, confirmar cambios y enviar actualizaciones. Estas habilidades son fundamentales para el control de código fuente y la colaboración en proyectos.
- **Comprensión de las tecnologías web**: se recomienda tener conocimientos prácticos de HTML, CSS y JavaScript. Estas tecnologías forman la base de la personalización y solución de problemas de los formularios.
- **Node.js (versión 16 o superior)**: se requiere Node.js para el desarrollo local y la ejecución de las herramientas de compilación. Asegúrese de que tiene instalada la versión 16 o posterior en el sistema.
- **Administrador de paquetes (npm o yarn)**: necesitará npm (Administrador de paquetes de nodos) o yarn para administrar dependencias y scripts de proyectos.

### Fondo recomendado

- **Conceptos de AEM Sites**: una comprensión básica de AEM Sites, que incluye la estructura del sitio y la creación de contenido, le ayudará a desplazarse por los formularios e integrarlos de manera eficaz.
- **Principios de diseño de formularios**: la familiaridad con las prácticas recomendadas en el diseño de formularios, como la facilidad de uso, la accesibilidad y la validación de datos, le permitirá crear formularios eficaces y fáciles de usar.
- **Experiencia con editores de WYSIWYG**: la experiencia previa con editores de tipo What You See Is What You Get (WYSIWYG, es decir, lo que ve es lo que obtiene) le ayudará a aprovechar las capacidades de creación visual del editor universal de forma más eficaz.

>[!TIP]
>
> ¿Es nuevo en AEM? Comience con la [Guía de introducción de AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=es).

## Ruta A: Crear un nuevo proyecto con formularios

**Recomendado para:** proyectos nuevos, proyectos piloto o iniciativas de prueba de concepto

Aproveche los elementos repetitivos de AEM Forms para acelerar la configuración del proyecto. Este elemento repetitivo está listo para usar e integra perfectamente el bloque de formularios adaptables, lo que le permite crear e implementar rápidamente formularios en su sitio de AEM.

### Información general

Para iniciar correctamente el nuevo proyecto con formularios integrados, deberá:

1. Crear un repositorio de GitHub con la plantilla de elemento repetitivo de AEM Forms.
2. Establecer la sincronización de código de AEM para automatizar la sincronización de contenido entre AEM y el repositorio.
3. Configurar la conexión entre el proyecto de GitHub y el entorno de AEM.
4. Establecer y publicar un nuevo sitio de AEM.
5. Añadir y administrar formularios mediante el editor universal.

Las siguientes secciones le guiarán a través de cada paso detalladamente, lo que garantiza una experiencia de configuración del proyecto fluida y eficiente.

+++Paso 1: Crear un repositorio de GitHub a partir de una plantilla

1. **Acceder a la plantilla de elementos repetitivos de AEM Forms**
   - Vaya a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

   ![Plantilla de elementos repetitivos de AEM Forms](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *Figura: Repositorio de elementos repetitivos de AEM Forms con bloque de formularios adaptables preconfigurado*

2. **Crear su repositorio**
   - Haga clic en **Usar esta plantilla** > **Crear un nuevo repositorio**.

   ![Crear un repositorio a partir de una plantilla](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *Imagen: Uso de la plantilla para crear un nuevo repositorio*

3. **Configurar el repositorio**
   - **Propietario**: seleccione su cuenta u organización de GitHub
   - **Nombre del repositorio**: elija un nombre descriptivo (por ejemplo, `my-forms-project`)
   - **Visibilidad**: seleccione **Público** (recomendado para Edge Delivery Services)
   - Haga clic en **Crear repositorio**.

   ![Configuración del repositorio](/help/edge/docs/forms/assets/name-eds-repo.png)
   *Imagen: Configuración del nuevo repositorio con visibilidad pública*

**Validación:** confirme que tiene un nuevo repositorio de GitHub basado en la plantilla de elementos repetitivos de AEM Forms.

+++

+++Paso 2: Instalar AEM Code Sync

AEM Code Sync sincroniza automáticamente los cambios de contenido entre el entorno de creación de AEM y el repositorio de GitHub.

1. **Instalación de la aplicación de GitHub**
   - Vaya a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).

2. **Configurar permisos de acceso**
   - Seleccione **Solo seleccionar repositorios**.
   - Elija el repositorio recién creado.
   - Haga clic en **Guardar**.

   ![Instalación de AEM Code Sync](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *Imagen: instalando AEM Code Sync con permisos específicos del repositorio*

**Punto de comprobación:** AEM Code Sync ya está instalado y tiene acceso a su repositorio.

+++

+++Paso 3: Configuración de la integración de AEM

El archivo `fstab.yaml` conecta el repositorio de GitHub con el entorno de creación de AEM para la sincronización de contenido.

1. **Vaya a su repositorio**
   - Vaya al repositorio de GitHub recién creado
   - Debería ver los archivos Boilerplate de AEM Forms

2. **Crear el archivo fstab.yaml**
   - Haga clic en **Agregar archivo** > **Crear nuevo archivo** en el directorio raíz
   - Nombre al archivo `fstab.yaml`

   ![Creación del archivo fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)
   *Figura: crear el archivo de configuración fstab.yaml*

3. **Agregue sus datos de conexión de AEM**

   Copie y pegue la siguiente configuración, reemplazando los marcadores de posición:

   ```yaml
   mountpoints:
     /: 
     url: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
     type: "markup" 
     suffix: ".html" 
   ```

   **Reemplazar:**
   - `<aem-author>`: su URL del autor de AEM as a Cloud Service (por ejemplo, `author-p12345-e67890.adobeaemcloud.com`)
   - `<owner>`: su nombre de usuario u organización de GitHub
   - `<repository>`: el nombre de su repositorio

   **Ejemplo:**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![Editar el archivo fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *Figura: configuración del punto de montaje para la integración de AEM*

4. **Confirme la configuración**
   - Añada el mensaje de compromiso: “Añadir configuración de la integración de AEM”
   - Haga clic en **Confirmar nuevo archivo**

   ![Confirmar cambios de fstab](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *Figura: confirmando la configuración de fstab.yaml*

**Validación:** confirme la conexión del repositorio de GitHub a AEM.

>[!NOTE]
>
> ¿Tiene problemas de compilación? Consulte [Solución de problemas de compilación de GitHub](#troubleshooting-github-build-issues).

+++

+++Paso 4: Crear un sitio de AEM conectado a su repositorio de GitHub.

1. **Acceder a la consola de AEM Sites**
   - Inicie sesión en la instancia de creación de AEM as a Cloud Service.
   - Vaya a **Sites**

   ![Consola de AEM Sites](/help/edge/assets/select-sites.png)
   *Figura: acceso a la consola de AEM Sites*

2. **Iniciar creación de sitios**
   - Haga clic en **Crear** > **Sitio a partir de una plantilla**

   ![Opción de creación de sitio](/help/edge/docs/forms/assets/create-sites.png)
   *Figura: creación de un nuevo sitio a partir de una plantilla*

3. **Seleccionar plantilla de Edge Delivery Services**
   - Elija la plantilla **sitio de Edge Delivery Services**
   - Haga clic en **Siguiente**

   ![Selección de plantilla de sitio](/help/edge/docs/forms/assets/select-site-template.png)
   *Figura: seleccionar la plantilla del sitio de Edge Delivery Services*

   >[!NOTE]
   >
   >**¿Plantilla no disponible?** Si no ve la plantilla de Edge Delivery Services:
   >
   >1. Haga clic en **Importar** para cargar la plantilla
   >2. Descargar plantillas de [versiones de GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)

4. **Configure el sitio**

   Especifique la siguiente información:

   | Campo | Valor | Ejemplo |
   |-----------------|-----------------------------|-----------------------------------------|
   | **Título del sitio** | Nombre descriptivo del sitio | &quot;Mi proyecto de Forms&quot; |
   | **Nombre del sitio** | Nombre descriptivo de la URL | &quot;mi-proyecto-forms&quot; |
   | **URL de GitHub** | URL del repositorio | `https://github.com/mycompany/my-forms-project` |

   ![Configuración del sitio](/help/edge/docs/forms/assets/create-aem-site.png)
   *Figura: configuración del nuevo sitio de AEM con la integración de GitHub*

5. **Creación completa de sitios**
   - Revise sus ajustes
   - Haga clic en **Crear**

   ![Confirmar creación del sitio](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *Figura: confirmación de la creación del sitio*

   **¡Correcto!** El sitio de AEM se ha creado y conectado a GitHub.

6. **Abrir en el editor universal**
   - En la consola Sitios, busque el nuevo sitio
   - Seleccione la página `index`
   - Haga clic en **Editar**.

   ![Editar sitio en el editor universal](/help/edge/docs/forms/assets/edit-site.png)
   *Imagen: abrir el sitio para editarlo*

   El editor universal se abre en una nueva pestaña, que proporciona funciones de creación de WYSIWYG.

   ![Interfaz del editor universal](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *Imagen: el sitio se abrió en el editor universal para la edición de WYSIWYG*

**Validación:** confirme que su sitio de AEM está listo para la creación de formularios.

+++

+++Paso 5: Publicación del sitio

La publicación hace que el sitio esté disponible en Edge Delivery Services para su acceso global.

1. **Publicación rápida desde la consola Sitios**
   - Vuelva a la consola de AEM Sites.
   - Seleccione las páginas del sitio (o seleccione todo con Ctrl+A)
   - Haga clic en **Publicación rápida**

   ![Editar sitio de AEM](/help/edge/docs/forms/assets/publish-sites.png)
   *Figura: seleccionando páginas para la publicación rápida*

2. **Confirmar publicación**
   - En el cuadro de diálogo de confirmación, haga clic en **Publicar**

   ![Cuadro de diálogo de publicación rápida](/help/edge/docs/forms/assets/quick-publish.png)
   *Figura: confirmando la acción de publicación*

   **Alternativa:** también puede publicar directamente desde el Editor universal pulsando el botón Publicar.

   ![Publicar desde el editor universal](/help/edge/docs/forms/assets/qui.png)
   *Figura: publicación directamente desde el editor universal*

3. **Acceda a su sitio activo**

   Su sitio está ahora activo en:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **Estructura URL explicada:**
   - `<branch>`: rama de GitHub (normalmente `main`)
   - `<repo>`: el nombre de su repositorio
   - `<owner>`: su nombre de usuario u organización de GitHub
   - `<site-name>`: el nombre de su sitio de AEM

   **Ejemplo:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**Validación:** confirme que su sitio está activo en Edge Delivery Services.

>[!TIP]
>
> **Patrones de URL:**
>
> - **Página de inicio:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **Otras páginas:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**Siguiente:**[creación del primer formulario](#create-your-first-form)

+++

## Ruta B: Agregar Forms a un proyecto existente

**Ideal para:** AEM Sites existentes con Edge Delivery Services

Si ya tiene un proyecto de AEM con Edge Delivery Services, puede agregar funcionalidades de formulario integrando el bloque de Forms adaptable.

### Requisitos previos para la ruta B

Para continuar con la integración de formularios en el proyecto de AEM existente, asegúrese de que se cumplan los siguientes requisitos previos:

- Ya tiene un proyecto de AEM creado con [AEM Boilerplate XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk).
- Tiene un [entorno de desarrollo local configurado](#set-up-local-development-environment)
- Dispone de acceso Git al repositorio del proyecto, lo que le permite clonar, modificar y enviar cambios según sea necesario.

>[!NOTE]
>
> Si el proyecto se configuró originalmente usando [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms), la funcionalidad del formulario ya se ha incluido. En este caso, puede pasar a la sección [Crear su primer formulario](#create-your-first-form).

La siguiente guía proporciona un enfoque estructurado para agregar capacidades de formulario al proyecto existente. Cada paso está diseñado para garantizar una integración perfecta y una funcionalidad óptima dentro del entorno del editor universal.

### Información general

Completará los siguientes pasos de alto nivel:

1. Copie los archivos del bloque de Forms adaptable en el proyecto.
2. Actualice la configuración del proyecto para reconocer y admitir componentes de formulario.
3. Ajuste las reglas de ESLint para dar cabida a los nuevos archivos y patrones de codificación.
4. Cree el proyecto y confirme los cambios en el repositorio.

+++Paso 1: Copiar archivos de bloque de formularios

1. **Vaya a su proyecto local**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **Descargue los archivos necesarios de las plantillas de AEM Forms**

   Copie estos archivos del [repositorio de AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms):

   | Origen | Destino | Función |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | Funcionalidad de formulario principal |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | Integración del editor universal |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | Estilo del editor |

3. **Compatibilidad con el editor de actualizaciones**
   - Reemplace su archivo `/scripts/editor-support.js` por [editor-support.js de AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)

**Validación:** confirme que los archivos de bloque de formulario se encuentran en el proyecto.

+++

+++Paso 2: Actualizar la configuración del componente

1. **Actualizar modelo de sección**

   Abra `/models/_section.json` y agregue componentes de formulario a los filtros:

   ```json
   {
        "filters": [
        {
      "id": "section",
      "components": [
           "text",
           "image",
           "button",
        "form",
        "embed-adaptive-form"
      ]
       }
     ]
   }
   ```

   **Qué hace:** habilita los componentes de formulario en el selector de componentes del editor universal.

**Validación:** confirme que los componentes de formulario aparecen en el editor universal.

+++

+++Paso 3: Configurar ESLint (opcional)

**Por qué este paso:** evita los errores de identificación de los archivos específicos del formulario y configura las reglas de validación adecuadas.

1. **Actualizar .eslintignore**

   Añada estas líneas a `/.eslintignore`:

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **Actualizar .eslintrc.js**

   Añada estas reglas al objeto `rules` en `/.eslintrc.js`:

   ```javascript
   {
     "rules": {
       // Existing rules...
   
       // Form component cell limits
    'xwalk/max-cells': ['error', {
         '*': 4, // default limit
      form: 15,
      wizard: 12,
      'form-button': 7,
      'checkbox-group': 20,
      checkbox: 19,
      'date-input': 21,
      'drop-down': 19,
      email: 22,
      'file-input': 20,
      'form-fragment': 15,
      'form-image': 7,
      'multiline-input': 23,
      'number-input': 22,
      panel: 17,
      'radio-group': 20,
      'form-reset-button': 7,
      'form-submit-button': 7,
      'telephone-input': 20,
      'text-input': 23,
      accordion: 14,
      modal: 11,
      rating: 18,
      password: 20,
         tnc: 12
       }],
   
       // Disable this rule for forms
       'xwalk/no-orphan-collapsible-fields': 'off'
     }
   }
   ```

**Validación:** confirme que ESLint funciona con los componentes del formulario.

+++

+++Paso 4: Creación e implementación

1. **Instalar dependencias y generar**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **Qué hace esto:**
   - Actualiza `component-definition.json` con componentes de formulario
   - Genera `component-models.json` con modelos de formulario
   - Crea `component-filters.json` con reglas de filtrado

2. **Verificar archivos generados**

   Compruebe que estos archivos de la raíz del proyecto contengan objetos relacionados con el formulario:
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **Confirmar y enviar cambios**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**Validación:** confirme que el proyecto incluye capacidades de formulario.

+++

**Siguiente:** [Crear el primer formulario](#create-your-first-form)

## Crear el primer formulario

**Quién debe seguir esta sección:**\
Esta sección es relevante para los usuarios que siguen la ruta A (nuevo proyecto) o la ruta B (proyecto existente).

Ahora que el proyecto está preparado para crear formularios, ya puede crear el primer formulario mediante el entorno de creación intuitivo WYSIWYG del editor universal. En los siguientes pasos se proporciona un enfoque estructurado para diseñar, configurar y publicar un formulario en el sitio de AEM.

### Información general

El proceso de creación de un formulario en el editor universal consta de varias fases clave:

1. **Insertar el bloque de formulario adaptable**\
   Comience añadiendo el bloque de formulario adaptable a la página elegida.

2. **Añadir componentes de formulario**\
   Rellene el formulario insertando componentes como campos de texto, botones y otros elementos de entrada.

3. **Configurar propiedades de los componentes**\
   Ajuste la configuración y las propiedades de cada componente para satisfacer los requisitos del formulario.

4. **Previsualizar y probar el formulario**\
   Utilice la funcionalidad de vista previa para validar el aspecto y el comportamiento del formulario antes de publicarlo.

5. **Publicar la página cargada**\
   Cuando esté satisfecho con la página, publíquela para que el formulario esté disponible para los usuarios finales.

Las siguientes secciones le guiarán detalladamente por cada uno de estos pasos, lo que garantiza una experiencia de creación de formularios fluida y eficaz.

+++Paso 1: Añadir bloque de formulario adaptable

1. **Abrir la página en el editor universal**
   - Vaya a la consola **Sitios** en AEM.
   - Seleccione la página donde desea añadir un formulario (por ejemplo, `index`).
   - Haga clic en **Editar**.

   La página se abrirá en el editor universal para la edición WYSIWYG.

2. **Añadir el componente de formulario adaptable**
   - Abra el panel **Árbol de contenido** (barra lateral izquierda).
   - Vaya a la sección donde desee añadir el formulario.
   - Haga clic en el icono **Añadir** (+). 
   - Seleccione **Formulario adaptable** en la lista de componentes.

   ![Adición de un bloque de formulario adaptable](/help/edge/docs/forms/assets/add-adaptive-form-block.png).
   *Figura: Añadir un bloque de formulario adaptable a la página*

**Validación:** confirme que tiene un contenedor de formulario vacío.

+++

+++Paso 2: Añadir componentes de formulario

1. **Vaya al bloque de formulario**
   - En el árbol de contenido, busque la sección Formulario adaptable recién añadida.

   ![Bloque de formulario adaptable añadido](/help/edge/docs/forms/assets/adative-form-block.png)
   *Figura: bloque de formulario adaptable en el árbol de contenido*

2. **Añadir componentes de formulario**

   Puede añadir componentes de las siguientes dos maneras:

   **Método A: haga clic en Agregar**
   - Haga clic en el icono **Agregar** (+) en la sección del formulario
   - Seleccione los componentes de la lista **Componentes de formularios adaptables**.

   **Método B: Arrastrar y soltar**
   - Arrastre los componentes directamente desde el panel de componentes al formulario

   ![Añadir componentes al formulario](/help/edge/docs/forms/assets/add-component.png)
   *Figura: añadir componentes al formulario*

   **Componentes de inicio recomendados**
   - Entrada de texto (para el nombre, correo electrónico)
   - Área de texto (para mensajes)
   - Botón Enviar

3. **Configure propiedades de los componentes**
   - Seleccione cualquier componente del formulario
   - Utilice el panel **Propiedades** (barra lateral derecha) para configurar:
      - Etiquetas y marcadores de posición
      - Reglas de validación
      - Configuración de campos obligatoria

   ![Panel de propiedades de componentes](/help/edge/docs/forms/assets/component-properties.png)
   *Figura: configuración de propiedades del componente*

4. **Seleccionar un formulario**

   El formulario tendrá un aspecto similar al siguiente:

   ![Vista previa del formulario completado](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *Figura: formulario de ejemplo creado con el editor universal*

**Validación:** confirme que el formulario está listo para su publicación.

>[!IMPORTANT]
>
> Recuerde publicar la página después de realizar cambios para ver las actualizaciones en el explorador.

+++

+++Paso 3: Publicar el formulario

1. **Publicar desde el editor universal**
   - Haga clic en el botón **Publicar** del Editor universal

   ![Formulario de publicación](/help/edge/docs/forms/assets/publish-form.png)
   *Imagen: publicación del formulario desde el Editor universal*

2. **Confirmar publicación**
   - En el cuadro de diálogo de confirmación, haga clic en **Publicar**.

   ![Confirmación de publicación](/help/edge/docs/forms/assets/publish-form1.png)
   *Figura: confirmando la acción de publicación*

   Verá un mensaje que confirma la publicación con éxito.

   ![Éxito de publicación](/help/edge/docs/forms/assets/publish-form2.png)
   *Figura: confirmación de publicación correcta*

3. **Ver el formulario activo**

   El formulario ya está activo en:

   ```
   https://<branch>--<repo>--<owner>.aem.live/content/<site-name>/
   ```

   **URL de ejemplo:**

   ```
   https://main--my-forms-project--mycompany.aem.live/content/my-forms-project/
   ```

   ![Página de formulario activo](/help/edge/docs/forms/assets/publish-index-page.png)
   *Imagen: la página de formulario publicada en Edge Delivery Services*

**¡Enhorabuena!** El formulario está ahora activo y listo para recopilar envíos.

+++

### Próximos pasos

Ahora que tiene un formulario en funcionamiento, puede:

- **Personalizar el estilo** al editar archivos CSS y JavaScript
- **Agregar características de formulario avanzadas** como reglas de validación y lógica condicional
- **Configure un entorno local** para una iteración más rápida
- **Cree formularios independientes** para casos de uso específicos

>[!TIP]
>
> **Más información:** [cree formularios independientes en el editor universal](/help/edge/docs/forms/universal-editor/create-forms.md)

## Configuración de un entorno de desarrollo de local

**Ideal para:** desarrolladores que desean personalizar el estilo y el comportamiento del formulario

Un entorno de desarrollo local le permite realizar cambios y verlos instantáneamente sin pasar por el ciclo de publicación.

+++Configure la CLI de AEM y el desarrollo local

1. **Instalación de la CLI de AEM**

   La CLI de AEM simplifica las tareas de desarrollo local:

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **Clone su repositorio**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   Reemplace `<owner>` y `<repo>` con la información real de GitHub.

3. **Inicie el servidor de desarrollo local**

   ```bash
   aem up
   ```

   Esto inicia un servidor local con capacidades de recarga en caliente.

4. **Realice personalizaciones**

   - Editar archivos en el directorio `blocks/form/` para determinar el estilo y el comportamiento del formulario
   - Modifique `form.css` para determinar el estilo
   - Actualice `form.js` para determinar el comportamiento

   **Vea los cambios al instante** en el explorador en `http://localhost:3000`

5. **Implemente los cambios**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   Los cambios estarán disponibles en:
   - **Vista previa:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **Producción:** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## Resolución de problemas

### Problemas comunes y soluciones

+++Problemas de compilación de GitHub

**Problema:** errores de compilación o errores de vinculación

**Solución 1: Controlar errores de vinculación**

Si se producen errores de vinculación:

1. Abra `package.json` en la raíz del proyecto
2. Busque el script `lint`:

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. Deshabilitar la vinculación temporalmente:

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. Confirmar e insertar los cambios

**Solución 2: Errores de ruta de módulo**

Si ve &quot;No se puede resolver la ruta al módulo &#39;/scripts/lib-franklin.js&#39;&quot;:

1. Navegue hasta `blocks/form/form.js`
2. Actualice la instrucción de importación:

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++Problemas de funcionalidad del formulario

**Problema:** los envíos de formularios no funcionan

**Soluciones:**

- Asegúrese de que tiene un componente de botón de envío
- Compruebe la configuración de la URL de acción del formulario
- Verifique las reglas de validación de formularios
- Pruebe primero en el modo de vista previa

**Problema:** Problemas de estilo

**Soluciones:**

- Compruebe las rutas de archivo CSS en `blocks/form/`
- Borre la caché del explorador
- Verifique la sintaxis CSS
- Haga la prueba en el entorno de desarrollo local

+++

+++Problemas del editor universal

**Problema:** los componentes del formulario no aparecen en el editor universal

**Soluciones:**

- Compruebe que AEM Code Sync está instalado y en ejecución
- Compruebe que `fstab.yaml` tenga la dirección URL del autor de AEM correcta
- Asegúrese de que la instancia de AEM tenga habilitado el acceso anticipado
- Confirmar que `component-definition.json` incluye componentes de formulario

**Problema:** los cambios no son visibles después de la publicación

**Soluciones:**

- Espere a que se actualice la caché de la CDN
- Compruebe la caché del explorador (pruebe el modo incógnito/privado)
- Compruebe que se está utilizando el formato de dirección URL correcto

+++



