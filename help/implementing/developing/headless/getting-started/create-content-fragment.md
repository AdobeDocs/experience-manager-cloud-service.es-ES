---
title: Creación de fragmentos de contenido Guía de Inicio rápido sin encabezado
description: Los fragmentos de contenido le permiten diseñar, crear, depurar y utilizar contenido independiente de la página que se puede distribuir sin problemas mediante AEM.
translation-type: tm+mt
source-git-commit: 712a99095494ab333cf0ebb2ac9fffe3f5945f3b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Creación de fragmentos de contenido Guía de Inicio rápido sin encabezado {#creating-content-fragments}

Los fragmentos de contenido le permiten diseñar, crear, depurar y utilizar contenido independiente de la página que se puede distribuir sin problemas mediante AEM.

## ¿Qué son los fragmentos de contenido? {#what-are-content-fragments}

[Ahora que ha creado una ](create-assets-folder.md) carpeta de recursos en la que puede almacenar los fragmentos de contenido, puede crear los fragmentos.

Los fragmentos de contenido le permiten diseñar, crear, depurar y publicar contenido independiente de la página. Permiten preparar contenido listo para su uso en varias ubicaciones y en varios canales.

Los fragmentos de contenido contienen contenido estructurado y se pueden entregar en formato JSON.

## Cómo crear un fragmento de contenido {#how-to-create-a-content-fragment}

Los autores de contenido crearán cualquier número de fragmentos de contenido para representar el contenido que crean. Esta será su principal tarea en AEM. Para los fines de esta guía de introducción, sólo necesitaremos crear una.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Navegación -> Recursos**.
1. Toque o haga clic en la carpeta [que creó anteriormente.](create-assets-folder.md)
1. Toque o haga clic en **Crear -> Fragmento de contenido**.
1. La creación de un fragmento de contenido se presenta como un asistente en dos pasos. Primero seleccione qué modelo desea utilizar para crear el fragmento de contenido y toque o haga clic en **Siguiente**.
   * Los modelos disponibles dependen de la [**Configuración de nube** que definió para la carpeta de recursos](create-assets-folder.md) en la que esté creando el fragmento de contenido.
   * Si recibe el mensaje `We could not find any models`, compruebe la configuración de la carpeta assets.

   ![Seleccionar modelo de fragmento de contenido](../assets/content-fragment-model-select.png)
1. Proporcione un **Título**, **Descripción** y **Etiquetas** según sea necesario y toque o haga clic en **Crear**.

   ![Crear fragmento de contenido](../assets/content-fragment-create.png)
1. Toque o haga clic en **Abrir** en la ventana de confirmación.

   ![Confirmación de creación del fragmento de contenido](../assets/content-fragment-confirmation.png)
1. Proporcione los detalles del fragmento de contenido en el Editor de fragmentos de contenido.

   ![Editor de fragmento de contenido](../assets/content-fragment-edit.png)
1. Toque o haga clic en **Guardar**.

Los fragmentos de contenido pueden hacer referencia a otros fragmentos de contenido, lo que permite una estructura de contenido anidada si es necesario.

Los fragmentos de contenido también pueden hacer referencia a otros recursos de AEM. [Estos recursos deben almacenarse en ](/help/assets/manage-digital-assets.md) AEM antes de crear un fragmento de contenido de referencia.

## Próximos pasos {#next-steps}

Ahora que ha creado un fragmento de contenido, puede pasar a la parte final de la guía de introducción y [crear solicitudes de API para acceder y entregar fragmentos de contenido.](create-api-request.md)

>!![TIP]
Para obtener información detallada sobre la administración de fragmentos de contenido, consulte la [documentación de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
