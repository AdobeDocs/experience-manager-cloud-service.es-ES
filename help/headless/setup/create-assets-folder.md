---
title: 'Creación de una carpeta de recursos: configuración sin encabezado'
description: Utilice modelos de fragmentos de contenido de AEM para definir la estructura de los fragmentos de contenido, la base del contenido sin encabezado.
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 86%

---

# Creación de una carpeta de recursos: configuración sin encabezado {#creating-an-assets-folder}

Utilice modelos de fragmentos de contenido de AEM para definir la estructura de los fragmentos de contenido, la base del contenido sin encabezado. A continuación, los fragmentos de contenido se almacenan en carpetas de recursos.

## ¿Qué es una carpeta de recursos? {#what-is-an-assets-folder}

[Ahora que ha creado modelos de fragmentos de contenido](create-content-model.md) que definen la estructura que desea para los futuros fragmentos de contenido, probablemente tenga ganas de crear algunos fragmentos.

Sin embargo, primero debe crear una carpeta de recursos en la que almacenarlos.

Las carpetas de recursos se utilizan para lo siguiente [organizar recursos de contenido tradicionales](/help/assets/manage-digital-assets.md) le gustan las imágenes y el vídeo y los fragmentos de contenido.

## Cómo crear una carpeta de recursos {#how-to-create-an-assets-folder}

Un administrador solo tendría que crear carpetas ocasionalmente para organizar el contenido a medida que se crea. Para los fines de esta guía de introducción, solo necesitamos crear una carpeta.

1. Inicie sesión en AEM as a Cloud Service y, en el menú principal, seleccione **Navegación -> Recursos -> Archivos**.
1. Haga clic o pulse en **Crear -> Carpeta**.
1. Proporcione un **Título** y **Nombre** para su carpeta.
   * El **Título** debe ser descriptivo.
   * El **Nombre** se convierte en el nombre de nodo del repositorio.
      * Se genera automáticamente en función del título y se ajusta según [AEM Convenciones de nomenclatura de](/help/implementing/developing/introduction/naming-conventions.md).
      * Se puede modificar si es necesario.

   ![Crear carpeta](../assets/assets-folder-create.png)
1. Seleccione la carpeta que acaba de crear pasando el puntero sobre ella y pulsando la marca de verificación. A continuación seleccione **Propiedades** en la barra de herramientas (o utilice la variable `p` [atajo de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)).
1. En la ventana **Propiedades**, seleccione la pestaña **Servicios de nube**.
1. Para la **Configuración de nube**, seleccione la [configuración que creó anteriormente.](create-configuration.md)
   ![Configurar la carpeta de recursos](../assets/assets-folder-configure.png)
1. Haga clic o pulse en **Guardar y cerrar**.
1. Toque o haga clic en **Aceptar** en la ventana de confirmación.

   ![Ventana de confirmación](../assets/assets-folder-confirmation.png)

Puede crear subcarpetas adicionales dentro de la carpeta que acaba de crear. Las subcarpetas heredarán la **Configuración de nube** de la carpeta principal. Sin embargo, esto se puede sobrescribir si desea utilizar modelos de otra configuración.

Si está usando una estructura de sitio localizada, puede [crear una raíz de idioma](/help/assets/translate-assets.md) debajo de la nueva carpeta.

## Siguientes pasos {#next-steps}

Ahora que ha creado una carpeta para los fragmentos de contenido, puede pasar a la cuarta parte de la guía de introducción y [crear fragmentos de contenido](create-content-fragment.md).

>[!TIP]
>
>Para obtener información detallada acerca de la administración de fragmentos de contenido, consulte la [Documentación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md)
