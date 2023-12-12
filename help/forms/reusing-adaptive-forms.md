---
title: ¿Cómo reutilizo las propiedades de metadatos de un formulario adaptable?
description: Descubra cómo reutilizar de forma eficaz un formulario adaptable existente para crear uno nuevo.
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
feature: Adaptive Forms, Foundation Components
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: f419883d0e83b5d711e0f594a8e14a8f2133f4b1
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 96%

---

# Reutilización de propiedades de metadatos de un formulario adaptable {#reusing-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/creating-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>


| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/reusing-adaptive-forms.html) |
| AEM as a Cloud Service | Este artículo |

Si desea utilizar algunas de las propiedades de un formulario adaptable existente para generar uno nuevo, puede utilizar simplemente la funcionalidad Copiar y pegar. Además, puede pegar el nuevo formulario adaptable en la ruta de carpeta deseada. Todas las propiedades de metadatos se replican, y también se copian los XFA y XSD de los formularios adaptables basados en XFA y XSD.

>[!NOTE]
>
>El estado y los detalles de la revisión no se copian. Por ejemplo, si el formulario adaptable se publica y, a continuación, lo copia, se cancelará la publicación del formulario adaptable pegado. Del mismo modo, si un recurso copiado está en revisión, el recurso pegado no estará incluido en la misma revisión.

## Copiar un formulario adaptable {#copy-an-adaptive-form}

Copie un formulario adaptable mediante cualquiera de los siguientes métodos:

1. Haga clic en el icono Copiar ![aem6forms_copy](assets/aem6forms_copy.png) en Acciones rápidas.

   >[!NOTE]
   >
   >Las acciones rápidas son los elementos de acción que se muestran sobre una miniatura al pasar el ratón por encima.

1. Seleccione el formulario adaptable. El proceso de selección es diferente para cada vista.

   Si está en la vista Tarjeta, vaya al modo de selección haciendo clic en el icono de selección ![aem6forms_check-círculo](assets/aem6forms_check-circle.png) y haga clic en todos los formularios adaptables que desee copiar.

   Si está en la vista Lista, haga clic en las casillas de verificación de todos los formularios adaptables para seleccionarlos.

   >[!NOTE]
   >
   >Todos los recursos seleccionados deben ser formularios adaptables, ya que la funcionalidad Copiar y pegar solo es compatible con formularios adaptables, y todos los recursos seleccionados deben encontrarse en la misma carpeta.

   Después de seleccionar los recursos, haga clic en el icono Copiar ![aem6forms_copy](assets/aem6forms_copy.png) que aparece en la barra de herramientas para copiar el formulario adaptable seleccionado.

## Copiar un formulario adaptable {#paste-an-adaptive-form}

Al hacer clic en la acción Copiar, abandonará automáticamente el modo de selección y podrá ver el icono Pegar ![Pegar](assets/Smock_Paste_18_N.svg). A continuación, vaya a la ruta de carpeta deseada y haga clic en el icono Pegar ![Pegar](assets/Smock_Paste_18_N.svg) para pegar el formulario adaptable copiado.

Si está pegando el formulario en la misma carpeta o existe otro archivo con el mismo nombre de nodo (con el que está almacenado en el repositorio CRX) en la carpeta de destino, se añade un 1 al sufijo (por ejemplo, myaf se convierte en myaf1, y si ya existe myaf1 en la misma ubicación, se convierte en myaf2). Todas las demás propiedades siguen siendo las mismas que las del formulario adaptable original.

Después de hacer clic en el icono Pegar ![Pegar](assets/Smock_Paste_18_N.svg), este se volverá a ocultar. Solo puede utilizar la opción Pegar una vez simultáneamente. Para volver a crear una copia del mismo recurso, cópielo de nuevo.

## Cambiar el contenido del nuevo formulario adaptable {#change-contents-of-new-adaptive-form}

El contenido de un formulario adaptable pegado se puede cambiar utilizando los siguientes métodos para diferenciarlo del formulario copiado:

1. **Cambiar las propiedades de los metadatos:**

   Puede cambiar las propiedades de los metadatos del formulario adaptable, por ejemplo, el título y la descripción. Para obtener más información sobre las propiedades de los metadatos y cómo se pueden cambiar, consulte [Administración de metadatos de formulario](manage-form-metadata.md).

1. **Cambiar el XFA/XSD de los formularios adaptables basados en XFA/XSD:**

   Puede cambiar el XFA/XSD utilizado en los formularios adaptables. Para obtener información sobre cómo puede cambiar estos formularios adaptables, consulte [Administrar metadatos de formulario](manage-form-metadata.md).

1. **Volver a publicar el formulario:**

   El recurso pegado es diferente del copiado. Puede publicarlo como un nuevo recurso para que esté disponible para los usuarios finales. Para obtener información sobre cómo publicar un recurso, <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->


## Vea también {#see-also}

{{see-also}}