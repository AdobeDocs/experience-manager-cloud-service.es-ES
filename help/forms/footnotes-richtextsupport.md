---
title: Compatibilidad con notas al pie
description: Compatibilidad con RTE para notas a pie de página.
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Componente de nota al pie {#footnotecomponent}

**[!UICONTROL Nota al pie]** es el bit adicional de información o notas que aparecen al final de la página. [!UICONTROL Nota al pie] comprende las notas que se indican en el texto con números como superíndice.

Las notas a pie de página se numeran secuencialmente en el orden en que aparecen en la página. Cada nota al pie tiene un número único como superíndice que corresponde al número que se coloca en la parte inferior de la página. Junto al número aparece la información complementaria como una descripción de la nota a pie de página.

![Descripción de la nota al pie](/help/forms/assets/footnote_description.png)


## Uso de la nota a pie de página {#usesoffootnotes}

* Ayuda a proporcionar citas.
* Proporciona información adicional que puede interrumpir el flujo normal de la información principal.
* Proporciona información paréntesis o permisos de copyright.

En Forms adaptable, [!UICONTROL nota al pie] se utiliza para mostrar la información sobre cómo rellenar o utilizar el formulario. Para obtener información sobre cómo crear un Forms adaptable, consulte [Creación de un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Nota al pie de página en Forms adaptable {#using-footnote-adaptiveforms}

Para agregar una nota al pie en Forms adaptable, realice los siguientes pasos:
1. Abra un formulario adaptable en **Editar** en el menú contextual.
1. Desde el navegador de componentes, arrastre y suelte el **[!UICONTROL Texto]** en el formulario adaptable.
1. Seleccione el **[!UICONTROL Texto]** componente que ha añadido y tocado ![cmppr](assets/configure-icon.svg) para editar sus propiedades.

   ![Nota al pie de página en Forms adaptable](/help/forms/assets/footnote_rte.png)

1. Seleccione el texto para el que desea agregar una descripción de nota al pie de página y haga clic en  ![star](/help/forms/assets/asterisk.svg) para aplicar estilo al **[!UICONTROL Nota al pie]** componente.

1. Haga clic en ![check](/help/forms/assets/save_icon.svg) para guardar los cambios y estilos.

   >[!NOTE]
   >
   >* Las notas de pie de página se numeran automáticamente y aparecen de la forma en que se crean en el formulario adaptable.
   >* Si hay notas al pie duplicadas, la numeración es la misma para todas las notas al pie duplicadas.


1. Desde el navegador de componentes, arrastre y suelte el **[!UICONTROL Marcador de posición de pie de página]** en el formulario adaptable.
   >[!NOTE]
   >
   >* En la instancia de publicación, las notas al pie se muestran en la posición en la que **[!UICONTROL Marcador de posición de pie de página]** se coloca en el formulario adaptable.
   >* Cuando navega entre paneles diferentes, solo aparecen notas al pie visibles en la variable **[!UICONTROL Marcador de posición de pie de página]** que están presentes en el panel navegado.


1. Guarde las propiedades.

Durante el tiempo de ejecución, el número aparece en el texto como superíndice y su descripción correspondiente aparece en la variable **[!UICONTROL Nota al pie]** en la posición donde [!UICONTROL Marcador de posición de pie de página] se coloca en el formulario adaptable. Puede navegar directamente a la descripción de la nota al pie haciendo clic en su número correspondiente en el [!UICONTROL Nota al pie].