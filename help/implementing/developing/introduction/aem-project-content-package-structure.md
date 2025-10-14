---
title: Estructura del proyecto AEM
description: Obtenga información sobre cómo definir estructuras de paquetes para su implementación en el Cloud Service de Adobe Experience Manager.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 4%

---

# Estructura del proyecto AEM

>[!TIP]
>
>AEM Familiarícese con [El tipo de archivo del proyecto &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) básico y con el [Complemento Maven de contenido de FileVault](/help/implementing/developing/tools/maven-plugin.md), ya que este artículo se basa en estos conocimientos y conceptos.

Este artículo describe los cambios necesarios para que los proyectos de Adobe Experience Manager Maven sean compatibles con AEM as a Cloud Service, asegurándose de que respetan la división del contenido mutable e inmutable. Además, las dependencias se establecen para crear implementaciones determinísticas y no conflictivas, y se empaquetan en una estructura implementable.

AEM AEM Las implementaciones de aplicaciones de la aplicación deben estar compuestas por un solo paquete de la aplicación A su vez, este paquete debe contener subpaquetes que incluyan todo lo necesario para que la aplicación funcione, incluido el código, la configuración y cualquier contenido de línea de base de soporte.

AEM La requiere una separación de **content** y **code**, lo que significa que un paquete de contenido único **no puede** implementarse en **ambas** `/apps` y áreas de tiempo de ejecución (por ejemplo, `/content`, `/conf`, `/home` o cualquier cosa que no sea `/apps`) del repositorio. En su lugar, la aplicación debe separar el código y el contenido en paquetes discretos para su implementación en AEM.

La estructura del paquete descrita en este documento es compatible **tanto** con las implementaciones de desarrollo local, como con las implementaciones de AEM Cloud Service.

>[!TIP]
>
>AEM Las configuraciones descritas en este documento son proporcionadas por [Proyecto Maven de tipo de archivo 24 o posterior del proyecto de](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutables e inmutables del repositorio {#mutable-vs-immutable}

AEM AEM Las áreas `/apps` y `/libs` de la se consideran **inmutables** porque no se pueden cambiar (crear, actualizar, eliminar) después de iniciarse la ejecución (es decir, durante el tiempo de ejecución). Cualquier intento de cambiar un área inmutable durante la ejecución falla.

Todo lo demás en el repositorio, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc., son áreas **mutables**, lo que significa que se pueden cambiar durante la ejecución.

>[!WARNING]
>
>AEM Al igual que en versiones anteriores de la, `/libs` no se debe modificar. AEM Solo se puede implementar código de producto en `/libs`.

### Índices Oak {#oak-indexes}

El proceso de implementación de AEM as a Cloud Service administra los índices Oak (`/oak:index`). El motivo es que Cloud Manager debe esperar hasta que se implemente cualquier nuevo índice y volver a indexar completamente antes de cambiar a la nueva imagen de código.

Por este motivo, aunque los índices Oak son mutables en tiempo de ejecución, deben implementarse como código para que se puedan instalar antes de instalar cualquier paquete mutable. Por lo tanto, las configuraciones de `/oak:index` forman parte del paquete de código y no del paquete de contenido [como se describe a continuación](#recommended-package-structure).

>[!TIP]
>
>Para obtener más información acerca de la indización en AEM as a Cloud Service, consulte [Búsqueda e indexación de contenido](/help/operations/indexing.md).

## Estructura del paquete recomendado {#recommended-package-structure}

![Estructura del paquete del proyecto Experience Manager](assets/content-package-organization.png)

Este diagrama proporciona información general sobre la estructura del proyecto recomendada y los artefactos de implementación de paquetes.

La estructura de implementación de la aplicación recomendada es la siguiente:

### Paquetes de código/paquetes OSGi

+ El archivo Jar del paquete OSGi se genera y se incrusta directamente en todo el proyecto.

+ El paquete `ui.apps` contiene todo el código que se va a implementar y solo se implementa en `/apps`. Los elementos comunes del paquete `ui.apps` incluyen, entre otros:
   + [Definiciones de componentes y scripts HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es)
      + `/apps/my-app/components`
   + JavaScript y CSS (a través de [Bibliotecas de cliente](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Superposiciones](/help/implementing/developing/introduction/overlays.md) de `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configuraciones según el contexto de reserva
      + `/apps/settings`
   + ACL (permisos)
      + Cualquier `rep:policy` para cualquier ruta de acceso bajo `/apps`
   + [Scripts agrupados precompilados](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html?lang=es)

>[!NOTE]
>
>Se debe implementar el mismo código en todos los entornos. Este código garantiza un nivel de confianza que las validaciones en el entorno de ensayo también están en producción. Para obtener más información, consulte la sección sobre [Modos de ejecución](/help/implementing/deploying/overview.md#runmodes).


### Paquetes de contenido

+ El paquete `ui.content` contiene todo el contenido y la configuración. El paquete de contenido contiene todas las definiciones de nodos que no están en los paquetes `ui.apps` o `ui.config`, o en otras palabras, cualquier elemento que no esté en `/apps` o `/oak:index`. Los elementos comunes del paquete `ui.content` incluyen, entre otros:
   + Configuraciones según el contexto
      + `/conf`
   + Estructuras de contenido complejas y requeridas (es decir, la creación de contenido que se basa y extiende más allá de las estructuras de contenido de línea de base definidas en el inicio del repositorio).
      + `/content`, `/content/dam`, etc.
   + taxonomías de etiquetado reguladas
      + `/content/cq:tags`
   + Nodos etc. heredados (lo ideal sería migrar estos nodos a ubicaciones que no sean o que no sean )
      + `/etc`

### Paquetes de contenedor

+ El paquete `all` es un paquete de contenedor que SOLAMENTE incluye artefactos implementables, el archivo Jar del paquete OSGI, `ui.apps`, `ui.config` y `ui.content` paquetes como incrustaciones. El paquete `all` no debe tener **ningún contenido o código** propio, sino delegar toda la implementación en el repositorio a sus subpaquetes o archivos Jar del paquete OSGi.

  Los paquetes ahora se incluyen usando la configuración incrustada del complemento Maven [FileVault Package](#embeddeds) de Maven, en lugar de la configuración `<subPackages>`.

  Para implementaciones de Experience Manager AEM complejas, puede ser deseable crear varios proyectos/paquetes de `ui.apps`, `ui.config` y `ui.content` que representen sitios o inquilinos específicos en las distintas áreas de trabajo de los usuarios de la red de trabajo de la. Si se realiza este método, asegúrese de que se respeta la división entre contenido mutable e inmutable, y de que los paquetes de contenido requeridos y los archivos Jar del paquete OSGi se incrustan como subpaquetes en el paquete de contenido del contenedor `all`.

  Por ejemplo, una estructura de paquete de contenido de implementación compleja podría tener este aspecto:

   + `all` paquete de contenido incrusta los siguientes paquetes para crear un único artefacto de implementación
      + `common.ui.apps` implementa el código requerido por **tanto el sitio A como el sitio B de**
      + `site-a.core` Jar de paquete OSGi requerido por el sitio A
      + `site-a.ui.apps` implementa el código requerido por el sitio A
      + `site-a.ui.config` implementa las configuraciones de OSGi requeridas por el sitio A
      + `site-a.ui.content` implementa el contenido y la configuración requeridos por el sitio A
      + `site-b.core` Jar de paquete OSGi requerido por el sitio B
      + `site-b.ui.apps` implementa el código requerido por el sitio B
      + `site-b.ui.config` implementa las configuraciones OSGi requeridas por el sitio B
      + `site-b.ui.content` implementa el contenido y la configuración requeridos por el sitio B

+ El paquete `ui.config` contiene todas las [configuraciones de OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Se considera código y pertenece a paquetes OSGi, pero no contiene nodos de contenido normales. Por lo tanto, se marca como paquete contenedor
   + Carpeta organizativa que contiene definiciones de configuración OSGi específicas del modo de ejecución
      + `/apps/my-app/osgiconfig`
   + Carpeta de configuración de OSGi común que contiene configuraciones de OSGi predeterminadas que se aplican a todos los destinos de implementación de AEM as a Cloud Service de destino
      + `/apps/my-app/osgiconfig/config`
   + Ejecute carpetas de configuración de OSGi específicas del modo que contengan las configuraciones de OSGi predeterminadas que se aplican a todos los destinos de implementación de AEM as a Cloud Service de destino
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Scripts de configuración OSGi de inicio de repo
      + AEM [Inicio de repo](#repo-init) es la forma recomendada de implementar contenido (mutable) que lógicamente forma parte de la aplicación de la aplicación de la. Las configuraciones de OSGi de inicio de repositorio deben colocarse en la carpeta `config.<runmode>` adecuada como se describe más arriba y utilizarse para definir lo siguiente:
         + Estructuras de contenido de referencia
         + Usuarios
         + Usuarios del servicio
         + Grupos
         + ACL (permisos)

### Paquetes de aplicaciones adicionales{#extra-application-packages}

AEM AEM Si la implementación utiliza otros proyectos de, que a su vez constan de sus propios paquetes de contenido y código, los paquetes de contenedor deben incrustarse en el paquete `all` del proyecto.

AEM AEM Por ejemplo, un proyecto de que incluya dos aplicaciones de proveedor puede tener un aspecto similar al siguiente:

+ `all` paquete de contenido incrusta los siguientes paquetes para crear un único artefacto de implementación
   + AEM `core` Jar de paquete OSGi requerido por la aplicación de
   + AEM `ui.apps` implementa el código requerido por la aplicación de
   + AEM `ui.config` implementa las configuraciones de OSGi requeridas por la aplicación de
   + AEM `ui.content` implementa el contenido y la configuración requeridos por la aplicación de
   + `vendor-x.all` implementa todo (código y contenido) requerido por la aplicación X del proveedor
   + `vendor-y.all` implementa todo (código y contenido) requerido por la aplicación Y del proveedor

## Tipos de paquetes {#package-types}

Los paquetes deben marcarse con el tipo de paquete declarado. Los tipos de paquete ayudan a aclarar el propósito y la implementación de un paquete.

+ Los paquetes de contenedores deben establecer su `packageType` en `container`. Los paquetes de contenedores no deben contener nodos regulares. Solo se permiten paquetes OSGi, configuraciones y subpaquetes. Los contenedores de AEM as a Cloud Service no pueden usar [vínculos de instalación](https://jackrabbit.apache.org/filevault/installhooks.html).
+ Los paquetes de código (inmutables) deben establecer su `packageType` en `application`.
+ Los paquetes de contenido (mutables) deben establecer su `packageType` en `content`.


Para obtener más información, consulte [Documentación del complemento Apache Jackrabbit FileVault - Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Tipos de paquetes Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html) y el [fragmento de configuración de FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) a continuación.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-package-types) a continuación para ver un fragmento completo.

## Marcado de paquetes para su implementación mediante Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

De forma predeterminada, Adobe Cloud Manager obtiene todos los paquetes producidos por la compilación de Maven. Sin embargo, dado que el paquete de contenedor (`all`) es el único artefacto de implementación que contiene todos los paquetes de contenido y código, debe asegurarse de que **solo** el paquete de contenedor (`all`) esté implementado. Para garantizar esto, otros paquetes que genera la compilación de Maven deben marcarse con la configuración del complemento Maven del paquete de contenido de FileVault `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#pom-xml-snippets) a continuación para ver un fragmento completo.

## Inicio de repo{#repo-init}

Repo Init proporciona instrucciones, o scripts, que definen estructuras JCR, que van desde estructuras de nodos comunes como árboles de carpetas, hasta usuarios, usuarios de servicio, grupos y definición de ACL.

Las ventajas clave de Repo Init son que tienen permisos implícitos para realizar todas las acciones definidas por sus scripts. Además, estos scripts se invocan al principio del ciclo vital de la implementación, lo que garantiza que todas las estructuras JCR necesarias existan antes de que se ejecute el código.

Aunque los scripts de inicio de repo se ejecutan en el proyecto `ui.config` como scripts, se pueden y deben usar para definir las siguientes estructuras mutables:

+ Estructuras de contenido de referencia
+ Usuarios del servicio
+ Usuarios
+ Grupos
+ ACL

Los scripts de inicio de repo se almacenan como `scripts` entradas de `RepositoryInitializer` configuraciones de fábrica de OSGi. AEM AEM De este modo, se pueden dirigir implícitamente al modo de ejecución, lo que permite diferencias entre los scripts de inicio de repo de Author y los de Publish Services, o incluso entre entornos (Dev, Stage y Prod).

Las configuraciones OSGi de inicio de repositorio se escriben mejor en el formato de configuración OSGi [`.config`](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1), ya que admiten varias líneas, lo que es una excepción a las prácticas recomendadas de usar [`.cfg.json` para definir las configuraciones OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Al definir Usuarios y Grupos, solo los grupos se consideran parte de la aplicación y parte integral de su función. AEM Aún puede definir Usuarios y grupos de organización durante la ejecución de la aplicación de en el tiempo de ejecución de la. AEM Por ejemplo, si un flujo de trabajo personalizado asigna trabajo a un grupo con nombre, defina ese grupo mediante Repo Init en la aplicación de la. AEM Sin embargo, si la Agrupación es meramente organizativa, como &quot;Equipo de Wendy&quot; y &quot;Equipo de Sean&quot;, estos grupos se definen y administran mejor durante la ejecución en el tiempo de ejecución de la.

>[!TIP]
>
>Los scripts de inicio de repo *deben* definirse en el campo `scripts` en línea o la configuración `references` no funcionará.

El vocabulario completo para los scripts de inicio de repo está disponible en la [documentación de inicio de repo de Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulte la sección [Fragmentos de inicio de repo](#snippet-repo-init) más abajo para ver un fragmento completo.

## Paquete de estructura de repositorio {#repository-structure-package}

Los paquetes de código requieren configurar la configuración del complemento FileVault Maven para hacer referencia a un `<repositoryStructurePackage>` que exige la corrección de las dependencias estructurales (para garantizar que un paquete de código no se instale sobre otro). Puede [crear su propio paquete de estructura de repositorio para su proyecto](repository-structure-package.md).

**Solo se requiere** para los paquetes de código, es decir, cualquier paquete marcado con `<packageType>application</packageType>`.

Para aprender a crear un paquete de estructura de repositorio para su aplicación, vea [Desarrollar un paquete de estructura de repositorio](repository-structure-package.md).

Los paquetes de contenido (`<packageType>content</packageType>`) **no** requieren este paquete de estructura de repositorio.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-repository-structure-package) a continuación para ver un fragmento completo.

## Incrustación de subpaquetes en el paquete de contenedor{#embeddeds}

AEM AEM Los paquetes de contenido o código se colocan en una carpeta &quot;side-car&quot; especial y se pueden dirigir para su instalación en las versiones de autor, publicación o ambas, utilizando la configuración `<embeddeds>` del complemento Maven de FileVault. No utilice la configuración `<subPackages>`.

Los casos de uso comunes incluyen:

+ AEM AEM ACL/permisos que difieren entre los usuarios de autor de la y los usuarios de publicación
+ AEM Configuraciones que se utilizan para admitir actividades solo en el autor de la
+ AEM Código, como las integraciones con sistemas de back-office, solo es necesario para ejecutarse en el creador de la

![Incrustación de paquetes](assets/embeddeds.png)

AEM AEM Para segmentar a los autores de la, a los editores de la publicación o a ambos, el paquete está incrustado en el paquete contenedor de `all` en una ubicación de carpeta especial, con el siguiente formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Desglose de esta estructura de carpetas:

+ La carpeta de primer nivel **debe ser** `/apps`.
+ La carpeta de segundo nivel representa la aplicación con `-packages` posfija al nombre de la carpeta. A menudo, solo hay una carpeta de segundo nivel en la que están incrustados todos los subpaquetes, aunque se puede crear cualquier número de carpetas de segundo nivel para representar mejor la estructura lógica de la aplicación:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >De forma predeterminada, las carpetas incrustadas de subpaquetes reciben el nombre del sufijo `-packages`. Este nombre garantiza que el código de implementación y los paquetes de contenido sean **no** implementados en las carpetas de destino de cualquier subpaquete `/apps/<app-name>/...`, lo que da como resultado un comportamiento de instalación destructivo y cíclico.

+ La carpeta de tercer nivel debe ser
  `application`, `content` o `container`
   + La carpeta `application` contiene paquetes de código
   + La carpeta `content` contiene paquetes de contenido
   + AEM La carpeta `container` contiene [paquetes de aplicación adicionales](#extra-application-packages) que la aplicación de la aplicación podría incluir.
Este nombre de carpeta corresponde a los [tipos de paquete](#package-types) de los paquetes que contiene.
+ La carpeta de cuarto nivel contiene los subpaquetes y debe ser uno de los siguientes:
   + AEM AEM `install`, por lo que debe instalar en **tanto** como autor de la y publicación de la misma
   + AEM `install.author`, por lo que instala **solamente** en el autor de la
   + AEM `install.publish`, por lo que instala **solamente** en la publicación de la
Solo `install.author` y `install.publish` son destinos admitidos. Otros modos de ejecución **no son** compatibles.

AEM Por ejemplo, una implementación que contenga paquetes específicos de autor y publicación de la aplicación puede tener el siguiente aspecto:

+ `all` El paquete de contenedor incrusta los siguientes paquetes para crear un artefacto de implementación único
   + AEM AEM `ui.apps` incrustado en `/apps/my-app-packages/application/install` implementa código tanto para el autor de la como para la publicación de la misma
   + AEM `ui.apps.author` incrustado en `/apps/my-app-packages/application/install.author` implementa código solo para el autor de la
   + AEM AEM `ui.content` incrustado en `/apps/my-app-packages/content/install` implementa contenido y configuración tanto para el autor como para la publicación de la publicación de la
   + AEM `ui.content.publish` incrustado en `/apps/my-app-packages/content/install.publish` implementa contenido y configuración solo para publicar en el sitio web de la manera de

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-embeddeds) a continuación para ver un fragmento completo.

### Definición del filtro del paquete del contenedor {#container-package-filter-definition}

Debido a la incrustación de los subpaquetes de código y contenido en el paquete contenedor, las rutas de destino incrustadas deben agregarse a `filter.xml` del proyecto contenedor. Al hacerlo, se garantiza que los paquetes incrustados se incluyan en el paquete contenedor cuando se creen.

Simplemente agregue las `<filter root="/apps/<my-app>-packages"/>` entradas para cualquier carpeta de segundo nivel que contenga subpaquetes para implementar.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-container-package-filters) a continuación para ver un fragmento completo.

## Incrustación de paquetes de terceros {#embedding-3rd-party-packages}

Todos los paquetes deben estar disponibles a través del [repositorio público de artefactos Maven del Adobe](https://repo1.maven.org/maven2/com/adobe/) o un repositorio de artefactos Maven público y referenciable de terceros al que se pueda acceder.

Si los paquetes de terceros están en el repositorio público de artefactos Maven de **Adobe**, no se necesita ninguna configuración adicional para que Cloud Manager de Adobe resuelva los artefactos.

Si los paquetes de terceros están en un **repositorio público de artefactos Maven de terceros**, este repositorio debe estar registrado en el `pom.xml` del proyecto e incrustado según el método [descrito anteriormente](#embeddeds).

Los conectores/aplicaciones de terceros deben incrustarse usando su paquete `all` como contenedor en el paquete de contenedor (`all`) de su proyecto.

La adición de dependencias Maven sigue las prácticas estándar de Maven y la incrustación de artefactos de terceros (paquetes de contenido y código) se [ha descrito anteriormente](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-3rd-party-maven-repositories) a continuación para ver un fragmento completo.

## Dependencias de paquete entre `ui.apps` de `ui.content` paquetes {#package-dependencies}

Para garantizar la correcta instalación de los paquetes, se recomienda establecer dependencias entre paquetes.

La regla general es que los paquetes que contienen contenido mutable (`ui.content`) deben depender del código inmutable (`ui.apps`) que admite la representación y el uso del contenido mutable.

Una excepción notable a esta regla general es si el paquete de código inmutable (`ui.apps` o cualquier otro), __solo__ contiene paquetes OSGi. AEM Si es así, ningún paquete de debe declarar una dependencia en él. AEM El motivo es que los paquetes de código inmutable que __solo__ contienen paquetes OSGi, no están registrados con [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) y no se han registrado con el paquete OSGi. AEM Por lo tanto, cualquier paquete de que dependa de él tiene una dependencia no satisfecha y no se puede instalar.

>[!TIP]
>
>Consulte la sección [Fragmentos XML de POM](#xml-package-dependencies) a continuación para ver un fragmento completo.

Los patrones comunes para las dependencias de paquetes de contenido son:

### Dependencias del paquete de implementación simple {#simple-deployment-package-dependencies}

El caso simple establece el paquete de contenido mutable `ui.content` para que dependa del paquete de código inmutable `ui.apps`.

+ `all` no tiene dependencias
   + `ui.apps` no tiene dependencias
   + `ui.content` depende de `ui.apps`

### Dependencias del paquete de implementación compleja {#complex-deploxment-package-dependencies}

Las implementaciones complejas amplían el caso simple y establecen dependencias entre el contenido mutable correspondiente y los paquetes de código inmutable. Según sea necesario, también se pueden establecer dependencias entre paquetes de código inmutable.

+ `all` no tiene dependencias
   + `common.ui.apps.common` no tiene dependencias
   + `site-a.ui.apps` depende de `common.ui.apps`
   + `site-a.ui.content` depende de `site-a.ui.apps`
   + `site-b.ui.apps` depende de `common.ui.apps`
   + `site-b.ui.content` depende de `site-b.ui.apps`

## Desarrollo e implementación locales {#local-development-and-deployment}

AEM Las estructuras y la organización del proyecto descritas en este artículo son **totalmente compatibles** instancias de desarrollo local de la aplicación de desarrollo de.

## Fragmentos XML de POM {#pom-xml-snippets}

Los siguientes son fragmentos de configuración de Maven `pom.xml` que se pueden agregar a proyectos Maven para alinearlos con las recomendaciones anteriores.

### Tipos de paquetes {#xml-package-types}

Los paquetes de código y contenido, que se implementan como subpaquetes, deben declarar un tipo de paquete de **application** o **content**, según lo que contengan.

#### Tipos de paquetes de contenedores {#container-package-types}

El contenedor `all/pom.xml` del proyecto **no** declara un `<packageType>`.

#### Tipos de paquetes de código (inmutables) {#immutable-package-types}

Los paquetes de código deben establecer su `packageType` en `application`.

En `ui.apps/pom.xml`, las directivas de configuración de compilación de `<packageType>application</packageType>` de la declaración del complemento `filevault-package-maven-plugin` declaran su tipo de paquete.

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

#### Tipos de paquetes de contenido (mutable) {#mutable-package-types}

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

### Inicio de repo{#snippet-repo-init}

Los scripts de inicio de repo que contienen los scripts de inicio de repo se definen en la configuración de fábrica de OSGi `RepositoryInitializer` mediante la propiedad `scripts`. Debido a que estos scripts se definen en configuraciones de OSGi, se pueden definir fácilmente mediante el modo de ejecución utilizando la semántica de carpeta habitual `../config.<runmode>`.

Dado que los scripts suelen ser declaraciones multilínea, es más fácil definirlos en el archivo `.config` que en el formato `.cfg.json` basado en JSON.

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

La propiedad OSGi `scripts` contiene directivas tal como se definen en el [idioma de inicialización de repositorio de Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Paquete de estructura de repositorio {#xml-repository-structure-package}

En `ui.apps/pom.xml` y en cualquier otro `pom.xml` que declare un paquete de código (`<packageType>application</packageType>`), agregue la siguiente configuración de paquete de estructura de repositorio al complemento Maven de FileVault. Puede [crear su propio paquete de estructura de repositorio para su proyecto](repository-structure-package.md).

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

En `all/pom.xml`, agregue las siguientes directivas `<embeddeds>` a la declaración del complemento `filevault-package-maven-plugin`. Recuerde, **no** utiliza la configuración `<subPackages>`. El motivo es que incluye los subpaquetes de `/etc/packages` en lugar de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

### Definición del filtro del paquete del contenedor {#xml-container-package-filters}

En `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) del proyecto `all`, **incluya** cualquier carpeta `-packages` que contenga subpaquetes para implementar:

```xml
<filter root="/apps/my-app-packages"/>
```

Si se usan varios `/apps/*-packages` en los destinos incrustados, entonces todos deben enumerarse aquí.

### Repositorios de Maven de terceros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Añadir más repositorios Maven puede ampliar los tiempos de compilación de Maven, ya que se comprueban las dependencias de otros repositorios Maven.

En `pom.xml` del proyecto del reactor, agregue cualquier directiva pública de repositorio de Maven necesaria. La configuración completa de `<repository>` debe estar disponible en el proveedor de repositorios de terceros.

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public Third-Party Repository</name>
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

### Dependencias de paquete entre `ui.apps` de `ui.content` paquetes {#xml-package-dependencies}

En `ui.content/pom.xml`, agregue las siguientes directivas `<dependencies>` a la declaración del complemento `filevault-package-maven-plugin`.

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

### Limpiar la carpeta de destino del proyecto de contenedor {#xml-clean-container-package}

En `all/pom.xml`, agregue el complemento `maven-clean-plugin` que limpia el directorio de destino antes de una compilación de Maven.

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

+ [Administración de paquetes mediante Maven](/help/implementing/developing/tools/maven-plugin.md)
+ [Complemento Maven del paquete de contenido FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
