---
title: Vista previa de un formulario
seo-title: Previewing a form
description: Puede obtener una vista previa de los formularios antes de publicarlos o activarlos para asegurarse de que cumplen las expectativas. Las opciones de vista previa pueden variar según los tipos de formulario admitidos.
seo-description: You can preview your forms before publishing or activating to ensure it meets the expectations. Preview options may vary across the supported form types.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 3%

---


# Vista previa de un formulario {#previewing-a-form}

## Información general {#overview}

En [!DNL AEM Forms], puede obtener una vista previa de los formularios y documentos presentes en el repositorio. La vista previa ayuda a saber exactamente cómo se ven y se comportan los formularios cuando se entregan a los usuarios finales.

Al obtener una vista previa de los formularios, se procesan en la interfaz interactiva y el usuario puede rellenar los formularios con datos. Al obtener una vista previa de los documentos, se procesan en modo no interactivo y el usuario solo puede ver el documento. Para los formularios, hay disponible una opción adicional de Vista previa personalizada . Con esta opción, puede obtener una vista previa del formulario utilizando datos de un archivo XML. Los datos rellenan algunos o todos los campos del formulario que se está previsualizando.

La tabla siguiente muestra las opciones de vista previa disponibles para los distintos tipos de formularios admitidos:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de recurso</strong><br /> </td>
   <td><strong>Opciones de vista previa disponibles</strong><br /> </td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>vista previa del PDF</td>
  </tr>
  <tr>
   <td>Formulario de PDF</td>
   <td>Vista previa y vista previa con datos del PDF<br /> </td>
  </tr>
  <tr>
   <td>Formulario adaptable</td>
   <td>Vista previa del HTML y vista previa del HTML con datos</td>
  </tr>
  <tr>
   <td>Plantilla de formulario</td>
   <td>vista previa del PDF, vista previa del PDF con datos, vista previa del HTML, vista previa del HTML con datos<br /> </td>
  </tr>
 </tbody>
</table>

## Vista previa de un formulario {#previewing-a-form-1}

1. Seleccione el recurso cuya vista previa desee obtener y haga clic en Vista previa ![aem6forms_preview](assets/aem6forms_preview.png) en la barra de herramientas de acciones.

   >[!NOTE]
   >
   >Para seleccionar un recurso, cambie a la vista Lista en la vista Tarjeta predeterminada. Haga clic en ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para cambiar de vista.

1. Al hacer clic en Vista previa , se enumeran las posibles opciones de vista previa aplicables al tipo de recurso seleccionado. Haga clic en la opción que desee para procesar el recurso seleccionado en una nueva pestaña.

   Las opciones son:

   * Vista previa como HTML
   * Vista previa con datos
   * Vista previa como PDF (disponible para plantillas de formulario)

## Vista previa con datos {#preview-with-data}

Al seleccionar **Vista previa con datos**, puede ver el aspecto del formulario con los datos reales introducidos en él. La opción Vista previa con datos permite cargar un XML que contenga datos de usuario de ejemplo. Los datos de usuario de ejemplo se utilizan para rellenar el formulario de vista previa en el formato que elija.

1. Seleccione un recurso y haga clic en Vista previa ![aem6forms_preview](assets/aem6forms_preview.png)y seleccione **Vista previa con datos**.
1. En el cuadro de diálogo Vista previa del formulario, proporcione FormData como archivo XML. Haga clic en Preview para procesar el formulario con los datos combinados de XML.

