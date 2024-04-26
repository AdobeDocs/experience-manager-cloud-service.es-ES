---
title: Editar programas
description: Obtenga información sobre cómo editar los programas de producción y de zonas protegidas para ajustar sus opciones después de crearlas.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 401f853b197e67a6c54e4bf168081dc8165bd505
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 30%

---


# Editar programas {#editing-programs}

Para administrar y editar programas, comience por la [**Mis programas** consola.](/help/implementing/cloud-manager/navigation.md) El **Mis programas** Esta página proporciona información general de todos los programas a los que tiene acceso. Al seleccionar un programa individual, la variable **Resumen del programa** Esta página proporciona detalles del programa de un vistazo.

Desde el **Resumen del programa**, los usuarios con los permisos necesarios pueden editar [programas de producción creados en su organización](creating-production-programs.md) y [programas de zona protegida creados en su organización.](creating-sandbox-programs.md) Al editar un programa, puede:

* Agregar la solución Sites a un programa existente con Assets y a la inversa.
* Eliminar Sites o Assets de un programa existente que incluya ambos.
* Agregue un segundo derecho de solución no utilizado a un programa existente o como nuevo programa.
* Eliminar programas de zona protegida.

## Permisos {#permissions}

Debe ser miembro de la **Propietario del negocio** función para editar programas o eliminar programas de zona protegida, así como para acceder al Tablero de licencias.

## Edición de un programa {#editing}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En el **[Mis programas](#my-programs)** , haga clic en el programa que desee editar para mostrar sus detalles.

1. Haga clic en el nombre del programa en la parte superior izquierda de la página y seleccione **Editar programa**.

   ![Opción Editar programa](assets/edit-program-overview.png)

1. El **Editar programa** página se abre para la **General** pestaña.

   ![Pestaña General](assets/edit-program-prod1.png)

1. Las opciones disponibles para editar el programa son las mismas que al crearlo.
   * Consulte los documentos [Creación de programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) y [Creación de programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) para obtener más información sobre las opciones individuales.
   * [Opciones adicionales](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) puede estar disponible para su programa de producción en función de los derechos de su organización.

1. Clic **Actualizar** para guardar los cambios en el programa.

Se guardarán los cambios realizados en el programa.

>[!NOTE]
>
>Cada vez que se edita un programa, incluida la adición o eliminación de una solución o complemento, esos cambios surten efecto después de la siguiente implementación.

## Eliminar programas de zona protegida {#delete-sandbox-program}

Al eliminar un programa de zona protegida se eliminan todos los entornos y canalizaciones asociados a él.

>[!TIP]
>
>Los usuarios con el rol de **Propietario del negocio** o **Administrador de implementación** pueden eliminar sus entornos de producción y ensayo en lugar de todo el programa de zona protegida.

Para eliminar un programa de zona protegida, haga lo siguiente.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En el **[Mis programas](#my-programs)** , haga clic en el programa que desee editar para mostrar sus detalles.

1. Haga clic en el nombre del programa en la parte superior izquierda de la página y seleccione **Eliminar programa**.

   ![Opción Eliminar programa](assets/delete-sandbox1.png)

También puede hacer clic en el botón de los tres puntos de la tarjeta del programa desde la página de información general de Cloud Manager y seleccionar **Eliminar programa**.

![Eliminar zona protegida de la tarjeta de programa](assets/delete-sandbox2.png)

>[!NOTE]
>
>Solo se pueden eliminar programas de zona protegida. Los programas de producción no se pueden eliminar.
