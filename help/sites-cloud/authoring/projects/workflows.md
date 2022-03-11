---
title: Uso de flujos de trabajo de proyecto
description: Hay varios flujos de trabajo de proyectos disponibles de forma integrada.
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 89972691dadb9573160ba16a220c5b7cb3ae9742
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 75%

---

# Uso de flujos de trabajo de proyecto {#working-with-project-workflows}

Entre los flujos de trabajo de proyecto disponibles de fábrica se incluye lo siguiente:

* **Flujo de trabajo de aprobación del proyecto** : este flujo de trabajo le permite asignar contenido a un usuario, revisarlo y aprobarlo.
* **Solicitar lanzamiento** : un flujo de trabajo solicita un lanzamiento.
* **Solicitar página de aterrizaje** : este flujo de trabajo solicita una página de aterrizaje.
* **Solicitar correo electrónico**: flujo de trabajo para solicitar un correo electrónico.
* **Crear y traducir copia DAM y Crear copia de idioma DAM**: crea elementos binarios, metadatos y etiquetas traducidos para los recursos y las carpetas.

Según la plantilla Proyecto que seleccione, tendrá a su disposición determinados flujos de trabajo:

|  | **Proyecto simple** | **Proyecto de traducción** |
|---|:-:|:-:|
| Flujo de trabajo de aprobación del proyecto | x |  |
| Solicitar lanzamiento | x |  |
| Solicitar página de aterrizaje | x |  |
| Solicitar correo electrónico | x |  |
| Creación de copia y último idioma de DAM; |  | x |
| Crear y traducir DAM copia y último idioma; |  | x |

>[!NOTE]
>
>&amp;ast; Estos flujos de trabajo no se inician desde la **Flujo de trabajo** en Proyectos. Consulte [Creación de copias de idioma para recursos](/help/sites-cloud/administering/translation/managing-projects.md). 

Las etapas para iniciar y completar flujos de trabajo no son las mismas, independientemente del flujo de trabajo que se elija. Solo las etapas cambian.

Un flujo de trabajo se inicia directamente en Proyectos (excepto Crear copia de idioma DAM y Crear y traducir copia de idioma DAM). La información sobre cualquier tarea pendiente de un proyecto aparece en el mosaico **Tareas**. Las notificaciones para las tareas que se deben completar aparecen junto al icono de usuario.

Para obtener más información sobre el trabajo con flujos de trabajo en AEM, consulte lo siguiente:

* [Participación en flujos de trabajo](/help/sites-cloud/authoring/workflows/participating.md)
* [Aplicación de flujos de trabajo a páginas](/help/sites-cloud/authoring/workflows/applying.md)
* [Configuración de flujos de trabajo ](/help/sites-cloud/administering/workflows-administering.md)

En esta sección se describen los flujos de trabajo disponibles para Proyectos.

## Flujo de trabajo Aprobación del proyecto {#project-approval-workflow}

En el flujo de trabajo Aprobación del proyecto, se asigna contenido a un usuario, el contenido se revisa y luego se aprueba.

1. En el proyecto simple, seleccione la opción **`+`** iniciar sesión en **Flujos de trabajo** mosaico y seleccione **Flujo de trabajo de aprobación del proyecto**.
1. Introduzca un título y seleccione a quién asignarlo de la lista del equipo. Si fuera necesario, introduzca una descripción, ruta de contenido, prioridad de las tareas y una fecha de vencimiento.

   ![Aprobación de solicitud](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Haga clic en **Crear**. Se inicia el flujo de trabajo. La tarea aparece en el mosaico **Tareas**.

## Flujo de trabajo Solicitar lanzamiento {#request-launch-workflow}

Este flujo de trabajo permite solicitar un lanzamiento.

1. En el proyecto simple, seleccione el signo **+** en el mosaico **Flujos de trabajo** y seleccione **Solicitar flujo de trabajo de lanzamiento**.
1. Introduzca un título para el lanzamiento y proporcione la ruta de origen de este. También puede añadir una descripción y la fecha de lanzamiento, si procede. Seleccione Heredar datos en directo de la página de origen o Excluir páginas secundarias según el comportamiento deseado del lanzamiento.

   ![Solicitar inicio](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Haga clic en **Crear**. Se inicia el flujo de trabajo. El flujo de trabajo aparece en la sección **Flujos de trabajo** lista (haga clic en elipses) **...** en el **Flujos de trabajo** para acceder a esta lista).

## Crear (y traducir) el flujo de trabajo de copia de idioma de los activos {#create-and-translate-language-copy-workflow-for-assets}

Los flujos de trabajo **Crear texto en idiomas** y **Crear y traducir texto en idiomas**[ se tratan detalladamente en la creación de textos de idiomas para los recursos.](/help/assets/translate-assets.md)
