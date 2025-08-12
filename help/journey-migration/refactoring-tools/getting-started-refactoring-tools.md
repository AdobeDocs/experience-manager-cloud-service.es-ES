---
title: Introducción a las herramientas de refactorización
description: Obtenga información sobre cómo empezar a utilizar las herramientas de refactorización en AEM as a Cloud Service
exl-id: 84394bdd-2b92-4f5d-b08a-7dc2c681baa4
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 4%

---

# Introducción a las herramientas de refactorización {#getting-started-refactoring-tools}

## Disponibilidad {#availability}

<!-- Alexandru: duplicate contextualhelp id, drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_rs_upload"
>title="Download"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=es" text="Release Notes"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution Portal"

-->

## Ejecución de las herramientas de refactorización {#running-refactoring-tools}

Utilice la herramienta de refactorización para migrar el código para comprobar la compatibilidad con AEM as a Cloud Service.

1. Si todavía no ha creado un proyecto CAM, consulte [Creación y administración de un proyecto en CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md#create-project).
1. Haga clic en la tarjeta **Refactorización de código** para cargar el código fuente.

   ![imagen](/help/journey-migration/refactoring-tools/assets/rscam1.png)

1. Cuando acceda por primera vez a la **Vista de código Source**, verá un estado vacío que le pedirá que cargue el código fuente.

   ![imagen](/help/journey-migration/refactoring-tools/assets/rscam2.png)

## Cargando código Source {#uploading}

Cuando los clientes acceden por primera vez a **Herramientas de refactorización**, aparecen con un estado vacío en la **Vista de código de Source**. Siga los pasos a continuación para cargar el proyecto e iniciar el proceso de inspección:

1. **Acceder a la página de carga del proyecto**\
   Haga clic en el botón **Cargar proyecto** en el estado vacío para iniciar el proceso de carga.

   ![imagen](/help/journey-migration/refactoring-tools/assets/rscam3.png)

1. **Cargue Su Código Source**
   - En el cuadro de diálogo de carga, seleccione el archivo ZIP del código fuente.
   - Haga clic en **Cargar** para comenzar.
   - El progreso de carga se mostrará en el cuadro de diálogo. La duración depende del tamaño del proyecto.

   ![imagen](/help/journey-migration/refactoring-tools/assets/rscam4.png)

1. **Proceso de inspección**
   - Después de la carga, el **proceso de inspección** se inicia automáticamente en segundo plano.
   - La **vista de código Source** ahora mostrará el proyecto cargado y su estado de inspección.

1. **Estado de la inspección** El proceso de inspección está diseñado para simplificar la ejecución de las herramientas de refactorización al reducir la sobrecarga de las configuraciones manuales.

   La inspección mostrará uno de los siguientes estados:
   - **En ejecución**: la inspección está en curso.
   - **Listo**: la inspección se ha completado. Ahora puede ejecutar herramientas de refactorización.
   - **Error**: se produjo un error. Haga clic en el proyecto para revisar el informe de inspección y resolver cualquier problema.

   ![imagen](/help/journey-migration/refactoring-tools/assets/rscam5.png)

>[!NOTE]
>
>Si se carga un proyecto nuevo, se eliminará el existente. Asegúrese de guardar los datos necesarios antes de continuar.

>[!NOTE]
>
>Los trabajos de refactorización solo se pueden ejecutar si la carga del código fuente se realiza correctamente.

## Trabajos de refactorización {#refactoring-jobs}

Al hacer clic en la ficha **Trabajo de refactorización**, verá una lista de los trabajos existentes. Si todavía no se han creado trabajos, se mostrará un estado vacío solicitando la creación del trabajo.

![imagen](/help/journey-migration/refactoring-tools/assets/rscam6.png)

### &#x200B;1. Crear un nuevo trabajo de refactorización

- Haga clic en el botón **Crear nuevo trabajo**.
- Seleccione las herramientas de refactorización que desee.
- Haga clic en **Iniciar** para iniciar el proceso de refactorización.

![imagen](/help/journey-migration/refactoring-tools/assets/rscam7.png)

>[!NOTE]
>
>Puede almacenar en déclencheur trabajos de refactorización individuales o ejecutar todas las herramientas disponibles de una sola vez mediante la opción **Todas las herramientas juntas**.

### &#x200B;2. Estado del puesto

- **En ejecución**: el trabajo está en curso. El estado se actualiza automáticamente tras la finalización o el error.
- **Completado** - El trabajo finalizó correctamente. Ahora puede revisar los resultados o descargar el código refactorizado.
- **Error** - El trabajo encontró un error. Haga clic en el trabajo para ver los registros detallados y solucionar el problema.

![imagen](/help/journey-migration/refactoring-tools/assets/rscam8.png)

Cuando el trabajo se complete correctamente, el botón **Descargar** estará disponible, lo que le permitirá recuperar:

- **El proyecto refactorizado**: este es el código actualizado después de aplicar la transformación. Los clientes pueden descargar el código más reciente para su proyecto.
- **Registros de actividades**: durante la ejecución del trabajo, todos los pasos realizados por la herramienta y los cambios realizados se registran como parte de este proceso.
- **Informe de conclusiones**: este informe contiene elementos que la herramienta no ejecutó por completo, pero que aún deben solucionarse. Todos estos cambios se registran aquí.

![imagen](/help/journey-migration/refactoring-tools/assets/rscam9.png)

>[!NOTE]
>
>Cada trabajo puede tardar hasta 1 hora en completarse. Si el estado no se actualiza, póngase en contacto con el Soporte técnico de Adobe.
