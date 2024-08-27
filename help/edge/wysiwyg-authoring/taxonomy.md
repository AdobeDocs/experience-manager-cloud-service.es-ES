---
title: Administración de datos de taxonomía
description: AEM Obtenga información sobre cómo administrar los datos de taxonomía para usar etiquetas con sus sitios de con Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 81aacb0c616490eed4589cb8927ea1316ca1670e
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 7%

---


# Administración de datos de taxonomía {#managing-taxonomy-data}

AEM Obtenga información sobre cómo administrar los datos de taxonomía para usar etiquetas con sus sitios de con Edge Delivery Services.

## Introducción {#introduction}

El etiquetado es una función importante que le ayuda a organizar y administrar sus páginas. AEM [La consola de etiquetado](/help/sites-cloud/administering/tags.md#tagging-console) en le permite crear una taxonomía completa de etiquetas para organizar sus páginas.

Estas etiquetas son útiles no solo para usted y sus autores a la hora de organizar el contenido, sino que también pueden serlo para sus lectores. Las etiquetas y su taxonomía se pueden utilizar en componentes de la página para ayudar a los lectores a navegar por el contenido.

El editor universal solo funciona con los ID de las etiquetas. Al crear una página de taxonomía para el contenido, se exponen las descripciones de estas etiquetas en todos los idiomas al editor universal para que pueda utilizar esa información al procesar el contenido.

## Creación de una página de taxonomía {#creating}

AEM Se crea una taxonomía como [cualquier otra página de la página en la que se haya creado la actividad de la segmentación de datos.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Vaya a la consola [**Sitios**.](/help/sites-cloud/authoring/sites-console/introduction.md)

1. Seleccione la ubicación donde desea crear la taxonomía.

1. Haga clic o pulse **Crear** -> **Página**.

   ![Creación de página](assets/taxonomy/create-page.png)

1. En la ficha **Plantilla** del asistente para **Crear página**, seleccione la plantilla **Taxonomía** y toque o haga clic en **Siguiente**.

   ![Plantilla de taxonomía](assets/taxonomy/taxonomy-template.png)

1. En la ficha **Propiedades** del asistente para **Crear página**, proporcione un **Título** significativo para la página y en el campo **Etiquetas**, [use el selector de etiquetas](/help/sites-cloud/authoring/sites-console/tags.md) para seleccionar las etiquetas o los espacios de nombres que desee incluir en su taxonomía.

   ![Propiedades de taxonomía](assets/taxonomy/create-page-wizard-properties.png)

1. Haga clic o pulse en **Crear**.

Se creará la página de taxonomía. En el cuadro de diálogo **Correcto**, puede tocar o hacer clic en el cuadro de diálogo **Listo** para descartar el mensaje o **Abrir** para editar la página en el [Editor de páginas.](/help/sites-cloud/authoring/page-editor/introduction.md)

Tome nota del nombre de página resultante de la página de taxonomía para utilizarlo en los pasos siguientes.

## Edición de una página de taxonomía {#editing}

AEM Puede empezar a editar una página de taxonomía como cualquier otra página de la lista de distribución de recursos

1. Vaya a la consola [**Sitios**.](/help/sites-cloud/authoring/sites-console/introduction.md)

1. Seleccione la taxonomía que desee editar.

1. Pulse o haga clic en **Editar** en la barra de acciones.

1. Se abrirá el Editor de páginas, donde se mostrará la taxonomía.

   * La página de taxonomía es de solo lectura en el Editor de páginas.

   ![Editar taxonomía](assets/taxonomy/edit-page.png)

1. Pulse o haga clic en el icono **Información de la página** de la barra de herramientas y seleccione **Abrir propiedades**.

   ![Abrir propiedades](assets/taxonomy/open-properties.png)

1. En la ventana **Propiedades de página**, puede actualizar el nombre de la página y usar el selector de etiquetas para actualizar las etiquetas y los espacios de nombres incluidos en su taxonomía.

   ![Editar propiedades de página](assets/taxonomy/edit-properties.png)

1. Haga clic o pulse en **Guardar y cerrar**.

La página mostrada en el Editor de páginas es de solo lectura porque el contenido de la taxonomía se genera automáticamente a partir de las etiquetas y los espacios de nombres seleccionados. Actúan como una especie de filtro para generar automáticamente el contenido de la taxonomía. Por lo tanto, no hay razón para editar directamente la página en el editor.

AEM El contenido de la página de taxonomía se actualiza automáticamente cuando se actualizan las etiquetas y los espacios de nombres subyacentes. Sin embargo, debe [volver a publicar la taxonomía](#publishing) después de cualquier cambio para que los cambios estén disponibles para los usuarios.

## Actualizar paths.json para la publicación de taxonomías {#paths-json}

Al igual que cuando [administra y publica datos tabulares para el sitio de Edge Delivery Services,](/help/edge/wysiwyg-authoring/tabular-data.md) necesita actualizar el archivo `paths.json` del proyecto para permitir la publicación de los datos de taxonomía.

1. Abra la raíz del proyecto en GitHub.

1. Haga clic o pulse en el archivo `paths.json` para abrir sus detalles y, a continuación, el icono **Editar**.

   ![archivo paths.json](assets/taxonomy/paths-json.png)

1. Agregue una línea para asignar la nueva página de taxonomía a un recurso `.json`.

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/<taxonomy-page-name>:/<taxonomy-json-name>.json"
     ]
   }
   ```

   * `<taxonomy-page-name>` debe coincidir con el nombre de la [página de taxonomía que creó.](#creating)
   * `<taxonomy-json-name>` puede ser cualquier nombre válido que elija.

1. Haga clic en **Confirmar cambios…** para guardar los cambios en `main`.

   * Confirme con `main` o cree una solicitud de extracción de acuerdo con su proceso.

Este proceso solo debe realizarse una vez por página de taxonomía. Una vez finalizado, puede publicar la taxonomía.

## Publicación de una taxonomía {#publishing}

El Editor universal o los usuarios no pueden acceder a una taxonomía hasta que se publique.

Las páginas de taxonomía se publican como cualquier otra página por [mediante los iconos **Quick Publish** o **Administrar publicación** de la barra de herramientas.](/help/sites-cloud/authoring/sites-console/publishing-pages.md)

Debe volver a publicar la página de taxonomía cada vez que:

* Edite la página de taxonomía.
* Edite o añada a las etiquetas y áreas de nombres incluidas en la página de taxonomía.

Si crea una nueva página de taxonomía, primero debe [agregarle una asignación al archivo `paths.json` de su proyecto.](#paths-json)

## Acceso a información de taxonomía {#accessing}

Una vez publicada la taxonomía, el Editor universal puede aprovechar su información y hacerla visible para los usuarios.

Puede acceder a la taxonomía como datos JSON en la siguiente dirección.

`https://<branch>--<repository>--<owner>.hlx.page/<taxonomy-json-name>.json`

Utilice el `<taxonomy-json-name>` que definió al [asignar su taxonomía al archivo `paths.json` de su proyecto.](#paths-json): los datos de taxonomía se devuelven como datos JSON, como en el ejemplo siguiente.

```json
{
  "total": 3,
  "offset": 0,
  "limit": 3,
  "data": [
    {
      "tag": "default:",
      "title": "Standard Tags"
    },
    {
      "tag": "do-not-translate",
      "title": "Do Not Translate"
    },
    {
      "tag": "translate",
      "title": "Translate"
    }
  ],
  ":type": "sheet"
}
```

Estos datos JSON se actualizarán automáticamente a medida que actualice la taxonomía y vuelva a publicarla. Su aplicación puede acceder mediante programación a esta información para los usuarios.

[Si mantiene etiquetas en varios idiomas,](/help/sites-cloud/administering/tags.md#managing-tags-in-different-languages) puede tener acceso a esos idiomas pasando el código de idioma ISO2 como valor de un parámetro `sheet=`.
