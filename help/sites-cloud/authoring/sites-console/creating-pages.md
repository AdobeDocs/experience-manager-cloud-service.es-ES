---
title: Creación de páginas
description: Obtenga información sobre cómo crear nuevas páginas para el sitio web mediante la consola Sitios.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 64%

---


# Creación de páginas {#creating-pages}

Obtenga información sobre cómo crear nuevas páginas para el sitio web mediante el **Sites** consola.

>[!TIP]
>
>Antes de empezar a crear páginas nuevas, familiarícese con [AEM cómo se organizan las páginas en las páginas de la página de.](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## Privilegios de acceso {#access-privileges}

Su cuenta necesita los derechos de acceso y permisos adecuados para crear páginas.

Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.

## Creación de una nueva página {#creating-a-new-page}

A menos que se hayan creado todas las páginas por adelantado, debe crear una página para poder empezar a crear contenido:

1. Abrir [el **Sites** consola.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Desplácese hasta la ubicación en la que desee crear la nueva página.
1. Abra el selector desplegable con **Crear** en la barra de herramientas y, a continuación, seleccione **Página** en la lista:

   ![Creación de una página](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. En el primer paso del asistente puede realizar una de las acciones siguientes:

   * Seleccione la plantilla que desee utilizar para crear la nueva página y, a continuación, seleccione **Siguiente** para continuar.

   * **Haga clic en Cancelar** para anular el proceso.

   ![Selección de una plantilla para una nueva página](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. En el último paso del asistente puede realizar una de las acciones siguientes:

   * Utilice las tres pestañas para introducir la variable [propiedades de página](/help/sites-cloud/authoring/sites-console/page-properties.md) Si desea asignar a la nueva página, seleccione **Crear** para crear la página.

   * Utilice **Atrás** para volver a la selección de plantilla.

   Los campos clave son los siguientes:

   * **Título**:

      * Se muestra al usuario y es obligatorio.

   * **Nombre**:

      * Se usa para generar la URI. Si no se especifica, el nombre se obtiene a partir del título.
      * Si proporciona una página **Nombre** AEM al crear una página, se debe hacer lo siguiente [valida el nombre según las convenciones](/help/implementing/developing/introduction/naming-conventions.md) AEM impuesta por el y el JCR.
      * **No se pueden enviar caracteres no válidos** desde el campo **Nombre**. Cuando AEM detecta caracteres no válidos, se resalta el campo y se muestra un mensaje explicativo para indicar los caracteres que deben eliminarse o reemplazarse.

   >[!TIP]
   >
   >Consulte [Convenciones de asignación de nombres a páginas](#page-naming-conventions).

   La información mínima necesaria para crear una página es la siguiente **Título**.

   ![Proporcionar título de página](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Utilice **Crear** para completar el proceso y crear la nueva página. El cuadro de diálogo de confirmación le preguntará si desea **abrir** la página inmediatamente o volver a la consola (**Listo**): 

   ![Éxito en la creación de páginas](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Si crea una página con un nombre que ya existe en la ubicación, el sistema generará automáticamente una variación del nombre añadiéndole un número. Por ejemplo, si `beach` ya existe, la página nueva pasará a llamarse `beach1`.

1. Si vuelve a la consola, podrá ver su nueva página:

   ![Nueva página resultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>Después de crear una página, su plantilla no se puede modificar, a menos que [cree un lanzamiento con una plantilla nueva](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), aunque así se pierda el contenido existente.
