---
title: Proyectos
description: Los proyectos le permiten agrupar recursos en una entidad cuyo entorno común compartido facilita la administración de sus proyectos
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
source-git-commit: 8ea043b4b6424d6922c41c143ca74fd25ac60cf8
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 51%

---

# Proyectos {#projects}

Los proyectos permiten agrupar los recursos en una entidad. Un entorno común y compartido facilita la administración de sus proyectos. AEM Los tipos de recursos que puede asociar a un proyecto se denominan en la sección Tipos de recursos (mosaicos), que se denominan en la sección Tipos de recursos (mosaicos) de los que se puede hacer referencia en la sección. Los mosaicos pueden incluir información sobre el proyecto y el equipo, los recursos, los flujos de trabajo y otro tipo de información, tal como se describe detalladamente en [Mosaicos del proyecto.](#project-tiles)

>[!CAUTION]
>
>Para que los usuarios de proyectos puedan ver a otros usuarios o grupos mientras utilizan funciones de Proyectos como crear proyectos, crear tareas/flujos de trabajo, ver y administrar al equipo, dichos usuarios deben tener acceso de lectura a `/home/users` y `/home/groups`. La forma más sencilla de implementar esto es proporcionar al grupo de **usuarios de proyectos** acceso de lectura a `/home/users` y `/home/groups`.

Como usuario, puede hacer lo siguiente:

* Creación de proyectos
* Asociar carpetas de contenido y recursos a un proyecto
* Eliminar proyectos
* Eliminar vínculos de contenido del proyecto

Consulte los siguientes temas adicionales:

* [Administración de proyectos](/help/sites-cloud/authoring/projects/managing.md)
* [Uso de tareas](/help/sites-cloud/authoring/projects/tasks.md)
* [Uso de flujos de trabajo de proyecto](/help/sites-cloud/authoring/projects/workflows.md)

## Consola Proyectos {#projects-console}

AEM En la consola Proyectos es donde puede acceder a sus proyectos y administrarlos dentro de su propio grupo de trabajo de proyectos de.

![La consola Proyectos](/help/sites-cloud/authoring/assets/projects-console.png)

* Seleccionar **Cronología** y luego un proyecto para ver su cronología.
* Hacer clic o tocar **Seleccionar** para entrar en el modo de selección.
* Clic **Crear** para agregar proyectos.
* **Alternar proyectos activos** permite alternar entre todos los proyectos y solo aquellos que están activos.
* **Mostrar vista de estadísticas** permite ver las estadísticas del proyecto relativas a las finalizaciones de tareas.

## Mosaicos del proyecto {#project-tiles}

Con Proyectos, puede asociar distintos tipos de información a sus proyectos. Estos se denominan **Mosaicos**. En esta sección se describe cada uno de los mosaicos y qué tipo de información contienen.

Puede tener los siguientes mosaicos asociados al proyecto. Cada uno de ellos se describe en las secciones siguientes:

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

En el **Assets** mosaico, puede recopilar todos los recursos que utiliza para un proyecto en particular.

![Mosaico de recursos](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

Puede cargar recursos directamente en el mosaico. Además, puede crear conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos si tiene el complemento de Dynamic Media.

![Conjunto de imágenes](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### Colecciones de recursos {#asset-collections}

De forma similar a los recursos, puede agregar [colecciones de recursos](/help/assets/manage-collections.md) directamente en el proyecto. Las colecciones se definen en Assets.

![Colección de recursos](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

Agregue una colección haciendo clic en **Agregar colección** y seleccionando la colección adecuada en la lista.

### Experiencias {#experiences}

El **Experiencias** El mosaico permite agregar una aplicación móvil, un sitio web o una publicación al proyecto.

![Experiencias](/help/sites-cloud/authoring/assets/project-experiences.png)

Los iconos indican qué tipo de experiencia se representa: sitio web, aplicación móvil o publicación. Para añadir experiencias, pulse o haga clic en las comillas angulares inferiores, pulse **Añadir experiencia** y seleccione el tipo de experiencia.

![Adición de una experiencia](/help/sites-cloud/authoring/assets/projects-add-experience.png)

Seleccione la ruta para las miniaturas y, si fuera necesario, cambie la miniatura de la experiencia. Las experiencias se agrupan en el mosaico **Experiencias.**

### Vínculos {#links}

El mosaico Vínculos permite asociar vínculos externos con el proyecto.

![Vínculos](/help/sites-cloud/authoring/assets/project-links.png)

Puede asignar al vínculo un nombre fácil de reconocer, así como cambiar la miniatura.

![Adición de un vínculo](/help/sites-cloud/authoring/assets/projects-add-link.png)

### Información del proyecto {#project-info}

El mosaico Información del proyecto proporciona información general sobre el proyecto, incluida una descripción, el estado del proyecto (inactivo o activo), una fecha de vencimiento y los miembros. Además, puede agregar una miniatura de proyecto, que se mostrará en la página principal Proyectos.

![Información del proyecto](/help/sites-cloud/authoring/assets/project-info.png)

Desde este mosaico, así como el mosaico Equipo, se pueden asignar o eliminar miembros, así como cambiar la función de estos.

![Adición de integrantes del equipo al proyecto](/help/sites-cloud/authoring/assets/projects-add-team.png)

### Trabajo de traducción {#translation-job}

El mosaico Trabajo de traducción es donde se inicia una traducción y también donde se ve el estado de las traducciones. Para configurar la traducción, consulte [Creación de proyectos de traducción](/help/assets/translate-assets.md).

![Trabajo de traducción](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Haga clic en los puntos suspensivos situados en la parte inferior de la tarjeta **Trabajo de traducción** para ver los recursos en el flujo de trabajo de traducción. En la lista de trabajos de traducción también se muestran las entradas para los metadatos y las etiquetas de los recursos. Estas entradas indican que los metadatos y las etiquetas de los recursos también se traducen.

![Detalles del trabajo de traducción](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### Equipo {#team}

En este mosaico, puede especificar los miembros del equipo del proyecto. Al editar, puede introducir el nombre del miembro del equipo y asignar la función del usuario.

![Mosaico de equipo](/help/sites-cloud/authoring/assets/projects-team-tile.png)

Puede añadir y eliminar miembros en el equipo. Además, puede editar la [función de usuario](#user-roles-in-a-project) asignada al miembro del equipo.

![Adición de un equipo de la lista](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### Flujos de trabajo {#workflows}

Puede asignar el proyecto para que siga ciertos flujos de trabajo. Si se está ejecutando algún flujo de trabajo, su estado se muestra en la variable **Flujos de trabajo** mosaico en Proyectos.

![Flujos de trabajo](/help/sites-cloud/authoring/assets/project-workflows.png)

Puede asignar el proyecto para que siga ciertos flujos de trabajo. Según el proyecto que elija, tendrá diferentes flujos de trabajo disponibles.

Estas se describen en [Uso de flujos de trabajo de proyecto.](/help/sites-cloud/authoring/projects/workflows.md)

### Lanzamientos {#launches}

El mosaico Lanzamientos muestra todos los lanzamientos que se han solicitado con una [Solicitar flujo de trabajo de Launch.](/help/sites-cloud/authoring/projects/workflows.md)

![Lanzamientos](/help/sites-cloud/authoring/assets/project-launches.png)

### Tareas {#tasks}

Las tareas permiten monitorizar el estado de cualquier tarea relacionada con el proyecto, incluidos los flujos de trabajo. Las tareas se describen detalladamente en [Uso de tareas](/help/sites-cloud/authoring/projects/tasks.md).

![Tareas](/help/sites-cloud/authoring/assets/projects-tasks.png)

## Plantillas de proyecto {#project-templates}

En AEM se incluyen tres plantillas predefinidas de fábrica:

* Un proyecto sencillo: una muestra de referencia para los proyectos que no se ajustan a otras categorías (una plantilla global). Incluye tres funciones básicas (propietarios, editores y observadores) y cuatro flujos de trabajo (Aprobación del borrador, Solicitud de lanzamiento, Solicitud de página de aterrizaje y Solicitud de correo electrónico).
* Un proyecto de medios: un proyecto de muestra de referencia para las actividades relacionadas con medios. Incluye varias funciones relacionadas con contenido multimedia del proyecto (fotógrafos, editores, redactores, diseñadores, propietarios y observadores). También incluye el flujo de trabajo Solicitar copia para solicitar y revisar texto.
* Un [proyecto de traducción](/help/sites-cloud/administering/translation/overview.md): una muestra de referencia para administrar las actividades relacionadas con la traducción. Incluye tres funciones básicas (propietarios, editores y observadores). Incluye dos flujos de trabajo a los que se accede en la interfaz de usuario Flujos de trabajo.

En función de la plantilla que seleccione, tiene diferentes opciones disponibles, especialmente en relación con los roles de usuario y los flujos de trabajo.

## Funciones de usuario en un proyecto {#user-roles-in-a-project}

Las diferentes funciones de usuario se establecen en una plantilla de proyecto y se utilizan por dos motivos principales:

1. Permisos. Las funciones de usuario se dividen en una de las tres categorías enumeradas: Observador, Editor, Propietario. Por ejemplo, puede que un fotógrafo o redactor tenga los mismos derechos que un editor. Los permisos determinan lo que un usuario puede hacer con el contenido de un proyecto.
1. Flujos de trabajo. Los flujos de trabajo determinan a quién se asignan las tareas de un proyecto. Las tareas se pueden asociar a una función del proyecto. Por ejemplo, se puede asignar una tarea a los fotógrafos para que todos los integrantes del equipo que tengan la función de fotógrafo obtengan la tarea.

Todos los proyectos admiten las siguientes funciones predeterminadas para permitirle administrar los permisos de seguridad y control:

| Función | Descripción | Permisos | Miembros del grupo |
|---|---|---|---|
| Observador | Un usuario con esta función puede ver los detalles del proyecto, incluido su estado. | Permisos de solo lectura en un proyecto | grupo `workflow-users` |
| Editor | Un usuario con esta función puede cargar y editar el contenido de un proyecto. | Acceso de lectura y escritura en un proyecto, metadatos asociados y recursos relacionados; privilegios para cargar una lista de tomas y revisar y aprobar recursos; permiso de escritura en /etc/commerce; permiso de modificación en un proyecto específico. | grupo workflow-users |
| Propietario | Un usuario con esta función puede iniciar un proyecto. Un propietario puede crear un proyecto e iniciar el trabajo y también mover los recursos aprobados a la carpeta Producción. El propietario también puede realizar y visualizar todas las demás tareas del proyecto. | Permiso de escritura en `/etc/commerce` | Grupo `dam-users` (para poder crear un proyecto), grupo de administradores de proyectos (para poder crear un proyecto y mover recursos) |

>[!NOTE]
>
>Al crear el proyecto y agregar usuarios a las distintas funciones, los grupos asociados con el proyecto se crean automáticamente para administrar los permisos asociados. Por ejemplo, un proyecto llamado Myproject tendría tres grupos: **Propietarios de Myproject**, **Editores de Myproject**, **Observadores de Myproject**. Sin embargo, si se elimina el proyecto, esos grupos no se eliminarán automáticamente. Un administrador debe eliminar manualmente los grupos en **Herramientas** > **Seguridad** > **Grupos**.
