---
title: Cómo agregar una nota al pie a un formulario adaptable
description: Utilizar el editor de texto enriquecido (RTE) para notas al pie de página en un formulario adaptable.
feature: Adaptive Forms, Foundation Components
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
role: User, Developer
source-git-commit: 76301ca614ae2256f5f8b00c41399298c761ee33
workflow-type: ht
source-wordcount: '429'
ht-degree: 100%

---

# Componente Nota al pie {#footnotecomponent}

>[!NOTE]
>
> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear nuevos formularios adaptables](/help/forms/creating-adaptive-form-core-components.md) o [adición de formularios adaptables a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear formularios adaptables con componentes de base.

La **[!UICONTROL Nota al pie]** es el extra de información o nota que aparece al final de la página. [!UICONTROL Nota al pie] comprende las notas que se indican en el texto con números como superíndice.

Las notas al pie se numeran secuencialmente en el orden en que aparecen en la página. Cada nota al pie tiene un número único como superíndice que corresponde al número que se coloca en la parte inferior de la página. Junto al número, aparece la información complementaria como descripción de la nota al pie.

![Descripción de la nota al pie](/help/forms/assets/footnote_description.png)


## Uso de la nota al pie {#usesoffootnotes}

* Ayuda a citar.
* Proporciona información adicional que puede interrumpir el flujo normal de la principal.
* Proporciona información entre paréntesis o permisos de copyright.

En formularios adaptables, la [!UICONTROL nota al pie] sirve para mostrar información sobre cómo completar o utilizar el formulario. Para obtener información sobre cómo crear un formulario adaptable, consulte [Creación de un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=es).

## Nota al pie en formularios adaptables {#using-footnote-adaptiveforms}

Para añadir una nota al pie en un formulario adaptable, siga estos pasos:
1. Abra un formulario adaptable en el modo **Edición**.
1. Desde el explorador de componentes, arrastre y suelte el componente **[!UICONTROL Texto]** en el formulario adaptable.
1. Seleccione el componente **[!UICONTROL Texto]** que ha añadido y seleccione ![cmppr](assets/configure-icon.svg) para editar sus propiedades.

   ![Nota al pie en formularios adaptables](/help/forms/assets/footnote_rte.png)

1. Seleccione el texto para el que desea agregar una descripción de nota al pie y haga clic en el botón de  ![estrella](/help/forms/assets/asterisk.svg) para aplicar estilo al componente **[!UICONTROL Nota al pie]**.

1. Haga clic en la ![verificación](/help/forms/assets/save_icon.svg) para guardar los cambios y estilos.

   >[!NOTE]
   >
   >* Las notas al pie se numeran automáticamente y aparecen de la manera en que se crean en el formulario adaptable.
   >* Si hay notas al pie duplicadas, la numeración es la misma para todas.

1. Desde el explorador de componentes, arrastre y suelte el componente **[!UICONTROL Marcador de nota al pie]** en el formulario adaptable.

   >[!NOTE]
   >
   >* En la instancia de publicación, las notas al pie se muestran en la posición en la que se coloca el componente **[!UICONTROL Marcador de nota al pie]** en el formulario adaptable.
   >* Cuando navega entre diferentes paneles, solo aparecen notas al pie visibles en el **[!UICONTROL Marcador de nota al pie]** que está presente en el panel por el que navega.

1. Guarde las propiedades.

Durante el tiempo de ejecución, el número aparece en el texto como un superíndice y su descripción correspondiente aparece en el componente **[!UICONTROL Nota al pie]** en la posición donde [!UICONTROL Marcador de nota al pie] está colocado en el formulario adaptable. Puede ir directamente a la descripción de la nota al pie haciendo clic en su número correspondiente en la [!UICONTROL Nota al pie].


## Ver también {#see-also}

{{see-also}}