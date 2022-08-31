---
title: Estructura del proyecto AEM
description: Obtenga información sobre cómo definir estructuras de paquetes para la implementación en Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '2930'
ht-degree: 13%

---

# Estructura del proyecto AEM

>[!TIP]
>
>Familiarícese con básico [Uso del tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)y [Complemento Maven de contenido de FileVault](/help/implementing/developing/tools/maven-plugin.md) a medida que este artículo se basa en estas lecciones y conceptos.

Este artículo describe los cambios necesarios para que los proyectos de Adobe Experience Manager Maven sean AEM compatibles de forma as a Cloud Service, asegurándose de que respeten la división del contenido mutable e inmutable, de que las dependencias se establezcan para crear implementaciones determinísticas y no conflictivas y de que se empaqueten en una estructura implementable.

AEM implementaciones de aplicaciones deben estar formadas por un único paquete de AEM. Este paquete debe a su vez contener subpaquetes que incluyan todo lo que requiere la aplicación para funcionar, incluyendo código, configuración y cualquier contenido de línea de base compatible.

AEM requiere una separación de **contenido** y **código**, lo que significa que un paquete de contenido único **no puede** implementarse **en ambas instancias** `/apps` y en áreas de tiempo de ejecución (p. ej. `/content`, `/conf`, `/home` o cualquier cosa que no sea `/apps`) del repositorio. En su lugar, la aplicación debe separar el código y el contenido en paquetes discretos para su implementación en AEM.

La estructura del paquete descrita en este documento es compatible **tanto** con las implementaciones de desarrollo local, como con las implementaciones de AEM Cloud Service.

>[!TIP]
>
>Las configuraciones descritas en este documento son proporcionadas por [AEM tipo de archivo Maven del proyecto 24 o posterior](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutables frente a inmutables del repositorio {#mutable-vs-immutable}

`/apps` y `/libs`**se consideran áreas inmutables de AEM, ya que no se pueden cambiar (crear, actualizar, eliminar) después de iniciarse AEM (es decir, durante la ejecución).** Cualquier intento de cambiar un área inmutable durante la ejecución fallará.

Todo lo demás en el repositorio, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc. son todos **mutable** , lo que significa que se pueden cambiar durante la ejecución.

>[!WARNING]
>
>Como en versiones anteriores de AEM, `/libs` no debe modificarse. Solo AEM código de producto puede implementarse en `/libs`.

### Índices Oak {#oak-indexes}

Índices de Oak (`/oak:index`) se administran específicamente mediante el proceso de implementación as a Cloud Service de AEM. Esto se debe a que Cloud Manager debe esperar hasta que se implemente cualquier nuevo índice y se vuelva a indexar completamente antes de cambiar a la nueva imagen de código.

Por este motivo, aunque los índices Oak son mutables en tiempo de ejecución, deben implementarse como código para que puedan instalarse antes de instalar cualquier paquete mutable. Por lo tanto, `/oak:index` las configuraciones forman parte del paquete de código y no del paquete de contenido [tal como se describe a continuación](#recommended-package-structure).

>[!TIP]
>
>Para obtener más información sobre la indexación en AEM as a Cloud Service, consulte el documento [Búsqueda de contenido e indexación](/help/operations/indexing.md).

## Estructura del paquete recomendado {#recommended-package-structure}

![Estructura del paquete de proyecto del Experience Manager](assets/content-package-organization.png)

Este diagrama proporciona información general sobre la estructura del proyecto y los artefactos de implementación de paquetes recomendados.

La estructura de implementación de aplicaciones recomendada es la siguiente:

### Paquetes de código / Paquetes OSGi

+ El archivo Jar del paquete OSGi se genera y se incrusta directamente en el proyecto completo.

+ La variable `ui.apps` contiene todo el código que se va a implementar y solo se implementa en `/apps`. Elementos comunes del `ui.apps` incluye, pero no se limita a:
   + [Definiciones de componentes y HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=es) scripts
      + `/apps/my-app/components`
   + JavaScript y CSS (a través de [Bibliotecas de cliente](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Superposiciones](/help/implementing/developing/introduction/overlays.md) de `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configuraciones de reserva según el contexto
      + `/apps/settings`
   + ACL (permisos)
      + Cualquiera `rep:policy` para cualquier ruta bajo `/apps`
   + [Secuencias de comandos agrupadas precompiladas](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>El mismo código debe implementarse en todos los entornos. Esto es necesario para garantizar que también se esté produciendo un nivel de validaciones de confianza en el entorno de ensayo. Para obtener más información, consulte la sección sobre [Modos de ejecución](/help/implementing/deploying/overview.md#runmodes).


### Paquetes de contenido

+ La variable `ui.content` contiene todo el contenido y la configuración. El paquete de contenido contiene todas las definiciones de nodo que no están en la `ui.apps` o `ui.config` paquetes, o en otras palabras, cualquier cosa que no esté en `/apps` o `/oak:index`. Elementos comunes del `ui.content` incluye, pero no se limita a:
   + Configuraciones según el contexto
      + `/conf`
   + Estructuras de contenido complejas y requeridas (por ejemplo, Generación de contenido que se basa en las estructuras de contenido de línea de base definidas en Repo Init y las extiende más allá de ellas).
      + `/content`, `/content/dam`, etc.
   + Etiquetado regulado de taxonomías
      + `/content/cq:tags`
   + Nodos preexistentes, etc. (Idealmente, migre estos a ubicaciones que no sean/etc.)
      + `/etc`

### Paquetes de contenedores

+ La variable `all` es un paquete de contenedor que SOLAMENTE incluye artefactos implementables, el archivo Jar del paquete OSGI, `ui.apps`, `ui.config` y `ui.content` paquetes como incrustaciones. La variable `all` el paquete no debe tener **cualquier contenido o código** por su cuenta, pero delega toda la implementación en el repositorio a sus subpaquetes o archivos Jar del paquete OSGi.

   Los paquetes ahora se incluyen utilizando Maven [Configuración integrada del complemento Maven del paquete FileVault](#embeddeds), en lugar de `<subPackages>` configuración.

   Para implementaciones de Experience Manager complejas, puede ser deseable crear varias `ui.apps`, `ui.config` y `ui.content` proyectos/paquetes que representan sitios específicos o inquilinos en AEM. Si esto se hace, asegúrese de que se respeta la división entre contenido mutable e inmutable, y que los paquetes de contenido requeridos y los archivos Jar del paquete OSGi están incrustados como subpaquetes en la variable `all` paquete de contenido del contenedor.

   Por ejemplo, una estructura de paquete de contenido de implementación compleja podría tener este aspecto:

   + `all` el paquete de contenido incrusta los siguientes paquetes para crear un único artefacto de implementación
      + `common.ui.apps` implementa el código requerido por **both** sitio A y sitio B
      + `site-a.core` Jar del paquete OSGi requerido por el sitio A
      + `site-a.ui.apps` implementa el código requerido por el sitio A
      + `site-a.ui.config` implementa las configuraciones de OSGi requeridas por el sitio A
      + `site-a.ui.content` implementa el contenido y la configuración requeridos por el sitio A
      + `site-b.core` Jar del paquete OSGi requerido por el sitio B
      + `site-b.ui.apps` implementa el código requerido por el sitio B
      + `site-b.ui.config` implementa las configuraciones de OSGi requeridas por el sitio B
      + `site-b.ui.content` implementa el contenido y la configuración requeridos por el sitio B

+ La variable `ui.config` contiene todo [Configuraciones de OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Se considera código y pertenece a paquetes OSGi, pero no contiene nodos de contenido normales. Por lo tanto, está marcado como un paquete de contenedor
   + Carpeta organizativa que contiene definiciones de configuración de OSGi específicas del modo de ejecución
      + `/apps/my-app/osgiconfig`
   + Carpeta de configuración común de OSGi que contiene configuraciones de OSGi predeterminadas que se aplican a todos los destinos de implementación as a Cloud Service de AEM de destino
      + `/apps/my-app/osgiconfig/config`
   + Ejecute carpetas de configuración OSGi específicas del modo que contengan configuraciones OSGi predeterminadas que se aplican a todos los destinos de implementación as a Cloud Service AEM destino
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Secuencias de comandos de configuración de Repo Init OSGi
      + [Punto de repo](#repo-init) es la forma recomendada de implementar contenido (mutable) que forma parte lógicamente de la aplicación AEM. Las configuraciones de OSGi de Repo Init deben ser lugares en el lugar apropiado `config.<runmode>` como se describe anteriormente, y se utilizará para definir:
         + Estructuras de contenido de línea de base
         + Usuarios
         + Usuarios de servicio
         + Grupos
         + ACL (permisos)

### Paquetes de aplicaciones adicionales{#extra-application-packages}

Si la implementación de AEM utiliza otros proyectos de AEM, que a su vez están formados por su propio código y paquetes de contenido, sus paquetes de contenedor deberían incrustarse en el `all` paquete.

Por ejemplo, un proyecto de AEM que incluya 2 aplicaciones de AEM de proveedor podría tener el siguiente aspecto:

+ `all` el paquete de contenido incrusta los siguientes paquetes para crear un único artefacto de implementación
   + `core` Jar del paquete OSGi requerido por la aplicación AEM
   + `ui.apps` implementa el código requerido por la aplicación AEM
   + `ui.config` implementa las configuraciones de OSGi requeridas por la aplicación AEM
   + `ui.content` implementa el contenido y la configuración requeridos por la aplicación AEM
   + `vendor-x.all` implementa todo (código y contenido) necesario para la aplicación de proveedor X
   + `vendor-y.all` implementa todo (código y contenido) necesario para la aplicación Y del proveedor

## Tipos de paquetes {#package-types}

Los paquetes deben marcarse con su tipo de paquete declarado. Los tipos de paquetes ayudan a aclarar el propósito y la implementación de un paquete.

+ Los paquetes de contenedores deben configurar su `packageType` a `container`. Los paquetes de contenedores no deben contener nodos regulares. Solo se permiten paquetes, configuraciones y subpaquetes OSGi. No se permite el uso de contenedores en AEM as a Cloud Service [instalar enlaces](https://jackrabbit.apache.org/filevault/installhooks.html).
+ Los paquetes de código (inmutables) deben configurar sus `packageType` a `application`.
+ Los paquetes de contenido (mutables) deben configurar sus `packageType` a `content`.


Para obtener más información, consulte [Apache Jackrabbit FileVault: Documentación del complemento Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Tipos de paquetes de Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html)y [Fragmento de configuración Maven de FileVault](#marking-packages-for-deployment-by-adoube-cloud-manager) más abajo.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-package-types) para ver un fragmento completo.

## Marcado de paquetes para la implementación por Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

De forma predeterminada, Adobe Cloud Manager obtiene todos los paquetes producidos por la compilación de Maven; sin embargo, dado que el paquete de contenedor (`all`) es el único artefacto de implementación que contiene todos los paquetes de contenido y código, debemos asegurarnos de que **solo** se implementa el paquete de contenedor (`all`). Para garantizar esto, otros paquetes que genera la compilación de Maven deben marcarse con la configuración del complemento Maven del paquete de contenido de FileVault `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#pom-xml-snippets) para ver un fragmento completo.

## Punto de repo{#repo-init}

Repo Init proporciona instrucciones, o secuencias de comandos, que definen estructuras JCR, desde estructuras de nodos comunes como árboles de carpetas, hasta usuarios, usuarios de servicios, grupos y definición de ACL.

Las ventajas clave de Repo Init son que tienen permisos implícitos para realizar todas las acciones definidas por sus secuencias de comandos y se invocan al principio del ciclo de vida de la implementación, lo que garantiza que el código de tiempo ejecute todas las estructuras JCR necesarias.

Mientras que los scripts de Init de Repo viven en el `ui.config` como secuencias de comandos, pueden y deben utilizarse para definir las siguientes estructuras mutables:

+ Estructuras de contenido de línea de base
+ Usuarios de servicio
+ Usuarios
+ Grupos
+ ACL

Los scripts de inicio de repositorios se almacenan como `scripts` entradas de `RepositoryInitializer` Las configuraciones de fábrica de OSGi, y por lo tanto, pueden ser dirigidas implícitamente por el modo de ejecución, lo que permite diferencias entre los scripts de inicio de repo de AEM Author y AEM Publish Services, o incluso entre entornos (Dev, Stage y Prod).

Las configuraciones de OSGi de Repo Init se escriben mejor en el [`.config` Formato de configuración OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) ya que admiten líneas múltiples, lo que supone una excepción a las prácticas recomendadas de [`.cfg.json` para definir las configuraciones de OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Tenga en cuenta que al definir Usuarios, y Grupos, solo los grupos se consideran parte de la aplicación, y la parte integral de su función debe definirse aquí. Los usuarios y grupos de organización deben seguir definidos durante la ejecución en AEM. por ejemplo, si un flujo de trabajo personalizado asigna trabajo a un grupo con nombre, ese grupo debe definirse en mediante Repo Init en la aplicación AEM; sin embargo, si el grupo es meramente organizativo, como &quot;Wendy&#39;s Team&quot; y &quot;Sean&#39;s Team&quot;, estos se definen mejor y se administran durante la ejecución en AEM.

>[!TIP]
>
>Secuencias de comandos de inicio de repositorios *must* se definirá en línea `scripts` y la variable `references` no funcionará.

El vocabulario completo de los scripts de inicio de repo está disponible en la [Documentación de Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulte la [Fragmentos de entrada de repositorios](#snippet-repo-init) para ver un fragmento completo.

## Paquete de estructura del repositorio {#repository-structure-package}

Los paquetes de código requieren la configuración del complemento FileVault Maven para hacer referencia a un `<repositoryStructurePackage>` que exige la corrección de las dependencias estructurales (para garantizar que un paquete de código no se instale sobre otro). Puede [cree su propio paquete de estructura de repositorio para su proyecto](repository-structure-package.md).

Esto **solo es necesario** para los paquetes de código, es decir, cualquier paquete marcado con `<packageType>application</packageType>`.

Para aprender a crear un paquete de estructura de repositorios para su aplicación, consulte [Desarrollo de un paquete de estructura de repositorio](repository-structure-package.md).

Tenga en cuenta que los paquetes de contenido (`<packageType>content</packageType>`) **no** requiere este paquete de estructura de repositorio.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-repository-structure-package) para ver un fragmento completo.

## Incrustación de subpaquetes en el paquete de contenedor{#embeddeds}

Los paquetes de contenido o código se colocan en una carpeta especial &quot;coche secundario&quot; y se pueden dirigir para su instalación en AEM autor, AEM publicación o ambos, mediante el complemento Maven de FileVault `<embeddeds>` configuración. Tenga en cuenta que `<subPackages>` no debe utilizarse.

Los casos de uso comunes incluyen:

+ ACL/permisos que difieren entre usuarios AEM autores y usuarios AEM publicación
+ Configuraciones que se usan para admitir actividades solo en AEM autor
+ Código como integraciones con sistemas de back-office, solo necesario para ejecutarse en AEM autor

![Incrustación de paquetes](assets/embeddeds.png)

Para dirigirse AEM autor, AEM publicar o ambos, el paquete está incrustado en el `all` paquete de contenedor en una ubicación de carpeta especial, en el siguiente formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Desglosar esta estructura de carpetas:

+ La carpeta de primer nivel **debe** `/apps`.
+ La carpeta de segundo nivel representa la aplicación con `-packages` se corrigió posteriormente al nombre de la carpeta. A menudo solo hay una carpeta de segundo nivel en la que se incrustan todos los subpaquetes, aunque se puede crear cualquier número de carpetas de segundo nivel para representar mejor la estructura lógica de la aplicación:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >De forma predeterminada, las carpetas incrustadas de subpaquetes reciben el nombre del sufijo de `-packages`. Esto garantiza que el código de implementación y los paquetes de contenido **no se implementen** en las carpetas de destino de ningún subpaquete `/apps/<app-name>/...` que tenga como resultado un comportamiento de instalación destructivo y cíclico.

+ La carpeta de tercer nivel debe ser
   `application`, `content` o `container`
   + La variable `application` la carpeta contiene paquetes de código
   + La variable `content` la carpeta contiene paquetes de contenido
   + La variable `container` la carpeta contiene cualquier [paquetes de aplicaciones adicionales](#extra-application-packages) que podría incluir la aplicación AEM.
Este nombre de carpeta corresponde a la variable [tipos de paquetes](#package-types) de los paquetes que contiene.
+ La carpeta de cuarto nivel contiene los subpaquetes y debe ser uno de los siguientes:
   + `install` para realizar la instalación en **AEM Author y AEM Publish**
   + `install.author` para instalar **solo** en AEM Author
   + `install.publish` a **only** instalar en AEM publicación Tenga en cuenta que solo `install.author` y `install.publish` son objetivos admitidos. Otros modos de ejecución **no son** compatibles.

Por ejemplo, una implementación que contenga AEM autor y publique paquetes específicos puede tener el siguiente aspecto:

+ `all` El paquete de contenedor incrusta los siguientes paquetes para crear un único artefacto de implementación
   + `ui.apps` incrustado en `/apps/my-app-packages/application/install` implementa código tanto para AEM autor como para AEM publicación
   + `ui.apps.author` incrustado en `/apps/my-app-packages/application/install.author` implementa código solo para AEM autor
   + `ui.content` incrustado en `/apps/my-app-packages/content/install` implementa contenido y configuración tanto para AEM autor como para AEM publicación
   + `ui.content.publish` incrustado en `/apps/my-app-packages/content/install.publish` implementa contenido y configuración para publicar solamente AEM

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-embeddeds) para ver un fragmento completo.

### Definición del filtro del paquete de contenedor {#container-package-filter-definition}

Debido a la incrustación de subpaquetes de contenido y código en el paquete de contenedor, las rutas de destino incrustadas deben agregarse al proyecto de contenedor `filter.xml` para garantizar que los paquetes incrustados se incluyen en el paquete de contenedor cuando se crean.

Simplemente agregue la variable `<filter root="/apps/<my-app>-packages"/>` para cualquier carpeta de segundo nivel que contenga subpaquetes que se van a implementar.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-container-package-filters) para ver un fragmento completo.

## Incrustación de paquetes de terceros {#embedding-3rd-party-packages}

Todos los paquetes deben estar disponibles a través de la variable [Repositorio público de artefactos Maven del Adobe](https://repo1.maven.org/maven2/com/adobe/) o un repositorio de artefactos Maven de terceros accesible público, referenciable y accesible.

Si los paquetes de terceros están en el repositorio **público de artefactos Maven de Adobe**, no se necesita ninguna configuración adicional para que Adobe Cloud Manager resuelva los artefactos.

Si los paquetes de terceros están en un **repositorio público de artefactos de terceros de Maven**, este repositorio debe estar registrado en el `pom.xml` del proyecto e incrustado según el método [descrito anteriormente](#embeddeds).

Los conectores/aplicaciones de terceros deben incrustarse utilizando su `all` paquete como contenedor en el contenedor de su proyecto (`all`).

La adición de dependencias Maven sigue las prácticas estándar de Maven y la incrustación de artefactos de terceros (paquetes de contenido y código) son [descrito anteriormente](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-3rd-party-maven-repositories) para ver un fragmento completo.

## Dependencias del paquete entre `ui.apps` from `ui.content` Paquetes {#package-dependencies}

Para garantizar la correcta instalación de los paquetes, se recomienda establecer dependencias entre paquetes.

La regla general son los paquetes que contienen contenido mutable (`ui.content`) debe depender del código inmutable (`ui.apps`) que admite la renderización y el uso del contenido mutable.

Una excepción notable a esta regla general es si el paquete de código inmutable (`ui.apps` o cualquier otro), __only__ contiene paquetes OSGi. Si es así, ningún paquete AEM debe declarar una dependencia de él. Esto se debe a que los paquetes de código inmutables __only__ Los paquetes que contienen OSGi no están registrados con AEM [Administrador de paquetes,](/help/implementing/developing/tools/package-manager.md) y, por lo tanto, cualquier paquete AEM que dependa de él tendrá una dependencia insatisfecha y no podrá instalarse.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-package-dependencies) para ver un fragmento completo.

Los patrones comunes para las dependencias de paquetes de contenido son:

### Dependencias simples de paquetes de implementación {#simple-deployment-package-dependencies}

El caso simple define la variable `ui.content` paquete de contenido mutable para depender de `ui.apps` paquete de código inmutable.

+ `all` no tiene dependencias
   + `ui.apps` no tiene dependencias
   + `ui.content` depende de `ui.apps`

### Dependencias de paquetes de implementación complejos {#complex-deploxment-package-dependencies}

Las implementaciones complejas se expanden en el caso simple y establecen dependencias entre el contenido mutable correspondiente y los paquetes de código inmutables. Si es necesario, también se pueden establecer dependencias entre paquetes de código inmutables.

+ `all` no tiene dependencias
   + `common.ui.apps.common` no tiene dependencias
   + `site-a.ui.apps` depende de `common.ui.apps`
   + `site-a.ui.content` depende de `site-a.ui.apps`
   + `site-b.ui.apps` depende de `common.ui.apps`
   + `site-b.ui.content` depende de `site-b.ui.apps`

## Desarrollo local e implementación {#local-development-and-deployment}

Las estructuras y la organización del proyecto descritas en este artículo son **totalmente compatible** instancias de AEM de desarrollo local.

## Fragmentos XML de POM {#pom-xml-snippets}

Los siguientes son Maven `pom.xml` fragmentos de configuración que se pueden agregar a proyectos de Maven para alinearlos con las recomendaciones anteriores.

### Tipos de paquetes {#xml-package-types}

Los paquetes de código y contenido, que se implementan como subpaquetes, deben declarar un tipo de paquete de **aplicación** o **contenido**, según lo que contengan.

#### Tipos de paquetes de contenedores {#container-package-types}

El contenedor `all/pom.xml` proyecto **no** declare `<packageType>`.

#### Tipos de paquetes de código (inmutables) {#immutable-package-types}

Los paquetes de código deben configurar sus `packageType` a `application`.

En el `ui.apps/pom.xml`, el `<packageType>application</packageType>` crear directivas de configuración de `filevault-package-maven-plugin` la declaración del complemento declara su tipo de paquete.

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

Los paquetes de contenido deben configurar sus `packageType` a `content`.

En el `ui.content/pom.xml`, el `<packageType>content</packageType>` directiva de configuración de compilación de `filevault-package-maven-plugin` la declaración del complemento declara su tipo de paquete.

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

En todos los proyectos que generan un paquete, **excepto** en el proyecto de contenedor (`all`), agregue `<cloudManagerTarget>none</cloudManagerTarget>` a la configuración de la declaración del complemento `<properties>` para garantizar `filevault-package-maven-plugin` que Adobe Cloud Manager **no** los implementa. El contenedor (`all`) debe ser el paquete singular implementado mediante Cloud Manager, que a su vez incorpora todos los paquetes de contenido y código necesarios.

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

### Punto de repo{#snippet-repo-init}

Los scripts de inicio de cesión temporal que contienen los scripts de introducción de cesión temporal se definen en la `RepositoryInitializer` Configuración de fábrica de OSGi a través de la variable `scripts` propiedad. Tenga en cuenta que, dado que estos scripts se definen dentro de las configuraciones de OSGi, se pueden crear ámbitos fácilmente mediante el modo de ejecución utilizando el `../config.<runmode>` semántica de carpeta.

Tenga en cuenta que, como los scripts suelen ser una declaración multilínea, es más fácil definirlos en la variable `.config` que está basado en JSON `.cfg.json` formato.

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

La variable `scripts` La propiedad OSGi contiene directivas como se define en la [Lenguaje Init de Repo de Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Paquete de estructura del repositorio {#xml-repository-structure-package}

En el `ui.apps/pom.xml` y cualquier otro `pom.xml` que declara un paquete de código (`<packageType>application</packageType>`), agregue la siguiente configuración de paquete de estructura de repositorio al complemento FileVault Maven. Puede [cree su propio paquete de estructura de repositorio para su proyecto](repository-structure-package.md).

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

En el `all/pom.xml`, agregue lo siguiente `<embeddeds>` directivas `filevault-package-maven-plugin` declaración del complemento. Recuerde: **no** use el `<subPackages>` , ya que esto incluirá los subpaquetes en `/etc/packages` en lugar de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

### Definición del filtro del paquete de contenedor {#xml-container-package-filters}

En el `all` del proyecto `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`), **incluya** todas `-packages` las carpetas que contengan subpaquetes para implementar:

```xml
<filter root="/apps/my-app-packages"/>
```

Si es múltiple `/apps/*-packages` se utilizan en los objetivos incrustados, entonces todos deben enumerarse aquí.

### Repositorios Maven de terceros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Añadir más repositorios Maven puede ampliar los tiempos de compilación de maven, ya que se buscarán dependencias en los repositorios Maven adicionales.

En el proyecto del reactor `pom.xml`, agregue las directivas de repositorio de Maven públicas de terceros necesarias. El `<repository>` La configuración de debe estar disponible desde el proveedor de repositorios de terceros.

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

### Dependencias del paquete entre `ui.apps` from `ui.content` Paquetes {#xml-package-dependencies}

En el `ui.content/pom.xml`, agregue lo siguiente `<dependencies>` directivas `filevault-package-maven-plugin` declaración del complemento.

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

En el `all/pom.xml` añada la variable `maven-clean-plugin` que limpiará el directorio de destino antes de las compilaciones de Maven.

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
+ [Complemento Maven del paquete de contenido de FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
