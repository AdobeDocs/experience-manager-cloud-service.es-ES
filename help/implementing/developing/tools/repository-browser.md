---
title: Explorador del repositorio
seo-title: Repository Browser
description: El explorador del repositorio proporciona una vista de solo lectura del repositorio para todos los entornos en los niveles de creación, publicación y vista previa.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: 43429562ea4292f38d3459e03185270ec950a58a
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---

# Explorador del repositorio {#repository-browser}

>[!NOTE]
>
>AEM El Explorador de repositorios está disponible en las versiones 6582 y posteriores de la.

>[!INFO]
>
>También puede ver [este clip](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) AEM para obtener una introducción rápida en vídeo sobre cómo utilizar el Explorador de repositorios para depurar los recursos as a Cloud Service de la.

## Introducción {#introduction}

El explorador del repositorio es una herramienta para desarrolladores que proporciona una vista de solo lectura del repositorio para todos los entornos en los niveles de creación, publicación y vista previa. Está diseñado para facilitar la visualización de la estructura de contenido y facilitar la visualización o depuración del contenido.

Se puede acceder a ella desde Developer Console y se puede utilizar para examinar el repositorio de una instancia de autor o publicación para un entorno seleccionado.

### Requisitos previos de acceso {#access-prerequisites}

Estas condiciones deben cumplirse para acceder a Developer Console o al Explorador de repositorios

Para acceder a Developer Console:

* Para los programas de producción, los usuarios deben tener **Cloud Manager: función de desarrollador** en el Admin Console
* AEM Para los programas de zonas protegidas, está disponible para cualquier usuario con un perfil de producto que les permita acceder a las zonas as a Cloud Service de la.

Para acceder al Explorador de repositorios:

* Los usuarios deben tener el **Cloud Manager: Desarrollador** Función en el Admin Console para ver instancias de autor y publicación.
* AEM Además, para el autor, los usuarios con el Perfil de producto de usuarios de la aplicación pueden ver el explorador del repositorio con un acceso de lectura mínimo; los permisos del usuario se respetan al examinar el repositorio. AEM Los usuarios con el Perfil de producto de los administradores de la pueden ver el explorador del repositorio con acceso de lectura completo.

Para obtener más información sobre la configuración de permisos de usuario, consulte la [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Inicio del Explorador de repositorios {#launching-the-repository-browser}

El explorador del repositorio se puede iniciar siguiendo los pasos a continuación.

1. En Cloud Manager, haga clic en los tres puntos junto al entorno que elija y seleccione **Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Haga clic en el botón **Explorador del repositorio** pestaña
1. Seleccione cualquier pod correspondiente a autor, publicación o vista previa haciendo clic en el **Pod** lista desplegable.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Inicie el explorador del repositorio haciendo clic en el icono **Abrir el Explorador del repositorio** vínculo más abajo. Esto inicia el explorador correspondiente a una instancia representativa (pod) para el nivel elegido. Esto inicia el explorador correspondiente a una instancia representativa (pod) para el nivel elegido. Tenga en cuenta que no puede controlar el pod específico para ese nivel que se inicia.

## Características {#features}

### Navegar por la jerarquía {#navigate-the-hierarchy}

Puede utilizar el panel de navegación de la izquierda para navegar por la jerarquía de contenido. Al hacer clic en cada carpeta o nodo, se muestran sus tareas secundarias. La estructura de carpetas refleja el árbol de recursos de Sling, que es un superconjunto del árbol de nodos JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

También puede navegar directamente a una ruta introduciéndola en el **Ruta** , como se muestra a continuación. Esto también expandirá su ubicación en la vista de jerarquía de contenido de la izquierda.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Cada vez que hace clic en una carpeta de la izquierda, el campo Ruta se rellena automáticamente con su ubicación. Esto resulta útil para copiar y pegar el valor para utilizarlo posteriormente.

Además, al hacer clic en una carpeta, la dirección URL se modifica dinámicamente para incluir la ruta a esa carpeta. Esto permite direcciones URL marcables.

Para la publicación, de forma predeterminada, el Explorador de repositorios solo mostrará contenido público, por lo que algunas carpetas como `/conf` o `/home` no será visible.

Para que esas ubicaciones sean visibles, debe seguir el siguiente procedimiento.

1. Haga clic en los tres puntos junto al entorno que desee y seleccione **Administrar acceso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Busque la instancia de publicación y haga clic en ella

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Cree un nuevo perfil de producto para administradores de publicación. En el ejemplo siguiente, se llama **AEM DEV - Publicación de administradores de**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Añada los usuarios adecuados, correspondientes a quién debe poder navegar por el explorador del repositorio de publicación con acceso completo, al nuevo perfil de producto

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Espere unos minutos y, a continuación, abra **AEM autor de la** consolar
1. Agregue el grupo correspondiente al nuevo perfil de producto como miembro del grupo de administradores. Para ello, haga clic en **Herramientas - Seguridad - Grupos de autor**, luego haciendo clic en **administradores** grupo. A continuación, añada el grupo como se muestra a continuación

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Activar el **administradores** y el nuevo **AEM DEV - Publicación de administradores de** para que estén disponibles durante la publicación

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Como práctica de seguridad recomendada, elimine el nuevo **AEM DEV - Publicación de administradores de** grupo del grupo de administradores en **autor** por lo tanto, el nuevo grupo está aislado para publicarse

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Al acceder al explorador de repositorios para una instancia de publicación, todas las carpetas son visibles, incluidas las siguientes `/home` y `/conf`.

### Ver propiedades JCR {#view-jcr-properties}

Al hacer clic en un nodo, se muestran sus propiedades JCR en el panel derecho del explorador de navegación. A continuación se muestra un ejemplo para la `experience-fragments` nodo.

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Ver contenido {#view-content}

Puede utilizar el explorador del repositorio para ver el contenido haciendo clic en un recurso del panel de navegación. Se abrirá una vista previa en el lado derecho del explorador, en una pestaña llamada así por el recurso correspondiente.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

Actualmente, la vista previa está disponible para los tipos de imagen de la lista siguiente:

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x-icon
* riña

Y para los siguientes tipos MIME basados en texto:

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### Descargar contenido {#download-content}

También puede utilizar el explorador del repositorio para descargar contenido. En el ejemplo siguiente, puede pulsar el botón **descargar** para descargar el `jcr:data` asociado con el nodo seleccionado. Esta función está disponible para todas las propiedades binarias navegando hasta el nodo que contiene la definición de la propiedad.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
