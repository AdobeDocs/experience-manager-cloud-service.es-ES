---
title: Creación de páginas
description: Obtenga información sobre cómo crear nuevas páginas para el sitio web mediante la consola Sitios.
exl-id: 77264562-e76a-40c8-9878-847a8878fb8e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 27%

---


# Creación de páginas {#creating-pages}

Aprenda a crear páginas nuevas para el sitio web mediante la consola **Sitios**.

>[!TIP]
>
>AEM Antes de empezar a crear páginas nuevas, familiarícese con [cómo se organizan las páginas en la organización de las páginas en la organización de las páginas en la organización de las páginas en la organización de las páginas en el sitio](/help/sites-cloud/authoring/sites-console/organizing-pages.md).

## Privilegios de acceso {#access-privileges}

Su cuenta necesita los derechos de acceso y permisos adecuados para crear páginas.

Si tiene algún problema, póngase en contacto con el administrador del sistema.

## Creación de una nueva página {#creating-a-new-page}

A menos que se hayan creado todas las páginas por adelantado, debe crear una página para poder empezar a crear contenido:

1. Abra [la consola **Sitios**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Desplácese hasta la ubicación en la que desee crear la nueva página.
1. Abra el selector desplegable con **Crear** en la barra de herramientas y, a continuación, seleccione **Página** en la lista:

   ![Creación de una página](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. En el primer paso del asistente, puede hacer lo siguiente:

   * Seleccione la plantilla que desee usar para crear la nueva página y, a continuación, seleccione **Siguiente** para continuar o **Cancelar** para anular el proceso.
   * Las plantillas son compatibles con [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md) y con [Editor universal](/help/sites-cloud/authoring/universal-editor/templates.md).

   ![Selección de una plantilla para una nueva página](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. En el último paso del asistente, puede hacer lo siguiente:

   * Use las tres fichas para escribir las [propiedades de página](/help/sites-cloud/authoring/sites-console/page-properties.md) que desee asignar a la nueva página y, a continuación, seleccione **Crear** para crear realmente la página.

   * Utilice **Atrás** para volver a la selección de plantilla.

   Los campos clave son los siguientes:

   * **Título**:

      * Se muestra al usuario y es obligatorio.

   * **Nombre**:

      * Se usa para generar la URI. Si no se especifica, el nombre se obtiene a partir del título.
      * AEM AEM Si proporciona una página **Name** al crear una página, [valida el nombre según las convenciones &#x200B;](/help/implementing/developing/introduction/naming-conventions.md) impuestas por el JCR y el.
      * **No se pueden enviar caracteres no válidos** desde el campo **Nombre**. AEM Cuando detecta caracteres no válidos, se resalta el campo y se muestra un mensaje explicativo para indicar los caracteres que deben eliminarse o reemplazarse.

   >[!TIP]
   >
   >Consulte [Convenciones de asignación de nombres a páginas](#page-naming-conventions).

   La información mínima requerida para crear una página es **Title**.

   ![Proporcionar título de página](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Pulse o haga clic en **Crear** para completar el proceso y crear su nueva página. El cuadro de diálogo de confirmación le pregunta si desea **abrir** la página inmediatamente o volver a la consola (**Listo**). Seleccione uno para finalizar el proceso de creación de página.

   ![Éxito en la creación de páginas](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   * Si elige **Abrir**, la consola **Sitios** abre el editor correspondiente basado en la plantilla de la nueva página, ya sea:
      * [El Editor de página](/help/sites-cloud/authoring/page-editor/introduction.md)
      * [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md)

Si vuelve a la consola, podrá ver la nueva página:

![Nueva página resultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!NOTE]
>
>AEM Si crea una página con un nombre que ya existe en la misma ubicación, crea la página con una variación del nombre especificado agregando un número. Por ejemplo, si `beach` ya existe, la nueva página se convierte en `beach1`.

>[!CAUTION]
>
>Una vez creada una página, su plantilla no se puede cambiar a menos que [cree un lanzamiento con una nueva plantilla](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), aunque así se perderá el contenido existente.
