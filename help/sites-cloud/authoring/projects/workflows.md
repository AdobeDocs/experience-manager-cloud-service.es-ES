---
title: Uso de flujos de trabajo de proyecto
description: Hay una variedad de flujos de trabajo de proyecto disponibles de forma predeterminada.
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 96%

---

# Uso de flujos de trabajo de proyecto {#working-with-project-workflows}

Los flujos de trabajo de proyecto disponibles de forma predeterminada incluyen lo siguiente:

* **Flujo de trabajo de aprobación del proyecto**: este flujo de trabajo le permite asignar contenido a un usuario, revisarlo y aprobarlo.
* **Solicitar lanzamiento**: un flujo de trabajo solicita un lanzamiento.
* **Solicitar página de aterrizaje**: este flujo de trabajo solicita una página de aterrizaje.
* **Solicitar correo electrónico**: flujo de trabajo para solicitar un correo electrónico.
* **Crear y traducir copia DAM y crear copia de idioma DAM**: crea archivos binarios, metadatos y etiquetas traducidos para archivos y carpetas.

Según la plantilla Proyecto que seleccione, tendrá a su disposición determinados flujos de trabajo:

|   | **Proyecto simple** | **Proyecto de traducción** |
|---|:-:|:-:|
| Flujo de trabajo de aprobación del proyecto | x |  |
| Solicitar lanzamiento | x |  |
| Solicitar página de aterrizaje | x |  |
| Solicitar correo electrónico | x | |
| Creación de copia de idioma de DAM&ast; |  | x |
| Creación y traducción de copia de idioma de DAM&ast; |   | x |

>[!NOTE]
>
>&ast; Estos flujos de trabajo no se inician desde el mosaico **Flujo de trabajo** en Proyectos. Consulte [Creación de copias de idioma para recursos](/help/sites-cloud/administering/translation/managing-projects.md).

Los pasos para iniciar y completar flujos de trabajo son los mismos independientemente del flujo de trabajo que se elija. Solo cambian los pasos.

Puede iniciar un flujo de trabajo directamente en los proyectos (excepto Crear copia de idioma DAM o Crear y traducir copia de idioma DAM). La información sobre cualquier tarea pendiente en un proyecto aparece en el mosaico **Tareas**. Las notificaciones de las tareas que se deben completar aparecen junto al icono del usuario.

Para obtener más información sobre el uso de flujos de trabajo en AEM, consulte lo siguiente:

* [Participación en flujos de trabajo](/help/sites-cloud/authoring/workflows/participating.md)
* [Aplicación de flujos de trabajo a páginas](/help/sites-cloud/authoring/workflows/applying.md)
* [Configuración de flujos de trabajo &#x200B;](/help/sites-cloud/administering/workflows-administering.md)

En esta sección se describen los flujos de trabajo disponibles para Proyectos.

## Flujo de trabajo de aprobación del proyecto {#project-approval-workflow}

En el flujo de trabajo de aprobación del proyecto, se asigna contenido a un usuario, se revisa y se aprueba el contenido.

1. En el proyecto sencillo, seleccione el inicio de sesión **`+`** en el mosaico **Flujos de trabajo** y seleccione **Flujo de trabajo Aprobación del proyecto**.
1. Introduzca un título y seleccione a quién desea asignarlo en la lista del equipo. Si procede, introduzca una descripción, una ruta de contenido, una prioridad de tarea y una fecha de vencimiento.

   ![Solicitar aprobación](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Haga clic en **Crear**. Se inicia el flujo de trabajo. La tarea aparece en el mosaico **Tareas**.

## Flujo de trabajo Solicitar lanzamiento {#request-launch-workflow}

Este flujo de trabajo permite solicitar un lanzamiento.

1. En el proyecto simple, seleccione el signo **+** en el mosaico **Flujos de trabajo** y seleccione **Solicitar flujo de trabajo de lanzamiento**.
1. Escriba un título para el lanzamiento y proporcione la ruta de origen del lanzamiento. También puede añadir una descripción y la fecha de lanzamiento, si procede. Seleccione Heredar datos en directo de la página de origen o excluir páginas secundarias según cómo desea que se comporte el lanzamiento.

   ![Solicitar lanzamiento](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Haga clic en **Crear**. Se inicia el flujo de trabajo. El flujo de trabajo aparece en la lista **Flujos de trabajo** (haga clic en los puntos suspensivos **...** del mosaico **Flujos de trabajo** para acceder a esta lista).

## Crear (y traducir) el flujo de trabajo de copia de idioma de los activos {#create-and-translate-language-copy-workflow-for-assets}

Los flujos de trabajo **Crear texto en idiomas** y **Crear y traducir texto en idiomas** se tratan detalladamente en la [creación de textos de idiomas para los recursos](/help/assets/translate-assets.md).
