---
title: Configuraciones y el navegador de configuración
description: Comprenda AEM configuraciones y cómo administran la configuración del espacio de trabajo en AEM.
source-git-commit: 4892f644929bc308762ca4fb8a2ebfb85e5fb5e2
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 2%

---


# Configuraciones y el navegador de configuración {#configuration-browser}

AEM configuraciones sirven para administrar la configuración en AEM y sirven como espacios de trabajo.

## ¿Qué es una configuración? {#what-is-a-configuration}

Se puede considerar una configuración desde dos puntos de vista diferentes.

* [Un ](#configurations-administrator) administrador utiliza las configuraciones como espacios de trabajo dentro de AEM para definir y administrar grupos de configuraciones.
* [Un ](#configurations-developer) desarrollador utiliza el mecanismo de configuración subyacente que implementa configuraciones para mantener y buscar ajustes en AEM.

En resumen: desde el punto de vista de un administrador, las configuraciones son cómo se crean espacios de trabajo para administrar la configuración en AEM, mientras que el desarrollador debe comprender cómo AEM utiliza y administra estas configuraciones dentro del repositorio.

Independientemente de su perspectiva, las configuraciones tienen dos propósitos principales en AEM:

* Las configuraciones habilitan ciertas funciones para determinados grupos de usuarios.
* Las configuraciones definen los derechos de acceso para esas funciones.

## Configuraciones como administrador {#configurations-administrator}

Tanto el administrador de AEM como los autores pueden considerar las configuraciones como espacios de trabajo. Estos espacios de trabajo se pueden utilizar para recopilar grupos de configuraciones juntas, así como su contenido asociado con fines organizativos mediante la implementación de derechos de acceso para esas funciones.

Las configuraciones se pueden crear para muchas funciones diferentes dentro de AEM.

* [Segmentos de Context Hub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Plantillas editables](/help/sites-cloud/authoring/features/templates.md)
* varias configuraciones de Cloud

### Ejemplo {#administrator-example}

Por ejemplo, un administrador puede crear dos configuraciones para plantillas editables.

* WKND-General
* WKND-Magazine

A continuación, el administrador puede crear plantillas de página generales utilizando la configuración de WKND-General y, a continuación, plantillas específicas para la revista en WKND-Magazine.

El administrador puede asociar el WKND-General con todo el contenido del sitio WKND. Sin embargo, la configuración de WKND-Magazine solo se asociaría con el sitio de la revista.

Haciendo esto:

* Cuando un autor de contenido crea una página nueva para la revista, el autor puede elegir entre plantillas generales (WKND-General) o plantillas de revista (WKND-Magazine).
* Cuando un autor de contenido crea una página nueva para otra parte del sitio que no es la revista, el autor solo puede elegir entre las plantillas generales (WKND-General).

Se pueden realizar configuraciones similares no solo para plantillas editables, sino también para configuraciones de nube, segmentos de ContextHub y modelos de fragmentos de contenido.

### Uso del explorador de configuración {#using-configuration-browser}

El navegador de configuración permite a un administrador crear, administrar y configurar fácilmente los derechos de acceso a las configuraciones en AEM.

>[!NOTE]
>
>Solo es posible crear configuraciones utilizando el navegador de configuración si el usuario tiene derechos `admin`. `admin` también se requieren para asignar derechos de acceso a la configuración o modificar una configuración de otro modo.

#### Creación de una configuración {#creating-a-configuration}

Es muy sencillo crear una nueva configuración en AEM utilizando el navegador de configuración.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Tools** -> **General** -> **Configuration Browser**.
1. Haga clic o pulse **Crear**.
1. Proporcione un **Título** y un **Nombre** para la configuración.

   ![Crear configuración](assets/configuration-create.png)

   * El **Título** debe ser descriptivo.
   * El **Name** se convertirá en el nombre de nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará según las [convenciones de nomenclatura de AEM.](naming-conventions.md)
      * Se puede ajustar si es necesario.
1. Compruebe el tipo de configuraciones que desea permitir.
   * [Segmentos de Context Hub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
   * [Plantillas editables](/help/sites-cloud/authoring/features/templates.md)
   * varias configuraciones de Cloud
1. Haga clic o pulse **Crear**.

>[!TIP]
>
>Las configuraciones se pueden anidar.

#### Edición de configuraciones y sus derechos de acceso {#access-rights}

Si piensa en las configuraciones como espacios de trabajo, se pueden establecer derechos de acceso en esas configuraciones para hacer cumplir quién puede acceder a esos espacios de trabajo y quién no.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Tools** -> **General** -> **Configuration Browser**.
1. Seleccione la configuración que desea modificar y, a continuación, toque o haga clic en **Propiedades** en la barra de herramientas.
1. Seleccione las funciones adicionales que desee agregar a la configuración
   >[!NOTE]
   >
   >No es posible anular la selección de una función una vez creada la configuración.
1. Utilice el botón **Permisos efectivos** para ver una matriz de funciones y qué permisos se conceden actualmente a las configuraciones.
   ![Ventana de permisos efectivos](assets/configuration-effective-permissions.png)
1. Para asignar nuevos permisos, introduzca el nombre de usuario o grupo en el campo **Seleccionar usuario o grupo** de la sección **Agregar nuevos permisos**.
   * El campo **Select user or group** ofrece la finalización automática en función de los usuarios y funciones existentes.
1. Seleccione el usuario o función apropiado en los resultados de autocompletar.
   * Puede seleccionar más de un usuario o función.
1. Compruebe las opciones de acceso que deben tener los usuarios o roles seleccionados y haga clic en **Agregar**.
   ![Añadir derechos de acceso a una configuración](assets/configuration-edit.png)
1. Repita los pasos para seleccionar usuarios o funciones y asigne derechos de acceso adicionales según sea necesario.
1. Toque o haga clic en **Guardar y cerrar** cuando termine.

## Configuraciones como Desarrollador {#configurations-developer}

Como desarrollador, es importante saber cómo funciona AEM como Cloud Service con las configuraciones y cómo procesa la resolución de la configuración.

### Separación de configuración y contenido {#separation-of-config-and-content}

Aunque el [administrador y los usuarios pueden pensar en las configuraciones como lugares de trabajo](#configurations-administrator) para administrar diferentes configuraciones y contenido, es importante comprender que las configuraciones y el contenido se almacenan y administran por separado por AEM en el repositorio.

* `/content` es el hogar de todo el contenido.
* `/conf` es el hogar de todas las configuraciones.

El contenido hace referencia a su configuración asociada mediante una propiedad `cq:conf` . AEM realiza una búsqueda basada en el contenido y es la propiedad contextual `cq:conf` para encontrar la configuración adecuada.

### Ejemplo {#developer-example}

Para este ejemplo, supongamos que tiene algún código de aplicación que esté interesado en la configuración de DAM.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

El punto de partida de todas las búsquedas de configuración es un recurso de contenido, normalmente en algún lugar en `/content`. Podría ser una página, un componente dentro de una página, un recurso o una carpeta DAM. Este es el contenido real para el que buscamos la configuración correcta que se aplica en este contexto.

Ahora con el objeto `Conf` en mano, podemos recuperar el elemento de configuración específico en el que estamos interesados. En este caso es `dam/imageserver`, que es una colección de configuraciones relacionadas con `imageserver`. La llamada `getItem` devuelve un `ValueMap`. Luego leemos una propiedad de cadena `bgkcolor` y proporcionamos un valor predeterminado de &quot;FFFFFF&quot; en caso de que la propiedad (o el elemento de configuración completo) no esté presente.

Ahora veamos el contenido JCR correspondiente:

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

En este ejemplo, asumimos una carpeta DAM específica de WKND aquí y una configuración correspondiente. A partir de esa carpeta `/content/dam/wknd`, veremos que hay una propiedad de cadena denominada `cq:conf` que hace referencia a la configuración que debe aplicarse al subárbol. La propiedad generalmente se establece en `jcr:content` de una carpeta o página de recursos. Estos `conf` vínculos son explícitos, por lo que es fácil seguirlos mirando el contenido en CRXDE.

Al saltar dentro de `/conf`, seguimos la referencia y vemos que hay un nodo `/conf/wknd`. Esta es una configuración. Tenga en cuenta que su búsqueda es completamente transparente para el código de la aplicación. El código de ejemplo nunca tiene una referencia dedicada a él, está oculto detrás del objeto `Conf`. La configuración que se aplica se controla completamente a través del contenido JCR.

Vemos que la configuración contiene un nodo con nombre fijo `settings` que contiene los elementos reales, incluido el `dam/imageserver` que necesitamos en nuestro caso. Este elemento se puede considerar como un &quot;documento de configuración&quot; y normalmente se representa mediante un `cq:Page` que incluye un `jcr:content` que contiene el contenido real.

Finalmente, vemos la propiedad `bgkcolor` que necesita nuestro código de muestra. El `ValueMap` que obtenemos de `getItem` se basa en el nodo `jcr:content` de la página.

### Resolución de configuración {#configuration-resolution}

El ejemplo básico anterior mostraba una sola configuración. Sin embargo, hay muchos casos en los que desea tener diferentes configuraciones, como una configuración global predeterminada, una diferente para cada marca y tal vez una específica para sus subproyectos.

Para admitir esto, la búsqueda de configuración en AEM tiene un mecanismo de herencia y reserva en el siguiente orden de preferencia:

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Configuración específica referenciada desde `cq:conf` en algún lugar de `/content`
   * La jerarquía es arbitraria y puede diseñarse como la estructura del sitio, no es negocio del código de la aplicación saber esto
   * Se puede cambiar en tiempo de ejecución por usuarios con privilegios de configuración
1. `/conf/<siteconfig>/<parentconfig>`
   * Principales de travesía para configuraciones de reserva
   * Se puede cambiar en tiempo de ejecución por usuarios con privilegios de configuración
1. `/conf/<siteconfig>`
   * Principales de travesía para configuraciones de reserva
   * Se puede cambiar en tiempo de ejecución por usuarios con privilegios de configuración
1. `/conf/global`
   * Configuración global del sistema
   * Normalmente, los valores predeterminados globales para la instalación
   * Configurado por una función `admin`
   * Se puede cambiar en tiempo de ejecución por usuarios con privilegios de configuración
1. `/apps`
   * Valores predeterminados de aplicación
   * Se ha corregido la implementación de la aplicación
   * Solo lectura en tiempo de ejecución
1. `/libs`
   * Valores predeterminados de AEM producto
   * Solo se puede cambiar por Adobe, no se permite el acceso al proyecto
   * Se ha corregido la implementación de la aplicación
   * Solo lectura en tiempo de ejecución

### Uso de configuraciones {#using-configurations}

Las configuraciones de AEM se basan en configuraciones según el contexto de Sling. Los paquetes de Sling proporcionan una API de servicio que puede utilizarse para obtener configuraciones según el contexto. Las configuraciones según el contexto son configuraciones relacionadas con un recurso de contenido o un árbol de recursos como se describió en el ejemplo anterior.](#developer-example)[

Para obtener más información sobre las configuraciones según el contexto, ejemplos y cómo utilizarlos, [consulte la documentación de Sling.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### Consola Web ConfMgr {#confmgr-web-console}

Para fines de depuración y prueba, existe una consola web **ConfMgr** en `https://<host>:<port>/system/console/conf`, que puede mostrar configuraciones para una ruta/elemento determinado.

![ConfMgr](assets/configuration-confmgr.png)

Simplemente proporcione:

* **Ruta de contenido**
* **Elemento**
* **Usuario**

Haga clic en **Resolver** para ver qué configuraciones se resuelven y recibir código de muestra que resuelva dichas configuraciones.

### Consola Web de configuración según el contexto {#context-aware-web-console}

Para fines de depuración y prueba, existe una consola web **Configuración según el contexto** en `https://<host>:<port>/system/console/slingcaconfig`, que permite consultar las configuraciones según el contexto en el repositorio y ver sus propiedades.

![Consola web de configuración según el contexto](assets/configuration-context-aware-console.png)

Simplemente proporcione:

* **Ruta de contenido**
* **Nombre de configuración**

Haga clic en **Resolver** para recuperar las rutas de contexto y propiedades asociadas para la configuración seleccionada.
