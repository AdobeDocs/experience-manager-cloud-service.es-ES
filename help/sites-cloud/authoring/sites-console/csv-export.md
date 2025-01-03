---
title: Exportar a CSV
description: Exportar información sobre sus páginas a un archivo CSV en su sistema local
exl-id: 818e927e-40b2-4ccb-bfb3-88284ad49829
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 90%

---

# Exportar a CSV   {#export-to-csv}

**Al crear un informe de CSV** puede exportar información sobre las páginas a un archivo CSV en el sistema local.

* El archivo descargado se llama `export.csv`.
* El contenido depende de las propiedades que seleccione.
* Puede definir la ruta de la exportación, así como la profundidad.

>[!NOTE]
>
>Se utiliza la función de descarga (y el destino predeterminado) de su navegador.

El asistente **Crear exportación de CSV** le permite seleccionar:

* Propiedades para exportar
   * Metadatos
      * Nombre
      * Modificado
      * Publicado
      * Plantilla
      * Flujo de trabajo
   * Traducción
      * Traducido
   * Análisis
      * Vistas de la página
      * Visitantes únicos
      * Tiempo empleado en la página
* Profundidad
   * Ruta principal
   * Solo elementos secundarios directos
   * Niveles adicionales de tareas secundarias
   * Niveles

El archivo `export.csv` resultante se puede abrir en Excel o en cualquier otra aplicación compatible.

Para crear una exportación de CSV: 

1. Abra la consola **Sites** y vaya a la ubicación requerida si es necesario.
   * La opción **Crear informe de CSV** está disponible al explorar la consola **Sitios** (en la vista de lista).
   * Es una opción del menú desplegable **Crear**:

     ![Opción Crear CSV](/help/sites-cloud/authoring/assets/csv-create.png)

1. Para abrir el asistente, en la barra de herramientas seleccione **Crear** y, a continuación, **Informe de CSV**:

   ![Opciones de exportación de CSV](/help/sites-cloud/authoring/assets/csv-options.png)

1. Seleccione las propiedades necesarias para exportar.
1. Seleccione **Crear**.
   ![Exportación de CSV resultante en Excel](/help/sites-cloud/authoring/assets/csv-example.png)
