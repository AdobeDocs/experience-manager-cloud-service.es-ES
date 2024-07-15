---
title: ¿Cómo se previsualiza un formulario adaptable?
description: Los usuarios pueden obtener una vista previa de los formularios antes de publicarlos o activarlos para asegurarse de que cumplen las expectativas.  Las opciones de vista previa pueden variar según los tipos de formulario admitidos.
topic-tags: author
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 72235277-6c34-4341-9a10-02afa753e7f5
source-git-commit: 05548d56d791584781606b02839c5602b4469f7b
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 100%

---

# Vista previa de un formulario {#previewing-a-form}

## Información general {#overview}

En [!DNL AEM Forms], puede obtener una vista previa de los formularios y los documentos presentes en el repositorio. La vista previa permite saber exactamente qué aspecto tienen los formularios y cómo se comportan cuando se entregan a los usuarios finales.

Al obtener una vista previa de los formularios, estos se representan en la interfaz interactiva, y el usuario puede rellenarlos con datos. Al obtener una vista previa de los documentos, estos se representan en el modo no interactivo, y el usuario únicamente puede ver el documento. En el caso de los formularios, hay disponible una opción adicional de vista previa personalizada. Con esta opción, puede obtener una vista previa del formulario utilizando datos de un archivo XML. Los datos rellenan algunos o todos los campos del formulario que se está previsualizando.

La siguiente tabla muestra las opciones de vista previa disponibles para los distintos tipos de formularios admitidos:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de recurso</strong><br /> </td>
   <td><strong>Opciones de vista previa disponibles</strong><br /> </td>
  </tr>
  <!--<tr>
   <td>Document</td>
   <td>PDF preview</td>
  </tr>-->
  <tr>
   <td>Formulario PDF</td>
   <td>Vista previa del PDF y vista previa con datos<br /> </td>
  </tr>
  <tr>
   <td>Formulario adaptable</td>
   <td>Vista previa del HTML y vista previa del HTML con datos</td>
  </tr>
  <!--<tr>
   <td>Form Template</td>
   <td>PDF preview, PDF preview with Data, HTML preview, HTML preview with Data<br /> </td>
  </tr>-->
 </tbody>
</table>

## Vista previa de un formulario {#previewing-a-form-1}

1. Seleccione el recurso que desea previsualizar, y haga clic en Vista previa ![aem6forms_preview](assets/aem6forms_preview.png) en la barra de herramientas de acciones.

   >[!NOTE]
   >
   >Para seleccionar un recurso, cambie a la vista Lista en la vista Tarjeta predeterminada. Haga clic en ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para cambiar de vista.

1. Al hacer clic en Vista previa, se muestran las posibles opciones de vista previa aplicables al tipo de recurso seleccionado. Haga clic en la opción que desee para representar el recurso seleccionado en una nueva pestaña.

   Las opciones son las siguientes:

   * Vista precia como HTML
   * Vista previa con datos
     <!--* Preview as PDF (available for form templates)-->

## Vista previa con datos {#preview-with-data}

Al seleccionar **Vista previa con datos**, puede ver el aspecto que tendrá el formulario una vez que se introduzcan datos reales en él. La opción Vista previa con datos permite cargar un XML con datos de usuario de ejemplo. Los datos de usuario de ejemplo se utilizan para rellenar el formulario de vista previa en el formato que elija.

1. Seleccione un recurso, haga clic en Vista previa ![aem6forms_preview](assets/aem6forms_preview.png) y seleccione **Vista previa con datos**.
1. En el cuadro de diálogo Vista previa de formulario, proporcione FormData como el archivo XML. Haga clic en Vista previa para representar el formulario con los datos combinados del XML.
