---
title: Proyectos
description: Los proyectos permiten agrupar los recursos en una entidad cuyo entorno común compartido facilita la administración de los proyectos.
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
source-git-commit: 8ea043b4b6424d6922c41c143ca74fd25ac60cf8
workflow-type: ht
source-wordcount: '1259'
ht-degree: 100%

---

# Proyectos {#projects}

Los proyectos le permiten agrupar los recursos en una entidad. Un entorno común y compartido facilita la administración de los proyectos. Los tipos de recursos que puede asociar con un proyecto se mencionan en AEM como Mosaicos. Los mosaicos pueden incluir información sobre el proyecto y el equipo, los recursos, los flujos de trabajo y otro tipo de información, tal como se describe detalladamente en [Mosaicos del proyecto.](#project-tiles)

>[!CAUTION]
>
>Para que los usuarios de proyectos puedan ver a otros usuarios o grupos mientras utilizan funciones de Proyectos como crear proyectos, crear tareas/flujos de trabajo, ver y administrar al equipo, dichos usuarios deben tener acceso de lectura a `/home/users` y `/home/groups`. La forma más sencilla de implementar esto es proporcionar al grupo de **usuarios de proyectos** acceso de lectura a `/home/users` y `/home/groups`.

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
* Páginas de destino
* Correos electrónicos
* Flujos de trabajo
* Lanzamientos
* Tareas

### Assets {#assets}

En el mosaico **Recursos**, puede reunir todos los recursos que utilice para un proyecto determinado.

![Mosaico de recursos](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

Los recursos se cargan directamente en el mosaico. Además, si dispone del complemento Dynamic Media, puede crear conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

![Conjunto de imágenes](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### Colecciones de recursos {#asset-collections}

Del mismo modo que con los recursos, puede agregar [colecciones de recursos](/help/assets/manage-collections.md) directamente al proyecto. Puede definir colecciones de recursos.

![Colección de recursos](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

Agregue una colección haciendo clic en **Agregar colección** y seleccionando la colección adecuada en la lista.

### Experiencias {#experiences}

El mosaico **Experiencias** permite añadir aplicación móvil, un sitio web o una publicación al proyecto.

![Experiencias](/help/sites-cloud/authoring/assets/project-experiences.png)

Los iconos indican qué tipo de experiencia se representa: sitio web, aplicación móvil o publicación. Para añadir experiencias, pulse o haga clic en las comillas angulares inferiores, pulse **Añadir experiencia** y seleccione el tipo de experiencia.

![Adición de una experiencia](/help/sites-cloud/authoring/assets/projects-add-experience.png)

Seleccione la ruta para las miniaturas y, si fuera necesario, cambie la miniatura de la experiencia. Las experiencias se agrupan en el mosaico **Experiencias.**

### Vínculos {#links}

El mosaico Vínculos permite asociar vínculos externos al proyecto.

![Vínculos](/help/sites-cloud/authoring/assets/project-links.png)

Puede asignar al vínculo un nombre fácil de reconocer, así como cambiar la miniatura.

![Adición de un vínculo](/help/sites-cloud/authoring/assets/projects-add-link.png)

### Información del proyecto {#project-info}

El mosaico Información del proyecto proporciona información general sobre el proyecto; por ejemplo, una descripción, el estado del proyecto (activo o inactivo), una fecha de vencimiento y los miembros. Además, puede añadir una miniatura de proyecto que se muestra en la página principal Proyectos.

![Información del proyecto](/help/sites-cloud/authoring/assets/project-info.png)

Desde este mosaico, así como el mosaico Equipo, se pueden asignar o eliminar miembros, así como cambiar la función de estos.

![Adición de integrantes del equipo al proyecto](/help/sites-cloud/authoring/assets/projects-add-team.png)

### Trabajo de traducción {#translation-job}

En el mosaico Trabajo de traducción puede iniciar una traducción y también puede ver el estado de las traducciones. Para configurar la traducción, consulte [Creación de proyectos de traducción](/help/assets/translate-assets.md).

![Trabajo de traducción](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Haga clic en los puntos suspensivos situados en la parte inferior de la tarjeta **Trabajo de traducción** para ver los recursos en el flujo de trabajo de traducción. En la lista de trabajos de traducción también se muestran las entradas para los metadatos y las etiquetas de los recursos. Estas entradas indican que los metadatos y las etiquetas de los recursos también se traducen.

![Detalles del trabajo de traducción](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### Equipo {#team}

En este mosaico puede especificar los miembros del equipo del proyecto. Durante la edición puede introducir el nombre del miembro del equipo y asignar la función de usuario.

![Mosaico de equipo](/help/sites-cloud/authoring/assets/projects-team-tile.png)

Puede añadir y eliminar miembros en el equipo. Además, puede editar la [función de usuario](#user-roles-in-a-project) asignada al miembro del equipo.

![Adición de un equipo de la lista](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### Flujos de trabajo {#workflows}

Puede asignar el proyecto para hacer un seguimiento de determinados flujos de trabajo. Si hay flujos de trabajo en ejecución, su estado se muestra en el mosaico **Flujos de trabajo** de Proyectos.

![Flujos de trabajo](/help/sites-cloud/authoring/assets/project-workflows.png)

Puede asignar el proyecto para hacer un seguimiento de determinados flujos de trabajo. Según el proyecto que elija, tiene diferentes flujos de trabajo disponibles.

Estos se describen en [Uso de flujos de trabajo del proyecto.](/help/sites-cloud/authoring/projects/workflows.md) 

### Lanzamientos {#launches}

El mosaico Lanzamientos muestra los lanzamientos que se hayan solicitado con un [flujo de trabajo de solicitud de lanzamiento.](/help/sites-cloud/authoring/projects/workflows.md) 

![Lanzamientos](/help/sites-cloud/authoring/assets/project-launches.png)

### Tareas {#tasks}

En Tareas puede supervisar el estado de cualquier tarea relacionada con el proyecto, incluidos los flujos de trabajo. Las tareas se describen detalladamente en [Uso de tareas](/help/sites-cloud/authoring/projects/tasks.md).

![Tareas](/help/sites-cloud/authoring/assets/projects-tasks.png)

## Plantillas de proyecto {#project-templates}

En AEM se incluyen tres plantillas predefinidas de fábrica:

* Un proyecto sencillo: una muestra de referencia para los proyectos que no se ajustan a otras categorías (una plantilla global). Incluye tres funciones básicas (propietarios, editores y observadores) y cuatro flujos de trabajo (Aprobación del borrador, Solicitud de lanzamiento, Solicitud de página de aterrizaje y Solicitud de correo electrónico).
* Un proyecto de medios: un proyecto de muestra de referencia para las actividades relacionadas con medios. Incluye varias funciones relacionadas con contenido multimedia del proyecto (fotógrafos, editores, redactores, diseñadores, propietarios y observadores). También incluye el flujo de trabajo Solicitar copia para solicitar y revisar texto.
* Un [proyecto de traducción](/help/sites-cloud/administering/translation/overview.md): una muestra de referencia para administrar las actividades relacionadas con la traducción. Incluye tres funciones básicas (propietarios, editores y observadores). Incluye dos flujos de trabajo a los que se accede en la interfaz de usuario Flujos de trabajo.

En función de la plantilla seleccionada, dispone de distintas opciones en relación con las funciones de usuario y los flujos de trabajo.

## Funciones de usuario en un proyecto {#user-roles-in-a-project}

Las diferentes funciones de usuario se establecen en una plantilla de proyecto y se utilizan por dos motivos principales:

1. Permisos. Las funciones de usuario se incluyen en una de las tres categorías enumeradas: Observador, Editor, Propietario. Por ejemplo, puede que un fotógrafo o redactor tenga los mismos derechos que un editor. Los permisos determinan lo que un usuario puede hacer con el contenido de un proyecto.
1. Flujos de trabajo. Los flujos de trabajo determinan a quién se asignan tareas en un proyecto. Las tareas se pueden asociar a una función del proyecto. Por ejemplo, una tarea puede asignarse a los fotógrafos, de manera que todos los miembros del equipo con la función Fotógrafo recibirán la tarea.

Todos los proyectos admiten las siguientes funciones predeterminadas para que pueda administrar los permisos de seguridad y control:

| Función | Descripción | Permisos | Miembros del grupo |
|---|---|---|---|
| Observador | Un usuario con esta función puede ver los detalles de un proyecto, incluido el estado del proyecto. | Permisos de lectura de un proyecto | grupo `workflow-users` |
| Editor | Un usuario con esta función puede cargar y editar el contenido de un proyecto. | Acceso de lectura y escritura en un proyecto, metadatos asociados y recursos relacionados; privilegios para cargar una lista de tomas y revisar y aprobar recursos; permiso de escritura en /etc/commerce; permiso de modificación en un proyecto específico. | grupo de flujo de trabajo-usuarios |
| Propietario | Un usuario con esta función puede iniciar un proyecto. Un propietario puede crear un proyecto e iniciar el trabajo y también mover los recursos aprobados a la carpeta Producción. El propietario también puede realizar y visualizar todas las demás tareas del proyecto. | Permiso de escritura en `/etc/commerce` | Grupo `dam-users` (para poder crear un proyecto), grupo de administradores de proyectos (para poder crear un proyecto y mover recursos) |

>[!NOTE]
>
>Al crear el proyecto y agregar usuarios a las distintas funciones, los grupos asociados con el proyecto se crean automáticamente para administrar los permisos asociados. Por ejemplo, un proyecto llamado Myproject tendría tres grupos: **Propietarios de Myproject**, **Editores de Myproject**, **Observadores de Myproject**. Sin embargo, si se elimina el proyecto, esos grupos no se eliminarán automáticamente. Un administrador debe eliminar manualmente los grupos en **Herramientas** > **Seguridad** > **Grupos**.
