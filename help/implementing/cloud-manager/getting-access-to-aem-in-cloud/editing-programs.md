---
title: Edición de programas
description: Obtenga información sobre cómo editar los programas de producción y de simulación de pruebas para ajustar sus opciones después de crearlas.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Edición de programas {#editing-programs}

Los usuarios con los permisos necesarios pueden editar [programas de producción creados en su organización](creating-production-programs.md) así como [programas de simulación de pruebas creados en su organización.](creating-sandbox-programs.md) Al editar un programa puede:

* Agregar la solución Sitios a un programa existente con Assets y viceversa.
* Elimine Sitios o Recursos de un programa existente con Sitios y Recursos.
* Agregue un segundo derecho de solución no utilizado a un programa existente o como un nuevo programa.
* Eliminar programas de simulación de pruebas.

>[!NOTE]
>
>Debe ser miembro de **Propietario empresarial** para editar programas o eliminar programas de espacio aislado.

Siga estos pasos para editar un programa.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa que desea editar para mostrar sus detalles.

1. Haga clic en el nombre del programa en la parte superior izquierda de la página y seleccione **Editar programa**.

   ![Opción Editar programa](assets/edit-program-overview.png)

1. La variable **Editar programa** muestra dos fichas: **General** y **Soluciones y complementos**. Seleccione el **General** para editar el nombre y la descripción del programa.

   * Se debe seleccionar al menos una solución para un programa.

   ![Ficha General](assets/edit-program-prod1.png)

1. Seleccione el **Soluciones y complementos** para modificar las soluciones del programa.

   ![Seleccionar soluciones](assets/edit-prg.png)

1. Haga clic en el elemento adicional antes de los nombres de las soluciones para mostrar complementos opcionales, como seleccionar la variable **Comercio** opción de complemento en **Sitios**.

   ![Editar complementos](assets/edit-program-add-on.png)

1. Haga clic en **Actualizar** para guardar los cambios en el programa.

Una vez realizadas las actualizaciones, si las soluciones seleccionadas han cambiado, esos cambios surtirán efecto después de la siguiente implementación.

## Eliminación de programas del Simulador para pruebas {#delete-sandbox-program}

Al eliminar un programa de simulación de pruebas se eliminarán todos los entornos y canalizaciones asociados a él.

>[!TIP]
>
>Los usuarios con la variable **Propietario empresarial** o **Administrador de implementación** las funciones de pueden eliminar sus entornos de producción y ensayo en lugar de todo el programa de simulación de pruebas.

Siga estos pasos para eliminar un programa de simulación de pruebas.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa que desea editar para mostrar sus detalles.

1. Haga clic en el nombre del programa en la parte superior izquierda de la página y seleccione **Eliminar programa**.

   ![Opción Eliminar programa](assets/delete-sandbox1.png)

También puede hacer clic en el botón de puntos suspensivos de la tarjeta del programa desde la página de información general de Cloud Manager y seleccionar **Eliminar programa**.

![Eliminar entorno limitado de la tarjeta de programa](assets/delete-sandbox2.png)

>[!NOTE]
>
>Solo se pueden eliminar programas de simulación de pruebas. Los programas de producción no se pueden eliminar.
