---
title: 'Edición de las propiedades de página  '
description: Obtenga información sobre cómo editar las propiedades de una página y cambiar el comportamiento de la página y cómo se administra.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 8fee7e24-bbaa-4cc4-a047-165c9f2cd973
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 24%

---

# Edición de las propiedades de página   {#page-properties}

Obtenga información sobre cómo editar [las propiedades de una página](/help/sites-cloud/authoring/sites-console/page-properties.md) y cambiar el comportamiento de la página y cómo se administra.

>[!TIP]
>
>Para obtener detalles sobre las propiedades de página individuales disponibles, consulte el documento [Propiedades de página.](/help/sites-cloud/authoring/sites-console/page-properties.md)

## Dónde editar propiedades de página {#where}

Puede editar las propiedades de página desde varios lugares de AEM.

* [Desde el &#x200B;](#from-the-sites-console)
* [Desde el editor de páginas](#from-the-page-editor)
* [Desde el editor universal](#from-the-universal-editor)

Con la consola Sitios también puede [editar las propiedades de varias páginas a la vez.](#editing-multiple-pages)

### Desde la consola Sitios {#from-the-sites-console}

Al examinar el contenido en la consola **Sitios**, puede usar el botón **Propiedades** de la barra de herramientas para editar las propiedades de la página:

1. Con la consola [**Sitios**,](/help/sites-cloud/authoring/sites-console/introduction.md) vaya a la ubicación de la página para la que desea ver y editar las propiedades.
1. Seleccione la opción **Propiedades** de la página requerida mediante:
   * [Acciones rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-cloud/authoring/basic-handling.md#selecting-resources)
   * Las propiedades de página se muestran mediante las pestañas adecuadas.
1. Visualice o edite las propiedades según sea oportuno. 
1. A continuación, utilice **Guardar** para guardar las actualizaciones, seguido de **Cerrar** para volver a la consola.

### Desde el editor de páginas {#from-the-page-editor}

Al editar una página con el Editor de páginas, puede usar **Información de la página** para definir las propiedades de la página:

1. En el [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md), abra la página para la que desee editar las propiedades.
1. Seleccione el icono **Información de página** para abrir el menú de selección:
1. Seleccione **Abrir propiedades** y se abrirá un cuadro de diálogo que le permitirá editar las propiedades, ordenadas por la pestaña correspondiente. Los siguientes botones están disponibles en la parte derecha de la barra de herramientas:
   * **Cancelar**
   * **Guardar y cerrar**
1. Utilice el botón **Guardar y cerrar** para guardar los cambios. 

## Desde el editor universal {#from-the-universal-editor}

Al editar una página con el Editor universal, puede usar el icono **Propiedades de página** para editar las propiedades:

1. En el [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties), abra la página para la que desea editar las propiedades.
1. Seleccione el icono **Propiedades de página** en la barra de herramientas.
1. La ventana de propiedades de página de AEM se abre en una nueva pestaña del explorador, como si estuviera editando propiedades de página desde el [Editor de páginas.](#from-the-page-editor) Los siguientes botones están disponibles a la derecha de la barra de herramientas:
   * **Cancelar**
   * **Guardar y cerrar**
1. Utilice el botón **Guardar y cerrar** para guardar los cambios. 
1. Vuelva a la pestaña del explorador del Editor universal.

## Edición de las propiedades de varias páginas {#editing-multiple-pages}

Desde la consola [**Sitios**](/help/sites-cloud/authoring/sites-console/introduction.md) puede seleccionar varias páginas y luego usar **Ver propiedades** para ver o editar las propiedades de la página. Esto se conoce como edición masiva de propiedades de página.

Puede seleccionar varias páginas para editarlas por lotes mediante varios métodos, entre ellos:

* Al examinar la consola **Sites**
* Después de usar **Buscar** para localizar un conjunto de páginas

Después de seleccionar las páginas y hacer clic o pulsar la opción **Propiedades**, se muestran las propiedades por lotes:

![Propiedades de la página de edición masivas](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Solo se pueden editar por lotes las siguientes páginas:

* Las que compartan el mismo tipo de recurso.
* No forman parte de una Live Copy
   * Si alguna de las páginas seleccionadas forma parte de una Live Copy, se muestra un mensaje cuando se abren las propiedades.

La ventana de edición en bloque se divide en dos:

* A la izquierda se muestra una lista de las páginas seleccionadas para la edición por lotes.

   * Puede seleccionar o deseleccionar las páginas según sea necesario.
   * De forma predeterminada, todas están seleccionadas.

* La derecha es una lista de [propiedades disponibles para la edición en lotes.](/help/implementing/developing/extending/bulk-editor.md)

   * Las propiedades se ordenan en pestañas, al igual que cuando se visualizan las propiedades de una página.
   * Se pueden ver las propiedades que están disponibles en todas las páginas seleccionadas (deben haberse marcado específicamente como disponibles para la edición por lotes).
   * Si reduce la selección de páginas a una sola página, se verán todas las propiedades.
   * Solo se muestran las propiedades con un valor común.
   * Cuando el campo tiene varios valores (por ejemplo, Etiquetas), los valores solo se mostrarán si *todos* son comunes. Si solo algunas son comunes, solo se mostrarán al editar.

* Los campos que son comunes en las páginas, pero que tienen diferentes valores, se indican con un valor especial; por ejemplo, el texto `<Mixed Entries>`.

Puede actualizar los valores en los campos disponibles en las páginas seleccionadas. Los nuevos valores se aplicarán a todas las páginas seleccionadas al seleccionar **Listo**. Cuando el campo tiene varios valores (por ejemplo, Etiquetas), puede anexar un nuevo valor o quitar un valor común.

## Herencia de propiedades {#inheritance}

Si la página se basa en un modelo o hereda contenido de otra página, la herencia se refleja en la ventana **Propiedades de página** para el campo individual.

![Propiedades heredadas](assets/property-inhertiance.png)

Las propiedades heredadas no se pueden editar. Toque o haga clic en el icono **Cancelar herencia** junto a un campo en particular para romper su herencia.

![Cancelar herencia](assets/cancel-inheritance.png)

Confirme la cancelación en el modal **Cancelar herencia**.

![Cancelar modal de confirmación de herencia](assets/cancel-inheriance-confirmation.png)

Una vez cancelada la herencia de un campo, se puede editar.

![Herencia cancelada](assets/property-inheritance-broken.png)

Para restablecer la herencia, pulse o haga clic en el icono **Revertir herencia** situado junto al campo.

![Revertir herencia](assets/revert-inheritance.png)

Confirme la reversión en el modal **Revertir herencia**.

![Revertir modal de confirmación de herencia](assets/revert-inhertiance-confirmation.png)

Seleccione **Sincronizar página después de revertir la herencia** para actualizar el campo con los valores más recientes del modelo. Si no lo hace, los valores se actualizarán la próxima vez que se sincronice LiveCopy.

>[!TIP]
>
>Para obtener más información acerca de la herencia, consulte el documento [Administrador de varios sitios y traducción](/help/sites-cloud/administering/msm-and-translation.md)
