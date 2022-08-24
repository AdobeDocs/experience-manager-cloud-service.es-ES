---
title: 'Creación de fragmentos de contenido: configuración sin encabezado'
description: Aprenda a utilizar fragmentos de contenido de AEM para diseñar, crear, depurar y utilizar contenido independiente de las páginas para una entrega sin encabezado.
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: d6038920a5866c19a94980cc14fa46dec48daf51
workflow-type: ht
source-wordcount: '348'
ht-degree: 100%

---

# Creación de fragmentos de contenido: configuración sin encabezado {#creating-content-fragments}

Aprenda a utilizar fragmentos de contenido de AEM para diseñar, crear, depurar y utilizar contenido independiente de las páginas para una entrega sin encabezado.

## ¿Qué son los fragmentos de contenido? {#what-are-content-fragments}

[Ahora que ha creado una carpeta de recursos](create-assets-folder.md) donde puede almacenar los fragmentos de contenido, puede crear los fragmentos.

Los fragmentos de contenido permiten diseñar, crear, depurar y publicar contenido independiente de cualquier página. Permiten preparar contenido listo para usarse en varias ubicaciones y en varios canales.

Los fragmentos de contenido contienen contenido estructurado y se pueden entregar en formato JSON.

## Cómo crear un fragmento de contenido {#how-to-create-a-content-fragment}

Los autores de contenido generarán el número de fragmentos de contenido que corresponda para representar el contenido que crean. Esta será su tarea principal en AEM. Para los fines de esta guía de introducción, solo necesitamos crear uno.

1. Inicie sesión en AEM as a Cloud Service y, en el menú principal, seleccione **Navegación** -> **Fragmentos de contenido**.

1. Toque o haga clic en la [carpeta creada anteriormente.](create-assets-folder.md)
1. Haga clic o pulse en **Crear**.
1. La creación de un fragmento de contenido se presenta como un cuadro de diálogo.
Seleccione la ubicación y el modelo que desea utilizar para crear el fragmento de contenido.

   * Los modelos disponibles dependen de la [**Configuración de nube** que definió para la carpeta de recursos](create-assets-folder.md) en el que está creando el fragmento de contenido.
   * Si el modelo no está disponible, compruebe la configuración de la carpeta de recursos.

   Añada el título, el nombre y, si es necesario, la descripción.

   ![Cuadro de diálogo Crear fragmento de contenido nuevo](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

1. Toque o haga clic en **Crear** o **Crear y abrir**.

Los fragmentos de contenido pueden hacer referencia a otros fragmentos de contenido, lo que permite anidar una estructura de contenido si es necesario.

Los fragmentos de contenido también pueden hacer referencia a otros recursos en AEM. [Estos recursos deben almacenarse en AEM](/help/assets/manage-digital-assets.md) antes de crear una referencia a un fragmento de contenido.

## Siguientes pasos {#next-steps}

Ahora que ha creado un fragmento de contenido, puede pasar a la parte final de la guía de introducción y [crear solicitudes de API para acceder y entregar fragmentos de contenido.](create-api-request.md)

>[!TIP]
>
>Para obtener información detallada acerca de la administración de fragmentos de contenido, consulte la [Documentación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md)
