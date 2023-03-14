---
title: Compatibilidad con notas al pie
description: Compatibilidad con RTE para notas al pie.
source-git-commit: 3d713304512065819ed16bbc9604f2cf9d1cf43f
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Componente Nota al pie {#footnotecomponent}

**[!UICONTROL Nota al pie]** es el bit adicional de información o notas que aparecen al final de la página. [!UICONTROL Nota al pie] comprende las notas que se indican en el texto con números como superíndice.

Las notas al pie se numeran secuencialmente en el orden en que aparecen en la página. Cada nota al pie tiene un número único como superíndice que corresponde al número que se coloca en la parte inferior de la página. Junto al número, aparece la información complementaria como descripción de nota al pie.

![Descripción de nota al pie](/help/forms/assets/footnote_description.png)


## Uso de la nota al pie {#usesoffootnotes}

* Ayuda a proporcionar citas.
* Proporciona información adicional que puede interrumpir el flujo normal de la información principal.
* Proporciona información entre paréntesis o permisos de copyright.

En Forms adaptable, [!UICONTROL nota al pie de página] se utiliza para mostrar la información sobre cómo completar o utilizar el formulario. Para obtener información sobre cómo crear un Forms adaptable, consulte [Creación de un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Nota al pie en Forms adaptable {#using-footnote-adaptiveforms}

Para añadir una nota al pie en un Forms adaptable, realice los siguientes pasos:
1. Abra un formulario adaptable en **Editar** modo.
1. Desde el explorador de componentes, arrastre y suelte el **[!UICONTROL Texto]** en el formulario adaptable.
1. Seleccione el **[!UICONTROL Texto]** componente que ha añadido y pulse ![cmppr](assets/configure-icon.svg) para editar sus propiedades.

   ![Nota al pie en Forms adaptable](/help/forms/assets/footnote_rte.png)

1. Seleccione el texto para el que desea agregar una descripción de nota al pie y haga clic en  ![estrella](/help/forms/assets/asterisk.svg) para aplicar estilo al **[!UICONTROL Nota al pie]** componente.

1. Clic ![check](/help/forms/assets/save_icon.svg) para guardar los cambios y estilos.

   >[!NOTE]
   >
   >* Las notas al pie se numeran automáticamente y aparecen de la manera en que se crean en el formulario adaptable.
   >* Si hay notas al pie duplicadas, la numeración es la misma para todas las notas al pie duplicadas.


1. Desde el explorador de componentes, arrastre y suelte el **[!UICONTROL Marcador de nota]** en el formulario adaptable.
   >[!NOTE]
   >
   >* En la instancia de publicación, las notas al pie se muestran en la posición donde **[!UICONTROL Marcador de nota]** se coloca en el formulario adaptable.
   >* Cuando navega entre diferentes paneles, solo aparecen notas al pie visibles en la **[!UICONTROL Marcador de nota]** que están presentes en el panel navegado.


1. Guarde las propiedades.

Durante el tiempo de ejecución, el número aparece en el texto como un superíndice y su descripción correspondiente aparece en la variable **[!UICONTROL Nota al pie]** componente en la posición donde [!UICONTROL Marcador de nota] se coloca en el formulario adaptable. Puede ir directamente a la descripción de la nota al pie de página haciendo clic en su número correspondiente en la [!UICONTROL Nota al pie].