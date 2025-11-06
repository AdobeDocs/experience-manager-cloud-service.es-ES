---
title: Adición de un repositorio de Adobe en Cloud Manager
description: Aprenda a añadir un repositorio administrado por Adobe en Cloud Manager.
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 100%

---

# Adición de un repositorio de Adobe en Cloud Manager {#adobe-repositories}

Aprenda a añadir un repositorio administrado por Adobe en Cloud Manager.

La página **Repositorios** facilita la adición de repositorios adicionales administrados por Adobe al programa seleccionado.

**Para añadir un repositorio de Adobe en Cloud Manager:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados al que desea añadir un repositorio administrado por Adobe.

1. En la página **Resumen del programa**, en el menú lateral, haga clic en la pestaña ![icono de carpeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Repositorios**.

1. En la página **Repositorios**, junto a la esquina superior derecha, haga clic en **Agregar repositorio**.

   ![Botón Añadir repositorio](assets/add-repository.png)

1. En el cuadro de diálogo **Agregar repositorio**, asegúrese de que **Repositorio de Adobe** está seleccionado como tipo de repositorio.

1. En los campos de texto correspondientes, introduzca lo siguiente:

   * **Nombre del repositorio**: un nombre expresivo para el nuevo repositorio.
   * **Vista previa de la URL del repositorio**: no es necesario que escriba una ruta de URL ni que edite la ruta existente porque la infraestructura del repositorio ya está configurada y está totalmente integrada y administrada por Adobe.
   * **Descripción (opcional)**: una descripción detallada del repositorio.

   ![Cuadro de diálogo Agregar repositorio](assets/add-adobe-repository.png)

1. Haga clic en **Guardar**.
El nuevo repositorio se muestra en la tabla de la página **Repositorios**.

Ahora puede asociar una [Canalización de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) con él o administrarlo dentro de la página [**Repositorios**](managing-repositories.md).

>[!TIP]
>
>También puede añadir repositorios de GitHub que administre usted mismo como [repositorios privados](private-repositories.md).
