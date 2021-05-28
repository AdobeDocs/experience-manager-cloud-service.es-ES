---
title: Estructura del proyecto AEM
description: Obtenga información sobre cómo definir estructuras de paquetes para la implementación en Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2869'
ht-degree: 13%

---

# Estructura del proyecto AEM

>[!TIP]
>
>Familiarícese con el [AEM tipo de archivo del proyecto básico use](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), y con el [complemento Maven de contenido de FileVault](/help/implementing/developing/tools/maven-plugin.md), ya que este artículo se basa en estos conocimientos y conceptos.

Este artículo describe los cambios necesarios para que los proyectos de Adobe Experience Manager Maven se AEM como Cloud Service compatibles, asegurándose de que respetan la división del contenido mutable e inmutable, las dependencias se establecen para crear implementaciones determinísticas y no conflictivas y que se empaquetan en una estructura implementable.

AEM implementaciones de aplicaciones deben estar formadas por un único paquete de AEM. Este paquete debe a su vez contener subpaquetes que incluyan todo lo que requiere la aplicación para funcionar, incluyendo código, configuración y cualquier contenido de línea de base compatible.

AEM requiere una separación de **contenido** y **código**, lo que significa que un paquete de contenido único **no puede** implementarse **en ambas instancias** `/apps` y en áreas de tiempo de ejecución (p. ej. `/content`, `/conf`, `/home` o cualquier cosa que no sea `/apps`) del repositorio. En su lugar, la aplicación debe separar el código y el contenido en paquetes discretos para su implementación en AEM.

La estructura del paquete descrita en este documento es compatible **tanto** con las implementaciones de desarrollo local, como con las implementaciones de AEM Cloud Service.

>[!TIP]
>
>Las configuraciones descritas en este documento las proporciona [AEM tipo de archivo del proyecto Maven 24 o posterior](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutables frente a inmutables del repositorio {#mutable-vs-immutable}

`/apps` y `/libs`**se consideran áreas inmutables de AEM, ya que no se pueden cambiar (crear, actualizar, eliminar) después de iniciarse AEM (es decir, durante la ejecución).** Cualquier intento de cambiar un área inmutable durante la ejecución fallará.

Todo lo demás en el repositorio, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc. son todas **áreas mutables**, lo que significa que se pueden cambiar durante la ejecución.

>[!WARNING]
>
>Como en versiones anteriores de AEM, `/libs` no debe modificarse. Solo AEM código de producto puede implementarse en `/libs`.

### Índices Oak {#oak-indexes}

Los índices Oak (`/oak:index`) son administrados específicamente por el AEM como proceso de implementación de Cloud Service. Esto se debe a que Cloud Manager debe esperar hasta que se implemente cualquier nuevo índice y se vuelva a indexar completamente antes de cambiar a la nueva imagen de código.

Por este motivo, aunque los índices Oak son mutables en tiempo de ejecución, deben implementarse como código para que puedan instalarse antes de instalar cualquier paquete mutable. Por lo tanto, las configuraciones de `/oak:index` son parte del paquete de código y no del paquete de contenido [como se describe a continuación](#recommended-package-structure).

>[!TIP]
>
>Para obtener más información sobre la indexación en AEM como Cloud Service, consulte el documento [Content Search and Indexing](/help/operations/indexing.md).

## Estructura del paquete recomendada {#recommended-package-structure}

![Estructura del paquete de proyecto del Experience Manager](assets/content-package-organization.png)

Este diagrama proporciona información general sobre la estructura del proyecto y los artefactos de implementación de paquetes recomendados.

La estructura de implementación de aplicaciones recomendada es la siguiente:

### Paquetes de código / Paquetes OSGi

+ El archivo Jar del paquete OSGi se genera y se incrusta directamente en el proyecto completo.

+ El paquete `ui.apps` contiene todo el código que se va a implementar y solo se implementa en `/apps`. Los elementos comunes del paquete `ui.apps` incluyen, entre otros:
   + [Definiciones de componentes y ](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=es) secuencias de comandos HTL
      + `/apps/my-app/components`
   + JavaScript y CSS (a través de [Client Libraries](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [](/help/implementing/developing/introduction/overlays.md) Superposición de  `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configuraciones de reserva según el contexto
      + `/apps/settings`
   + ACL (permisos)
      + Cualquier `rep:policy` para cualquier ruta en `/apps`

+ El paquete `ui.config` contiene todas las [configuraciones de OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Carpeta organizativa que contiene definiciones de configuración de OSGi específicas del modo de ejecución
      + `/apps/my-app/osgiconfig`
   + Carpeta de configuración común de OSGi que contiene configuraciones de OSGi predeterminadas que se aplican a todos los AEM de destino como destinos de implementación de Cloud Service
      + `/apps/my-app/osgiconfig/config`
   + Ejecute carpetas de configuración OSGi específicas del modo que contengan configuraciones OSGi predeterminadas que se aplican a todos los destinos de implementación de AEM como Cloud Service
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Secuencias de comandos de configuración de Repo Init OSGi
      + [Repositorio ](#repo-init) Inicia la forma recomendada de implementar contenido (mutable) que forma parte lógicamente de la aplicación AEM. Las configuraciones de OSGi de Repo Init deben estar situadas en la carpeta `config.<runmode>` adecuada, tal como se describe más arriba, y deben utilizarse para definir:
         + Estructuras de contenido de línea de base
         + Usuarios
         + Usuarios de servicio
         + Grupos
         + ACL (permisos)

>[!NOTE]
>
>El mismo código debe implementarse en todos los entornos. Esto es necesario para garantizar que también se esté produciendo un nivel de validaciones de confianza en el entorno de ensayo. Para obtener más información, consulte la sección sobre [Modos de ejecución](/help/implementing/deploying/overview.md#runmodes).


### Paquetes de contenido

+ El paquete `ui.content` contiene todo el contenido y la configuración. El paquete de contenido contiene todas las definiciones de nodo que no están en los paquetes `ui.apps` o `ui.config`, o en otras palabras, que no están en `/apps` o `/oak:index`. Los elementos comunes del paquete `ui.content` incluyen, entre otros:
   + Configuraciones según el contexto
      + `/conf`
   + Estructuras de contenido complejas y requeridas (por ejemplo, La creación de contenido que se basa en y extiende más allá de las estructuras de contenido de línea de base definidas en Repo Init).
      + `/content`,  `/content/dam`, etc.
   + Etiquetado regulado de taxonomías
      + `/content/cq:tags`
   + Nodos preexistentes, etc. (Idealmente, migre estos a ubicaciones que no sean/etc.)
      + `/etc`

### Paquetes de contenedores

+ El paquete `all` es un paquete de contenedor que SOLAMENTE incluye artefactos implementables, el archivo Jar del paquete OSGI, los paquetes `ui.apps`, `ui.config` y `ui.content` como incrustaciones. El paquete `all` no debe tener **ningún contenido o código** propio, sino delegar toda la implementación al repositorio a sus subpaquetes o archivos Jar del paquete OSGi.

   Los paquetes ahora se incluyen usando la configuración integrada del complemento Maven [FileVault Package Maven](#embeddeds), en lugar de la configuración `<subPackages>`.

   Para implementaciones de Experience Manager complejas, puede ser deseable crear varios `ui.apps`, `ui.config` y `ui.content` proyectos/paquetes que representen sitios o inquilinos específicos en AEM. Si esto se hace, asegúrese de que se respeta la división entre contenido mutable e inmutable, y que los paquetes de contenido requeridos y los archivos Jar del paquete OSGi están incrustados como subpaquetes en el paquete de contenido del contenedor `all` .

   Por ejemplo, una estructura de paquete de contenido de implementación compleja podría tener este aspecto:

   + `all` el paquete de contenido incrusta los siguientes paquetes para crear un único artefacto de implementación
      + `common.ui.apps` implementa el código requerido por el  **** sitio A y el sitio B
      + `site-a.core` Jar del paquete OSGi requerido por el sitio A
      + `site-a.ui.apps` implementa el código requerido por el sitio A
      + `site-a.ui.config` implementa las configuraciones de OSGi requeridas por el sitio A
      + `site-a.ui.content` implementa el contenido y la configuración requeridos por el sitio A
      + `site-b.core` Jar del paquete OSGi requerido por el sitio B
      + `site-b.ui.apps` implementa el código requerido por el sitio B
      + `site-b.ui.config` implementa las configuraciones de OSGi requeridas por el sitio B
      + `site-b.ui.content` implementa el contenido y la configuración requeridos por el sitio B

### Paquetes de aplicaciones adicionales{#extra-application-packages}

Si la implementación de AEM utiliza otros proyectos de AEM, que a su vez están compuestos por su propio código y paquetes de contenido, sus paquetes de contenedor deben integrarse en el paquete `all` del proyecto.

Por ejemplo, un proyecto de AEM que incluya 2 aplicaciones de AEM de proveedor podría tener el siguiente aspecto:

+ `all` el paquete de contenido incrusta los siguientes paquetes para crear un único artefacto de implementación
   + `core` Jar del paquete OSGi requerido por la aplicación AEM
   + `ui.apps` implementa el código requerido por la aplicación AEM
   + `ui.config` implementa las configuraciones de OSGi requeridas por la aplicación AEM
   + `ui.content` implementa el contenido y la configuración requeridos por la aplicación AEM
   + `vendor-x.all` implementa todo (código y contenido) necesario para la aplicación de proveedor X
   + `vendor-y.all` implementa todo (código y contenido) necesario para la aplicación Y del proveedor

## Tipos de paquetes {#package-types}

Los paquetes deben marcarse con su tipo de paquete declarado.

+ Los paquetes de contenedores deben establecer su `packageType` en `container`. Los paquetes de contenedores no deben contener directamente paquetes OSGi, configuraciones OSGi y no se les permite utilizar [enlaces de instalación](http://jackrabbit.apache.org/filevault/installhooks.html).
+ Los paquetes de código (inmutables) deben establecer su `packageType` en `application`.
+ Los paquetes de contenido (mutables) deben establecer su `packageType` en `content`.


Para obtener más información, consulte la [documentación del Apache Jackrabbit FileVault - Package Maven Plugin](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) y el [fragmento de configuración de FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) a continuación.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-package-types) a continuación para obtener un fragmento completo.

## Marcado de paquetes para la implementación por Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

De forma predeterminada, Adobe Cloud Manager obtiene todos los paquetes producidos por la compilación de Maven; sin embargo, dado que el paquete de contenedor (`all`) es el único artefacto de implementación que contiene todos los paquetes de contenido y código, debemos asegurarnos de que **solo** se implementa el paquete de contenedor (`all`). Para garantizar esto, otros paquetes que genera la compilación de Maven deben marcarse con la configuración del complemento Maven del paquete de contenido de FileVault `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#pom-xml-snippets) a continuación para obtener un fragmento completo.

## Init. repo{#repo-init}

Repo Init proporciona instrucciones, o secuencias de comandos, que definen estructuras JCR, desde estructuras de nodos comunes como árboles de carpetas, hasta usuarios, usuarios de servicios, grupos y definición de ACL.

Las ventajas clave de Repo Init son que tienen permisos implícitos para realizar todas las acciones definidas por sus secuencias de comandos y se invocan al principio del ciclo de vida de la implementación, lo que garantiza que el código de tiempo ejecute todas las estructuras JCR necesarias.

Aunque las secuencias de comandos Repo Init se encuentran en el proyecto `ui.config` como secuencias de comandos, pueden y deben utilizarse para definir las siguientes estructuras mutables:

+ Estructuras de contenido de línea de base
+ Usuarios de servicio
+ Usuarios
+ Grupos
+ ACL

Los scripts de inicio de repositorios se almacenan como entradas `scripts` de `RepositoryInitializer` configuraciones de fábrica de OSGi y, por lo tanto, pueden ser dirigidos implícitamente por el modo de ejecución, lo que permite diferencias entre los scripts de inicio de repo de AEM Author y AEM Publish Services, o incluso entre entornos (Dev, Stage y Prod).

Las configuraciones OSGi de Repo Init se escriben mejor en el [`.config` formato de configuración OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) ya que admiten líneas múltiples, lo que supone una excepción a las prácticas recomendadas de usar [`.cfg.json` para definir configuraciones OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Tenga en cuenta que al definir Usuarios, y Grupos, solo los grupos se consideran parte de la aplicación, y la parte integral de su función debe definirse aquí. Los usuarios y grupos de organización deben seguir definidos durante la ejecución en AEM. por ejemplo, si un flujo de trabajo personalizado asigna trabajo a un grupo con nombre, ese grupo debe definirse en mediante Repo Init en la aplicación AEM; sin embargo, si el grupo es meramente organizativo, como &quot;Wendy&#39;s Team&quot; y &quot;Sean&#39;s Team&quot;, estos se definen mejor y se administran durante la ejecución en AEM.

>[!TIP]
>
>Los scripts de inicio de repositorios *deben* definirse en el campo en línea `scripts` y la configuración `references` no funcionará.

El vocabulario completo para las secuencias de comandos Repo Init está disponible en la [documentación de Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulte la sección [Repo Init Snippets](#snippet-repo-init) a continuación para ver un fragmento completo.

## Paquete de estructura del repositorio {#repository-structure-package}

Los paquetes de código requieren configurar la configuración del complemento FileVault Maven para hacer referencia a un `<repositoryStructurePackage>` que exige la corrección de las dependencias estructurales (para garantizar que un paquete de código no se instale sobre otro). Puede [crear su propio paquete de estructura de repositorio para su proyecto](repository-structure-package.md).

Esto **solo es necesario** para los paquetes de código, es decir, cualquier paquete marcado con `<packageType>application</packageType>`.

Para aprender a crear un paquete de estructura de repositorios para su aplicación, consulte [Desarrollo de un paquete de estructura de repositorios](repository-structure-package.md).

Tenga en cuenta que los paquetes de contenido (`<packageType>content</packageType>`) **no** requieren este paquete de estructura de repositorio.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-repository-structure-package) a continuación para obtener un fragmento completo.

## Incrustación de subpaquetes en el paquete de contenedor{#embeddeds}

Los paquetes de contenido o código se colocan en una carpeta especial &quot;coche secundario&quot; y se pueden dirigir para su instalación en AEM autor, AEM publicación o en ambos, mediante la configuración `<embeddeds>` del complemento FileVault Maven. Tenga en cuenta que la configuración `<subPackages>` no debe usarse.

Los casos de uso comunes incluyen:

+ ACL/permisos que difieren entre usuarios AEM autores y usuarios AEM publicación
+ Configuraciones que se usan para admitir actividades solo en AEM autor
+ Código como integraciones con sistemas de back-office, solo necesario para ejecutarse en AEM autor

![Incrustación de paquetes](assets/embeddeds.png)

Para dirigirse AEM autor, AEM publicar o ambos, el paquete está incrustado en el paquete de contenedor `all` en una ubicación de carpeta especial, con el siguiente formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Desglosar esta estructura de carpetas:

+ La carpeta de primer nivel **debe ser** `/apps`.
+ La carpeta de segundo nivel representa la aplicación con `-packages` posfijo en el nombre de la carpeta. A menudo solo hay una carpeta de segundo nivel en la que se incrustan todos los subpaquetes, aunque se puede crear cualquier número de carpetas de segundo nivel para representar mejor la estructura lógica de la aplicación:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >De forma predeterminada, las carpetas incrustadas de subpaquetes reciben el nombre del sufijo de `-packages`. Esto garantiza que el código de implementación y los paquetes de contenido **no se implementen** en las carpetas de destino de ningún subpaquete `/apps/<app-name>/...` que tenga como resultado un comportamiento de instalación destructivo y cíclico.

+ La carpeta de tercer nivel debe ser
   `application`,  `content` o  `container`
   + La carpeta `application` contiene paquetes de código
   + La carpeta `content` contiene paquetes de contenido
   + La carpeta `container` contiene los [paquetes de aplicaciones adicionales](#extra-application-packages) que podría incluir la aplicación AEM.
Este nombre de carpeta corresponde a los [tipos de paquete](#package-types) de los paquetes que contiene.
+ La carpeta de cuarto nivel contiene los subpaquetes y debe ser uno de los siguientes:
   + `install` para realizar la instalación en **AEM Author y AEM Publish**
   + `install.author` para instalar **solo** en AEM Author
   + `install.publish` para instalar  **** solo en AEM publicación Tenga en cuenta que solo  `install.author` y  `install.publish` son destinatarios admitidos. Otros modos de ejecución **no son** compatibles.

Por ejemplo, una implementación que contenga AEM autor y publique paquetes específicos puede tener el siguiente aspecto:

+ `all` El paquete de contenedor incrusta los siguientes paquetes para crear un único artefacto de implementación
   + `ui.apps` incrustado en  `/apps/my-app-packages/application/install` implementa código tanto AEM autor como AEM publicación
   + `ui.apps.author` incrustado en  `/apps/my-app-packages/application/install.author` implementa código solo para AEM autor
   + `ui.content` incrustado en  `/apps/my-app-packages/content/install` implementa contenido y configuración tanto para AEM autor como para AEM publicación
   + `ui.content.publish` incrustado en  `/apps/my-app-packages/content/install.publish` implementa contenido y configuración para publicar solamente AEM

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-embeddeds) a continuación para obtener un fragmento completo.

### Definición de filtro del paquete de contenedor {#container-package-filter-definition}

Debido a la incrustación del código y los subpaquetes de contenido en el paquete de contenedor, las rutas de destino incrustadas deben agregarse al `filter.xml` del proyecto de contenedor para garantizar que los paquetes incrustados se incluyen en el paquete de contenedor cuando se crean.

Simplemente añada las entradas `<filter root="/apps/<my-app>-packages"/>` para cualquier carpeta de segundo nivel que contenga subpaquetes que desee implementar.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-container-package-filters) a continuación para obtener un fragmento completo.

## Incrustación de paquetes de terceros {#embedding-3rd-party-packages}

Todos los paquetes deben estar disponibles a través del [repositorio público de artefactos Maven](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) del Adobe o a través de un repositorio público de artefactos Maven de terceros referenciable y accesible.

Si los paquetes de terceros están en el repositorio **público de artefactos Maven de Adobe**, no se necesita ninguna configuración adicional para que Adobe Cloud Manager resuelva los artefactos.

Si los paquetes de terceros están en un **repositorio público de artefactos de terceros de Maven**, este repositorio debe estar registrado en el `pom.xml` del proyecto e incrustado según el método [descrito anteriormente](#embeddeds).

Los conectores/aplicaciones de terceros deben incrustarse utilizando su paquete `all` como contenedor en el paquete de contenedor (`all`) del proyecto.

Añadir dependencias Maven sigue las prácticas estándar de Maven, y la incrustación de artefactos de terceros (paquetes de contenido y código) se [describe más arriba](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-3rd-party-maven-repositories) a continuación para obtener un fragmento completo.

## Dependencias del paquete entre los `ui.apps` de `ui.content` paquetes {#package-dependencies}

Para garantizar la correcta instalación de los paquetes, se recomienda establecer dependencias entre paquetes.

La regla general es que los paquetes que contienen contenido mutable (`ui.content`) deben depender del código inmutable (`ui.apps`) que admita la renderización y el uso del contenido mutable.

Una excepción notable a esta regla general es si el paquete de código inmutable (`ui.apps` o cualquier otro), __only__ contiene paquetes OSGi. Si es así, ningún paquete AEM debe declarar una dependencia de él. Esto se debe a que los paquetes de código inmutables __only__ que contienen paquetes OSGi no están registrados con AEM Administrador de paquetes y, por lo tanto, cualquier paquete de AEM que dependa de él tendrá una dependencia insatisfecha y no podrá instalarse.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-package-dependencies) a continuación para obtener un fragmento completo.

Los patrones comunes para las dependencias de paquetes de contenido son:

### Dependencias simples de paquetes de implementación {#simple-deployment-package-dependencies}

El caso simple define el paquete de contenido mutable `ui.content` para que dependa del paquete de código inmutable `ui.apps` .

+ `all` no tiene dependencias
   + `ui.apps` no tiene dependencias
   + `ui.content` depende de  `ui.apps`

### Dependencias complejas del paquete de implementación {#complex-deploxment-package-dependencies}

Las implementaciones complejas se expanden en el caso simple y establecen dependencias entre el contenido mutable correspondiente y los paquetes de código inmutables. Si es necesario, también se pueden establecer dependencias entre paquetes de código inmutables.

+ `all` no tiene dependencias
   + `common.ui.apps.common` no tiene dependencias
   + `site-a.ui.apps` depende de  `common.ui.apps`
   + `site-a.ui.content` depende de  `site-a.ui.apps`
   + `site-b.ui.apps` depende de  `common.ui.apps`
   + `site-b.ui.content` depende de  `site-b.ui.apps`

## Desarrollo local e implementación {#local-development-and-deployment}

Las estructuras y la organización del proyecto que se describen en este artículo son **instancias de AEM de desarrollo local totalmente compatibles**.

## Fragmentos XML de POM {#pom-xml-snippets}

A continuación se muestran los fragmentos de configuración `pom.xml` de Maven que se pueden agregar a los proyectos de Maven para alinearlos con las recomendaciones anteriores.

### Tipos de paquetes {#xml-package-types}

Los paquetes de código y contenido, que se implementan como subpaquetes, deben declarar un tipo de paquete de **aplicación** o **contenido**, según lo que contengan.

#### Tipos de paquetes de contenedores {#container-package-types}

El proyecto `all/pom.xml` **del contenedor** no declara `<packageType>`.

#### Tipos de paquetes de código (inmutables) {#immutable-package-types}

Los paquetes de código deben establecer su `packageType` en `application`.

En `ui.apps/pom.xml`, las `<packageType>application</packageType>` directivas de configuración de compilación de la declaración del complemento `filevault-package-maven-plugin` declaran su tipo de paquete.

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

Los paquetes de contenido deben establecer su `packageType` en `content`.

En `ui.content/pom.xml`, la directiva de configuración de compilación `<packageType>content</packageType>` de la declaración del complemento `filevault-package-maven-plugin` declara su tipo de paquete.

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

En todos los proyectos que generan un paquete, **excepto** en el proyecto de contenedor (`all`), agregue `<cloudManagerTarget>none</cloudManagerTarget>` a la configuración de la declaración del complemento `<properties>` para garantizar `filevault-package-maven-plugin` que Adobe Cloud Manager **no** los implementa. El paquete de contenedor (`all`) debe ser el paquete singular implementado mediante Cloud Manager, que a su vez incorpora todos los paquetes de contenido y código necesarios.

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

### Init. repo{#snippet-repo-init}

Las secuencias de comandos Repo Init que contienen las secuencias de comandos Repo Init se definen en la configuración de fábrica de OSGi `RepositoryInitializer` a través de la propiedad `scripts`. Tenga en cuenta que, dado que estas secuencias de comandos se definen dentro de las configuraciones de OSGi, se pueden crear ámbitos fácilmente mediante el modo de ejecución utilizando la semántica de carpeta habitual `../config.<runmode>`.

Tenga en cuenta que, como los scripts suelen ser de declaración multilínea, es más fácil definirlos en el archivo `.config` que en el formato `.cfg.json` basado en JSON.

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

La propiedad `scripts` OSGi contiene directivas como se define en el [lenguaje Repo Init de Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Paquete de estructura del repositorio {#xml-repository-structure-package}

En `ui.apps/pom.xml` y cualquier otro `pom.xml` que declara un paquete de código (`<packageType>application</packageType>`), agregue la siguiente configuración del paquete de estructura del repositorio al complemento Maven de FileVault. Puede [crear su propio paquete de estructura de repositorio para su proyecto](repository-structure-package.md).

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

### Incrustación de subpaquetes en el paquete de contenedor {#xml-embeddeds}

En `all/pom.xml`, agregue las siguientes `<embeddeds>` directivas a la declaración del complemento `filevault-package-maven-plugin`. Recuerde, **no** utiliza la configuración `<subPackages>`, ya que esto incluirá los subpaquetes en `/etc/packages` en lugar de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

Si se utilizan varios `/apps/*-packages` en los objetivos incrustados, todos deben enumerarse aquí.

### Repositorios Maven de terceros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Añadir más repositorios Maven puede ampliar los tiempos de compilación de maven, ya que se buscarán dependencias en los repositorios Maven adicionales.

En el `pom.xml` del proyecto del reactor, agregue las directivas de repositorio Maven públicas de terceros necesarias. La configuración completa `<repository>` debe estar disponible en el proveedor de repositorios de terceros.

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

### Dependencias del paquete entre los `ui.apps` de `ui.content` paquetes {#xml-package-dependencies}

En `ui.content/pom.xml`, agregue las siguientes `<dependencies>` directivas a la declaración del complemento `filevault-package-maven-plugin`.

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

### Limpieza de la carpeta de destino del proyecto de contenedor {#xml-clean-container-package}

En `all/pom.xml` agregue el complemento `maven-clean-plugin` que limpiará el directorio de destino antes de las compilaciones de Maven.

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

+ [Administración de paquetes con Maven](/help/implementing/developing/tools/maven-plugin.md)
+ [Complemento Maven del paquete de contenido de FileVault](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
