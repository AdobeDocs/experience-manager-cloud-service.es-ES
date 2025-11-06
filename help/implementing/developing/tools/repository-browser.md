---
title: Explorador del repositorio
seo-title: Repository Browser
description: El explorador del repositorio proporciona una vista de solo lectura del repositorio para todos los entornos en los niveles de creación, publicación y vista previa.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# Explorador del repositorio {#repository-browser}

>[!NOTE]
>
>El Explorador de repositorios está disponible en las versiones 6582 y posteriores de AEM.

>[!INFO]
>
>También puede ver [este clip](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) para ver un vídeo introductorio rápido sobre cómo usar el Explorador de repositorios para depurar AEM as a Cloud Service.

## Introducción {#introduction}

El explorador del repositorio es una herramienta para desarrolladores que proporciona una vista de solo lectura del repositorio para todos los entornos en los niveles de creación, publicación y vista previa. Está diseñado para facilitar la visualización de la estructura de contenido y facilitar la visualización o depuración del contenido.

Se puede acceder a ella desde [AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) y se puede usar para examinar el repositorio de una instancia de autor o publicación para un entorno seleccionado.

### Requisitos previos de acceso {#access-prerequisites}

Se deben cumplir las siguientes condiciones para acceder a AEM as a Cloud Service Developer Console o al Explorador de repositorios

Para obtener acceso a AEM as a Cloud Service Developer Console, consulte [Acceso a Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access).

Para acceder al Explorador de repositorios, los requisitos son los mismos que para AEM as a Cloud Service Developer Console (especificado anteriormente). Para ver el contenido del Explorador de repositorios de una instancia concreta:

* Instancias de autor: Los usuarios con el perfil de producto de usuarios de AEM para la **instancia de autor** pueden ver el explorador del repositorio con un acceso de lectura mínimo; los permisos del usuario se respetan al examinar el repositorio. Los usuarios con el Perfil de producto de los administradores de AEM pueden ver el explorador del repositorio con acceso de lectura completo.

* Instancias de publicación: los usuarios con el perfil de producto de usuarios de AEM para la **instancia de publicación** pueden ver el explorador del repositorio con un acceso de lectura mínimo. Sin ese conjunto de perfiles de producto, los usuarios navegarán como usuarios anónimos y algunas rutas no aparecerán debido a permisos limitados.

Para obtener más información sobre cómo configurar permisos de usuario, consulte la [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html).

### Inicio del Explorador de repositorios {#launching-the-repository-browser}

El explorador del repositorio se puede iniciar siguiendo los pasos a continuación.

1. En Cloud Manager, haga clic en los tres puntos junto al entorno que elija y seleccione **Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. A continuación, haga clic en la ficha **Explorador de repositorios**
1. Elija cualquier pod que corresponda a autor, publicación o vista previa haciendo clic en la lista desplegable **Pod**.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Inicie el explorador del repositorio haciendo clic en el vínculo **Abrir explorador del repositorio** que hay más abajo. Se inicia el explorador correspondiente a una instancia representativa (pod) del nivel elegido. No puede controlar el pod específico para ese nivel que se inicia.

## Características {#features}

### Navegar por la jerarquía {#navigate-the-hierarchy}

Puede utilizar el panel de navegación de la izquierda para navegar por la jerarquía de contenido. Al hacer clic en cada carpeta o nodo, se muestran sus tareas secundarias. La estructura de carpetas refleja el árbol de recursos de Sling, que es un superconjunto del árbol de nodos JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

También puede navegar directamente a una ruta de acceso si la escribe en el campo **Ruta**, como se muestra a continuación. Esta ruta también expande su ubicación en la vista de jerarquía de contenido de la izquierda.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Al hacer clic en una carpeta de la izquierda, el campo Ruta se rellena automáticamente con su ubicación. Esta funcionalidad es útil para copiar y pegar el valor para utilizarlo posteriormente.

Además, al hacer clic en una carpeta, la dirección URL se modifica dinámicamente para incluir la ruta a esa carpeta. Esta funcionalidad permite direcciones URL marcables.

Para la publicación, de forma predeterminada, el Explorador de repositorios solo muestra contenido público, por lo que ciertas carpetas como `/conf` o `/home` no están visibles.

Para que esas ubicaciones sean visibles, haga lo siguiente.

1. Haga clic en los tres puntos junto al entorno que elija y seleccione **Administrar acceso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Busque la instancia de publicación y haga clic en ella

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Cree un perfil de producto para administradores de publicación. En el ejemplo siguiente, se llama **DEV - AEM Administrators Publish**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Añada los usuarios adecuados, correspondientes a quién debe poder navegar por el explorador del repositorio de publicación con acceso completo, al nuevo perfil de producto

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Espere unos minutos y, a continuación, abra la consola **AEM author**
1. Agregue el grupo correspondiente al nuevo perfil de producto como miembro del grupo del administrador haciendo clic en **Herramientas - Seguridad - Grupos en autor** y, a continuación, haciendo clic en el grupo **administradores**. A continuación, añada el grupo como se muestra a continuación

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Active los **administradores** y el nuevo grupo **DEV - Administradores de AEM Publish** para que estén disponibles durante la publicación

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Como práctica de seguridad recomendada, quite el nuevo grupo **DEV - AEM Administrators Publish** del grupo del administrador en **author** para que el nuevo grupo quede aislado para la publicación

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Al acceder al explorador del repositorio para una instancia de publicación, todas las carpetas son visibles, incluidas `/home` y `/conf`.

### Ver propiedades JCR {#view-jcr-properties}

Al hacer clic en un nodo, se muestran sus propiedades JCR en el panel derecho del explorador de navegación. A continuación se muestra un ejemplo para el nodo `experience-fragments`.

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Ver contenido {#view-content}

Puede utilizar el explorador del repositorio para ver el contenido. Haga clic en un recurso en el panel de navegación para abrir una vista previa en el lado derecho del explorador, en una pestaña denominada en honor al recurso correspondiente.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

La vista previa está disponible para los siguientes tipos de imagen:

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

También puede utilizar el explorador del repositorio para descargar contenido. En el ejemplo siguiente, puede pulsar el vínculo **descargar** para descargar `jcr:data` asociado al nodo seleccionado. Esta función está disponible para todas las propiedades binarias navegando hasta el nodo que contiene la definición de la propiedad.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
