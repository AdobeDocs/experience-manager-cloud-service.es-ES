---
title: Crear contenido sin encabezado
description: Utilice el modelo de fragmento de contenido que creó anteriormente para crear contenido que se pueda usar para la creación de páginas o como base para el contenido sin encabezado.
hidefromtoc: true
index: false
exl-id: d74cf5fb-4c4a-4363-a500-6e2ef6811e60
source-git-commit: 1456891dc3b13b3d79fa8ee9f3ded37e92cfbc85
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 1%

---

# Crear contenido sin encabezado {#create-content}

Siguiendo el módulo de aprendizaje del producto, aprenda a utilizar [los modelos de fragmento de contenido que creó anteriormente](content-structure.md) para crear contenido que se pueda utilizar para la creación de páginas o como base para el contenido sin encabezado. Este documento sirve como complemento de la gira interactiva, abarcando los mismos pasos y vinculando con recursos adicionales cuando corresponde.

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content"
>title="Crear nuevo contenido"
>abstract="Basándose en los modelos que ha creado en el módulo 1, aprenderá a crear contenido que se pueda utilizar para la creación de páginas o como base del contenido sin encabezado."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide"
>title="Iniciar la consola Fragmento de contenido"
>abstract="En AEM CMS sin encabezado, los &quot;fragmentos de contenido&quot; son todos fragmentos de contenido que se ajustan a la estructura predefinida denominada &quot;modelo de fragmento de contenido&quot;. En este tutorial, aprenderá a crear contenido para su modelo de fragmento de contenido.<br><br>Haga clic a continuación para iniciar la función en una nueva pestaña y siga este documento de aprendizaje para crear su primer fragmento de contenido."
>additional-url="https://video.tv.adobe.com/v/328618" text="Marcador de posición para el vídeo de introducción"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home_c1.png" text="Miniatura de vídeo: Adición de contenido: la fórmula ganadora"

## Fragmentos de contenido {#introduction}

En AEM as a Cloud Service, los fragmentos de contenido son fragmentos de contenido sin encabezado basados en la estructura definida por un modelo de fragmento de contenido. Puede crear su propio fragmento de contenido empezando en la consola Fragmento de contenido . La consola Fragmento de contenido se puede considerar como una biblioteca de contenido sin encabezado. La consola se utiliza para crear nuevos fragmentos de contenido y administrar los fragmentos existentes. La consola empieza vacía, así que vamos a crear un nuevo fragmento.

![Edición del contenido del fragmento](assets/create-content/content-fragment-console.png)

Si desea navegar a la consola Fragmento de contenido por su cuenta fuera de la guía en la aplicación, se encuentra con el icono de Adobe en la parte superior izquierda de la página. Esto abre la navegación global de AEM. Desde aquí puede elegir el **Navegación** pestaña y luego **Fragmentos de contenido**.

>[!TIP]
>
>Si desea obtener más información sobre la navegación en AEM, consulte la [Sección Recursos adicionales](#additional-resources) de este documento para obtener más información sobre AEM gestión básica.

## Crear un fragmento de contenido {#create-fragment}

Los fragmentos de contenido representan su contenido sin encabezado. Sin embargo, solo se pueden crear en función de una estructura de contenido predefinida. El modelo de fragmento de contenido que ha creado anteriormente sirve como esa estructura.

1. Toque o haga clic en el botón **Crear** en la parte superior derecha de la consola para abrir **Nuevo fragmento de contenido** para empezar a crear un nuevo fragmento de contenido.

   ![Cuadro de diálogo Crear fragmento de contenido](assets/create-content/create-content-fragment.png)

1. Si sigue las directrices en la aplicación, **Ubicación** se rellenará automáticamente.

   1. Si no sigue las directrices, utilice el navegador de rutas para seleccionar la carpeta del proyecto.

   1. En el **Nuevo fragmento de contenido** , toque o haga clic en el botón **Elegir ubicación** (el icono que se parece a una carpeta) en la **Ubicación** campo .

      ![Cuadro de diálogo Elegir ubicación](assets/create-content/choose-location.png)
   * También puede seleccionar la ruta en el panel de navegación izquierdo de la consola Fragmento de contenido antes de hacer clic en **Crear**.


1. En el **Modelo de fragmento de contenido** , seleccione el modelo de fragmento de contenido que creó anteriormente en la lista desplegable.

1. Agregue un **Título** para el fragmento de contenido.

1. Toque o haga clic **Crear y abrir**.

## Editor de fragmentos de contenido {#edit-fragment}

Una vez guardado el nuevo fragmento de contenido, se abre el editor de fragmentos de contenido, donde puede proporcionar el contenido real del fragmento.

1. El editor muestra los campos definidos en el modelo seleccionado. Aquí puede editarlos para completar el fragmento de contenido. El progreso se guarda automáticamente.

   ![Editor de fragmentos de contenido](assets/create-content/content-fragment-editor.png)

1. Si el modelo del fragmento de contenido tiene muchos campos, puede saltar rápidamente a cualquier campo utilizando la variable **Variables** en el lado izquierdo del editor. Los campos con errores se marcan aquí.

1. Para que el fragmento de contenido esté disponible para su consumo en una aplicación externa, debe publicarlo. Toque o haga clic en el botón **Publicación** en la parte superior derecha del editor.

1. Select **Ahora** en la lista desplegable . También puede programarlo para publicarlo más adelante.

   ![Botón Publicar](assets/create-content/publish.png)

   >[!TIP]
   >
   >Si desea obtener más información sobre la publicación de contenido en AEM, consulte la [Sección Recursos adicionales](#additional-resources) de este documento para obtener más información sobre la publicación.

1. AEM realiza automáticamente una comprobación de referencia para asegurarse de que se publican todos los recursos necesarios para el fragmento de contenido. En este caso, también deberá publicar el modelo que ha creado. Haga clic o pulse **Publicar**.

   ![Comprobación de referencia](assets/create-content/references.png)

1. La publicación se confirma en un banner.

   ![Confirmación de la publicación](assets/create-content/publish-confirm.png)

## ¡Ha aprendido a crear un fragmento de contenido! {#conclusion}

En este módulo, ha aprendido a crear un fragmento de contenido basado en el modelo que ha creado anteriormente. Así es como un autor de contenido crearía contenido sin encabezado estructurado.

Ahora que el contenido se ha creado y publicado, ahora puede extraer ese contenido a través de Graph QL mediante API AEM. Aprenderá sobre esto en el módulo [Extraer contenido a través de la API de GraphQL.](extract-content.md)

Para volver a la pantalla de inicio de la versión de prueba, haga clic en **Soluciones** en la parte superior derecha de la barra de navegación y seleccione **Experience Manager**.

![Vaya a casa](assets/create-content/home.png)

## Recursos adicionales {#additional-resources}

Para obtener más información sobre los fragmentos de contenido y AEM, considere la posibilidad de revisar esta documentación adicional.

* [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md) : Documentación sobre cómo navegar y utilizar AEM para nuevos usuarios
* [Administración de fragmentos de contenido: publicación y referencia](/help/assets/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment) : Detalles sobre cómo publicar contenido en AEM
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) : Información general sobre los fragmentos de contenido y vínculos a documentación completa sobre los fragmentos de contenido
* [Administración de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) - Cómo crear y administrar fragmentos de contenido
