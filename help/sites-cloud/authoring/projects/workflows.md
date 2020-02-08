---
title: Uso de flujos de trabajo de proyecto
description: Hay varios flujos de trabajo de proyectos disponibles de forma integrada.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Uso de flujos de trabajo de proyecto {#working-with-project-workflows}

Entre los flujos de trabajo de proyecto disponibles de fábrica se incluye lo siguiente:

* **Flujo de trabajo** de aprobación de proyectos: este flujo de trabajo le permite asignar contenido a un usuario, revisarlo y aprobarlo.
* **Inicio** de solicitud: flujo de trabajo que solicita un inicio.
* **Solicitud de página** de aterrizaje: este flujo de trabajo solicita una página de aterrizaje.
* **Solicitar correo electrónico**: flujo de trabajo para solicitar un correo electrónico.
* **Crear y traducir copia DAM y Crear copia de idioma DAM**: crea elementos binarios, metadatos y etiquetas traducidos para los recursos y las carpetas.

Según la plantilla Proyecto que seleccione, tendrá a su disposición determinados flujos de trabajo:

|  | **Proyecto simple** | **Proyecto multimedia** | **Proyecto de traducción** |
|---|:-:|:-:|:-:|
| Solicitar copia |  | x |  |
| Sesión fotográfica del producto |  | x |  |
| Aprobación del proyecto | x |  |  |
| Solicitar lanzamiento | x |  |  |
| Solicitar página de aterrizaje | x |  |  |
| Solicitar correo electrónico | x |  |  |
| DAM Crear copia&amp;amp de idioma;último; |  |  | x |
| DAM Crear y traducir copia y registro de idioma;último; |  |  | x |

>[!NOTE]
>
>&amp;ast; These workflows are not started from the **Workflow** tile in Projects. Consulte Creación de copias de idioma para recursos. 
<!--
>&ast; These workflows are not started from the **Workflow** tile in Projects. See [Creating Language Copies for Assets.](/help/sites-administering/tc-manage.md)
-->

Las etapas para iniciar y completar flujos de trabajo no son las mismas, independientemente del flujo de trabajo que se elija. Solo las etapas cambian.

Un flujo de trabajo se inicia directamente en Proyectos (excepto Crear copia de idioma DAM y Crear y traducir copia de idioma DAM). La información sobre cualquier tarea pendiente de un proyecto aparece en el mosaico **Tareas**. Las notificaciones para las tareas que se deben completar aparecen junto al icono de usuario.

Para obtener más información sobre cómo trabajar con flujos de trabajo en AEM, consulte lo siguiente:

* [Participación en flujos de trabajo](/help/sites-cloud/authoring/workflows/participating.md)
* [Aplicación de flujos de trabajo a páginas](/help/sites-cloud/authoring/workflows/applying.md)
* Configuración de flujos de trabajo<!--* [Configuring workflows](/help/sites-administering/workflows.md)--> 

En esta sección se describen los flujos de trabajo disponibles para Proyectos.

## Flujo de trabajo Solicitar copia {#request-copy-workflow}

Este flujo de trabajo permite solicitar un manuscrito de un usuario y, a continuación, aprobarlo. Para iniciar el flujo de trabajo Solicitar copia:

1. En el proyecto multimedia, seleccione el signo **+** en el mosaico **Flujos de trabajo** y seleccione **Flujo de trabajo Solicitar copia**.
1. Introduzca un título para el manuscrito y un breve resumen de lo que se solicita. Si fuera necesario, introduzca un recuento de palabras de destino, la prioridad de las tareas y una fecha de vencimiento.

   ![Flujo de trabajo de copia de solicitudes](/help/sites-cloud/authoring/assets/projects-request-copy.png)

1. Haga clic en **Crear**. Se inicia el flujo de trabajo. La tarea aparece en el mosaico **Tareas**.

   ![Se agregó la copia de solicitud](/help/sites-cloud/authoring/assets/projects-request-copy-add.png)

## Flujo de trabajo Aprobación del proyecto {#project-approval-workflow}

En el flujo de trabajo Aprobación del proyecto, se asigna contenido a un usuario, el contenido se revisa y luego se aprueba.

1. In your Simple project, select the **`+`** sign in the **Workflows** tile and select **Project Approval Workflow**.
1. Introduzca un título y seleccione a quién asignarlo de la lista del equipo. Si fuera necesario, introduzca una descripción, ruta de contenido, prioridad de las tareas y una fecha de vencimiento.

   ![Solicitud de aprobación](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Haga clic en **Crear**. Se inicia el flujo de trabajo. La tarea aparece en el mosaico **Tareas**.

   ![Se agregó la aprobación de solicitud](/help/sites-cloud/authoring/assets/projects-approval-add.png)

## Flujo de trabajo Solicitar lanzamiento {#request-launch-workflow}

Este flujo de trabajo permite solicitar un lanzamiento.

1. En el proyecto sencillo, seleccione el signo **+** en el mosaico **Flujos de trabajo** y seleccione **Flujo de trabajo Solicitar lanzamiento**.
1. Introduzca un título para el lanzamiento y proporcione la ruta de origen de este. También puede añadir una descripción y la fecha de lanzamiento, si procede. Seleccione Heredar datos en directo de la página de origen o Excluir páginas secundarias según el comportamiento deseado del lanzamiento.

   ![Solicitar inicio](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Haga clic en **Crear**. Se inicia el flujo de trabajo. **El flujo de trabajo aparece en la lista** Flujos **de trabajo (haga clic en elipses**... en el mosaico **Flujos de trabajo** para acceder a esta lista).

## Crear (y traducir) el flujo de trabajo de copia de idioma de los activos {#create-and-translate-language-copy-workflow-for-assets}

The **Create Language Copy** and the **Create and Translate Language Copy** workflows are covered in detail in creating language copies for assets.
