---
title: Creación de una carpeta de recursos Guía de Inicio rápido sin encabezado
description: Los modelos de fragmento de contenido definen la estructura de los fragmentos de contenido. Los fragmentos de contenido se almacenan en carpetas de recursos.
translation-type: tm+mt
source-git-commit: 259d54a225f8dee5929f62b784e28f3fc2bb794a
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---


# Creación de una guía de Inicio rápido sin encabezado de carpeta de recursos{#creating-an-assets-folder}

Los modelos de fragmento de contenido definen la estructura de los fragmentos de contenido. Los fragmentos de contenido se almacenan en carpetas de recursos.

##  ¿Qué es una carpeta de recursos? {#what-is-an-assets-folder}

[Ahora que ha creado ](create-content-model.md) modelos de fragmento de contenido que definen la estructura que desea para sus futuros fragmentos de contenido, probablemente le entusiasme crear algunos fragmentos.

Sin embargo, primero deberá crear una carpeta de recursos en la que se almacenarán.

Las carpetas de recursos se utilizan para [organizar recursos de contenido tradicionales](/help/assets/manage-digital-assets.md) como imágenes y vídeo, así como fragmentos de contenido.

## Cómo crear una carpeta de recursos {#how-to-create-an-assets-folder}

Un administrador solo tendría que crear carpetas ocasionalmente para organizar el contenido a medida que se crea. A efectos de esta guía de introducción, solo necesitamos crear una carpeta.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Navegación -> Recursos -> Archivos**.
1. Toque o haga clic en **Crear -> Carpeta**.
1. Proporcione un **Título** y un **Nombre** para la carpeta.
   * El **Título** debe ser descriptivo.
   * El **Nombre** se convertirá en el nombre del nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará en función de [convenciones de nombres de AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Puede ajustarse si es necesario.

   ![Crear carpeta](../assets/assets-folder-create.png)
1. Seleccione la carpeta que acaba de crear y, a continuación, seleccione **Propiedades** en la barra de herramientas (o utilice el método abreviado de teclado `p` [.](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md))
1. En la ventana **Propiedades**, seleccione la ficha **Cloud Services**.
1. Para la **Configuración de nube** Seleccione la configuración [que creó anteriormente.](create-configuration.md)

   ![Configurar carpeta de recursos](../assets/assets-folder-configure.png)
1. Toque o haga clic en **Guardar y cerrar**.
1. Toque o haga clic en **Aceptar** en la ventana de confirmación.

   ![Ventana Confirmación](../assets/assets-folder-confirmation.png)

Puede crear subcarpetas adicionales dentro de la carpeta que acaba de crear. Las subcarpetas heredarán la **Configuración de nube** de la carpeta principal. Sin embargo, esto se puede anular si desea utilizar modelos de otra configuración.

Si utiliza una estructura de sitio localizada, puede [crear una raíz de idioma](/help/assets/translate-assets.md) debajo de la nueva carpeta.

## Próximos pasos {#next-steps}

Ahora que ha creado una carpeta para sus fragmentos de contenido, puede pasar a la cuarta parte de la guía de introducción y [crear fragmentos de contenido.](create-content-fragment.md)

>[!TIP]
>
>Para obtener información detallada sobre la administración de fragmentos de contenido, consulte la [documentación de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
