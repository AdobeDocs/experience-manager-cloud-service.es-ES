---
title: Explorador del repositorio
seo-title: Repository Browser
description: El explorador del repositorio proporciona una vista de solo lectura en el repositorio para todos los entornos en los niveles de autor, publicación y vista previa.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: b4d28a0c827fb07d6f731118078ecdf448e2f58b
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---

# Explorador del repositorio {#repository-browser}

>[!NOTE]
>
>El Explorador de repositorios está disponible en AEM versiones 6582 y posteriores.

>[!INFO]
>
>También puede ver [este clip](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) para ver un vídeo introductorio sobre cómo utilizar el explorador de repositorios para depurar AEM as a Cloud Service.

## Introducción {#introduction}

El navegador de repositorios es una herramienta para desarrolladores que proporciona una vista de solo lectura en el repositorio para todos los entornos en los niveles de autor, publicación y vista previa. Está diseñado para facilitar la visualización de la estructura de contenido con el fin de facilitar la visualización o depuración del contenido.

Se puede acceder desde Developer Console para examinar el repositorio de un autor o publicar instancias de un entorno seleccionado.

### Requisitos previos de acceso {#access-prerequisites}

Se deben cumplir las siguientes condiciones para acceder a Developer Console o al explorador del repositorio

Para acceder a Developer Console:

* Para los programas de producción, los usuarios deben tener la variable **Cloud Manager: función de desarrollador** en el Admin Console
* Para los programas de entornos limitados, está disponible para cualquier usuario con un perfil de producto que les permita acceder a AEM as a Cloud Service.

Para acceder al Explorador de repositorios:

* Los usuarios deben tener la variable **Cloud Manager: desarrollador** Función en el Admin Console para ver instancias de Autor y Publicación.
* Además, para el autor, los usuarios con el perfil de producto de usuario de AEM pueden ver el navegador del repositorio con acceso de lectura mínimo; los permisos del usuario se respetan al explorar el repositorio. Los usuarios con el perfil de producto de los administradores de AEM pueden ver el explorador del repositorio con acceso de lectura completo.

Para obtener más información sobre la configuración de permisos de usuario, consulte la [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Inicio del explorador del repositorio {#launching-the-repository-browser}

El explorador del repositorio se puede iniciar siguiendo los pasos a continuación.

1. En Cloud Manager, haga clic en los tres puntos junto al entorno que elija y seleccione **Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. A continuación, haga clic en el **Explorador del repositorio** ficha
1. Seleccione cualquier pod correspondiente al autor, la publicación o la vista previa haciendo clic en el botón **Pod** lista desplegable.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Inicie el explorador del repositorio haciendo clic en el **Abrir explorador de repositorios** más abajo. Esto iniciará el explorador correspondiente a una instancia representativa (pod) para el nivel seleccionado. Esto iniciará el explorador correspondiente a una instancia representativa (pod) para el nivel seleccionado. Tenga en cuenta que no puede controlar el pod específico para ese nivel que se inicia.

## Características {#features}

### Navegar por la jerarquía {#navigate-the-hierarchy}

Puede utilizar el panel de navegación izquierdo para desplazarse por la jerarquía de contenido. Al hacer clic en cada carpeta o nodo, se mostrarán sus elementos secundarios. La estructura de carpetas refleja el árbol de recursos de Sling, que es un superconjunto del árbol de nodos JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

<!-- Alexandru: temporarily commenting this out, please don't delete. 

Alternatively, you can navigate directly to a path by entering it in the **Path** field, as shown below. This will also expand its location in the content hierarcy view on the left.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Whenever you click a folder on the left, the Path field automatically populates with its location. This is useful for copying and pasting the value for later usage.

Additionally, when you click on a folder, the URL is dynamically modified to include the path to that folder. This allows for bookmarkable URLs.

-->

Para publicar, de forma predeterminada, el Explorador de repositorios solo mostrará contenido público, por lo que determinadas carpetas como `/conf` o `/home` no será visible.

Para que estas ubicaciones sean visibles, debe seguir el siguiente procedimiento.

1. Haga clic en los tres puntos junto al entorno que elija y seleccione **Administrar acceso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Busque la instancia de publicación y haga clic en ella

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Cree un nuevo perfil de producto para los administradores de publicación. En el ejemplo siguiente, se llama **DEV: Publicación para administradores de AEM**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Agregue los usuarios adecuados, correspondientes a quién debería poder navegar por el explorador del repositorio de publicación con acceso completo, al nuevo perfil de producto

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Espere unos minutos y, a continuación, abra la **AEM autor** consola
1. Agregue el grupo correspondiente al nuevo perfil de producto como miembro del grupo de administradores. Para ello, haga clic en **Herramientas - Seguridad - Grupos en autor** y, a continuación, haga clic en el botón **administradores** grupo. A continuación, añada el grupo como se muestra a continuación

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Active la variable **administradores** y el nuevo **DEV: Publicación para administradores de AEM** para que estén disponibles en la publicación

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Como práctica de seguridad, elimine el nuevo **DEV: Publicación para administradores de AEM** del grupo de administradores en **author** por lo tanto, el nuevo grupo está aislado para publicarse

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Al acceder al explorador del repositorio para una instancia de publicación, todas las carpetas están visibles, incluido `/home` y `/conf`.

### Ver propiedades JCR {#view-jcr-properties}

Al hacer clic en un nodo se mostrarán sus propiedades JCR en el panel derecho del navegador de navegación. A continuación se muestra un ejemplo para la variable `experience-fragments` nodo .

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Ver contenido {#view-content}

Puede utilizar el navegador del repositorio para ver el contenido haciendo clic en un recurso del panel de navegación. Se abrirá una vista previa en el lado derecho del explorador, bajo una pestaña denominada como el recurso respectivo.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

Actualmente, la vista previa está disponible para los tipos de imágenes de la lista siguiente:

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x-icon
* tiff

Y para los siguientes tipos de mime basados en texto:

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### Descargar contenido {#download-content}

También puede utilizar el navegador del repositorio para descargar contenido. En el ejemplo siguiente, puede pulsar el botón **descargar** vínculo para descargar el `jcr:data` asociado al nodo seleccionado. Esta función está disponible para todas las propiedades binarias navegando hasta el nodo que contiene la definición de propiedad.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
