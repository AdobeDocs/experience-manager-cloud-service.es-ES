---
title: Editar programas
description: Obtenga información sobre cómo editar los programas de producción y de zonas protegidas para ajustar sus opciones después de crearlas.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 50%

---

# Editar programas {#editing-programs}

Los usuarios con los permisos necesarios pueden editar [programas de producción creados en su organización](creating-production-programs.md) y [programas de zona protegida creados en su organización.](creating-sandbox-programs.md) Al editar un programa, puede:

* Agregar la solución Sites a un programa existente con Assets y a la inversa.
* Eliminar Sites o Assets de un programa existente que incluya ambos.
* Agregue un segundo derecho de solución no utilizado a un programa existente o como nuevo programa.
* Eliminar programas de zona protegida.

## Permisos {#permissions}

Debe ser miembro de la función **Propietario empresarial** para editar programas o eliminar programas de zona protegida.

## Edición de un programa {#editing}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa que desea editar para mostrar sus detalles.

1. Haga clic en el nombre del programa en la parte superior izquierda de la página y seleccione **Editar programa**.

   ![Opción Editar programa](assets/edit-program-overview.png)

1. Se abrirá la página **Editar programa**. En la pestaña **General**, edite el nombre y la descripción del programa.

   * Debe seleccionar al menos una solución para un programa.

   ![Pestaña General](assets/edit-program-prod1.png)

1. En la pestaña **Soluciones y complementos**, modifique las soluciones para el programa.

   ![Seleccionar soluciones](assets/edit-prg.png)

1. Haga clic en las comillas angulares antes del nombre de la solución para mostrar complementos opcionales, como seleccionar la opción **Comercio** opción de complemento en **Sites**.

   ![Editar complementos](assets/edit-program-add-on.png)

1. En la pestaña **Configuración de Go live**, modifique la fecha de go-live planeada para el programa.

   ![Editar la configuración de go-live](assets/edit-program-go-live.png)

   * Esta fecha es solo para uso informativo. Almacena en déclencheur el widget Go Live en la página de información general del programa. A su vez, proporciona vínculos internos del producto a la documentación de prácticas recomendadas as a Cloud Service de Adobe Experience Manager AEM () para que se ajuste a su recorrido, lo que culmina en una experiencia de Go Live exitosa.
   * Esta pestaña no está disponible para programas de zonas protegidas.

1. Clic **Actualizar** para guardar los cambios en el programa.

Cada vez que se edita un programa, incluida la adición o eliminación de una solución o complemento, esos cambios surten efecto después de la siguiente implementación.

Si el programa de producción tiene habilitada la seguridad mejorada, aparece la pestaña adicional **Seguridad mejorada** en la ventana **Editar programa** para confirmar que la funcionalidad está activa para el programa.

![Seguridad mejorada activa para un programa](assets/edit-program-enhanced.png)

No puede editar esta configuración después de crear el programa. Para obtener más información sobre la opción de seguridad mejorada, consulte [Creación de programas de producción](creating-production-programs.md).

## Eliminar programas de zona protegida {#delete-sandbox-program}

Al eliminar un programa de zona protegida se eliminan todos los entornos y canalizaciones asociados a él.

>[!TIP]
>
>Los usuarios con el rol de **Propietario del negocio** o **Administrador de implementación** pueden eliminar sus entornos de producción y ensayo en lugar de todo el programa de zona protegida.

Para eliminar un programa de zona protegida, haga lo siguiente.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa que desea editar para mostrar sus detalles.

1. Haga clic en el nombre del programa en la parte superior izquierda de la página y seleccione **Eliminar programa**.

   ![Opción Eliminar programa](assets/delete-sandbox1.png)

También puede hacer clic en el botón de los tres puntos de la tarjeta del programa desde la página de información general de Cloud Manager y seleccionar **Eliminar programa**.

![Eliminar zona protegida de la tarjeta de programa](assets/delete-sandbox2.png)

>[!NOTE]
>
>Solo se pueden eliminar programas de zona protegida. Los programas de producción no se pueden eliminar.
