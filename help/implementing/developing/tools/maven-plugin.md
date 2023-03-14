---
title: Complemento Maven del paquete de contenido de Adobe
description: AEM Utilice el complemento Maven del paquete de contenido para implementar aplicaciones de
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: ba4e2427873fc9f5d91ee4f520df01018000a4c7
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 6%

---

# Complemento Maven del paquete de contenido de Adobe {#adobe-content-package-maven-plugin}

Utilice el complemento Maven del paquete de contenido de Adobe para integrar las tareas de implementación y administración de paquetes en sus proyectos Maven.

AEM La implementación de los paquetes construidos en el se realiza mediante el complemento Maven del paquete de contenido de Adobe AEM y permite la automatización de las tareas que se realizan normalmente mediante el uso de la aplicación de paquetes de [Administrador de paquetes:](/help/implementing/developing/tools/package-manager.md)

* Cree nuevos paquetes a partir de los archivos del sistema de archivos.
* AEM Instale y desinstale paquetes en el entorno de la aplicación de.
* AEM Genere paquetes que ya estén definidos en el servicio de correo electrónico de.
* AEM Obtenga una lista de los paquetes instalados en los paquetes de.
* AEM Elimine un paquete de la lista de distribución de.

Este documento detalla cómo utilizar Maven para administrar estas tareas. Sin embargo, también es importante comprender [AEM cómo se estructuran los proyectos de y sus paquetes de datos.](#aem-project-structure)

>[!NOTE]
>
>Paquete **creación** ahora es propiedad de [Complemento Maven del paquete Apache Jackrabbit FileVault.](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>* El `content-package-maven-plugin` ya no es compatible con el empaquetado de la versión 1.0.2.
>* Este artículo describe la **implementación** AEM Uno de los paquetes construidos que se van a lo realiza el complemento Maven del paquete de contenido de Adobe.


## AEM Paquetes y la estructura del proyecto de {#aem-project-structure}

AEM El as a Cloud Service AEM se adhiere a las prácticas recomendadas más recientes para la administración de paquetes y la estructura de proyectos implementadas por el último tipo de archivo del proyecto de.

>[!TIP]
>
>Para obtener más información, consulte la [AEM Estructura del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) AEM artículo en la documentación as a Cloud Service de la, así como el [AEM Tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) documentación. AEM Ambos son totalmente compatibles con la versión 6.5 de la.

## Obtención del complemento Maven del paquete de contenido {#obtaining-the-content-package-maven-plugin}

El complemento está disponible en [Repositorio de Maven Central.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Parámetros y objetivos del complemento Maven del paquete de contenido

Para utilizar el complemento Maven del paquete de contenido, agregue el siguiente elemento de complemento dentro del elemento de compilación del archivo POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>1.0.4</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Para permitir que Maven descargue el complemento, utilice el perfil proporcionado en la [Obtención del complemento Maven del paquete de contenido](#obtaining-the-content-package-maven-plugin) de esta página.

## Objetivos del complemento Maven del paquete de contenido {#goals-of-the-content-package-maven-plugin}

Los objetivos y parámetros de objetivo que proporciona el complemento Paquete de contenido se describen en las secciones siguientes. Los parámetros que se describen en la sección Parámetros comunes se pueden utilizar para la mayoría de los objetivos. Los parámetros que se aplican a un objetivo se describen en la sección para ese objetivo.

### Prefijo de complemento {#plugin-prefix}

El prefijo del complemento es `content-package`. Utilice este prefijo para ejecutar un objetivo desde la línea de comandos, como en el siguiente ejemplo:

```shell
mvn content-package:build
```

### Prefijo de parámetro {#parameter-prefix}

A menos que se indique lo contrario, los objetivos y parámetros del complemento utilizan la variable `vault` prefijo, como en el siguiente ejemplo:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

AEM Los objetivos que utilizan proxies para el uso de la primera configuración de proxy válida que se encuentra en la configuración de Maven. Si no se encuentra ninguna configuración proxy, no se utiliza ningún proxy. Consulte la `useProxy` en el campo [Parámetros comunes](#common-parameters) sección.

### Parámetros comunes {#common-parameters}

Los parámetros de la siguiente tabla son comunes a todos los objetivos, excepto cuando se indican en la **Metas** columna.

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción | Objetivos |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valor de `true` provoca que la generación falle cuando se produce un error. Un valor de `false` hace que la generación ignore el error. | Todas las metas excepto `package` |
| `name` | `String` | `build`: Sí, `install`: No, `rm`: sí | `build`: Sin valor predeterminado, `install`: El valor del `artifactId` propiedad del proyecto Maven | Nombre del paquete sobre el que se va a actuar | Todas las metas excepto `ls` |
| `password` | `String` | Sí | `admin` | AEM La contraseña utilizada para la autenticación con el servicio de autenticación de | Todas las metas excepto `package` |
| `serverId` | `String` | No | Identificador de servidor desde el que se recuperan el nombre de usuario y la contraseña para la autenticación | Todas las metas excepto `package` |
| `targetURL` | `String` | Sí | `http://localhost:4502/crx/packmgr/service.jsp` | AEM La dirección URL de la API del servicio HTTP del administrador de paquetes de | Todas las metas excepto `package` |
| `timeout` | `int` | No | `5` | Tiempo de espera de conexión para comunicarse con el servicio administrador de paquetes, en segundos | Todas las metas excepto `package` |
| `useProxy` | `boolean` | No | `true` | Un valor de `true` hace que Maven utilice la primera configuración proxy activa que se encuentre para enviar solicitudes de proxy al Administrador de paquetes. | Todas las metas excepto `package` |
| `userId` | `String` | Sí | `admin` | AEM El nombre de usuario con el que autenticarse en el servicio de autenticación de | Todas las metas excepto `package` |
| `verbose` | `boolean` | No | `false` | Activa o desactiva el registro detallado | Todas las metas excepto `package` |

### generar {#build}

AEM Crea un paquete de contenido que ya está definido en una instancia de.

>[!NOTE]
>
>No es necesario ejecutar este objetivo dentro de un proyecto Maven.

#### Parámetros {#parameters}

Todos los parámetros del objetivo de compilación se describen en la sección [Parámetros comunes](#common-parameters) sección.

### instalar {#install}

Instala un paquete en el repositorio. La ejecución de esta meta no requiere un proyecto Maven. El objetivo está enlazado al `install` fase del ciclo de vida de la versión de Maven.

#### Parámetros {#parameters-1}

Además de los siguientes parámetros, consulte las descripciones en la sección [Parámetros comunes](#common-parameters) sección.

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `artifact` | `String` | No | El valor del `artifactId` propiedad del proyecto Maven | Una cadena del formulario `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Ninguno | El ID del artefacto que se va a instalar |
| `groupId` | `String` | No | Ninguno | El `groupId` del artefacto a instalar |
| `install` | `boolean` | No | `true` | Determina si se debe desempaquetar el paquete automáticamente cuando se carga |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | El valor del `localRepository` variable del sistema | El repositorio local de Maven que no se puede configurar con la configuración del complemento, ya que la propiedad del sistema siempre se utiliza |
| `packageFile` | `java.io.File` | No | El artefacto principal que se define para el proyecto Maven | Nombre del archivo del paquete que se va a instalar |
| `packaging` | `String` | No | `zip` | El tipo de paquete del artefacto que se va a instalar |
| `pomRemoteRepositories` | `java.util.List` | Sí | El valor del `remoteArtifactRepositories` propiedad definida para el proyecto Maven | Este valor no se puede configurar con la configuración del complemento y debe especificarse en el proyecto. |
| `project` | `org.apache.maven.project.MavenProject` | Sí | El proyecto para el que está configurado el complemento | El proyecto Maven, que está implícito porque el proyecto contiene la configuración del complemento |
| `repositoryId` (POM), `repoID` (línea de comandos) | `String` | No | `temp` | El ID del repositorio del que se recupera el artefacto |
| `repositoryUrl` (POM), `repoURL` (línea de comandos) | `String` | No | Ninguno | La dirección URL del repositorio desde el que se recupera el artefacto |
| version | Cadena | No | Ninguno | La versión del artefacto que se va a instalar |

### ls {#ls}

Enumera los paquetes implementados en [Administrador de paquetes.](/help/implementing/developing/tools/package-manager.md)

#### Parámetros {#parameters-2}

Todos los parámetros del objetivo ls se describen en la sección [Parámetros comunes](#common-parameters) sección.

### rm {#rm}

Quita un paquete de [Administrador de paquetes.](/help/implementing/developing/tools/package-manager.md)

#### Parámetros {#parameters-3}

Todos los parámetros de la meta rm se describen en la sección [Parámetros comunes](#common-parameters) sección.

### desinstalar {#uninstall}

Desinstala un paquete. El paquete permanece en el servidor en estado desinstalado.

#### Parámetros {#parameters-4}

Todos los parámetros del objetivo de desinstalación se describen en la [Parámetros comunes](#common-parameters) sección.

### paquete {#package}

Crea un paquete de contenido. La configuración predeterminada del objetivo del paquete incluye el contenido del directorio donde se guardan los archivos compilados. La ejecución del objetivo del paquete requiere que la fase de compilación haya finalizado. El objetivo del paquete está enlazado a la fase de paquetes del ciclo vital de generación de Maven.

#### Parámetros {#parameters-5}

Además de los siguientes parámetros, consulte la descripción del `name` en el campo [Parámetros comunes](#common-parameters) sección.

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | No | Ninguno | La configuración del archivo que se va a utilizar |
| `builtContentDirectory` | `java.io.File` | Sí | El valor del directorio de salida de la compilación de Maven | El directorio que contiene el contenido que se va a incluir en el paquete |
| `dependencies` | `java.util.List` | No | Ninguno |  |
| `embeddedTarget` | `java.lang.String` | No | Ninguno |  |
| `embeddeds` | `java.util.List` | No | Ninguno |  |
| `failOnMissingEmbed` | `boolean` | Sí | `false` | Un valor de `true` provoca que la generación falle cuando no se encuentra un artefacto incrustado en las dependencias del proyecto. Un valor de `false` hace que la generación ignore estos errores. |
| `filterSource` | `java.io.File` | No | Ninguno | Este parámetro define un archivo que especifica el origen del filtro del espacio de trabajo. Los filtros especificados en la configuración e insertados mediante incrustaciones o subpaquetes se combinan con el contenido del archivo. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | No | Ninguno | Este parámetro contiene elementos de filtro que definen el contenido del paquete. Cuando se ejecutan, los filtros se incluyen en `filter.xml` archivo. Consulte la [Uso de filtros](#using-filters) más abajo. |
| `finalName` | `java.lang.String` | Sí | El `finalName` definido en el proyecto Maven (fase de compilación) | El nombre del archivo ZIP del paquete generado, sin el `.zip` extensión de archivo |
| `group` | `java.lang.String` | Sí | El `groupID` definido en el proyecto Maven | El `groupId` del paquete de contenido generado que forma parte de la ruta de instalación de target para el paquete de contenido |
| `outputDirectory` | `java.io.File` | Sí | El directorio de compilación definido en el proyecto Maven | El directorio local donde se guarda el paquete de contenido |
| `prefix` | `java.lang.String` | No | Ninguno |  |
| `project` | `org.apache.maven.project.MavenProject` | Sí | Ninguno | El proyecto Maven |
| `properties` | `java.util.Map` | No | Ninguno | Estos parámetros definen propiedades adicionales que puede establecer en la variable `properties.xml` archivo. Estas propiedades no pueden sobrescribir las siguientes propiedades predefinidas: `group` (use `group` parámetro que se va a establecer), `name` (use `name` parámetro que se va a establecer), `version` (use `version` parámetro que se va a establecer), `description` (configurado a partir de la descripción del proyecto), `groupId` (`groupId` del descriptor de proyecto Maven), `artifactId` (`artifactId` del descriptor de proyecto Maven), `dependencies` (use `dependencies` parámetro que se va a establecer), `createdBy` (el valor de la variable `user.name` propiedad del sistema), `created` (la hora actual del sistema), `requiresRoot` (use `requiresRoot` parámetro que se va a establecer), `packagePath` (generado automáticamente a partir del nombre del grupo y del paquete) |
| `requiresRoot` | `boolean` | Sí | false | Define si el paquete requiere raíz. Esto se convertirá en el `requiresRoot` propiedad del `properties.xml` archivo. |
| `subPackages` | `java.util.List` | No | Ninguno |  |
| `version` | `java.lang.String` | Sí | La versión definida en el proyecto de Maven | La versión del paquete de contenido |
| `workDirectory` | `java.io.File` | Sí | El directorio definido en el proyecto Maven (fase de compilación) | El directorio que contiene el contenido que se va a incluir en el paquete |

#### Uso de filtros {#using-filters}

Utilice el elemento filters para definir el contenido del paquete. Los filtros se añaden a `workspaceFilter` elemento en el `META-INF/vault/filter.xml` del paquete.

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

El `mode` define cómo se ve afectado el contenido del repositorio cuando se importa el paquete. Se pueden utilizar los siguientes valores:

* **Combinar:** Se añade contenido en el paquete que no está ya en el repositorio. El contenido que está en el paquete y en el repositorio no cambia. No se elimina contenido del repositorio.
* **Reemplazar:** El contenido del paquete que no está en el repositorio se agrega al repositorio. El contenido del repositorio se reemplaza con el contenido coincidente del paquete. El contenido se elimina del repositorio cuando no existe en el paquete.
* **Actualización:** El contenido del paquete que no está en el repositorio se agrega al repositorio. El contenido del repositorio se reemplaza con el contenido coincidente del paquete. El contenido existente se elimina del repositorio.

Cuando el filtro no contiene `mode` , el valor predeterminado de `replace` se utiliza.

### help {#help}

#### Parámetros {#parameters-6}

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina si se deben mostrar todas las propiedades configurables para cada objetivo |
| `goal` | `String` | No | Ninguno | Estos parámetros definen el nombre del objetivo para el que se va a mostrar ayuda. Si no se especifica ningún valor, se muestra la ayuda para todas las metas. |
| `indentSize` | `int` | No | `2` | El número de espacios que se utilizarán para la sangría de cada nivel (debe ser positivo si está definido) |
| `lineLength` | `int` | No | `80` | Longitud máxima de una línea de visualización (debe ser positiva si se define) |

## Inclusión de una imagen en miniatura o un archivo de propiedades en el paquete {#including-a-thumbnail-image-or-properties-file-in-the-package}

Reemplace los archivos de configuración predeterminados del paquete para personalizar las propiedades del paquete. Por ejemplo, incluya una imagen en miniatura para distinguir el paquete en [Administrador de paquetes.](/help/implementing/developing/tools/package-manager.md)

Los archivos de origen se pueden encontrar en cualquier lugar del sistema de archivos. En el archivo POM, defina los recursos de compilación para copiar los archivos de origen en el `target/vault-work/META-INF` para su inclusión en el envase.

El siguiente código POM agrega los archivos en la `META-INF` carpeta del origen del proyecto al paquete:

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

El siguiente código POM agrega solo una imagen en miniatura al paquete. La imagen en miniatura debe tener el nombre `thumbnail.png`, y debe estar ubicado en el `META-INF/vault/definition` del paquete. En este ejemplo, el archivo de origen se encuentra en `/src/main/content/META-INF/vault/definition` carpeta del proyecto:

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

## AEM AEM Uso del tipo de archivo del proyecto de para generar proyectos de {#using-archetypes}

AEM AEM El último tipo de archivo del proyecto de implementa la estructura de paquetes de prácticas recomendadas tanto para implementaciones locales como de AMS, y se recomienda para todos los proyectos de.

>[!TIP]
>
>Para obtener más información, consulte la [AEM Estructura del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) AEM artículo en la documentación as a Cloud Service de la, así como el [AEM Tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) documentación. AEM Ambos son totalmente compatibles con la versión 6.5 de la.
