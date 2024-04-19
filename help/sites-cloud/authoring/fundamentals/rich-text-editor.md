---
title: Use el Editor de texto enriquecido en  [!DNL Adobe Experience Manager] para crear contenido
description: Use el  [!DNL Experience Manager] Editor de texto enriquecido para crear contenido.
exl-id: 15c175f8-11de-4475-87a9-920219a4c004
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 100%

---

# Use el Editor de texto enriquecido para crear contenido {#use-rich-text-editor-to-author-content}

El Editor de texto enriquecido (RTE) es componente básico para agregar contenido textual a [!DNL Adobe Experience Manager]. Además, muchos otros componentes que permiten crear contenido se basan en RTE. Los desarrolladores de Experience Manager pueden personalizar RTE y los administradores pueden configurar RTE para que lo utilicen los autores.

## Edición in-situ {#in-place-editing}

Seleccionar un componente basado en texto con un solo clic para mostrar la [barra de herramientas de componentes](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar).

![La barra de herramientas de componentes](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

Hacer clic nuevamente o seleccionar inicialmente el componente con un doble clic lento abre la edición in-situ. El modo de edición contiene una barra de herramientas. Puede editar el contenido y realizar cambios básicos de formato.

![Edición local con RTE](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

Generalmente, la barra de herramientas ofrece las siguientes opciones:

* **Formato**: resalta el texto como negrita, cursiva o subrayado.
* **Listas**: crea listas con viñetas o numeradas y define la sangría.
* **Hipervínculo**: crea vínculos.
* **Desvincular**: quita el hipervínculo.
* **Pantalla completa**: abre el editor en modo de pantalla completa.
* **Cerrar**: detiene la edición.
* **Guardar**: guarda los cambios.

## Edición en pantalla completa {#full-screen-editing}

Para los componentes basados en texto, haga clic en el botón de modo de pantalla completa ![RTE de pantalla completa](/help/sites-cloud/authoring/assets/editing-full-screen.png) desde la [barra de herramientas](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) para abrir el editor de texto enriquecido y ocultar el resto del contenido de la página.

El modo de pantalla completa muestra todas las opciones configuradas que puede utilizar para la fase de creación. La disponibilidad de las opciones [depende de la configuración](/help/implementing/developing/extending/rich-text-editor.md).

![RTE en modo de pantalla completa](/help/sites-cloud/authoring/assets/rte-full-screen.png)

Las opciones adicionales del editor de texto enriquecido incluyen:

* **Anclaje**: crea en el texto un anclaje al que posteriormente puede hacer referencia o crear una referencia.
* **Alinear texto a la izquierda**.
* **Centrar texto**.
* **Alinear texto a la derecha**.

Haga clic en minimizar para cerrar el modo de pantalla completa.

>[!TIP]
>
>Copiar listas anidadas de [!DNL Microsoft Word] en RTE puede arrojar resultados incoherentes. En su lugar, pegue como un texto y realice ajustes manuales.

>[!MORELIKETHIS]
>
>* [Configurar el editor de texto enriquecido](/help/implementing/developing/extending/rich-text-editor.md)
