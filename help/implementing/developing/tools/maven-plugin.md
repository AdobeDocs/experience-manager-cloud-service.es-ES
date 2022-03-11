---
title: Complemento Maven del paquete de contenido de Adobe
description: Utilice el complemento Maven del paquete de contenido para implementar aplicaciones AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: 278470482a582db7d88bfbe6f851eb3070afc0df
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 5%

---

# Complemento Maven del paquete de contenido de Adobe {#adobe-content-package-maven-plugin}

Utilice el complemento Maven del paquete de contenido de Adobe para integrar las tareas de implementación y administración de paquetes en sus proyectos de Maven.

La implementación de los paquetes construidos en AEM se realiza mediante el complemento Maven del paquete de contenido de Adobe y permite la automatización de las tareas que normalmente se realizan mediante AEM [Administrador de paquetes:](/help/implementing/developing/tools/package-manager.md)

* Cree nuevos paquetes a partir de archivos en el sistema de archivos.
* Instale y desinstale paquetes en AEM.
* Generar paquetes que ya están definidos en AEM.
* Obtenga una lista de paquetes instalados en AEM.
* Elimine un paquete de AEM.

Este documento detalla cómo utilizar Maven para administrar estas tareas. Sin embargo, también es importante entender [cómo se estructuran AEM proyectos y sus paquetes.](#aem-project-structure)

>[!NOTE]
>
>La creación de paquetes ahora es propiedad de [Complemento Maven del paquete Apache Jackrabbit FileVault Package](https://jackrabbit.apache.org/filevault-package-maven-plugin/). La implementación de los paquetes construidos en AEM es realizada por el complemento Maven del paquete de contenido de Adobe como se describe aquí.

## Paquetes y la estructura AEM del proyecto {#aem-project-structure}

AEM as a Cloud Service se adhiere a las prácticas recomendadas más recientes para la administración de paquetes y la estructura del proyecto, tal como se implementó en el último tipo de archivo AEM del proyecto.

>[!TIP]
>
>Para obtener más información, consulte la [AEM estructura del proyecto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) artículo de la documentación as a Cloud Service AEM así como el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) documentación. Ambos son totalmente compatibles con la versión AEM 6.5.

## Obtención del complemento Maven del paquete de contenido {#obtaining-the-content-package-maven-plugin}

El complemento está disponible desde la [Repositorio Central Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Parámetros y objetivos del complemento Maven del paquete de contenido

Para utilizar el complemento Maven del paquete de contenido, agregue el siguiente elemento de complemento dentro del elemento de compilación del archivo POM:

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

Para permitir que Maven descargue el complemento, utilice el perfil proporcionado en la variable [Obtención del complemento Maven del paquete de contenido](#obtaining-the-content-package-maven-plugin) en esta página.

## Objetivos del complemento Maven del paquete de contenido {#goals-of-the-content-package-maven-plugin}

Los objetivos y parámetros de objetivo que proporciona el complemento Paquete de contenido se describen en las secciones siguientes. Los parámetros que se describen en la sección Parámetros comunes se pueden utilizar para la mayoría de los objetivos. Los parámetros que se aplican a un objetivo se describen en la sección para ese objetivo.

### Prefijo de complemento {#plugin-prefix}

El prefijo del complemento es `content-package`. Utilice este prefijo para ejecutar un objetivo desde la línea de comandos, como en el siguiente ejemplo:

```shell
mvn content-package:build
```

### Prefijo de parámetro {#parameter-prefix}

A menos que se indique lo contrario, los objetivos y parámetros del complemento utilizan la variable `vault` , como en el siguiente ejemplo:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

Los objetivos que utilizan proxies para AEM utilizan la primera configuración de proxy válida que se encuentra en la configuración de Maven. Si no se encuentra ninguna configuración de proxy, no se utiliza ningún proxy. Consulte la `useProxy` en el [Parámetros comunes](#common-parameters) para obtener más información.

### Parámetros comunes {#common-parameters}

Los parámetros de la tabla siguiente son comunes para todos los objetivos excepto cuando se señalan en la **Objetivos** para abrir el Navegador.

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción | Objetivos |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valor de `true` hace que la compilación falle cuando se produce un error. Un valor de `false` hace que la compilación ignore el error. | Todos los objetivos excepto `package` |
| `name` | `String` | `build`: Sí, `install`: No, `rm`: Sí | `build`: Sin predeterminado, `install`: El valor de la variable `artifactId` propiedad del proyecto Maven | El nombre del paquete en el que debe actuar | Todos los objetivos excepto `ls` |
| `password` | `String` | Sí | `admin` | La contraseña utilizada para la autenticación con AEM | Todos los objetivos excepto `package` |
| `serverId` | `String` | No | El ID de servidor desde el que se recuperarán el nombre de usuario y la contraseña para la autenticación | Todos los objetivos excepto `package` |
| `targetURL` | `String` | Sí | `http://localhost:4502/crx/packmgr/service.jsp` | La URL de la API de servicio HTTP del administrador de paquetes AEM | Todos los objetivos excepto `package` |
| `timeout` | `int` | No | `5` | Tiempo de espera de conexión para comunicarse con el servicio del administrador de paquetes, en segundos | Todos los objetivos excepto `package` |
| `useProxy` | `boolean` | No | `true` | Un valor de `true` hace que Maven utilice la primera configuración de proxy activa que se encuentra para las solicitudes de proxy al Administrador de paquetes. | Todos los objetivos excepto `package` |
| `userId` | `String` | Sí | `admin` | El nombre de usuario que se va a autenticar con AEM | Todos los objetivos excepto `package` |
| `verbose` | `boolean` | No | `false` | Habilita o deshabilita el registro detallado | Todos los objetivos excepto `package` |

### versión {#build}

Crea un paquete de contenido que ya está definido en una instancia de AEM.

>[!NOTE]
>
>No es necesario ejecutar este objetivo dentro de un proyecto de Maven.

#### Parámetros {#parameters}

Todos los parámetros para el objetivo de compilación se describen en la sección [Parámetros comunes](#common-parameters) para obtener más información.

### instalar {#install}

Instala un paquete en el repositorio. La ejecución de este objetivo no requiere un proyecto Maven. El objetivo está enlazado con la variable `install` del ciclo vital de la compilación de Maven.

#### Parámetros {#parameters-1}

Además de los parámetros siguientes, consulte las descripciones en la [Parámetros comunes](#common-parameters) para obtener más información.

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `artifact` | `String` | No | El valor de la variable `artifactId` propiedad del proyecto Maven | Una cadena del formulario `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Ninguno | El ID del artefacto que se va a instalar |
| `groupId` | `String` | No | Ninguno | La variable `groupId` del artefacto que se va a instalar |
| `install` | `boolean` | No | `true` | Determina si se desempaqueta automáticamente el paquete cuando se carga |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | El valor de la variable `localRepository` variable del sistema | El repositorio local de Maven que no se puede configurar usando la configuración del complemento como propiedad del sistema siempre se utiliza |
| `packageFile` | `java.io.File` | No | El artefacto principal definido para el proyecto Maven | El nombre del archivo del paquete que se va a instalar |
| `packaging` | `String` | No | `zip` | El tipo de embalaje del artefacto que se va a instalar |
| `pomRemoteRepositories` | `java.util.List` | Sí | El valor de la variable `remoteArtifactRepositories` propiedad definida para el proyecto Maven | Este valor no se puede configurar con la configuración del complemento y debe especificarse en el proyecto. |
| `project` | `org.apache.maven.project.MavenProject` | Sí | El proyecto para el que está configurado el complemento | El proyecto Maven que está implícito porque el proyecto contiene la configuración del complemento |
| `repositoryId` (POM), `repoID` (línea de comandos) | `String` | No | `temp` | ID del repositorio desde el que se recupera el artefacto |
| `repositoryUrl` (POM), `repoURL` (línea de comandos) | `String` | No | Ninguno | La dirección URL del repositorio desde el que se recupera el artefacto |
| version | Cadena | No | Ninguno | Versión del artefacto que se va a instalar |

### ls {#ls}

Enumera los paquetes que se implementan en [Administrador de paquetes.](/help/implementing/developing/tools/package-manager.md)

#### Parámetros {#parameters-2}

Todos los parámetros del objetivo ls se describen en la sección [Parámetros comunes](#common-parameters) para obtener más información.

### rm {#rm}

Elimina un paquete de [Administrador de paquetes.](/help/implementing/developing/tools/package-manager.md)

#### Parámetros {#parameters-3}

Todos los parámetros del objetivo rm se describen en la sección [Parámetros comunes](#common-parameters) para obtener más información.

### desinstalar {#uninstall}

Desinstala un paquete. El paquete permanece en el servidor en estado desinstalado.

#### Parámetros {#parameters-4}

Todos los parámetros del objetivo de desinstalación se describen en la sección [Parámetros comunes](#common-parameters) para obtener más información.

### paquete {#package}

Crea un paquete de contenido. La configuración predeterminada del objetivo del paquete incluye el contenido del directorio donde se guardan los archivos compilados. La ejecución del objetivo del paquete requiere que la fase de compilación se haya completado. El objetivo del paquete está enlazado a la fase del paquete del ciclo vital de la compilación de Maven.

#### Parámetros {#parameters-5}

Además de los parámetros siguientes, consulte la descripción de la variable `name` en el [Parámetros comunes](#common-parameters) para obtener más información.

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | No | Ninguno | La configuración del archivo que se va a utilizar |
| `builtContentDirectory` | `java.io.File` | Sí | El valor del directorio de salida de la compilación de Maven | El directorio que contiene el contenido que se va a incluir en el paquete |
| `dependencies` | `java.util.List` | No | Ninguno |  |
| `embeddedTarget` | `java.lang.String` | No | Ninguno |  |
| `embeddeds` | `java.util.List` | No | Ninguno |  |
| `failOnMissingEmbed` | `boolean` | Sí | `false` | Un valor de `true` hace que la compilación falle cuando no se encuentra un artefacto incrustado en las dependencias del proyecto. Un valor de `false` hace que la compilación ignore estos errores. |
| `filterSource` | `java.io.File` | No | Ninguno | Este parámetro define un archivo que especifica el origen del filtro de espacio de trabajo. Los filtros especificados en la configuración e insertados mediante emebed o subpackages se combinan con el contenido del archivo. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | No | Ninguno | Este parámetro contiene elementos de filtro que definen el contenido del paquete. Cuando se ejecuta, los filtros se incluyen en la variable `filter.xml` archivo. Consulte la [Uso de filtros](#using-filters) a continuación. |
| `finalName` | `java.lang.String` | Sí | La variable `finalName` definida en el proyecto Maven (fase de compilación) | El nombre del archivo ZIP del paquete generado, sin la variable `.zip` extensión de archivo |
| `group` | `java.lang.String` | Sí | La variable `groupID` definida en el proyecto Maven | La variable `groupId` del paquete de contenido generado que forma parte de la ruta de instalación de destino para el paquete de contenido |
| `outputDirectory` | `java.io.File` | Sí | El directorio de compilación definido en el proyecto Maven | El directorio local donde se guarda el paquete de contenido |
| `prefix` | `java.lang.String` | No | Ninguno |  |
| `project` | `org.apache.maven.project.MavenProject` | Sí | Ninguno | El proyecto Maven |
| `properties` | `java.util.Map` | No | Ninguno | Estos parámetros definen propiedades adicionales que puede establecer en la variable `properties.xml` archivo. Estas propiedades no pueden sobrescribir las siguientes propiedades predefinidas: `group` (use `group` parámetro a establecer), `name` (use `name` parámetro a establecer), `version` (use `version` parámetro a establecer), `description` (definido a partir de la descripción del proyecto), `groupId` (`groupId` del descriptor del proyecto Maven), `artifactId` (`artifactId` del descriptor del proyecto Maven), `dependencies` (use `dependencies` parámetro a establecer), `createdBy` (el valor de la variable `user.name` propiedad del sistema), `created` (la hora del sistema actual), `requiresRoot` (use `requiresRoot` parámetro a establecer), `packagePath` (generado automáticamente a partir del nombre del grupo y del paquete) |
| `requiresRoot` | `boolean` | Sí | false | Define si el paquete requiere root. Esto se convertirá en el `requiresRoot` propiedad de la variable `properties.xml` archivo. |
| `subPackages` | `java.util.List` | No | Ninguno |  |
| `version` | `java.lang.String` | Sí | La versión definida en el proyecto Maven | La versión del paquete de contenido |
| `workDirectory` | `java.io.File` | Sí | El directorio definido en el proyecto Maven (fase de compilación) | El directorio que contiene el contenido que se va a incluir en el paquete |

#### Uso de filtros {#using-filters}

Utilice el elemento filters para definir el contenido del paquete. Los filtros se añaden al `workspaceFilter` en el `META-INF/vault/filter.xml` del paquete.

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

La variable `mode` define cómo se ve afectado el contenido del repositorio cuando se importa el paquete. Se pueden utilizar los siguientes valores:

* **Combinar:** Se añade contenido en el paquete que no está ya en el repositorio. El contenido que se encuentra tanto en el paquete como en el repositorio no cambia. No se elimina ningún contenido del repositorio.
* **Reemplazar:** El contenido del paquete que no está en el repositorio se agrega al repositorio. El contenido del repositorio se reemplaza por contenido coincidente en el paquete. El contenido se elimina del repositorio cuando no existe en el paquete.
* **Actualización:** El contenido del paquete que no está en el repositorio se agrega al repositorio. El contenido del repositorio se reemplaza por contenido coincidente en el paquete. El contenido existente se elimina del repositorio.

Cuando el filtro contiene no `mode` elemento, el valor predeterminado de `replace` se utiliza.

### ayuda {#help}

#### Parámetros {#parameters-6}

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina si se mostrarán todas las propiedades configurables para cada objetivo |
| `goal` | `String` | No | Ninguno | Estos parámetros definen el nombre del objetivo para el que mostrar la ayuda. Si no se especifica ningún valor, se muestra ayuda para todos los objetivos. |
| `indentSize` | `int` | No | `2` | El número de espacios que se deben utilizar para la sangría de cada nivel (debe ser positivo si se define) |
| `lineLength` | `int` | No | `80` | La longitud máxima de una línea de visualización (debe ser positiva si se define) |

## Inclusión de una imagen en miniatura o un archivo de propiedades en el paquete {#including-a-thumbnail-image-or-properties-file-in-the-package}

Reemplace los archivos de configuración de paquetes predeterminados para personalizar las propiedades del paquete. Por ejemplo, incluya una imagen en miniatura para distinguir el paquete en [Administrador de paquetes.](/help/implementing/developing/tools/package-manager.md)

Los archivos de origen se pueden ubicar en cualquier lugar del sistema de archivos. En el archivo POM, defina los recursos de compilación para copiar los archivos de origen en la variable `target/vault-work/META-INF` para su inclusión en el paquete.

El siguiente código POM agrega los archivos en la variable `META-INF` carpeta del origen del proyecto al paquete:

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

El siguiente código POM añade solo una imagen en miniatura al paquete. Se debe asignar un nombre a la imagen en miniatura `thumbnail.png`y debe estar ubicado en la variable `META-INF/vault/definition` carpeta del paquete. En este ejemplo, el archivo de origen se encuentra en la variable `/src/main/content/META-INF/vault/definition` carpeta del proyecto:

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

## Uso del tipo de archivo del proyecto AEM para generar AEM proyectos {#using-archetypes}

El último tipo de archivo del proyecto de AEM implementa la estructura de paquetes de prácticas recomendadas tanto para implementaciones locales como de AMS y se recomienda para todos los proyectos de AEM.

>[!TIP]
>
>Para obtener más información, consulte la [AEM estructura del proyecto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) artículo de la documentación as a Cloud Service AEM así como el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) documentación. Ambos son totalmente compatibles con la versión AEM 6.5.
