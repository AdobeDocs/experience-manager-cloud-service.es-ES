---
title: Estructura del proyecto AEM
description: Obtenga información sobre cómo definir estructuras de paquetes para su implementación en el Cloud Service de Adobe Experience Manager.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 92c123817a654d0103d0f7b8e457489d9e82c2ce
workflow-type: tm+mt
source-wordcount: '2918'
ht-degree: 4%

---

# Estructura del proyecto AEM

>[!TIP]
>
>Familiarícese con las [AEM Uso del tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), y el [Complemento Maven de contenido de FileVault](/help/implementing/developing/tools/maven-plugin.md) ya que este artículo se basa en estos conocimientos y conceptos.

Este artículo describe los cambios necesarios para que los proyectos de Adobe Experience Manager AEM Maven sean compatibles en términos as a Cloud Service, asegurándose de que respetan la división del contenido mutable e inmutable. Además, las dependencias se establecen para crear implementaciones determinísticas y no conflictivas, y se empaquetan en una estructura implementable.

AEM AEM Las implementaciones de aplicaciones de la aplicación deben estar compuestas por un solo paquete de la aplicación A su vez, este paquete debe contener subpaquetes que incluyan todo lo necesario para que la aplicación funcione, incluido el código, la configuración y cualquier contenido de línea de base de soporte.

AEM La requiere una separación de **content** y **código**, lo que significa un paquete de contenido único **no puede** implementar en **ambos** `/apps` y áreas de tiempo de ejecución (por ejemplo, `/content`, `/conf`, `/home`, o cualquier cosa que no `/apps`) del repositorio. En su lugar, la aplicación debe separar el código y el contenido en paquetes discretos para su implementación en AEM.

La estructura del paquete descrita en este documento es compatible **tanto** con las implementaciones de desarrollo local, como con las implementaciones de AEM Cloud Service.

>[!TIP]
>
>Las configuraciones descritas en este documento las proporciona [AEM Arquetipo 24 o posterior del proyecto Maven](https://github.com/adobe/aem-project-archetype/releases).

## Áreas mutables e inmutables del repositorio {#mutable-vs-immutable}

El `/apps` y `/libs` AEM se consideran las áreas de la **inmutable** AEM porque no se pueden cambiar (crear, actualizar, eliminar) después de iniciarse el inicio de la (es decir, durante la ejecución). Cualquier intento de cambiar un área inmutable durante la ejecución falla.

Todo lo demás en el repositorio, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, etc., son todos **mutable** , lo que significa que se pueden cambiar durante la ejecución.

>[!WARNING]
>
>AEM Al igual que en versiones anteriores de la aplicación de `/libs` no debe modificarse. AEM Solo puede implementarse el código de producto de la en `/libs`.

### Índices Oak {#oak-indexes}

Índices Oak (`/oak:index`AEM ) se gestionan mediante el proceso de implementación as a Cloud Service de la. El motivo es que Cloud Manager debe esperar hasta que se implemente cualquier nuevo índice y se vuelva a indexar completamente antes de cambiar a la nueva imagen de código.

Por este motivo, aunque los índices Oak son mutables en tiempo de ejecución, deben implementarse como código para que se puedan instalar antes de instalar cualquier paquete mutable. Por lo tanto `/oak:index` Las configuraciones de forman parte del paquete de código y no del paquete de contenido [como se describe a continuación](#recommended-package-structure).

>[!TIP]
>
>AEM Para obtener más información sobre la indexación en el as a Cloud Service, consulte [Búsqueda de contenido e indexación](/help/operations/indexing.md).

## Estructura del paquete recomendado {#recommended-package-structure}

![Estructura del paquete del proyecto de Experience Manager](assets/content-package-organization.png)

Este diagrama proporciona información general sobre la estructura del proyecto recomendada y los artefactos de implementación de paquetes.

La estructura de implementación de la aplicación recomendada es la siguiente:

### Paquetes de código/paquetes OSGi

+ El archivo Jar del paquete OSGi se genera y se incrusta directamente en todo el proyecto.

+ El `ui.apps` contiene todo el código que se va a implementar y solo se implementa en `/apps`. Elementos comunes del `ui.apps` Los paquetes incluyen, entre otros, lo siguiente:
   + [Definiciones de componentes y HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es) scripts
      + `/apps/my-app/components`
   + JavaScript y CSS (mediante [Bibliotecas de cliente](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Superposiciones](/help/implementing/developing/introduction/overlays.md) de `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configuraciones según el contexto de reserva
      + `/apps/settings`
   + ACL (permisos)
      + Cualquiera `rep:policy` para cualquier ruta en `/apps`
   + [Scripts agrupados precompilados](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>Se debe implementar el mismo código en todos los entornos. Este código garantiza un nivel de confianza que las validaciones en el entorno de ensayo también están en producción. Para obtener más información, consulte la sección sobre [Modos de ejecución](/help/implementing/deploying/overview.md#runmodes).


### Paquetes de contenido

+ El `ui.content` contiene todo el contenido y la configuración. El paquete de contenido contiene todas las definiciones de nodos que no están en la `ui.apps` o `ui.config` paquetes, o en otras palabras, cualquier cosa que no esté en `/apps` o `/oak:index`. Elementos comunes del `ui.content` Los paquetes incluyen, entre otros, lo siguiente:
   + Configuraciones según el contexto
      + `/conf`
   + Estructuras de contenido complejas y requeridas (es decir, la creación de contenido que se basa y extiende más allá de las estructuras de contenido de línea de base definidas en el inicio del repositorio).
      + `/content`, `/content/dam`, etc.
   + taxonomías de etiquetado reguladas
      + `/content/cq:tags`
   + Nodos etc. heredados (lo ideal sería migrar estos nodos a ubicaciones que no sean o que no sean )
      + `/etc`

### Paquetes de contenedor

+ El `all` es un paquete de contenedor que SOLAMENTE incluye artefactos implementables, el archivo Jar del paquete OSGI, `ui.apps`, `ui.config`, y `ui.content` paquetes como incrustaciones. El `all` el paquete no debe tener **cualquier contenido o código** por sí solo, sino que delega toda la implementación en el repositorio a sus subpaquetes o archivos Jar del paquete OSGi.

  Los paquetes ahora se incluyen usando Maven [Configuración integrada del complemento Maven del paquete FileVault](#embeddeds), en lugar de `<subPackages>` configuración.

  Para implementaciones de Experience Manager complejas, puede ser deseable crear varias `ui.apps`, `ui.config`, y `ui.content` AEM proyectos/paquetes que representan sitios o inquilinos específicos en el área de trabajo de la. Si se realiza este enfoque, asegúrese de que se respeta la división entre contenido mutable e inmutable, y de que los paquetes de contenido requeridos y los archivos Jar del paquete OSGi están incrustados como subpaquetes en el `all` paquete de contenido de contenedor.

  Por ejemplo, una estructura de paquete de contenido de implementación compleja podría tener este aspecto:

   + `all` paquete de contenido incrusta los siguientes paquetes para crear un único artefacto de implementación
      + `common.ui.apps` implementa el código requerido por **ambos** Sitio A y sitio B
      + `site-a.core` Jar de paquete OSGi requerido por el sitio A
      + `site-a.ui.apps` implementa el código requerido por el sitio A
      + `site-a.ui.config` implementa las configuraciones de OSGi requeridas por el sitio A
      + `site-a.ui.content` implementa el contenido y la configuración requeridos por el sitio A
      + `site-b.core` Jar de paquete OSGi requerido por el sitio B
      + `site-b.ui.apps` implementa el código requerido por el sitio B
      + `site-b.ui.config` implementa las configuraciones de OSGi requeridas por el sitio B
      + `site-b.ui.content` implementa el contenido y la configuración requeridos por el sitio B

+ El `ui.config` el paquete contiene todo [Configuraciones de OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Se considera código y pertenece a paquetes OSGi, pero no contiene nodos de contenido normales. Por lo tanto, se marca como paquete contenedor
   + Carpeta organizativa que contiene definiciones de configuración OSGi específicas del modo de ejecución
      + `/apps/my-app/osgiconfig`
   + AEM Carpeta de configuración de OSGi común que contiene configuraciones de OSGi predeterminadas que se aplican a todos los destinos de implementación as a Cloud Service de Target
      + `/apps/my-app/osgiconfig/config`
   + AEM Ejecute carpetas de configuración de OSGi específicas del modo que contengan las configuraciones de OSGi predeterminadas que se aplican a todos los destinos de implementación as a Cloud Service de OSGi de destino
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Scripts de configuración OSGi de inicio de repo
      + [Inicio de repo](#repo-init) AEM es la forma recomendada de implementar contenido (mutable) que lógicamente forma parte de la aplicación de la. Las configuraciones de OSGi de inicio de repo deben colocarse en la ubicación adecuada `config.<runmode>` como se ha descrito anteriormente, y se utilizará para definir lo siguiente:
         + Estructuras de contenido de referencia
         + Usuarios
         + Usuarios de servicio
         + Grupos
         + ACL (permisos)

### Paquetes de aplicaciones adicionales{#extra-application-packages}

AEM AEM Si la implementación utiliza otros proyectos de, que a su vez están compuestos por su propio código y paquetes de contenido, los paquetes de contenedores deben incrustarse en los paquetes de contenido del proyecto `all` paquete.

AEM AEM Por ejemplo, un proyecto de que incluya dos aplicaciones de proveedor puede tener un aspecto similar al siguiente:

+ `all` paquete de contenido incrusta los siguientes paquetes para crear un único artefacto de implementación
   + `core` AEM Jar de paquete OSGi requerido por la aplicación de
   + `ui.apps` AEM implementa el código requerido por la aplicación de
   + `ui.config` AEM implementa las configuraciones de OSGi requeridas por la aplicación de
   + `ui.content` AEM implementa el contenido y la configuración requeridos por la aplicación de
   + `vendor-x.all` implementa todo (código y contenido) necesario para la aplicación del proveedor X
   + `vendor-y.all` implementa todo (código y contenido) requerido por la aplicación Y del proveedor

## Tipos de paquetes {#package-types}

Los paquetes deben marcarse con el tipo de paquete declarado. Los tipos de paquete ayudan a aclarar el propósito y la implementación de un paquete.

+ Los paquetes de contenedores deben establecer su `packageType` hasta `container`. Los paquetes de contenedores no deben contener nodos regulares. Solo se permiten paquetes OSGi, configuraciones y subpaquetes. AEM No se permite el uso de contenedores en los contenedores de la as a Cloud Service [instalar ganchos](https://jackrabbit.apache.org/filevault/installhooks.html).
+ Los paquetes de código (inmutables) deben establecer su `packageType` hasta `application`.
+ Los paquetes de contenido (mutables) deben establecer su `packageType` hasta `content`.


Para obtener más información, consulte [Apache Jackrabbit FileVault: documentación del complemento Maven del paquete](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Tipos de paquetes de Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html), y el [Fragmento de configuración de FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) más abajo.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-package-types) para ver un fragmento completo.

## Marcado de paquetes para su implementación mediante Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

De forma predeterminada, Adobe Cloud Manager obtiene todos los paquetes producidos por la compilación de Maven. Sin embargo, debido a que el contenedor (`all`) es el único artefacto de implementación que contiene todos los paquetes de contenido y código. Debe asegurarse de que **solamente** el contenedor (`all`) se haya implementado el paquete. Para garantizar esto, otros paquetes que genera la compilación de Maven deben marcarse con la configuración del complemento Maven del paquete de contenido de FileVault `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#pom-xml-snippets) para ver un fragmento completo.

## Inicio de repo{#repo-init}

Repo Init proporciona instrucciones, o scripts, que definen estructuras JCR, que van desde estructuras de nodos comunes como árboles de carpetas, hasta usuarios, usuarios de servicio, grupos y definición de ACL.

Las ventajas clave de Repo Init son que tienen permisos implícitos para realizar todas las acciones definidas por sus scripts. Además, estos scripts se invocan al principio del ciclo vital de la implementación, lo que garantiza que todas las estructuras JCR necesarias existan antes de que se ejecute el código.

Mientras que los scripts de inicio de repo se activan en la variable `ui.config` proyecto como secuencias de comandos, se pueden y se deben utilizar para definir las siguientes estructuras mutables:

+ Estructuras de contenido de referencia
+ Usuarios de servicio
+ Usuarios
+ Grupos
+ ACL

Los scripts de inicio de repo se almacenan como `scripts` entradas de `RepositoryInitializer` Configuraciones de fábrica de OSGi. Como tal, se pueden dirigir implícitamente al modo de ejecución, lo que permite diferencias entre los scripts de inicio de repositorios de AEM Author y AEM Publish Services, o incluso entre entornos (Desarrollo, Ensayo y Producción).

Las configuraciones OSGi de inicio de repo se escriben mejor en la variable [`.config` Formato de configuración OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) ya que admiten varias líneas, lo que supone una excepción a las prácticas recomendadas de uso de [`.cfg.json` para definir las configuraciones de OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Al definir Usuarios y Grupos, solo los grupos se consideran parte de la aplicación y parte integral de su función. AEM Aún puede definir Usuarios y grupos de organización durante la ejecución de la aplicación de en el tiempo de ejecución de la. AEM Por ejemplo, si un flujo de trabajo personalizado asigna trabajo a un grupo con nombre, defina ese grupo mediante Repo Init en la aplicación de la. AEM Sin embargo, si la Agrupación es meramente organizativa, como &quot;Equipo de Wendy&quot; y &quot;Equipo de Sean&quot;, estos grupos se definen y administran mejor durante la ejecución en el tiempo de ejecución de la.

>[!TIP]
>
>Scripts de inicio de repo *debe* se definirá en la línea `scripts` o el campo `references` La configuración de no funciona.

El vocabulario completo para los scripts de inicio de repo está disponible en la [Documentación de inicio del repositorio de Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulte la [Fragmentos de inicio de repo](#snippet-repo-init) para ver un fragmento completo.

## Paquete de estructura de repositorio {#repository-structure-package}

Los paquetes de código requieren configurar la configuración del complemento FileVault Maven para hacer referencia a un `<repositoryStructurePackage>` que exige la corrección de las dependencias estructurales (para garantizar que un paquete de código no se instale sobre otro). Puede [cree su propio paquete de estructura de repositorio para el proyecto](repository-structure-package.md).

**Solo obligatorio** para paquetes de código, es decir, cualquier paquete marcado con `<packageType>application</packageType>`.

Para obtener información sobre cómo crear un paquete de estructura de repositorio para la aplicación, consulte [Desarrollo de un paquete de estructura de repositorio](repository-structure-package.md).

Paquetes de contenido (`<packageType>content</packageType>`) **no** requiere este paquete de estructura de repositorio.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-repository-structure-package) para ver un fragmento completo.

## Incrustación de subpaquetes en el paquete de contenedor{#embeddeds}

AEM AEM Los paquetes de contenido o código se colocan en una carpeta especial &quot;side-car&quot; y se pueden segmentar para su instalación en los programas de autor, publicación o ambos, mediante el complemento de Maven de FileVault `<embeddeds>` configuración. No use el `<subPackages>` configuración.

Los casos de uso comunes incluyen:

+ AEM AEM ACL/permisos que difieren entre los usuarios de autor de la y los usuarios de publicación
+ AEM Configuraciones que se utilizan para admitir actividades solo en el autor de la
+ AEM Código, como las integraciones con sistemas de back-office, solo es necesario para ejecutarse en el creador de la

![Incrustación de paquetes](assets/embeddeds.png)

AEM AEM Para segmentar a los autores de la, las publicaciones o ambas, el paquete está incrustado en `all` paquete de contenedor en una ubicación de carpeta especial, con el siguiente formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Desglose de esta estructura de carpetas:

+ La carpeta de primer nivel **debe ser** `/apps`.
+ La carpeta de segundo nivel representa la aplicación con `-packages` se ha corregido la publicación en el nombre de la carpeta. A menudo, solo hay una carpeta de segundo nivel en la que están incrustados todos los subpaquetes, aunque se puede crear cualquier número de carpetas de segundo nivel para representar mejor la estructura lógica de la aplicación:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >De forma predeterminada, las carpetas incrustadas de subpaquetes reciben el nombre del sufijo de `-packages`. Esta denominación garantiza que el código de implementación y los paquetes de contenido sean **no** implementación de las carpetas de destino de cualquier subpaquete `/apps/<app-name>/...`  que da como resultado un comportamiento de instalación destructivo y cíclico.

+ La carpeta de tercer nivel debe ser
  `application`, `content` o `container`
   + El `application` La carpeta contiene paquetes de código
   + El `content` la carpeta contiene paquetes de contenido
   + El `container` la carpeta contiene cualquier [paquetes de aplicaciones adicionales](#extra-application-packages) AEM que puede incluir la aplicación de la.
Este nombre de carpeta corresponde a la variable [tipos de paquetes](#package-types) de los paquetes que contiene.
+ La carpeta de cuarto nivel contiene los subpaquetes y debe ser uno de los siguientes:
   + `install` para instalar en **ambos** AEM AEM Publicación de autor y de datos
   + `install.author` para instalar **solamente** AEM en el autor del
   + `install.publish` para instalar **solamente** AEM Solo en publicación de `install.author` y `install.publish` son destinos admitidos. Otros modos de ejecución **no son** compatibles.

AEM Por ejemplo, una implementación que contenga paquetes específicos de autor y publicación de la aplicación puede tener el siguiente aspecto:

+ `all` El paquete de contenedor incrusta los siguientes paquetes para crear un único artefacto de implementación
   + `ui.apps` incrustado en `/apps/my-app-packages/application/install` AEM AEM implementa el código tanto para el autor de la como para la publicación de la misma
   + `ui.apps.author` incrustado en `/apps/my-app-packages/application/install.author` AEM implementa el código solo para el autor de la
   + `ui.content` incrustado en `/apps/my-app-packages/content/install` AEM AEM implementa el contenido y la configuración tanto para el autor de la como para la publicación de la misma
   + `ui.content.publish` incrustado en `/apps/my-app-packages/content/install.publish` AEM implementa contenido y configuración solo para publicar en el sitio web de la manera más

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-embeddeds) para ver un fragmento completo.

### Definición del filtro del paquete del contenedor {#container-package-filter-definition}

Debido a la incrustación de los subpaquetes de código y contenido en el paquete contenedor, las rutas de destino incrustadas deben agregarse al proyecto contenedor `filter.xml`. Al hacerlo, se garantiza que los paquetes incrustados se incluyan en el paquete contenedor cuando se creen.

Simplemente añada el `<filter root="/apps/<my-app>-packages"/>` entradas para cualquier carpeta de segundo nivel que contenga subpaquetes para implementar.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-container-package-filters) para ver un fragmento completo.

## Incrustación de paquetes de terceros {#embedding-3rd-party-packages}

Todos los paquetes deben estar disponibles a través de la [Repositorio de artefactos Maven públicos de Adobe](https://repo1.maven.org/maven2/com/adobe/) o un repositorio de artefactos Maven público y referenciable de terceros.

Si los paquetes de terceros están en **Repositorio de artefactos Maven públicos de Adobe** Sin embargo, no se necesita ninguna configuración adicional para que Adobe Cloud Manager resuelva los artefactos.

Si los paquetes de terceros están en un **repositorio de artefactos Maven de terceros públicos**, este repositorio debe estar registrado en el `pom.xml` e incrustado siguiendo el método [descrito anteriormente](#embeddeds).

Los conectores/aplicaciones de terceros deben incrustarse con su `all` como contenedor en el contenedor de su proyecto (`all`) paquete.

La adición de dependencias Maven sigue las prácticas estándar de Maven y la incrustación de artefactos de terceros (paquetes de contenido y código) son [descrito anteriormente](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-3rd-party-maven-repositories) para ver un fragmento completo.

## Dependencias del paquete entre `ui.apps` de `ui.content` Paquetes {#package-dependencies}

Para garantizar la correcta instalación de los paquetes, se recomienda establecer dependencias entre paquetes.

La regla general son los paquetes que contienen contenido mutable (`ui.content`) debe depender del código inmutable (`ui.apps`) que admite la renderización y el uso del contenido mutable.

Una excepción notable a esta regla general es si el paquete de código inmutable (`ui.apps` o cualquier otro), __solamente__ contiene paquetes OSGi. AEM Si es así, ningún paquete de debe declarar una dependencia en él. El motivo es que los paquetes de código inmutable que __solamente__ AEM contiene paquetes OSGi, no están registrados con los paquetes OSGi [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md). AEM Por lo tanto, cualquier paquete de que dependa de él tiene una dependencia no satisfecha y no se puede instalar.

>[!TIP]
>
>Consulte la [Fragmentos XML de POM](#xml-package-dependencies) para ver un fragmento completo.

Los patrones comunes para las dependencias de paquetes de contenido son:

### Dependencias del paquete de implementación simple {#simple-deployment-package-dependencies}

El caso simple establece el `ui.content` paquete de contenido mutable que dependerá del `ui.apps` paquete de código inmutable.

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

Las estructuras y organización del proyecto descritas en este artículo son las siguientes **totalmente compatible** AEM desarrollo local de instancias de.

## Fragmentos XML de POM {#pom-xml-snippets}

Los siguientes son Maven `pom.xml` fragmentos de configuración que se pueden añadir a los proyectos de Maven para alinearlos con las recomendaciones anteriores.

### Tipos de paquetes {#xml-package-types}

Los paquetes de código y contenido, que se implementan como subpaquetes, deben declarar un tipo de paquete de **aplicación** o **content**, dependiendo de lo que contengan.

#### Tipos de paquetes de contenedores {#container-package-types}

El contenedor `all/pom.xml` proyecto **no tiene** declarar un `<packageType>`.

#### Tipos de paquetes de código (inmutables) {#immutable-package-types}

Los paquetes de código deben establecer su `packageType` hasta `application`.

En el `ui.apps/pom.xml`, el `<packageType>application</packageType>` generar directivas de configuración de `filevault-package-maven-plugin` la declaración del complemento declara su tipo de paquete.

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

Los paquetes de contenido deben establecer su `packageType` hasta `content`.

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

### Marcar paquetes para la implementación de Adobe Cloud Manager {#cloud-manager-target}

En todos los proyectos que generan un paquete, **excepto** en el proyecto de contenedor (`all`), agregue `<cloudManagerTarget>none</cloudManagerTarget>` a la configuración de la declaración del complemento `<properties>` para garantizar `filevault-package-maven-plugin` que Adobe Cloud Manager **no** los implementa. El contenedor (`all`) paquete debe ser el paquete singular implementado mediante Cloud Manager, que a su vez incorpora todos los paquetes de contenido y código necesarios.

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

Los scripts de inicio de repo que contienen los scripts de inicio de repo se definen en `RepositoryInitializer` Configuración de fábrica de OSGi a través de `scripts` propiedad. Como estos scripts se definen en configuraciones de OSGi, se pueden definir fácilmente mediante el modo de ejecución `../config.<runmode>` semántica de carpetas.

Dado que los scripts suelen ser declaraciones multilínea, es más fácil definirlos en la variable `.config` que el basado en JSON `.cfg.json` formato.

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

El `scripts` La propiedad OSGi contiene directivas tal como se definen en [Lenguaje de inicialización del repositorio de Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Paquete de estructura de repositorio {#xml-repository-structure-package}

En el `ui.apps/pom.xml` y cualquier otro `pom.xml` que declara un paquete de código (`<packageType>application</packageType>`), agregue la siguiente configuración del paquete de estructura del repositorio al complemento FileVault Maven. Puede [cree su propio paquete de estructura de repositorio para el proyecto](repository-structure-package.md).

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

En el `all/pom.xml`, agregue lo siguiente `<embeddeds>` directivas al `filevault-package-maven-plugin` declaración del complemento. Recuerde, **no** use el `<subPackages>` configuración. El motivo es que incluye los subpaquetes en `/etc/packages` en lugar de `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

En el `all` del proyecto `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`), **include** cualquiera `-packages` carpetas que contienen subpaquetes para implementar:

```xml
<filter root="/apps/my-app-packages"/>
```

Si hay varios `/apps/*-packages` se utilizan en los destinos incrustados, entonces todos deben enumerarse aquí.

### Repositorios de Maven de terceros {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Añadir más repositorios Maven puede ampliar los tiempos de compilación de Maven, ya que se comprueban las dependencias de otros repositorios Maven.

En el del proyecto del reactor `pom.xml`, agregue cualquier directiva pública de repositorio de Maven necesaria. El completo `<repository>` La configuración de debe estar disponible en el proveedor de repositorios de terceros.

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

### Dependencias del paquete entre `ui.apps` de `ui.content` Paquetes {#xml-package-dependencies}

En el `ui.content/pom.xml`, agregue lo siguiente `<dependencies>` directivas al `filevault-package-maven-plugin` declaración del complemento.

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

En el `all/pom.xml`, añada el `maven-clean-plugin` que limpia el directorio de destino antes de una compilación de Maven.

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
+ [Complemento Maven del paquete de contenido de FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
