---
title: Estructura del proyecto AEM
description: Obtenga información sobre cómo definir estructuras de paquetes para la implementación en Adobe Experience Manager Cloud Service.
translation-type: tm+mt
source-git-commit: 1a282bdaca02f47d7936222da8522e74831a4572
workflow-type: tm+mt
source-wordcount: '2828'
ht-degree: 13%

---


# Estructura del proyecto AEM

>[!TIP]
>
>Familiarícese con el uso [básico](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html)AEM del arquetipo del proyecto, y con el complemento [Maven de contenido de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) FileVault, ya que este artículo se basa en estos conocimientos y conceptos.

Este artículo describe los cambios necesarios para que los proyectos de Adobe Experience Manager Maven se AEM como Cloud Service compatibles, asegurándose de que respetan la división del contenido mutable e inmutable, las dependencias se establecen para crear implementaciones determinísticas y no conflictivas y que se empaquetan en una estructura implementable.

AEM implementaciones de aplicaciones deben estar compuestas por un único paquete AEM. A su vez, este paquete debe contener subpaquetes que comprenden todo lo que la aplicación necesita para funcionar, incluyendo código, configuración y cualquier contenido de línea de base compatible.

AEM requiere una separación de **contenido** y **código**, lo que significa que un paquete de contenido único **no puede** implementarse **en ambas instancias** `/apps` y en áreas de tiempo de ejecución (p. ej. `/content`, `/conf`, `/home` o cualquier cosa que no sea `/apps`) del repositorio. En su lugar, la aplicación debe separar el código y el contenido en paquetes discretos para su implementación en AEM.

La estructura del paquete descrita en este documento es compatible **tanto** con las implementaciones de desarrollo local, como con las implementaciones de AEM Cloud Service.

>[!TIP]
>
>Las configuraciones descritas en este documento son proporcionadas por [AEM Project Maven Archetype 24 o posterior](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutables vs. inmutables del repositorio {#mutable-vs-immutable}

`/apps` y `/libs`**se consideran áreas inmutables de AEM, ya que no se pueden cambiar (crear, actualizar, eliminar) después de iniciarse AEM (es decir, durante la ejecución).** Cualquier intento de cambiar un área inmutable durante la ejecución fallará.

Everything else in the repository, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc. are all **mutable** areas, meaning they can be changed at runtime.

>[!WARNING]
>
>Como en versiones anteriores de AEM, no `/libs` debe modificarse. Sólo se puede implementar AEM código de producto en `/libs`.

### Índices de roble {#oak-indexes}

Los índices Oak (`/oak:index`) son administrados específicamente por el AEM como un proceso de implementación de Cloud Service. Esto se debe a que el Administrador de nube debe esperar hasta que se implemente cualquier nuevo índice y se vuelva a indexar completamente antes de cambiar a la nueva imagen de código.

Por este motivo, aunque los índices Oak son mutables en tiempo de ejecución, deben implementarse como código para que se puedan instalar antes de instalar cualquier paquete mutable. Por lo tanto, `/oak:index` las configuraciones forman parte del paquete de código y no del paquete de contenido [como se describe a continuación](#recommended-package-structure).

>[!TIP]
>
>Para obtener más información acerca de la indexación en AEM como Cloud Service, consulte Búsqueda de [contenido de documento e Indexación](/help/operations/indexing.md).

## Estructura de paquete recomendada {#recommended-package-structure}

![Estructura del paquete de proyectos de Experience Manager](assets/content-package-organization.png)

Este diagrama proporciona una visión general de la estructura de proyecto recomendada y de los artefactos de implementación de paquetes.

La estructura de implementación de aplicaciones recomendada es la siguiente:

### Paquetes de código / Paquetes OSGi

+ El archivo Jar del paquete OSGi se genera y se incrusta directamente en el proyecto all.

+ El `ui.apps` paquete contiene todo el código que se va a implementar y solo se implementa en `/apps`. Los elementos comunes del `ui.apps` paquete incluyen, entre otros:
   + [Definiciones de componentes y secuencias de comandos HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html)
      + `/apps/my-app/components`
   + JavaScript y CSS (a través de [bibliotecas](/help/implementing/developing/introduction/clientlibs.md)de cliente)
      + `/apps/my-app/clientlibs`
   + [Superposiciones](/help/implementing/developing/introduction/overlays.md) de `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configuraciones de reserva según el contexto
      + `/apps/settings`
   + ACL (permisos)
      + Cualquiera `rep:policy` para cualquier ruta debajo de `/apps`

+ El `ui.config` paquete contiene todas las configuraciones [](/help/implementing/deploying/configuring-osgi.md)OSGi:
   + Carpeta de organización que contiene definiciones de configuración de OSGi específicas del modo de ejecución
      + `/apps/my-app/osgiconfig`
   + Carpeta de configuración OSGi común que contiene configuraciones OSGi predeterminadas que se aplican a todos los AEM de destinatario como destinatarios de implementación de Cloud Service
      + `/apps/my-app/osgiconfig/config`
   + Ejecutar carpetas de configuración OSGi específicas del modo que contienen configuraciones OSGi predeterminadas que se aplican a todos los AEM de destinatario como destinatarios de implementación de Cloud Service
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Secuencias de comandos de configuración de Repo Init OSGi
      + [Repo Init](#repo-init) es la forma recomendada de implementar contenido (mutable) que forma parte lógicamente de la aplicación AEM. Las configuraciones de OSGi de Repo Init deben ubicarse en la `config.<runmode>` carpeta adecuada, tal como se describe anteriormente, y utilizarse para definir:
         + Estructuras de contenido de línea base
         + Usuarios
         + Usuarios de servicio
         + Grupos
         + ACL (permisos)

### Paquetes de contenido

+ El `ui.content` paquete contiene todo el contenido y la configuración. El paquete de contenido contiene todas las definiciones de nodo que no están en los paquetes `ui.apps` o `ui.config` , o en otras palabras, que no están en `/apps` o `/oak:index`. Los elementos comunes del `ui.content` paquete incluyen, entre otros:
   + Configuraciones según el contexto
      + `/conf`
   + Estructuras de contenido complejas y requeridas (por ejemplo: Generación de contenido que se basa en estructuras de contenido de línea de base definidas en la opción de repo y que se extiende más allá de ellas).
      + `/content`, `/content/dam`, etc.
   + Etiquetado de taxonomías gobernadas
      + `/content/cq:tags`
   + Nodos preexistentes, etc. (Idealmente, migre estos nodos a ubicaciones que no sean/etc.)
      + `/etc`

### Paquetes contenedor

+ El `all` paquete es un paquete de contenedor que SÓLO incluye artefactos implementables, el archivo Jar del paquete OSGI `ui.apps`, `ui.config` y `ui.content` paquetes como incrustado. The `all` package must not have **any content or code** of its own, but rather delegate all deployment to the repository to its sub-packages or OSGi bundle Jar files.

   Los paquetes ahora se incluyen mediante la configuración [integrada del complemento Maven](#embeddeds)FileVault Package Maven en lugar de la configuración `<subPackages>` .

   Para implementaciones de Experience Manager complejas, puede ser conveniente crear varios `ui.apps`proyectos `ui.config` y `ui.content` paquetes que representen sitios específicos o inquilinos en AEM. Si esto se hace, asegúrese de que se respeta la división entre contenido mutable e inmutable, y que los paquetes de contenido necesarios y los archivos Jar del paquete OSGi se incrustan como subpaquetes en el paquete de contenido de `all` contenedor.

   Por ejemplo, una estructura compleja del paquete de contenido de implementación podría tener este aspecto:

   + `all` el paquete de contenido incorpora los siguientes paquetes para crear un artefacto de implementación único
      + `common.ui.apps` implementa el código requerido por **ambos** sitios: A y B
      + `site-a.core` Jar de paquete OSGi requerido por el sitio A
      + `site-a.ui.apps` implementa el código requerido por el sitio A
      + `site-a.ui.config` implementa las configuraciones de OSGi requeridas por el sitio A
      + `site-a.ui.content` implementa el contenido y la configuración requeridos por el sitio A
      + `site-b.core` Jar de paquete OSGi requerido por el sitio B
      + `site-b.ui.apps` implementa el código requerido por el sitio B
      + `site-b.ui.config` implementa las configuraciones de OSGi requeridas por el sitio B
      + `site-b.ui.content` implementa el contenido y la configuración requeridos por el sitio B

### Paquetes de aplicaciones adicionales{#extra-application-packages}

Si la implementación de AEM utiliza otros proyectos de AEM, que a su vez están compuestos por su propio código y paquetes de contenido, sus paquetes de contenedor deberían estar integrados en el paquete `all` del proyecto.

Por ejemplo, un proyecto AEM que incluya dos aplicaciones AEM de proveedores podría tener el siguiente aspecto:

+ `all` el paquete de contenido incorpora los siguientes paquetes para crear un artefacto de implementación único
   + `core` Jar del paquete OSGi requerido por la aplicación AEM
   + `ui.apps` implementa el código requerido por la aplicación AEM
   + `ui.config` implementa las configuraciones de OSGi requeridas por la aplicación AEM
   + `ui.content` implementa el contenido y la configuración requeridos por la aplicación AEM
   + `vendor-x.all` implementa todo (código y contenido) que requiere la aplicación X del proveedor
   + `vendor-y.all` implementa todo lo que la aplicación Y del proveedor necesita (código y contenido)

## Tipos de paquetes {#package-types}

Los paquetes se marcarán con su tipo de paquete declarado.

+ Los paquetes de contenedor deben configurar su `packageType` en `container`.
+ Los paquetes de código (inmutables) deben configurar su `packageType` en `application`.
+ Los paquetes de contenido (mutable) deben configurarse `packageType` en `content`.

Para obtener más información, consulte la documentación [del plugin](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) Apache Jackrabbit FileVault - Package Maven y el fragmento [](#marking-packages-for-deployment-by-adoube-cloud-manager) de configuración FileVault Maven más abajo.

>[!TIP]
>
>Consulte la sección Fragmentos [XML de](#xml-package-types) POM más abajo para ver un fragmento completo.

## Marcado de paquetes para implementación por Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

De forma predeterminada, Adobe Cloud Manager obtiene todos los paquetes producidos por la compilación de Maven; sin embargo, dado que el paquete de contenedor (`all`) es el único artefacto de implementación que contiene todos los paquetes de contenido y código, debemos asegurarnos de que **solo** se implementa el paquete de contenedor (`all`). Para garantizar esto, otros paquetes que genera la compilación de Maven deben marcarse con la configuración del complemento Maven del paquete de contenido de FileVault `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte la sección Fragmentos [XML de](#pom-xml-snippets) POM más abajo para ver un fragmento completo.

## Tiempo de espera de repo{#repo-init}

Repo Init proporciona instrucciones, o secuencias de comandos, que definen estructuras JCR, desde estructuras de nodos comunes como árboles de carpetas hasta usuarios, usuarios de servicios, grupos y definición de ACL.

Las ventajas clave de Repo Init son que tienen permisos implícitos para realizar todas las acciones definidas por sus secuencias de comandos y se invocan al principio del ciclo vital de implementación, lo que garantiza que todas las estructuras JCR necesarias existan al ejecutar el código de tiempo.

Mientras que los scripts de Repo Init viven en el `ui.config` proyecto como scripts, pueden y deben utilizarse para definir las siguientes estructuras mutables:

+ Estructuras de contenido de línea base
+ Usuarios de servicio
+ Usuarios
+ Grupos
+ ACL

Las secuencias de comandos Repo Init se almacenan como `scripts` entradas de configuraciones de fábrica de `RepositoryInitializer` OSGi y, por tanto, se pueden dirigir implícitamente al modo de ejecución, lo que permite diferencias entre las secuencias de comandos Repo Init de AEM Author y AEM Publish Services, o incluso entre entornos (Dev, Stage y Prod).

Las configuraciones de OSGi de Repo Init se escriben mejor en el formato [`.config` de configuración OSGi, ya que admiten varias líneas, lo cual es una excepción a las prácticas recomendadas de](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) definir configuraciones [`.cfg.json`](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)OSGi.

Tenga en cuenta que al definir usuarios y grupos, solo los grupos se consideran parte de la aplicación y se debe definir una parte integral de su función aquí. Los usuarios y grupos de la organización deben seguir definidos durante la ejecución en AEM; por ejemplo, si un flujo de trabajo personalizado asigna trabajo a un grupo con nombre, dicho grupo debe definirse mediante Repo Init en la aplicación AEM; sin embargo, si el grupo es meramente organizativo, como &quot;Wendy&#39;s Team&quot; y &quot;Sean&#39;s Team&quot;, se definirán mejor y se gestionarán en tiempo de ejecución en AEM.

>[!TIP]
>
>Las secuencias de comandos Repo Init *deben* definirse en el `scripts` campo en línea y la configuración no `references` funcionará.

El vocabulario completo para los scripts Repo Init está disponible en la documentación [](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)de Apache Sling Repo Init.

>[!TIP]
>
>Consulte la sección [Recortes](#snippet-repo-init) de inicio de la repo más abajo para ver un fragmento completo.

## Paquete de estructura de repositorio {#repository-structure-package}

Los paquetes de código requieren configurar la configuración del complemento FileVault Maven para hacer referencia a una `<repositoryStructurePackage>` que exige la exactitud de las dependencias estructurales (para garantizar que un paquete de código no se instale sobre otro). Puede [crear su propio paquete de estructura de repositorio para su proyecto](repository-structure-package.md).

Esto **solo es necesario** para los paquetes de código, es decir, cualquier paquete marcado con `<packageType>application</packageType>`.

Para obtener información sobre cómo crear un paquete de estructura de repositorio para la aplicación, consulte [Desarrollar un paquete](repository-structure-package.md)de estructura de repositorio.

Tenga en cuenta que los paquetes de contenido (`<packageType>content</packageType>`) **no** requieren este paquete de estructura de repositorio.

>[!TIP]
>
>Consulte la sección Fragmentos [XML de](#xml-repository-structure-package) POM más abajo para ver un fragmento completo.

## Incrustación de subpaquetes en el paquete de Contenedor{#embeddeds}

Los paquetes de contenido o código se colocan en una carpeta especial de &quot;coche lateral&quot; y se pueden dirigir para la instalación en AEM autor, AEM publicación o en ambos, mediante la configuración del complemento FileVault Maven `<embeddeds>` . Tenga en cuenta que no se debe utilizar la `<subPackages>` configuración.

Entre los casos de uso comunes se incluyen:

+ ACL/permisos que difieren entre los usuarios autores de AEM y los usuarios AEM publicación
+ Configuraciones que se utilizan para admitir actividades solo en AEM autor
+ Código como integraciones con sistemas de back-office, solo necesario para ejecutarse en AEM autor

![Incrustación de paquetes](assets/embeddeds.png)

Para dar destinatario AEM autor, AEM publicar o ambos, el paquete se incrusta en el paquete de `all` contenedor en una ubicación de carpeta especial, con el siguiente formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Desglosar la estructura de carpetas:

+ La carpeta de primer nivel **debe ser** `/apps`.
+ La carpeta de segundo nivel representa la aplicación con `-packages` una publicación fija en el nombre de la carpeta. A menudo, solo hay una carpeta de segundo nivel en la que se incrustan todos los subpaquetes, aunque se puede crear cualquier número de carpetas de segundo nivel para representar mejor la estructura lógica de la aplicación:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >De forma predeterminada, las carpetas incrustadas de subpaquetes reciben el nombre del sufijo de `-packages`. Esto garantiza que el código de implementación y los paquetes de contenido **no se implementen** en las carpetas de destino de ningún subpaquete `/apps/<app-name>/...` que tenga como resultado un comportamiento de instalación destructivo y cíclico.

+ La carpeta de tercer nivel debe ser
   `application`, `content` o `container`
   + La `application` carpeta contiene paquetes de código
   + La `content` carpeta contiene paquetes de contenido
   + La `container` carpeta contiene todos los paquetes [de aplicaciones](#extra-application-packages) adicionales que pueda incluir la aplicación AEM.
Este nombre de carpeta corresponde a los tipos [de](#package-types) paquete de los paquetes que contiene.
+ La carpeta de cuarto nivel contiene los subpaquetes y debe ser uno de los siguientes:
   + `install` para realizar la instalación en **AEM Author y AEM Publish**
   + `install.author` para instalar **solo** en AEM Author
   + `install.publish` para **instalar únicamente** en AEM publicaciónTenga en cuenta que solo `install.author` y `install.publish` son destinatarios compatibles. Otros modos de ejecución **no son** compatibles.

Por ejemplo, una implementación que contenga AEM creación y publicación de paquetes específicos puede tener el siguiente aspecto:

+ `all` El paquete contenedor incorpora los siguientes paquetes para crear un artefacto de implementación único
   + `ui.apps` incrustado en `/apps/my-app-packages/application/install` implementa código tanto para AEM autor como para AEM publicación.
   + `ui.apps.author` incrustado en `/apps/my-app-packages/application/install.author` implementa código solo para AEM autor
   + `ui.content` integrado en `/apps/my-app-packages/content/install` implementa contenido y configuración tanto para AEM autor como para AEM publicación
   + `ui.content.publish` incrustado en `/apps/my-app-packages/content/install.publish` implementa contenido y configuración para AEM solo publicación

>[!TIP]
>
>Consulte la sección Fragmentos [XML de](#xml-embeddeds) POM más abajo para ver un fragmento completo.

### Definición de filtro del paquete de contenedor {#container-package-filter-definition}

Debido a la incrustación del código y los subpaquetes de contenido en el paquete de contenedor, las rutas de destinatario incrustadas deben agregarse a las del proyecto de contenedor `filter.xml` para garantizar que los paquetes incrustados se incluyen en el paquete de contenedor cuando se generan.

Simplemente agregue las `<filter root="/apps/<my-app>-packages"/>` entradas de las carpetas de segundo nivel que contengan subpaquetes para la implementación.

>[!TIP]
>
>Consulte la sección Fragmentos [XML de](#xml-container-package-filters) POM más abajo para ver un fragmento completo.

## Incrustación de paquetes de terceros {#embedding-3rd-party-packages}

Todos los paquetes deben estar disponibles a través del repositorio [público de artefactos Maven del](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) Adobe o de un repositorio de artefactos Maven público y accesible, referenciable por terceros.

Si los paquetes de terceros están en el repositorio **público de artefactos Maven de Adobe**, no se necesita ninguna configuración adicional para que Adobe Cloud Manager resuelva los artefactos.

Si los paquetes de terceros están en un **repositorio público de artefactos de terceros de Maven**, este repositorio debe estar registrado en el `pom.xml` del proyecto e incrustado según el método [descrito anteriormente](#embeddeds).

Los conectores/aplicaciones de terceros deben incrustarse utilizando su `all` paquete como contenedor en el paquete de contenedor (`all`) del proyecto.

Añadir las dependencias de Maven sigue las prácticas estándar de Maven, y la incrustación de artefactos de terceros (código y paquetes de contenido) se [describe más arriba](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte la sección Fragmentos [XML de](#xml-3rd-party-maven-repositories) POM más abajo para ver un fragmento completo.

## Dependencias de paquetes entre los `ui.apps` de `ui.content` paquetes {#package-dependencies}

Para garantizar la correcta instalación de los paquetes, se recomienda establecer dependencias entre paquetes.

La regla general es que los paquetes que contienen contenido mutable (`ui.content`) deben depender del código inmutable (`ui.apps`) que admite la representación y el uso del contenido mutable.

Una excepción notable a esta regla general es si el paquete de código inmutable (`ui.apps` o cualquier otro) __solo__ contiene paquetes OSGi. En caso afirmativo, ningún paquete AEM debe declarar una dependencia de él. Esto se debe a que los paquetes de código inmutables que __solo__ contienen paquetes OSGi no están registrados en AEM administrador de paquetes y, por lo tanto, cualquier paquete AEM que dependa de él tendrá una dependencia insatisfecha y no se podrá instalar.

>[!TIP]
>
>Consulte la sección Fragmentos [XML de](#xml-package-dependencies) POM más abajo para ver un fragmento completo.

Los patrones comunes para las dependencias de paquetes de contenido son:

### Dependencias del paquete de implementación simple {#simple-deployment-package-dependencies}

El caso simple define el paquete de contenido `ui.content` mutable para que dependa del paquete de código `ui.apps` inmutable.

+ `all` no tiene dependencias
   + `ui.apps` no tiene dependencias
   + `ui.content` depende de `ui.apps`

### Dependencias complejas del paquete de implementación {#complex-deploxment-package-dependencies}

Las implementaciones complejas se expanden en el caso simple y establecen dependencias entre el contenido mutable correspondiente y los paquetes de código inmutables. Si es necesario, también se pueden establecer dependencias entre paquetes de código inmutables.

+ `all` no tiene dependencias
   + `common.ui.apps.common` no tiene dependencias
   + `site-a.ui.apps` depende de `common.ui.apps`
   + `site-a.ui.content` depende de `site-a.ui.apps`
   + `site-b.ui.apps` depende de `common.ui.apps`
   + `site-b.ui.content` depende de `site-b.ui.apps`

## Desarrollo e implementación locales {#local-development-and-deployment}

Las estructuras y la organización del proyecto que se describen en este artículo son **totalmente compatibles** con los ejemplos de AEM de desarrollo local.

## Recortes XML de POM {#pom-xml-snippets}

Los siguientes son fragmentos de configuración Maven `pom.xml` que se pueden agregar a los proyectos Maven para alinearse con las recomendaciones anteriores.

### Tipos de paquetes {#xml-package-types}

Los paquetes de código y contenido, que se implementan como subpaquetes, deben declarar un tipo de paquete de **aplicación** o **contenido**, según lo que contengan.

#### Tipos de paquetes de contenedor {#container-package-types}

El proyecto contenedor `all/pom.xml` **no** declara un `<packageType>`.

#### Tipos de paquetes de código (inmutables) {#immutable-package-types}

Los paquetes de código deben configurar su `packageType` en `application`.

En la `ui.apps/pom.xml`, las directivas de configuración de `<packageType>application</packageType>` compilación de la declaración del `filevault-package-maven-plugin` complemento declaran su tipo de paquete.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.apps</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### Tipos de paquetes de contenido (mutables) {#mutable-package-types}

Los paquetes de contenido deben establecer su `packageType` valor en `content`.

En la `ui.content/pom.xml`, la directiva de configuración de `<packageType>content</packageType>` compilación de la declaración del `filevault-package-maven-plugin` complemento declara su tipo de paquete.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.content</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Marcado de paquetes para la implementación de Adobe Cloud Manager {#cloud-manager-target}

En todos los proyectos que generan un paquete, **excepto** en el proyecto de contenedor (`all`), agregue `<cloudManagerTarget>none</cloudManagerTarget>` a la configuración de la declaración del complemento `<properties>` para garantizar `filevault-package-maven-plugin` que Adobe Cloud Manager **no** los implementa. The container (`all`) package should be the singular package deployed via Cloud Manager, which in turn embeds all required code and content packages.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Tiempo de espera de repo{#snippet-repo-init}

Las secuencias de comandos Repo Init que contienen las secuencias de comandos Repo Init se definen en la configuración de fábrica de `RepositoryInitializer` OSGi mediante la `scripts` propiedad. Tenga en cuenta que, dado que estas secuencias de comandos se definen en las configuraciones de OSGi, se pueden crear fácilmente en el modo de ejecución utilizando la semántica de `../config.<runmode>` carpetas habitual.

Tenga en cuenta que, como las secuencias de comandos suelen ser declaraciones multilínea, es más fácil definirlas en el `.config` archivo que en el formato `.cfg.json` basado en JSON.

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

La propiedad `scripts` OSGi contiene directivas según la definición del lenguaje [](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)Repo de Apache Sling.

### Paquete de estructura de repositorio {#xml-repository-structure-package}

En `ui.apps/pom.xml` y en cualquier otro `pom.xml` que declare un paquete de código (`<packageType>application</packageType>`), agregue la siguiente configuración de paquete de estructura de repositorio al complemento FileVault Maven. Puede [crear su propio paquete de estructura de repositorio para su proyecto](repository-structure-package.md).

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### Incrustación de subpaquetes en el paquete de Contenedor {#xml-embeddeds}

En la `all/pom.xml`, agregue las siguientes `<embeddeds>` directivas a la declaración del `filevault-package-maven-plugin` complemento. Recuerde, **no** use la `<subPackages>` configuración, ya que esto incluirá los subpaquetes en `/etc/packages` lugar de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- OSGi Bundle Jar file that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.core</artifactId>
              <type>jar</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

           <!-- OSGi configuration code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.config</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### Definición de filtro del paquete de contenedor {#xml-container-package-filters}

En el `all` del proyecto `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`), **incluya** todas `-packages` las carpetas que contengan subpaquetes para implementar:

```xml
<filter root="/apps/my-app-packages"/>
```

Si `/apps/*-packages` se utilizan varios en los destinatarios incrustados, todos deben enumerarse aquí.

### Repositorios de muevos de terceros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Añadir más repositorios de Maven puede extender los tiempos de generación, ya que se comprobarán las dependencias de repositorios de Maven adicionales.

En el proyecto del reactor `pom.xml`, agregue las directivas de repositorio de Maven públicas de terceros necesarias. La configuración completa debe estar disponible `<repository>` desde el proveedor de repositorio de terceros.

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public 3rd Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### Dependencias de paquetes entre los `ui.apps` de `ui.content` paquetes {#xml-package-dependencies}

En la `ui.content/pom.xml`, agregue las siguientes `<dependencies>` directivas a la declaración del `filevault-package-maven-plugin` complemento.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### Limpieza de la carpeta de Destinatario del proyecto de Contenedor {#xml-clean-container-package}

En el `all/pom.xml` complemento agregue el `maven-clean-plugin` complemento que limpiará el directorio de destinatario antes de crear Maven.

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## Recursos adicionales {#additional-resources}

+ [Administración de paquetes con Maven](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html)
+ [Complemento Maven del paquete de contenido de FileVault](http://jackrabbit.apache.org/filevault-package-maven-plugin/)