---
title: Introducción a Edge Delivery Services para AEM Forms con el editor universal
description: Aprenda a crear y publicar formularios de alto rendimiento con Edge Delivery Services con la creación de WYSIWYG en el Editor universal.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: '2609'
ht-degree: 1%

---


# Introducción a Edge Delivery Services para AEM Forms con el editor universal

| Método de creación | Guía  |
|---------------------------------|-----------------------------------------------------------------------|
| **Editor universal (WYSIWYG)** | Este artículo |
| **Creación basada en documentos** | [Tutorial basado en documentos](/help/edge/docs/forms/tutorial.md) |

Edge Delivery Services para AEM Forms combina la entrega web de alto rendimiento con la creación de WYSIWYG en el editor universal. Esta guía explica cómo crear, personalizar y publicar formularios de carga rápida.

## Lo que vas a lograr

Al final de este tutorial, deberá hacer lo siguiente:

- Configuración de un repositorio de GitHub con el bloque de Forms adaptable
- Creación de un sitio de AEM integrado con Edge Delivery Services
- Generar y publicar formularios con el Editor universal
- Configuración del entorno de desarrollo local

## Elija su ruta

Seleccione el enfoque que coincida con su escenario:

![Elegir La Guía De Decisión De Ruta](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*Figura: Guía visual para ayudarlo a elegir la ruta de implementación correcta*

| **Ruta A: Nuevo Proyecto** | **Ruta B: Proyecto Existente** |
|----------------------------------------|-------------------------------------------|
| Comience con una plantilla preconfigurada | Añadir formularios al proyecto actual de AEM |
| **Lo mejor para:** Nuevas implementaciones | **Mejor para:** AEM Sites existente |
| **Lo que obtienes:** Bloque preconfigurado de Forms | **Lo que obtienes:** Forms se agregó al sitio existente |
| **Pasos:** → de plantilla → Forms | **Pasos:** Integración → Configuración → Forms |
| [Iniciar con ruta de acceso A](#path-a-create-new-project-with-forms) | [Iniciar con ruta de acceso B](#path-b-add-forms-to-existing-project) |

## Requisitos previos

Para garantizar una experiencia agradable y sin problemas con Edge Delivery Services para AEM Forms mediante el editor universal, revise y confirme los siguientes requisitos previos antes de continuar:

### Requisitos de acceso

- **Cuenta de GitHub**: debe tener una cuenta de GitHub con permisos para crear nuevos repositorios. Esto es esencial para administrar el código fuente del proyecto y colaborar con el equipo.
- **Acceso de creación de AEM as a Cloud Service**: Asegúrese de que tenga acceso de nivel de autor a su entorno de AEM as a Cloud Service. Este acceso es necesario para crear, editar y publicar formularios.

### Requisitos técnicos

- **Familiaridad con Git**: debería sentirse cómodo realizando operaciones básicas de Git, como clonar repositorios, confirmar cambios y enviar actualizaciones. Estas habilidades son fundamentales para el control de código fuente y la colaboración en proyectos.
- **Comprensión de las tecnologías web**: se recomienda tener conocimientos prácticos de HTML, CSS y JavaScript. Estas tecnologías forman la base de la personalización y solución de problemas de los formularios.
- **Node.js (versión 16 o superior)**: Se requiere Node.js para el desarrollo local y la ejecución de las herramientas de compilación. Asegúrese de que tiene instalada la versión 16 o posterior de en el sistema.
- **Administrador de paquetes (npm o yarn)**: Necesitará npm (Administrador de paquetes de nodos) o yarn para administrar dependencias y scripts de proyectos.

### Fondo recomendado

- **Conceptos de AEM Sites**: Una comprensión básica de AEM Sites, que incluye la estructura del sitio y la creación de contenido, le ayudará a desplazarse por los formularios e integrarlos de manera eficaz.
- **Principios de diseño de formularios**: La familiaridad con las prácticas recomendadas en el diseño de formularios, como la facilidad de uso, la accesibilidad y la validación de datos, le permitirá crear formularios eficaces y fáciles de usar.
- **Experiencia con editores de WYSIWYG**: La experiencia previa con editores de What You See Is What You Get (WYSIWYG) le ayudará a aprovechar las capacidades de creación visual del editor universal de forma más eficaz.

>[!TIP]
>
> ¿Es nuevo en AEM? Comience con la [Guía de introducción de AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=es).

## Ruta A: Crear un nuevo proyecto con Forms

**Recomendado para:** Proyectos nuevos, proyectos piloto o iniciativas de prueba de concepto

Aproveche las plantillas de AEM Forms para acelerar la configuración del proyecto. Esta plantilla ofrece una plantilla lista para usar que integra perfectamente el bloque de Forms adaptable, lo que le permite crear e implementar rápidamente formularios en su sitio de AEM.

### Información general

Para iniciar correctamente el nuevo proyecto con formularios integrados, deberá:

1. Cree un repositorio de GitHub con la plantilla de plantillas de AEM Forms.
2. Configure AEM Code Sync para automatizar la sincronización de contenido entre AEM y el repositorio.
3. Configure la conexión entre el proyecto de GitHub y el entorno de AEM.
4. Establezca y publique un nuevo sitio de AEM.
5. Agregar y administrar formularios mediante el Editor universal.

Las siguientes secciones le guiarán a través de cada paso en detalle, lo que garantiza una experiencia de configuración del proyecto fluida y eficiente.

+++Paso 1: Crear un repositorio de GitHub a partir de una plantilla

1. **Acceder a la plantilla de plantillas de AEM Forms**
   - Ir a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![Plantilla de plantillas de AEM Forms](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *Figura: Repositorio de plantillas de AEM Forms con bloque de Forms adaptable preconfigurado*

2. **Crear su repositorio**
   - Haga clic en **Usar esta plantilla** > **Crear un nuevo repositorio**

   ![Crear repositorio a partir de la plantilla](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *Imagen: uso de la plantilla para crear un nuevo repositorio*

3. **Configurar la configuración del repositorio**
   - **Propietario**: seleccione su cuenta u organización de GitHub
   - **Nombre del repositorio**: Elija un nombre descriptivo (por ejemplo, `my-forms-project`)
   - **Visibilidad**: Seleccione **Público** (recomendado para Edge Delivery Services)
   - Haga clic en **Crear repositorio**

   ![Configuración del repositorio](/help/edge/docs/forms/assets/name-eds-repo.png)
   *Imagen: Configuración del nuevo repositorio con visibilidad pública*

**Validación:** Confirme que tiene un nuevo repositorio de GitHub basado en la plantilla de plantillas de AEM Forms.

+++

+++Paso 2: Instalar AEM Code Sync

AEM Code Sync sincroniza automáticamente los cambios de contenido entre el entorno de creación de AEM y el repositorio de GitHub.

1. **Instalar la aplicación de GitHub**
   - Ir a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **Configurar permisos de acceso**
   - Seleccionar **Solo seleccionar repositorios**
   - Elija el repositorio recién creado
   - Haga clic en **Guardar**

   ![Instalación de sincronización de código de AEM](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *Imagen: instalando AEM Code Sync con permisos específicos del repositorio*

**Punto de comprobación:** La sincronización de código de AEM ya está instalada y tiene acceso a su repositorio.

+++

+++Paso 3: Configuración de la integración de AEM

El archivo `fstab.yaml` conecta el repositorio de GitHub con el entorno de creación de AEM para la sincronización de contenido.

1. **Vaya a su repositorio**
   - Vaya al repositorio de GitHub recién creado
   - Debería ver los archivos de plantillas de AEM Forms

2. **Crear el archivo fstab.yaml**
   - Haga clic en **Agregar archivo** > **Crear nuevo archivo** en el directorio raíz
   - Asigne un nombre al archivo `fstab.yaml`

   ![Creando archivo fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)
   *Figura: Creando el archivo de configuración fstab.yaml*

3. **Agregue sus detalles de conexión de AEM**

   Copie y pegue la siguiente configuración, reemplazando los marcadores de posición:

   ```yaml
   mountpoints:
     /: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
   ```

   **Reemplazar:**
   - `<aem-author>`: su URL de autor de AEM as a Cloud Service (por ejemplo, `author-p12345-e67890.adobeaemcloud.com`)
   - `<owner>`: su nombre de usuario u organización de GitHub
   - `<repository>`: el nombre de su repositorio

   **Ejemplo:**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![Editando archivo fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *Figura: Configuración del punto de montaje para la integración de AEM*

4. **Confirmar la configuración**
   - Añada un mensaje de compromiso: &quot;Add AEM integration configuration&quot;
   - Haga clic en **Confirmar nuevo archivo**

   ![Confirmando cambios fstab](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *Figura: confirmando la configuración de fstab.yaml*

**Validación:** Confirme la conexión del repositorio de GitHub a AEM.

    >[!NOTE]
    >
    >¿Tiene problemas de compilación? Ver [solución de problemas de compilación de GitHub](#troubleshooting-github-build-issues).

+++

+++Paso 4: Crear un sitio de AEM conectado a su repositorio de GitHub.

1. **Acceder a la consola de AEM Sites**
   - Inicie sesión en la instancia de creación de AEM as a Cloud Service.
   - Vaya a **Sitios**

   ![Consola AEM Sites](/help/edge/assets/select-sites.png)
   *Imagen: acceso a la consola de AEM Sites*

2. **Iniciar la creación del sitio**
   - Haga clic en **Crear** > **Sitio a partir de la plantilla**

   ![Crear opción de sitio](/help/edge/docs/forms/assets/create-sites.png)
   *Imagen: creando un nuevo sitio a partir de una plantilla*

3. **Seleccione la plantilla de Edge Delivery Services**
   - Elija la plantilla **Edge Delivery Services Site**
   - Haga clic en **Siguiente**

   ![Selección de plantilla del sitio](/help/edge/docs/forms/assets/select-site-template.png)
   *Figura: seleccionar la plantilla del sitio de Edge Delivery Services*

   >[!NOTE]
   >
   >¿No está disponible la plantilla **?** Si no ve la plantilla de Edge Delivery Services:
   >
   >1. Haga clic en **Importar** para cargar la plantilla
   >2. Descargar plantillas de [versiones de GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)

4. **Configurar el sitio**

   Especifique la siguiente información:

   | Campo | Valor | Ejemplos |
   |-----------------|-----------------------------|-----------------------------------------|
   | **Título del sitio** | Nombre descriptivo del sitio | &quot;Mi proyecto de Forms&quot; |
   | **Nombre del sitio** | Nombre descriptivo de la URL | &quot;my-forms-project&quot; |
   | **URL de GitHub** | La URL de su repositorio | `https://github.com/mycompany/my-forms-project` |

   ![Configuración del sitio](/help/edge/docs/forms/assets/create-aem-site.png)
   *Imagen: Configuración del nuevo sitio de AEM con la integración de GitHub*

5. **Creación completa del sitio**
   - Revise la configuración
   - Haga clic en **Crear**

   ![Confirmar la creación del sitio](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *Imagen: confirmando la creación del sitio*

   **¡Correcto!**: el sitio de AEM se ha creado y conectado a GitHub.

6. **Abrir en editor universal**
   - En la consola Sitios, busque el nuevo sitio
   - Seleccionar la página `index`
   - Haga clic en **Editar**

   ![Editar sitio en el editor universal](/help/edge/docs/forms/assets/edit-site.png)
   *Imagen: abriendo el sitio para editarlo*

   El editor universal se abre en una nueva pestaña, que proporciona funciones de creación de WYSIWYG.

   ![Interfaz de editor universal](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *Imagen: el sitio se abrió en el editor universal para la edición de WYSIWYG*

**Validación:** Confirme que su sitio de AEM está listo para la creación de formularios.

+++

+++Paso 5: Publicación del sitio

La publicación hace que el sitio esté disponible en Edge Delivery Services para el acceso global.

1. **Publicación rápida desde la consola Sitios**
   - Vuelva a la consola de AEM Sites.
   - Seleccione las páginas del sitio (o seleccione todo con Ctrl+A)
   - Haga clic en **Publicación rápida**

   ![Publicando sitio de AEM](/help/edge/docs/forms/assets/publish-sites.png)
   *Imagen: seleccionando páginas para la publicación rápida*

2. **Confirmar publicación**
   - En el cuadro de diálogo de confirmación, haga clic en **Publicar**

   ![Cuadro De Diálogo De Publicación Rápida](/help/edge/docs/forms/assets/quick-publish.png)
   *Figura: Confirmando la acción de publicación*

   **Alternativa:** También puede publicar directamente desde el Editor universal con el botón Publicar.

   ![Publicar desde el editor universal](/help/edge/docs/forms/assets/qui.png)
   *Figura: Publicación directamente desde el editor universal*

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

**Validación:** Confirma que tu sitio está activo en Edge Delivery Services.

>[!TIP]
>
> **Patrones de URL:**
>
> - **Página de inicio:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **Otras páginas:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**Siguiente:** [Cree su primer formulario](#create-your-first-form)

+++

## Ruta B: Agregar Forms a un proyecto existente

**Ideal para:** AEM Sites existente con Edge Delivery Services

Si ya tiene un proyecto de AEM con Edge Delivery Services, puede agregar funcionalidades de formulario integrando el bloque de Forms adaptable.

### Requisitos previos para la ruta B

Para continuar con la integración de formularios en el proyecto de AEM existente, asegúrese de que se cumplan los siguientes requisitos previos:

- Ya tiene un proyecto de AEM creado con la [Plataforma de AEM XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk).
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

+++Paso 1: Copiar archivos de bloque de Forms

1. **Vaya a su proyecto local**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **Descargar los archivos necesarios de las plantillas de AEM Forms**

   Copie estos archivos del [repositorio de plantillas de AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms):

   | Origen | Destino | Función |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | Funcionalidad de formulario principal |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | Integración del editor universal |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | Estilo del editor |

3. **Compatibilidad con el editor de actualizaciones**
   - Reemplace su archivo de `/scripts/editor-support.js` por [editor-support.js de AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)

**Validación:** Confirme que los archivos de bloque de formulario se encuentran en el proyecto.

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

   **Lo que hace esto:** Habilita los componentes de formulario en el selector de componentes del editor universal.

**Validación:** Confirmar que los componentes de formulario aparecen en el Editor universal.

+++

+++Paso 3: Configurar ESLint (opcional)

**Por qué este paso:** evita los errores de identificación de los archivos específicos del formulario y configura las reglas de validación adecuadas.

1. **Actualizar .eslintignore**

   Agregar estas líneas a `/.eslintignore`:

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **Actualizar .eslintrc.js**

   Agregar estas reglas al objeto `rules` en `/.eslintrc.js`:

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

**Validación:** Confirme que ESLint funciona con los componentes del formulario.

+++

+++Paso 4: Creación e implementación

1. **Instalar dependencias y compilar**

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

**Validación:** Confirme que su proyecto incluye capacidades de formulario.

+++

**Siguiente:** [Cree Su Primer Formulario](#create-your-first-form)

## Creación De Su Primer Formulario

**Quién debe seguir esta sección:**\
Esta sección es relevante para los usuarios que siguen la Ruta A (nuevo proyecto) o la Ruta B (proyecto existente).

Ahora que el proyecto está preparado para crear formularios, ya puede crear el primer formulario con el entorno de creación intuitivo de WYSIWYG del Editor universal. Los siguientes pasos proporcionan un enfoque estructurado para diseñar, configurar y publicar un formulario en el sitio de AEM.

### Información general

El proceso de creación de un formulario en el Editor universal consta de varias fases clave:

1. **Insertar el bloque de formulario adaptable**\
   Comience agregando el bloque de formulario adaptable a la página elegida.

2. **Agregar componentes de formulario**\
   Rellene el formulario insertando componentes como campos de texto, botones y otros elementos de entrada.

3. **Configurar propiedades del componente**\
   Ajuste la configuración y las propiedades de cada componente para satisfacer los requisitos del formulario.

4. **Previsualizar y probar el formulario**\
   Utilice la funcionalidad de vista previa para validar el aspecto y el comportamiento del formulario antes de publicarlo.

5. **Publicar la página actualizada**\
   Una vez satisfecho, publique la página para que el formulario esté disponible para los usuarios finales.

Las siguientes secciones le guiarán en detalle por cada uno de estos pasos, lo que garantiza una experiencia de creación de formularios fluida y eficaz.

+++Paso 1: Agregar bloque de formulario adaptable

1. **Abrir la página en el editor universal**
   - Vaya a la consola **Sitios** en AEM
   - Seleccione la página donde desea agregar un formulario (por ejemplo, `index`)
   - Haga clic en **Editar**

   La página se abrirá en el Editor universal para la edición de WYSIWYG.

2. **Agregar el componente de formulario adaptable**
   - Abra el panel **Árbol de contenido** (barra lateral izquierda)
   - Vaya a la sección donde desee agregar el formulario
   - Haga clic en el icono **Agregar** (+)
   - Seleccione **Formulario adaptable** de la lista de componentes

   ![Agregando bloque de formulario adaptable](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *Imagen: agregando un bloque de formulario adaptable a su página*

**Validación:** Confirme que tiene un contenedor de formulario vacío.

+++

+++Paso 2: Agregar componentes de formulario

1. **Vaya a su bloque de formulario**
   - En el árbol de contenido, busque la sección Formulario adaptable recién agregado

   ![Bloque de formulario adaptable agregado](/help/edge/docs/forms/assets/adative-form-block.png)
   *Figura: bloque de formulario adaptable en el árbol de contenido*

2. **Agregar componentes de formulario**

   Puede agregar componentes de dos formas:

   **Método A: haga clic para agregar**
   - Haga clic en el icono **Agregar** (+) de la sección del formulario
   - Seleccionar componentes de la lista **Componentes de formulario adaptable**

   **Método B: Arrastrar y soltar**
   - Arrastre componentes directamente desde el panel de componentes al formulario

   ![Agregando componentes de formulario](/help/edge/docs/forms/assets/add-component.png)
   *Imagen: agregando componentes al formulario*

   **Componentes de inicio recomendados:**
   - Entrada de texto (para nombre, correo electrónico)
   - Área de texto (para mensajes)
   - Botón Enviar

3. **Configurar propiedades de componentes**
   - Seleccionar cualquier componente del formulario
   - Utilice el panel **Propiedades** (barra lateral derecha) para configurar:
      - Etiquetas y marcadores de posición
      - Reglas de validación
      - Configuración de campo obligatoria

   ![Panel de propiedades del componente](/help/edge/docs/forms/assets/component-properties.png)
   *Figura: Configurar propiedades del componente*

4. **Vista previa del formulario**

   El formulario tendrá un aspecto similar al siguiente:

   ![Vista previa del formulario completado](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *Figura: Formulario de ejemplo creado con el editor universal*

**Validación:** Confirme que el formulario está listo para la publicación.

>[!IMPORTANT]
>
> Recuerde publicar la página después de realizar cambios para ver las actualizaciones en el explorador.

+++

+++Paso 3: Publicar el formulario

1. **Publicar desde el editor universal**
   - Haga clic en el botón **Publicar** del Editor universal

   ![Formulario de publicación](/help/edge/docs/forms/assets/publish-form.png)
   *Imagen: publicando el formulario desde el Editor universal*

2. **Confirmar publicación**
   - En el cuadro de diálogo de confirmación, haga clic en **Publicar**

   ![Confirmación de publicación](/help/edge/docs/forms/assets/publish-form1.png)
   *Figura: Confirmando la acción de publicación*

   Verá un mensaje de éxito que confirma la publicación.

   ![Éxito de publicación](/help/edge/docs/forms/assets/publish-form2.png)
   *Imagen: confirmación de publicación correcta*

3. **Ver tu formulario activo**

   El formulario ya está activo en:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL de ejemplo:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

   ![Página de formulario activo](/help/edge/docs/forms/assets/publish-index-page.png)
   *Imagen: tu página de formulario publicada en Edge Delivery Services*

**¡Felicitaciones!** El formulario está ahora activo y listo para recopilar envíos.

+++

### Próximos pasos

Ahora que tiene un formulario en funcionamiento, puede:

- **Personalizar estilo** al editar archivos CSS y JavaScript
- **Agregar características de formulario avanzadas** como reglas de validación y lógica condicional
- **Configure el desarrollo local** para una iteración más rápida
- **Crear formularios independientes** para casos de uso específicos

>[!TIP]
>
> **Más información:** [Crear formularios independientes en el editor universal](/help/edge/docs/forms/universal-editor/create-forms.md)

## Configuración del entorno de desarrollo local

**Ideal para:** desarrolladores que desean personalizar el estilo y el comportamiento del formulario

Un entorno de desarrollo local le permite realizar cambios y verlos instantáneamente sin pasar por el ciclo de publicación.

+++Configure la CLI de AEM y el desarrollo local

1. **Instalar CLI de AEM**

   La CLI de AEM simplifica las tareas de desarrollo local:

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **Clonar el repositorio**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   Reemplace `<owner>` y `<repo>` por sus detalles reales de GitHub.

3. **Iniciar el servidor de desarrollo local**

   ```bash
   aem up
   ```

   Esto inicia un servidor local con capacidades de recarga en caliente.

4. **Realizar personalizaciones**

   - Editar archivos en el directorio `blocks/form/` para el estilo y el comportamiento del formulario
   - Modificar `form.css` para el estilo
   - Actualizar `form.js` para el comportamiento

   **Ver cambios al instante** en el explorador a las `http://localhost:3000`

5. **Implemente sus cambios**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   Los cambios estarán disponibles en:
   - **Vista previa:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **Producción:** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## Solución de problemas

### Problemas comunes y soluciones

+++Problemas de compilación de GitHub

**Problema:** errores de compilación o errores de vinculación

**Solución 1: Controlar Errores De Vinculación**

Si se producen errores de vinculación:

1. Abra `package.json` en la raíz del proyecto
2. Buscar el script `lint`:

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

**Solución 2: errores de ruta de módulo**

Si ve &quot;No se puede resolver la ruta al módulo &#39;/scripts/lib-franklin.js&#39;&quot;:

1. Navegue hasta `blocks/form/form.js`
2. Actualice la instrucción import:

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++Problemas del editor universal

**Problema:** Los componentes de formulario no aparecen en el editor universal

**Soluciones:**

- Compruebe que AEM Code Sync está instalado y en ejecución
- Compruebe que `fstab.yaml` tenga la dirección URL de autor de AEM correcta
- Asegúrese de que la instancia de AEM tenga habilitado el acceso anticipado
- Confirmar que `component-definition.json` incluye componentes de formulario

**Problema:** Los cambios no son visibles después de la publicación

**Soluciones:**

- Esperar a que se actualice la caché de CDN
- Compruebe la caché del explorador (pruebe de incógnito/modo privado)
- Compruebe que se está utilizando el formato de dirección URL correcto

+++

+++Problemas de funcionalidad del formulario

**Problema:** Los envíos de formularios no funcionan

**Soluciones:**

- Asegúrese de que tiene un componente de botón de envío
- Comprobar configuración de URL de acción de formulario
- Verificar reglas de validación de formularios
- Probar primero en el modo de vista previa

**Problema:** Problemas de estilo

**Soluciones:**

- Comprobar rutas de archivo CSS en `blocks/form/`
- Borrar caché del explorador
- Verificar sintaxis CSS
- Realizar pruebas en el entorno de desarrollo local

+++

