---
title: Adobe Content Package Maven Plugin
description: Utilice el complemento Content Package Maven para implementar aplicaciones AEM
translation-type: tm+mt
source-git-commit: 2cdbbe9b8f6608cbdd299889be515d421e3d9ad3
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 7%

---


# Complemento Maven del paquete de contenido de Adobe {#adobe-content-package-maven-plugin}

Utilice el complemento Adobe Content Package Maven para integrar la implementación de paquetes y tareas de administración en sus proyectos de Maven.

La implementación de los paquetes construidos en AEM es realizada por el complemento Adobe Content Package Maven y permite la automatización de tareas que se realizan normalmente mediante AEM Administrador de paquetes:

* Cree nuevos paquetes a partir de archivos del sistema de archivos.
* Instale y desinstale paquetes en AEM.
* Cree paquetes que ya estén definidos en AEM.
* Obtenga una lista de paquetes instalados en AEM.
* Elimine un paquete de AEM.

Este documento detalla cómo usar el Maven para administrar estas tareas. Sin embargo, también es importante comprender [cómo se estructuran AEM proyectos y sus paquetes.](#aem-project-structure)

>[!NOTE]
>
>La creación de paquetes ahora es propiedad del [complemento Apache Jackrabbit FileVault Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/). La implementación de los paquetes construidos en AEM es realizada por el complemento Adobe Content Package Maven como se describe aquí.

## Paquetes y la estructura del proyecto AEM {#aem-project-structure}

AEM 6.5 se adhiere a las prácticas recomendadas más recientes para la gestión de paquetes y la estructura de proyectos, tal como se aplican en el último arquetipo del proyecto AEM para las implementaciones locales y AMS.

>[!TIP]
>
>Para obtener más información, consulte el artículo [AEM Estructura del proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) en el AEM como documentación de Cloud Service, así como la documentación de [AEM Arquetipo del proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html). Ambos son totalmente compatibles con AEM 6.5.

## Obtención del complemento Maven del paquete de contenido {#obtaining-the-content-package-maven-plugin}

El complemento está disponible en el [Repositorio central de Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Objetivos y parámetros del complemento Maven del paquete de contenido

Para utilizar el complemento Maven del paquete de contenido, agregue el siguiente elemento de complemento dentro del elemento build del archivo POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Para habilitar Maven para descargar el complemento, utilice el perfil proporcionado en la sección [Obtención del complemento Maven del paquete de contenido](#obtaining-the-content-package-maven-plugin) de esta página.

## Objetivos del complemento Maven del paquete de contenido {#goals-of-the-content-package-maven-plugin}

Los objetivos y parámetros de objetivo que proporciona el complemento Paquete de contenido se describen en las secciones siguientes. Los parámetros que se describen en la sección Parámetros comunes pueden utilizarse para la mayoría de los objetivos. Los parámetros que se aplican a un objetivo se describen en la sección correspondiente.

### Prefijo del complemento {#plugin-prefix}

El prefijo del complemento es `content-package`. Utilice este prefijo para ejecutar un objetivo desde la línea de comandos, como en el ejemplo siguiente:

```shell
mvn content-package:build
```

### Prefijo de parámetro {#parameter-prefix}

A menos que se indique lo contrario, los objetivos y parámetros del complemento utilizan el prefijo `vault`, como en el siguiente ejemplo:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

Los objetivos que utilizan proxies para AEM utilizan la primera configuración de proxy válida que se encuentra en la configuración de Maven. Si no se encuentra ninguna configuración proxy, no se utiliza ningún proxy. Consulte el parámetro `useProxy` en la sección [Parámetros comunes](#common-parameters).

### Parámetros comunes {#common-parameters}

Los parámetros de la siguiente tabla son comunes a todos los objetivos excepto cuando se indican en la columna **Objetivos**.

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción | Objetivos |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valor de `true` hace que la compilación falle cuando se produce un error. Un valor de `false` hace que la compilación ignore el error. | Todos los objetivos excepto `package` |
| `name` | `String` | `build`:: Sí,  `install`: No,  `rm`: Sí | `build`:: Sin valor predeterminado,  `install`: El valor de la  `artifactId` propiedad del proyecto Maven | Nombre del paquete en el que se va a actuar | Todos los objetivos excepto `ls` |
| `password` | `String` | Sí | `admin` | La contraseña utilizada para la autenticación con AEM | Todos los objetivos excepto `package` |
| `serverId` | `String` | No | ID de servidor desde el que se recuperarán el nombre de usuario y la contraseña para la autenticación | Todos los objetivos excepto `package` |
| `targetURL` | `String` | Sí | `http://localhost:4502/crx/packmgr/service.jsp` | Dirección URL de la API de servicio HTTP del administrador de paquetes de AEM | Todos los objetivos excepto `package` |
| `timeout` | `int` | No | `5` | Tiempo de espera de conexión para comunicarse con el servicio del administrador de paquetes, en segundos | Todos los objetivos excepto `package` |
| `useProxy` | `boolean` | No | `true` | Un valor de `true` hace que Maven utilice la primera configuración de proxy activa que se encuentra para las solicitudes de proxy al Administrador de paquetes. | Todos los objetivos excepto `package` |
| `userId` | `String` | Sí | `admin` | El nombre de usuario con el que se autenticará AEM | Todos los objetivos excepto `package` |
| `verbose` | `boolean` | No | `false` | Habilita o deshabilita el registro detallado | Todos los objetivos excepto `package` |

### build {#build}

Crea un paquete de contenido que ya está definido en una instancia de AEM.

>[!NOTE]
>
>Este objetivo no necesita ser ejecutado dentro de un proyecto Maven.

#### Parámetros {#parameters}

Todos los parámetros para el objetivo de compilación se describen en la sección [Parámetros comunes](#common-parameters).

### install {#install}

Instala un paquete en el repositorio. La ejecución de este objetivo no requiere un proyecto Maven. El objetivo está enlazado a la fase `install` del ciclo de vida de la compilación de Maven.

#### Parámetros {#parameters-1}

Además de los parámetros siguientes, consulte las descripciones en la sección [Parámetros comunes](#common-parameters).

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|---|
| `artifact` | `String` | No | El valor de la propiedad `artifactId` del proyecto Maven | Una cadena del formulario `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Ninguna | ID del artefacto que se va a instalar |
| `groupId` | `String` | No | Ninguna | El `groupId` artefacto que se va a instalar |
| `install` | `boolean` | No | `true` | Determina si se desempaqueta automáticamente el paquete al cargarse |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | El valor de la variable de sistema `localRepository` | Repositorio local de Maven que no se puede configurar usando la configuración del complemento ya que la propiedad del sistema siempre se utiliza |
| `packageFile` | `java.io.File` | No | El artefacto principal definido para el proyecto Maven | El nombre del archivo de paquete que se va a instalar |
| `packaging` | `String` | No | `zip` | Tipo de embalaje del artefacto que se va a instalar |
| `pomRemoteRepositories` | `java.util.List` | Sí | El valor de la propiedad `remoteArtifactRepositories` que se define para el proyecto Maven | Este valor no se puede configurar con la configuración del complemento y debe especificarse en el proyecto. |
| `project` | `org.apache.maven.project.MavenProject` | Sí | Proyecto para el cual se configura el complemento | Proyecto Maven implícito porque el proyecto contiene la configuración del complemento |
| `repositoryId` (POM),  `repoID` (línea de comandos) | `String` | No | `temp` | ID del repositorio desde el que se recupera el artefacto |
| `repositoryUrl` (POM),  `repoURL` (línea de comandos) | `String` | No | Ninguna | Dirección URL del repositorio desde el que se recupera el artefacto |
| version | Cadena | No | Ninguna | Versión del artefacto que se va a instalar |

### ls {#ls}

Lista los paquetes implementados en el Administrador de paquetes.

#### Parámetros {#parameters-2}

Todos los parámetros del objetivo ls se describen en la sección [Parámetros comunes](#common-parameters).

### rm {#rm}

Quita un paquete del Administrador de paquetes.

#### Parámetros {#parameters-3}

Todos los parámetros del objetivo rm se describen en la sección [Parámetros comunes](#common-parameters).

### desinstalar {#uninstall}

Desinstala un paquete. El paquete permanece en el servidor en estado desinstalado.

#### Parámetros {#parameters-4}

Todos los parámetros del objetivo de desinstalación se describen en la sección [Parámetros comunes](#common-parameters).

### paquete {#package}

Crea un paquete de contenido. La configuración predeterminada del objetivo del paquete incluye el contenido del directorio donde se guardan los archivos compilados. La ejecución del objetivo del paquete requiere que la fase de compilación se haya completado. El objetivo del paquete está enlazado a la fase del paquete del ciclo vital de la compilación de Maven.

#### Parámetros {#parameters-5}

Además de los parámetros siguientes, consulte la descripción del parámetro `name` en la sección [Parámetros comunes](#common-parameters).

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | No | Ninguna | La configuración del archivo que se va a utilizar |
| `builtContentDirectory` | `java.io.File` | Sí | El valor del directorio de salida de la compilación de Maven | El directorio que contiene el contenido que se incluirá en el paquete |
| `dependencies` | `java.util.List` | No | Ninguna |  |
| `embeddedTarget` | `java.lang.String` | No | Ninguna |  |
| `embeddeds` | `java.util.List` | No | Ninguna |  |
| `failOnMissingEmbed` | `boolean` | Sí | `false` | Un valor de `true` hace que la compilación falle cuando no se encuentra un artefacto incrustado en las dependencias del proyecto. Un valor de `false` hace que la compilación ignore estos errores. |
| `filterSource` | `java.io.File` | No | Ninguna | Este parámetro define un archivo que especifica el origen del filtro de espacio de trabajo. Los filtros especificados en la configuración e insertados mediante emebed o subpackages se combinan con el contenido del archivo. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | No | Ninguna | Este parámetro contiene elementos de filtro que definen el contenido del paquete. Cuando se ejecutan, los filtros se incluyen en el archivo `filter.xml`. Consulte la sección [Uso de Filtros](#using-filters) a continuación. |
| `finalName` | `java.lang.String` | Sí | El `finalName` definido en el proyecto Maven (fase de compilación) | El nombre del archivo ZIP del paquete generado, sin la extensión de archivo `.zip` |
| `group` | `java.lang.String` | Sí | El `groupID` definido en el proyecto Maven | El `groupId` del paquete de contenido generado que forma parte de la ruta de instalación de destinatario para el paquete de contenido |
| `outputDirectory` | `java.io.File` | Sí | El directorio de compilación definido en el proyecto Maven | El directorio local donde se guarda el paquete de contenido |
| `prefix` | `java.lang.String` | No | Ninguna |  |
| `project` | `org.apache.maven.project.MavenProject` | Sí | Ninguna | El proyecto Maven |
| `properties` | `java.util.Map` | No | Ninguna | Estos parámetros definen propiedades adicionales que se pueden definir en el archivo `properties.xml`. Estas propiedades no pueden sobrescribir las siguientes propiedades predefinidas: `group` (utilice el parámetro `group` para establecer), `name` (utilice el parámetro `name` para establecer), `version` (utilice el parámetro `version` para establecer), `description` (establecido a partir de la descripción del proyecto), `groupId` (`groupId` del descriptor del proyecto Maven), `artifactId` (`artifactId`) Descriptor de proyecto de maven), `dependencies` (utilice el parámetro `dependencies` para establecer), `createdBy` (el valor de la propiedad del sistema `user.name`), `created` (el tiempo del sistema actual), `requiresRoot` (use el parámetro `requiresRoot` para establecer), &lt;a118/>)> (generado automáticamente a partir del nombre del grupo y del paquete)`packagePath` |
| `requiresRoot` | `boolean` | Sí | false | Define si el paquete requiere root. Se convertirá en la propiedad `requiresRoot` del archivo `properties.xml`. |
| `subPackages` | `java.util.List` | No | Ninguna |  |
| `version` | `java.lang.String` | Sí | Versión definida en el proyecto Maven | Versión del paquete de contenido |
| `workDirectory` | `java.io.File` | Sí | El directorio definido en el proyecto Maven (fase de compilación) | El directorio que contiene el contenido que se incluirá en el paquete |

#### Uso de filtros {#using-filters}

Utilice el elemento filtros para definir el contenido del paquete. Los filtros se agregan al elemento `workspaceFilter` del archivo `META-INF/vault/filter.xml` del paquete.

El siguiente ejemplo de filtro muestra la estructura XML que se va a utilizar:

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

##### Modo de importación {#import-mode}

El elemento `mode` define cómo se ve afectado el contenido del repositorio cuando se importa el paquete. Se pueden utilizar los siguientes valores:

* **Combinar:se agrega** el contenido del paquete que aún no está en el repositorio. El contenido que se encuentra tanto en el paquete como en el repositorio no cambia. No se elimina contenido del repositorio.
* **Reemplazar:** el contenido del paquete que no está en el repositorio se agrega al repositorio. El contenido del repositorio se sustituye por el contenido coincidente del paquete. El contenido se elimina del repositorio cuando no existe en el paquete.
* **Actualización:** El contenido del paquete que no está en el repositorio se agrega al repositorio. El contenido del repositorio se sustituye por el contenido coincidente del paquete. El contenido existente se elimina del repositorio.

Cuando el filtro no contiene ningún elemento `mode`, se utiliza el valor predeterminado de `replace`.

### ayuda {#help}

#### Parámetros {#parameters-6}

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina si se muestran todas las propiedades configurables de cada objetivo |
| `goal` | `String` | No | Ninguna | Estos parámetros definen el nombre del objetivo para el cual mostrar la ayuda. Si no se especifica ningún valor, se muestra la ayuda para todos los objetivos. |
| `indentSize` | `int` | No | `2` | Número de espacios que se utilizarán para la sangría de cada nivel (debe ser positivo si se define) |
| `lineLength` | `int` | No | `80` | Longitud máxima de una línea de visualización (debe ser positiva si se define) |

## Inclusión de una imagen en miniatura o un archivo de propiedades en el paquete {#including-a-thumbnail-image-or-properties-file-in-the-package}

Reemplace los archivos de configuración de paquete predeterminados para personalizar las propiedades del paquete. Por ejemplo, incluya una imagen en miniatura para distinguir el paquete en el Administrador de paquetes y Uso compartido de paquetes.

Los archivos de origen pueden ubicarse en cualquier lugar del sistema de archivos. En el archivo POM, defina los recursos de compilación para copiar los archivos de origen en `target/vault-work/META-INF` para incluirlos en el paquete.

El siguiente código POM agrega los archivos de la carpeta `META-INF` del origen del proyecto al paquete:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

El siguiente código POM sólo agrega una imagen en miniatura al paquete. La imagen en miniatura debe tener el nombre `thumbnail.png` y debe encontrarse en la carpeta `META-INF/vault/definition` del paquete. En este ejemplo, el archivo de origen se encuentra en la carpeta `/src/main/content/META-INF/vault/definition` del proyecto:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Uso del arquetipo del proyecto de AEM para generar AEM proyectos {#using-archetypes}

El último arquetipo del proyecto AEM implementa la estructura del paquete de mejores prácticas para las implementaciones locales y AMS y se recomienda para todos los proyectos AEM.

>[!TIP]
>
>Para obtener más información, consulte el artículo [AEM Estructura del proyecto](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) en el AEM como documentación de Cloud Service, así como la documentación de [AEM Arquetipo del proyecto](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html). Ambos son totalmente compatibles con AEM 6.5.
