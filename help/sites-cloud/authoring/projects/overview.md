---
title: Proyectos
description: Los proyectos permiten agrupar los recursos en una entidad cuyo entorno común compartido facilita la administración de los proyectos.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 79%

---


# Proyectos {#projects}

Los proyectos le permiten agrupar los recursos en una entidad. Un entorno común y compartido facilita la administración de los proyectos. Los tipos de recursos que puede asociar con un proyecto se mencionan en AEM como Mosaicos. Tiles may include project and team information, assets, workflows, and other types of information, as described in detail in [Project Tiles.](#project-tiles)

>[!CAUTION]
>
>For users in projects to see other users/groups while using Projects functionality like creating projects, creating tasks/workflows, seeing and managing the team, those users need to have read access on `/home/users` and `/home/groups`. The easiest way to implement this is to give the **projects-users** group read access to `/home/users` and `/home/groups`.

Como usuario, puede hacer lo siguiente:

* Crear proyectos
* Asociar carpetas de contenido y recursos a un proyecto
* Eliminar proyectos
* Quitar vínculos de contenido del proyecto

Consulte los siguientes temas adicionales:

* [Administración de proyectos](/help/sites-cloud/authoring/projects/managing.md)
* [Uso de tareas](/help/sites-cloud/authoring/projects/tasks.md)
* [Uso de flujos de trabajo de proyecto](/help/sites-cloud/authoring/projects/workflows.md)

## Consola Proyectos {#projects-console}

La consola Proyectos permite acceder a los proyectos en AEM y administrarlos.

![La consola Proyectos](/help/sites-cloud/authoring/assets/projects-console.png)

* Seleccione **Escala de tiempo** y elija un proyecto para ver su escala de tiempo.
* Pulse o haga clic en **Seleccionar** para entrar en el modo Selección.
* Haga clic en **Crear** para añadir proyectos.
* La opción **Alternar proyectos activos** permite cambiar entre todos los proyectos y solamente los que están activos.
* La opción **Mostrar vista de estadísticas** permite ver estadísticas del proyecto relacionadas con las tareas completadas.

## Mosaicos del proyecto {#project-tiles}

Con la consola Proyectos, se asocian distintos tipos de información a los proyectos. Estos se llaman **Mosaicos**. En esta sección se describe cada uno de los mosaicos y el tipo de información que contienen.

Puede tener los siguientes mosaicos asociados al proyecto. Cada uso de ellos se describe en las secciones siguientes:

* Recursos y colecciones de recursos
* Experiencias
* Vínculos
* Información del proyecto
* Equipo
* Páginas de aterrizaje
* Correo electrónico
* Flujos de trabajo
* Lanzamientos
* Tareas

### Assets {#assets}

En el mosaico **Recursos**, puede reunir todos los recursos que utilice para un proyecto determinado.

![Mosaico de recursos](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

Los recursos se cargan directamente en el mosaico. Además, si dispone del complemento Dynamic Media, puede crear conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

![Conjunto de imágenes](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### Colecciones de recursos {#asset-collections}

Del mismo modo que con los recursos, puede agregar colecciones de recursos directamente al proyecto. Puede definir colecciones de recursos. <!--Similar to assets, you can add [asset collections](/help/assets/managing-collections-touch-ui.md) directly to your project. You define collections in Assets.-->

![Colección de recursos](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

Para añadir una colección, haga clic en **Agregar colección** y seleccione la colección adecuada de la lista.

### Experiencias {#experiences}

El mosaico **Experiencias** permite añadir aplicación móvil, un sitio web o una publicación al proyecto.

![Experiencias](/help/sites-cloud/authoring/assets/project-experiences.png)

Los iconos indican qué tipo de experiencia se representa: sitio web, aplicación móvil o publicación. Para agregar experiencias, haga clic en el signo + o en **Agregar experiencia** y seleccione el tipo de experiencia.

![Añadir una experiencia](/help/sites-cloud/authoring/assets/projects-add-experience.png)

Seleccione la ruta para las miniaturas y, si fuera necesario, cambie la miniatura de la experiencia. Las experiencias se agrupan en el mosaico **Experiencias.**

### Vínculos {#links}

El mosaico Vínculos permite asociar vínculos externos al proyecto.

![Vínculos](/help/sites-cloud/authoring/assets/project-links.png)

Puede asignar al vínculo un nombre fácil de reconocer, así como cambiar la miniatura.

![Añadir vínculo](/help/sites-cloud/authoring/assets/projects-add-link.png)

### Información del proyecto {#project-info}

El mosaico Información del proyecto proporciona información general sobre el proyecto; por ejemplo, una descripción, el estado del proyecto (activo o inactivo), una fecha de vencimiento y los miembros. Además, puede añadir una miniatura de proyecto que se muestra en la página principal Proyectos.

![Información del proyecto](/help/sites-cloud/authoring/assets/project-info.png)

Desde este mosaico, así como el mosaico Equipo, se pueden asignar o eliminar miembros, así como cambiar la función de estos.

![Añadir miembros del equipo al proyecto](/help/sites-cloud/authoring/assets/projects-add-team.png)

### Trabajo de traducción {#translation-job}

En el mosaico Trabajo de traducción puede iniciar una traducción y también puede ver el estado de las traducciones. Para configurar la traducción, consulte Creación de proyectos de traducción. <!--To set up your translation, see [Creating Translation Projects](/help/assets/translation-projects.md).-->

![Trabajo de traducción](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Click the ellipsis at the bottom of the **Translation Job** card to view the assets in the translation workflow. En la lista de trabajos de traducción también se muestran las entradas para los metadatos y las etiquetas de los recursos. Estas entradas indican que los metadatos y las etiquetas de los recursos también se traducen.

![Detalle del trabajo de traducción](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### Equipo {#team}

En este mosaico puede especificar los miembros del equipo del proyecto. Durante la edición puede introducir el nombre del miembro del equipo y asignar la función de usuario.

![Mosaico de equipo](/help/sites-cloud/authoring/assets/projects-team-tile.png)

Puede añadir y eliminar miembros en el equipo. Además, puede editar la [función de usuario](#user-roles-in-a-project) asignada al miembro.

![Añadir equipo de lista](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### Flujos de trabajo {#workflows}

Puede asignar el proyecto para hacer un seguimiento de determinados flujos de trabajo. Si hay flujos de trabajo en ejecución, su estado se muestra en el mosaico **Flujos de trabajo** de Proyectos.

![Flujos de trabajo](/help/sites-cloud/authoring/assets/project-workflows.png)

Puede asignar el proyecto para hacer un seguimiento de determinados flujos de trabajo. Según el proyecto que elija, tiene diferentes flujos de trabajo disponibles.

Estos se describen en [Uso de flujos de trabajo del proyecto.](/help/sites-cloud/authoring/projects/workflows.md) 

### Lanzamientos {#launches}

El mosaico Lanzamientos muestra los lanzamientos que se hayan solicitado con un [flujo de trabajo de solicitud de lanzamiento.](/help/sites-cloud/authoring/projects/workflows.md) 

![Lanzamientos](/help/sites-cloud/authoring/assets/project-launches.png)

### Tareas {#tasks}

En Tareas puede supervisar el estado de cualquier tarea relacionada con el proyecto, incluidos los flujos de trabajo. Tasks are covered in detail at [Working with Tasks](/help/sites-cloud/authoring/projects/tasks.md).

![Tareas](/help/sites-cloud/authoring/assets/projects-tasks.png)

## Plantillas de proyecto {#project-templates}

En AEM se incluyen tres plantillas predefinidas de fábrica:

* Un proyecto simple: muestra de referencia para cualquier proyecto que no encaje en otras categorías (un captador global). Incluye tres funciones básicas (propietarios, editores y observadores) y cuatro flujos de trabajo (Aprobación del borrador, Solicitud de lanzamiento, Solicitud de página de aterrizaje y Solicitud de correo electrónico).
* Un proyecto de medios: un proyecto de muestra de referencia para actividades relacionadas con los medios. Incluye varias funciones relacionadas con contenido multimedia del proyecto (fotógrafos, editores, redactores, diseñadores, propietarios y observadores). También incluye dos flujos de trabajo relacionados con el contenido multimedia: Solicitar copia (para solicitar y revisar texto) y Fotografía del producto (para administrar la fotografía relacionada con el producto)
* Proyecto de traducción: una muestra de referencia para la administración de las actividades relacionadas con la traducción. Incluye tres funciones básicas (propietarios, editores y observadores). Incluye dos flujos de trabajo a los que se accede en la interfaz de usuario Flujos de trabajo. <!--* [A translation project](/help/sites-administering/translation.md) - A reference sample for managing translation related activities. It includes three basic roles (Owners, Editors, and Observers). It includes two workflows that are accessed in the Workflows user interface.-->

En función de la plantilla seleccionada, dispone de distintas opciones en relación con las funciones de usuario y los flujos de trabajo.

## Funciones de usuario en un proyecto {#user-roles-in-a-project}

Las diferentes funciones de usuario se establecen en una plantilla de proyecto y se utilizan por dos motivos principales:

1. Permisos. Las funciones de usuario se incluyen en una de las tres categorías enumeradas: Observador, Editor, Propietario. Por ejemplo, puede que un fotógrafo o redactor tenga los mismos derechos que un editor. Los permisos determinan lo que un usuario puede hacer con el contenido de un proyecto.
1. Flujos de trabajo. Los flujos de trabajo determinan a quién se asignan tareas en un proyecto. Las tareas se pueden asociar a una función del proyecto. Por ejemplo, una tarea puede asignarse a los fotógrafos, de manera que todos los miembros del equipo con la función Fotógrafo recibirán la tarea.

Todos los proyectos admiten las siguientes funciones predeterminadas para que pueda administrar los permisos de seguridad y control:

| Función | Descripción | Permisos  | Pertenencia a grupos |
|---|---|---|---|
| Observador | Un usuario con esta función puede ver los detalles de un proyecto, incluido el estado del proyecto. | Permisos de lectura de un proyecto | `workflow-users` grupo |
| Editor | Un usuario con esta función puede cargar y editar el contenido de un proyecto. | Acceso de lectura y escritura en un proyecto, metadatos asociados y recursos relacionados; privilegios para cargar una lista de toma, una sesión fotográfica y revisar y aprobar recursos; escribir permiso en /etc/commerce; modificar permisos en un proyecto específico | grupo de flujo de trabajo-usuarios |
| Propietario | Un usuario con esta función puede iniciar un proyecto. Un propietario puede crear un proyecto, iniciar el trabajo en un proyecto y también mover los recursos aprobados a la carpeta Producción. El propietario también puede realizar y visualizar todas las demás tareas del proyecto. | Write permission on `/etc/commerce` | `dam-users` grupo (para poder crear un proyecto) grupo de administradores de proyectos (para poder mover recursos) |

>[!NOTE]
>
>Al crear el proyecto y agregar usuarios a las distintas funciones, los grupos asociados con el proyecto se crean automáticamente para administrar los permisos asociados. Por ejemplo, un proyecto llamado Myproject tendría tres grupos: **Propietarios de Myproject**, **Editores de Myproject**, **Observadores de Myproject**. Sin embargo, si se elimina el proyecto, esos grupos no se eliminarán automáticamente. Un administrador debe eliminar manualmente los grupos en **Herramientas** > **Seguridad** > **Grupos**.
