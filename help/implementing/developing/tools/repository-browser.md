---
title: Explorador del repositorio
seo-title: Repository Browser
description: El explorador del repositorio proporciona una vista de solo lectura del repositorio para todos los entornos en los niveles de creación, publicación y vista previa.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Developer
source-git-commit: 414608955bce3feebd1249a91e4f77161144e51e
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# Explorador del repositorio {#repository-browser}

>[!NOTE]
>
>El Explorador de repositorios está disponible en las versiones 6582 y posteriores de AEM.

>[!INFO]
>
>También puede ver [este clip](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=es) para ver un vídeo introductorio rápido sobre cómo usar el Explorador de repositorios para depurar AEM as a Cloud Service.

## Introducción {#introduction}

El explorador del repositorio es una herramienta para desarrolladores que proporciona una vista de solo lectura del repositorio para todos los entornos en los niveles de creación, publicación y vista previa. Está diseñado para facilitar la visualización de la estructura de contenido y facilitar la visualización o depuración del contenido.

Se puede acceder a ella desde [AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) y se puede usar para examinar el repositorio de una instancia de autor o publicación para un entorno seleccionado.

### Requisitos previos de acceso {#access-prerequisites}

Se deben cumplir las siguientes condiciones para acceder a AEM as a Cloud Service Developer Console o al Explorador de repositorios

Para obtener acceso a AEM as a Cloud Service Developer Console, consulte [Acceso a Developer Console](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access).

Para acceder al Explorador de repositorios, los requisitos son los mismos que para AEM as a Cloud Service Developer Console (especificado anteriormente). Para ver el contenido del Explorador de repositorios de una instancia concreta:

* Instancias de autor: Los usuarios con el perfil de producto de usuarios de AEM para la **instancia de autor** pueden ver el explorador del repositorio con un acceso de lectura mínimo; los permisos del usuario se respetan al examinar el repositorio. Los usuarios con el Perfil de producto de los administradores de AEM pueden ver el explorador del repositorio con acceso de lectura completo.

* Instancias de publicación: los usuarios con el perfil de producto de usuarios de AEM para la **instancia de publicación** pueden ver el explorador del repositorio con un acceso de lectura mínimo. Sin ese conjunto de perfiles de producto, los usuarios navegarán como usuarios anónimos y algunas rutas no aparecerán debido a permisos limitados.

Para obtener más información sobre cómo configurar permisos de usuario, consulte la [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html?lang=es).

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

Para que esas ubicaciones sean visibles, utilice el Perfil del producto de publicación de administradores de AEM. Para obtener más información, consulte la [Documentación de perfiles de equipo y de producto](/help/onboarding/aem-cs-team-product-profiles.md).

<!-- Drafting because of CQDOC-23204

1. Click the three dots next to the environment of your choice and select **Manage Access**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Find your publish instance, then click it

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Create a product profile for publish administrators. In the example below, it is called **DEV - AEM Administrators Publish**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Add the appropriate users, corresponding to who should be able to navigate the publish repository browser with full access, to the new product profile

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Wait for a few minutes, then open the **AEM author** console
1. Add the group corresponding to the new product profile as a member of the administrator's group by clicking **Tools - Security - Groups on author**, then clicking the **administrators** group. Then, add the group as shown below

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Activate the **administrators** and the new **DEV - AEM Administrators Publish** group so that they become available on publish

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. As a good security practice, remove the new **DEV - AEM Administrators Publish** group from the administrator's group on **author** so the new group is isolated to publish 

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Upon accessing repository browser for a publish instance, all folders are visible, including `/home` and `/conf`.

-->

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
