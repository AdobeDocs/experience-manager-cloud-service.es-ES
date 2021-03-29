---
title: Creación de una carpeta de recursos Guía de inicio rápido sin encabezado
description: Utilice AEM modelos de fragmento de contenido para definir la estructura de los fragmentos de contenido, la base del contenido sin encabezado.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---


# Creación de una guía de inicio rápido sin encabezado de carpeta de recursos {#creating-an-assets-folder}

Utilice AEM modelos de fragmento de contenido para definir la estructura de los fragmentos de contenido, la base del contenido sin encabezado. A continuación, los fragmentos de contenido se almacenan en carpetas de recursos.

##  ¿Qué es una carpeta de recursos? {#what-is-an-assets-folder}

[Ahora que ha creado ](create-content-model.md) modelos de fragmento de contenido que definen la estructura que desea para sus futuros fragmentos de contenido, es probable que esté encantado de crear algunos fragmentos.

Sin embargo, primero debe crear una carpeta de recursos en la que almacenarlos.

Las carpetas de recursos se utilizan para [organizar los recursos de contenido tradicionales](/help/assets/manage-digital-assets.md), como imágenes y vídeos, así como los fragmentos de contenido.

## Cómo crear una carpeta de recursos {#how-to-create-an-assets-folder}

Un administrador solo tendría que crear carpetas ocasionalmente para organizar el contenido a medida que se crea. Para los fines de esta guía de introducción, solo necesitamos crear una carpeta.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Navegación -> Recursos -> Archivos**.
1. Toque o haga clic en **Crear -> Carpeta**.
1. Proporcione un **Título** y un **Nombre** para la carpeta.
   * El **Título** debe ser descriptivo.
   * El **Name** se convertirá en el nombre de nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará según las [convenciones de nomenclatura de AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Se puede ajustar si es necesario.

   ![Crear carpeta](../assets/assets-folder-create.png)
1. Seleccione la carpeta que acaba de crear y, a continuación, seleccione **Properties** en la barra de herramientas (o utilice el `p` [atajo de teclado.](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md))
1. En la ventana **Properties**, seleccione la pestaña **Cloud Services**.
1. Para **Cloud Configuration** Seleccione la [configuración que creó anteriormente.](create-configuration.md)

   ![Configurar la carpeta de recursos](../assets/assets-folder-configure.png)
1. Toque o haga clic en **Guardar y cerrar**.
1. Toque o haga clic **OK** en la ventana de confirmación.

   ![Ventana de confirmación](../assets/assets-folder-confirmation.png)

Puede crear subcarpetas adicionales dentro de la carpeta que acaba de crear. Las subcarpetas heredarán la **Cloud Configuration** de la carpeta principal. Sin embargo, esto se puede sobrescribir si desea utilizar modelos de otra configuración.

Si utiliza una estructura de sitio localizada, puede [crear una raíz de idioma](/help/assets/translate-assets.md) debajo de la nueva carpeta.

## Pasos siguientes {#next-steps}

Ahora que ha creado una carpeta para los fragmentos de contenido, puede pasar a la cuarta parte de la guía de introducción y [crear fragmentos de contenido.](create-content-fragment.md)

>[!TIP]
>
>Para obtener más información sobre la administración de fragmentos de contenido, consulte la [documentación de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
