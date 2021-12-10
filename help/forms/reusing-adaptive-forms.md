---
title: Reutilizar propiedades de metadatos de un formulario adaptable
seo-title: Reuse metadata properties of an Adaptive Form
description: Puede reutilizar un formulario adaptable existente para crear un nuevo Forms adaptable.
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Reutilizar propiedades de metadatos de un formulario adaptable {#reusing-adaptive-forms}

Si desea utilizar algunas de las propiedades de un formulario adaptable existente para generar uno nuevo, simplemente puede utilizar la funcionalidad de copiar y pegar. Además, puede pegar el nuevo formulario adaptable en la ruta de carpeta deseada. Todas las propiedades de metadatos se replican y también se copian los XFA y XSD para los Forms adaptables basados en XFA y XSD.

>[!NOTE]
>
>El estado y los detalles de la revisión no se copian. Por ejemplo, si el formulario adaptable se publica y, a continuación, si lo copia, el formulario adaptable pegado se encuentra en estado de cancelación de publicación. Del mismo modo, si un recurso copiado está en revisión, el activo pegado no se encuentra en la misma revisión.

## Copiar un formulario adaptable {#copy-an-adaptive-form}

Copie un formulario adaptable mediante cualquiera de los siguientes métodos:

1. Haga clic en Copiar ![aem6forms_copy](assets/aem6forms_copy.png) de Acciones rápidas.

   >[!NOTE]
   >
   >Las acciones rápidas son los elementos de acción que se muestran sobre una miniatura al pasar el ratón por encima.

1. Seleccione el formulario adaptable. El proceso de selección es diferente para las diferentes vistas.

   Si está en la vista de tarjeta, vaya al modo de selección haciendo clic en la selección ![aem6forms_check-círculo](assets/aem6forms_check-circle.png) y haga clic en todo el Forms adaptable que desee copiar.

   Si está en la vista de lista, haga clic en las casillas de verificación de todas las Forms adaptables para seleccionarlas.

   >[!NOTE]
   >
   >Todos los recursos seleccionados deben ser de Forms adaptable, ya que la funcionalidad de copiar y pegar solo es compatible con Forms adaptable y todos los recursos seleccionados deben estar presentes en la misma carpeta.

   Después de seleccionar los recursos, haga clic en la copia ![aem6forms_copy](assets/aem6forms_copy.png) presente en la barra de herramientas para copiar el formulario adaptable seleccionado.

## Pegar un formulario adaptable {#paste-an-adaptive-form}

Al hacer clic en la acción copiar , se sale automáticamente del modo de selección y se pega ![Pegar](assets/Smock_Paste_18_N.svg) icono visible. A continuación, vaya a la ruta de carpeta deseada y haga clic en pegar . ![Pegar](assets/Smock_Paste_18_N.svg) para pegar el formulario adaptable copiado.

Si está pegando en la misma carpeta o en otro archivo con el mismo nombre de nodo (con el que está almacenado en el repositorio CRX) existe en esta carpeta de destino, se añade 1 al sufijo (por ejemplo, myaf se convierte en myaf1 y si myaf1 existe en la misma ubicación, myaf se convierte en myaf2. Todas las demás propiedades siguen siendo las mismas que el formulario adaptable original.

Después de hacer clic en el botón pegar ![Pegar](assets/Smock_Paste_18_N.svg) , se volverá a ocultar. Al mismo tiempo, solo puede pegar una vez. Para volver a crear una copia del mismo recurso, cópiela de nuevo.

## Cambiar el contenido del nuevo formulario adaptable {#change-contents-of-new-adaptive-form}

El contenido de una Forms adaptable pegada se puede cambiar utilizando los siguientes métodos para distinguirlo del formulario copiado:

1. **Cambiar propiedades de metadatos:**

   Puede cambiar las propiedades de metadatos del formulario adaptable, por ejemplo, el título y la descripción. Para obtener más información sobre las propiedades de metadatos y cómo se pueden cambiar, consulte [Administración de metadatos de formulario](manage-form-metadata.md)

1. **Cambiar XFA/XSD para Forms adaptable basado en XFA/XSD:**

   Puede cambiar el XFA/XSD utilizado en Adaptive Forms. Para saber cómo se pueden cambiar estos Forms adaptables, consulte [Administración de metadatos de formulario](manage-form-metadata.md)

1. **Volver a publicar:**

   El recurso pegado es diferente del copiado. Puede publicarlo como un nuevo recurso para que esté disponible para los usuarios finales. Para saber cómo publicar un recurso, <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
