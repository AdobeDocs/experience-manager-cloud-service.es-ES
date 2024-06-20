---
title: Adición de repositorios de Adobe en Cloud Manager
description: Aprenda a crear repositorios administrados por Adobe en Cloud Manager.
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 100%

---

# Adición de repositorios de Adobe en Cloud Manager {#adobe-repositories}

Aprenda a crear repositorios administrados por Adobe en Cloud Manager.

## Adición de un repositorio administrado por Adobe {#add-adobe-repository}

La ventana **Repositorios** facilita la adición de repositorios adicionales administrados por Adobe a su programa.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En la página **Información general del programa**, seleccione la pestaña **Repositorios** para pasar a la página **Repositorios**.

1. Haga clic en **Añadir repositorio** en la barra de herramientas.

   ![Botón Agregar repositorio](assets/add-repository.png)

1. Introduzca el nombre y la descripción como se solicita y haga clic en **Guardar**.

   ![Cuadro de diálogo Agregar repositorio](assets/add-adobe-repository.png)

Cuando se cierra el asistente, el nuevo repositorio se muestra en la tabla de la ventana **Repositorios**. Ahora puede asociar una [CI/CD Pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) con este o administrarlo dentro de la ventana [**Repositorios**.](managing-repositories.md)

>[!TIP]
>
>También puede añadir repositorios de GitHub que administre usted mismo como [repositorios privados.](private-repositories.md)
