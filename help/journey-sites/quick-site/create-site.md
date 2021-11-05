---
title: Crear sitio a partir de una plantilla
description: Obtenga información sobre cómo crear rápidamente un nuevo sitio AEM con una plantilla de sitio.
source-git-commit: 73e9d1debe70aff7f53d658bbac074fc53d8f1ae
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 0%

---


# Crear sitio a partir de una plantilla {#create-site-from-template}

Obtenga información sobre cómo crear rápidamente un nuevo sitio AEM con una plantilla de sitio.

>[!CAUTION]
>
>La herramienta Creación rápida de sitios es actualmente una vista previa técnica. Está disponible con fines de ensayo y evaluación y no está pensado para su uso en producción a menos que se acuerde con la asistencia al Adobe.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de Creación Rápida del Sitio de AEM, [Comprender Cloud Manager y el flujo de trabajo de creación rápida de sitios,](cloud-manager.md) ha aprendido sobre Cloud Manager y cómo vincula el nuevo proceso de creación rápida de sitios, y ahora debería:

* Comprender cómo AEM Sites y Cloud Manager trabajan juntos para facilitar el desarrollo del front-end
* Vea cómo el paso de personalización del front-end está completamente disociado del AEM y no requiere conocimientos AEM.

Este artículo se basa en estos aspectos básicos para que pueda realizar el primer paso de configuración y crear un nuevo sitio a partir de una plantilla que luego pueda personalizar posteriormente mediante herramientas front-end.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo crear rápidamente un nuevo sitio AEM con una plantilla de sitio. Después de leer, debe:

* Obtenga información sobre cómo obtener AEM plantillas del sitio.
* Aprenda a crear un nuevo sitio con una plantilla.
* Consulte cómo descargar la plantilla del nuevo sitio para proporcionarla al desarrollador del front-end.

## Función responsable {#responsible-role}

Esta parte del recorrido se aplica al administrador de AEM.

## Plantillas de sitios {#site-templates}

Las plantillas de sitio son una forma de combinar el contenido básico del sitio en un paquete conveniente y reutilizable. Las plantillas de sitio generalmente contienen contenido y estructura base del sitio, así como información de estilo del sitio para comenzar el nuevo sitio rápidamente. La estructura real es la siguiente:

* `files`: Carpeta con el kit de interfaz de usuario, XD archivo y, posiblemente, otros archivos
* `previews`: Carpeta con capturas de pantalla de la plantilla del sitio
* `site`: Paquete de contenido del contenido que se copia para cada sitio creado a partir de esta plantilla, como plantillas de página, páginas, etc.
* `theme`: Fuentes del tema de la plantilla para modificar el aspecto del sitio, incluyendo CSS, JavaScript, etc.

Las plantillas son potentes porque se pueden reutilizar para que los autores de contenido puedan crear rápidamente un sitio. Y dado que puede tener varias plantillas disponibles en su instalación de AEM, tiene la flexibilidad para satisfacer diversas necesidades comerciales.

>[!NOTE]
>
>La plantilla del sitio no se debe confundir con las plantillas de página. Las plantillas de sitio descritas aquí definen la estructura general de un sitio. Una plantilla de página define la estructura y el contenido inicial de una página individual.

## Obtención de una plantilla de sitio {#obtaining-template}

La forma más sencilla de empezar es [descargue la última versión de la plantilla de sitio estándar de AEM desde su repositorio de GitHub.](https://github.com/adobe/aem-site-template-standard/releases)

Una vez descargado, puede cargarlo en su entorno de AEM como lo haría con cualquier otro paquete. Consulte la [Sección Recursos adicionales](#additional-resources) para obtener más información sobre cómo trabajar con paquetes si necesita más información sobre este tema.

>[!TIP]
>
>La plantilla AEM del sitio estándar se puede personalizar para satisfacer las necesidades del proyecto y puede obviar la necesidad de una mayor personalización. Sin embargo, este tema está fuera del ámbito de este recorrido. Consulte la documentación de GitHub de la plantilla de sitio estándar para obtener más información.

>[!TIP]
>
>También puede optar por crear la plantilla a partir del origen como parte del flujo de trabajo del proyecto. Sin embargo, este tema está fuera del ámbito de este recorrido. Consulte la documentación de GitHub de la plantilla de sitio estándar para obtener más información.

## Instalación de una plantilla de sitio {#installing-template}

El uso de una plantilla para crear un nuevo sitio es muy sencillo.

1. Inicie sesión en el entorno de creación de AEM y vaya a la consola Sitios .

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Toque o haga clic **Crear** en la parte superior derecha de la pantalla y en el menú desplegable , seleccione **Sitio a partir de una plantilla**.

   ![Creación de un nuevo sitio a partir de una plantilla](assets/create-site-from-template.png)

1. En el asistente Crear sitio , toque o haga clic en **Importar** en la parte superior de la columna izquierda.

   ![Asistente de creación de sitios](assets/site-creation-wizard.png)

1. En el explorador de archivos, busque la plantilla [descargó anteriormente](#obtaining-template) y toque o haga clic en **Cargar**.

1. Una vez cargado, aparece en la lista de plantillas disponibles. Toque o haga clic en ella para seleccionarla (que también muestra información sobre la plantilla en la columna derecha) y luego toque o haga clic en ella **Siguiente**.

   ![Seleccionar una plantilla](assets/select-site-template.png)

1. Proporcione un título para el sitio. Se puede proporcionar un nombre de sitio o se generará a partir del título si se omite.

   * El título del sitio aparece en la barra de título de los navegadores.
   * El nombre del sitio forma parte de la dirección URL.

1. Toque o haga clic **Crear** y el nuevo sitio se crea a partir de la plantilla de sitio.

   ![Detalles del nuevo sitio](assets/create-site-details.png)

1. En el cuadro de diálogo de confirmación que aparece, toque o haga clic en **Listo**.

   ![Cuadro de diálogo de éxito](assets/success.png)

1. En la consola Sitios, los nuevos sitios son visibles y se puede navegar para explorar su estructura básica según se define en la plantilla.

   ![Nueva estructura del sitio](assets/new-site.png)

Los autores de contenido ahora pueden empezar a crear.

## ¿Es necesaria una mayor personalización? {#customization-required}

Las plantillas de sitio son muy potentes y flexibles y se puede crear cualquier número para un proyecto, lo que permite crear fácilmente variaciones de sitio. Según el nivel de personalización que ya se haya realizado en la plantilla de sitio que utilice, es posible que ni siquiera necesite una personalización del front-end adicional.

* Si su sitio no requiere mayor personalización, ¡felicitaciones! ¡Tu recorrido termina aquí!
* Si todavía necesita una personalización del front-end adicional, o simplemente desea comprender el proceso completo en caso de que necesite una personalización futura, continúe leyendo.

## Página de ejemplo {#example-page}

Si necesita personalizar el front-end adicional, tenga en cuenta que el desarrollador del front-end puede no estar familiarizado con los detalles del contenido. Por lo tanto, es aconsejable proporcionar al desarrollador una ruta al contenido típico que se pueda utilizar como base de referencia cuando el tema se personalice. Un ejemplo típico es la página principal del idioma maestro del sitio.

1. En el navegador del sitio, vaya a la página principal del idioma maestro del sitio y, a continuación, toque o haga clic en la página para seleccionarla y, a continuación, pulse o haga clic en **Editar** en la barra de menús.

   ![Página de inicio típica](assets/home-page-in-console.png)

1. En el editor, seleccione la opción **Información de la página** en la barra de herramientas y, a continuación, **Ver como publicado**.

   ![Edición de la página principal](assets/home-page-edit.png)

1. En la pestaña que se abre, copie la ruta del contenido de la barra de direcciones. Se parecerá a `/content/<your-site>/en/home.html?wcmmode=disabled`.

   ![Página principal](assets/home-page.png)

1. Guarde la ruta para proporcionarla más adelante al desarrollador del front-end.

## Descargar el tema {#download-theme}

Ahora que el sitio se ha creado, el tema del sitio generado por la plantilla se puede descargar y proporcionar al desarrollador del front-end para su personalización.

1. En la consola Sitios, muestre la **Sitio** carril.

   ![Mostrar carril de sitios](assets/show-site-rail.png)

1. Toque o haga clic en la raíz del nuevo sitio y, a continuación, toque o haga clic en **Descargar fuentes de temas** en el carril del sitio.

   ![Descargar fuentes de temas](assets/download-theme-sources.png)

Ahora tiene una copia de los archivos de origen del tema en los archivos de descarga.

## Configuración del usuario proxy {#proxy-user}

Para que el desarrollador del front-end pueda previsualizar las personalizaciones utilizando contenido AEM real de su sitio, debe configurar un usuario proxy.

1. En AEM de la navegación principal vaya a **Herramientas** -> **Seguridad** -> **Usuarios**.
1. En la consola de administración de usuarios, toque o haga clic en **Crear**.

   ![Consola de administración de usuarios](assets/user-management-console.png)
1. En el **Crear nuevo usuario** debe proporcionar como mínimo:
   * **ID** : tome nota de este valor, ya que debe proporcionárselo al desarrollador del front-end.
   * **Contraseña** - Guarde este valor de forma segura en un almacén de contraseñas, ya que debe proporcionárselo al desarrollador del front-end.

   ![Nuevos detalles de usuario](assets/new-user-details.png)

1. En el **Grupos** , agregue el usuario del proxy a la pestaña `contributors` grupo.
   * Escribir en el término `contributors` déclencheur AEM función de autocompletar para facilitar la selección del grupo.

   ![Agregar al grupo](assets/add-to-group.png)

1. Toque o haga clic **Guardar y cerrar**.

Ahora ha completado la configuración. Los autores de contenido ahora pueden empezar a crear contenido en el momento en que comienza la preparación del sitio para la personalización del front-end en el siguiente paso del recorrido.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de creación rápida AEM sitio, debe:

* Obtenga información sobre cómo obtener AEM plantillas del sitio.
* Aprenda a crear un nuevo sitio con una plantilla.
* Consulte cómo descargar la plantilla del nuevo sitio para proporcionarla al desarrollador del front-end.

Aproveche este conocimiento y continúe con su recorrido de Creación Rápida AEM Sitio revisando el documento [Configurar la canalización,](pipeline-setup.md) donde creará una canalización front-end para administrar la personalización del tema de su sitio.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de creación rápida del sitio revisando el documento [Configurar la canalización,](pipeline-setup.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido.

* [Plantilla de sitio estándar AEM](https://github.com/adobe/aem-site-template-standard) - Este es el repositorio de GitHub de la plantilla de Sitio estándar AEM.
* [Creación y organización de páginas](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) - Esta guía detalla cómo administrar las páginas de su sitio AEM si desea personalizarlo aún más después de crearlo a partir de la plantilla.
* [Cómo trabajar con el paquete](/help/implementing/developing/tools/package-manager.md) : Los paquetes permiten importar y exportar el contenido del repositorio. Este documento explica cómo trabajar con paquetes en AEM 6.5, que también se aplica a AEMaaCS.
* [Documentación de administración del sitio](/help/sites-cloud/administering/site-creation/create-site.md) - Consulte los documentos técnicos sobre la creación de sitios para obtener más información sobre las funciones de la herramienta de creación rápida de sitios.
