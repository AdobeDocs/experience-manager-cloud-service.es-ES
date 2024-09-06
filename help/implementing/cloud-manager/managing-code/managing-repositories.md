---
title: Administración de repositorios en Cloud Manager
description: Obtenga información sobre cómo crear, ver y eliminar repositorios de Git en Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 92%

---


# Administración de repositorios en Cloud Manager {#managing-repos}

Obtenga información sobre cómo crear, ver y eliminar repositorios de Git en Cloud Manager.

## Información general {#overview}

Los repositorios se utilizan para almacenar y administrar el código del proyecto mediante Git. Cada programa que cree en Cloud Manager tiene un repositorio administrado por Adobe creado para él.

Puede elegir crear repositorios adicionales administrados por Adobe y también añadir sus propios repositorios privados. Todos los repositorios asociados con su programa se pueden ver en la ventana **Repositorios**.

Los repositorios creados en Cloud Manager también estarán disponibles para su selección al añadir o editar canalizaciones. Consulte [Canalizaciones de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información.

Hay un único repositorio principal o una rama para una canalización determinada. La [compatibilidad con los submódulos de Git](git-submodules.md) permite incluir muchas ramas secundarias en el momento de la compilación.

## Ventana Repositorios {#repositories-window}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En la página **Información general del programa**, seleccione la pestaña **Repositorios** para pasar a la página **Repositorios**.

1. La ventana **Repositorios** muestra todos los repositorios asociados con su programa.

   ![Ventana Repositorios](assets/repositories.png)

La ventana **Repositorios** proporciona detalles sobre los repositorios:

* El tipo de repositorio
   * **Adobe** indica repositorios administrados por Adobe
   * **GitHub** indica los repositorios de GitHub que se administran
* Cuándo se creó
* Canalizaciones asociadas con el repositorio

Puede seleccionar el repositorio en la ventana y hacer clic en el botón de puntos suspensivos para realizar una acción en el repositorio seleccionado.

* **[Comprobar ramas / Crear proyecto](#check-branches)** (solo disponible para repositorios de Adobe)
* **[Copiar URL del repositorio](#copy-url)**
* **[Ver y actualizar](#view-update)**
* **[Eliminar](#delete)**

![Acciones de repositorio](assets/repository-actions.png)

## Adición de repositorios {#adding-repositories}

Pulse o haga clic en el botón **Añadir repositorio** de la ventana **Repositorios** para iniciar el asistente **Añadir repositorio**.

![Asistente para la adición de repositorios](assets/add-repository-wizard.png)

Cloud Manager admite ambos repositorios administrados por Adobe (**Repositorio de Adobe**), así como sus propios repositorios autoadministrados (**Repositorio privado**). Los campos obligatorios difieren según el tipo de repositorio que decida añadir. Consulte los siguientes documentos para obtener más información.

* [Adición de repositorios de Adobe en Cloud Manager](adobe-repositories.md)
* [Adición de repositorios privados en Cloud Manager](private-repositories.md)

>[!NOTE]
>
>* Un usuario debe tener la función **Administrador de implementación** o **Propietario empresarial** para poder añadir un repositorio.
>* Hay un límite de 300 repositorios en todos los programas de cualquier compañía u organización de IMS.

## Acceder a la info del repositorio {#repo-info}

Al ver los repositorios en la ventana **Repositorios**, puede ver los detalles sobre cómo acceder mediante programación a los repositorios administrados por Adobe haciendo clic en el botón **Acceder a la info del repositorio** de la barra de herramientas.

![Información del repositorio](assets/repo-info.png)

La ventana **Información del repositorio** se abre con los detalles. Para obtener más información sobre el acceso a la información del repositorio, consulte el documento [Acceso a la información del repositorio](accessing-repos.md).

## Comprobar ramas/Crear proyecto {#check-branches}

La acción **Comprobar ramas/Crear proyecto** realiza dos funciones según el estado del repositorio.

* Si el repositorio es de nueva creación, la acción crea un proyecto de ejemplo basado en [el tipo de archivo del proyecto de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/developing/archetype/overview).
* Si al repositorio ya se le ha creado el proyecto de muestra, compruebe el estado del repositorio y sus ramas e informes de nuevo si el proyecto de muestra ya existe.

![Acción Comprobar ramas](assets/check-branches.png)

## Copiar la URL del repositorio {#copy-url}

La acción **Copiar la URL del repositorio** copia la URL del repositorio seleccionado en la ventana **Repositorios** en el portapapeles para utilizarla en otra parte.

## Ver y actualizar {#view-update}

La acción **Ver y actualizar** abre el cuadro de diálogo **Actualizar repositorio**. Con esta acción puede ver el **Nombre** y la **Vista previa de la URL del repositorio**, así como actualizar la **Descripción** del repositorio.

![Ver y actualizar la información del repositorio](assets/view-update.png)

## Eliminar {#delete}

La acción **Eliminar** elimina el repositorio del proyecto. Un repositorio no se puede eliminar si está asociado con una canalización.

![Eliminar](assets/delete.png)

Al eliminar un repositorio:

* Se impide que el nombre del repositorio eliminado se pueda utilizar para nuevos repositorios que se puedan crear en el futuro.
   * El mensaje de error `Repository name should be unique within organization.` aparece en estos casos.
* Se hace que el repositorio eliminado no esté disponible en Cloud Manager y no esté disponible para vincularlo a una canalización.
