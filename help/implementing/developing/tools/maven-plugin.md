---
title: Complemento Maven del paquete de contenido de Adobe
description: Utilice el complemento Maven del paquete de contenido para implementar aplicaciones de AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
feature: Developing
role: Admin, Developer
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---

# Complemento Maven del paquete de contenido de Adobe {#adobe-content-package-maven-plugin}

Utilice el complemento Maven del paquete de contenido de Adobe para integrar las tareas de implementación y administración de paquetes en sus proyectos Maven.

La implementación de los paquetes construidos en AEM la realiza el complemento Maven del paquete de contenido de Adobe y permite la automatización de las tareas que se realizan normalmente con AEM [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md)

* Cree nuevos paquetes a partir de los archivos del sistema de archivos.
* Instale y desinstale paquetes en AEM.
* Genere paquetes que ya estén definidos en AEM.
* Obtenga una lista de los paquetes instalados en AEM.
* Elimine un paquete de AEM.

Este documento detalla cómo utilizar Maven para administrar estas tareas. Sin embargo, también es importante comprender [cómo se estructuran los proyectos de AEM y sus paquetes](#aem-project-structure).

>[!NOTE]
>
>Utilice siempre las versiones más recientes de estos complementos.

>[!NOTE]
>
>La creación del paquete **creation** ahora es propiedad del complemento [Apache Jackrabbit FileVault Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/).
>
>Este artículo describe la **implementación** de los paquetes construidos en AEM tal como lo realiza el complemento Maven del paquete de contenido de Adobe.

## Paquetes y la estructura del proyecto de AEM {#aem-project-structure}

AEM as a Cloud Service se adhiere a las últimas prácticas recomendadas para la administración de paquetes y la estructura de proyectos implementadas por el último tipo de archivo del proyecto de AEM.

>[!TIP]
>
>Consulte el artículo [Estructura del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) en la documentación de AEM as a Cloud Service y la documentación de [Arquetipo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es). Ambos son totalmente compatibles con AEM 6.5.

## Obtención del complemento Maven del paquete de contenido {#obtaining-the-content-package-maven-plugin}

El complemento está disponible en el [Repositorio de Maven Central](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public).

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

Para permitir que Maven descargue el complemento, use el perfil proporcionado en la sección [Obtención del complemento Maven del paquete de contenido](#obtaining-the-content-package-maven-plugin) de esta página.

## Objetivos del complemento Maven del paquete de contenido {#goals-of-the-content-package-maven-plugin}

Los objetivos y parámetros de objetivo que proporciona el complemento Paquete de contenido se describen en las secciones siguientes. Los parámetros que se describen en la sección Parámetros comunes se pueden utilizar para la mayoría de los objetivos. Los parámetros que se aplican a un objetivo se describen en la sección para ese objetivo.

### Prefijo de complemento {#plugin-prefix}

El prefijo del complemento es `content-package`. Utilice este prefijo para ejecutar un objetivo desde la línea de comandos, como en el siguiente ejemplo:

```shell
mvn content-package:build
```

### Prefijo de parámetro {#parameter-prefix}

A menos que se indique lo contrario, los parámetros y objetivos del complemento utilizan el prefijo `vault`, como en el siguiente ejemplo:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

Los objetivos que utilizan proxies para AEM utilizan la primera configuración de proxy válida que se encuentra en la configuración de Maven. Si no se encuentra ninguna configuración proxy, no se utiliza ningún proxy. Vea el parámetro `useProxy` en la sección [Parámetros comunes](#common-parameters).

### Parámetros comunes {#common-parameters}

Los parámetros de la tabla siguiente son comunes a todas las metas, excepto cuando se indican en la columna **Goals**.

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción | Metas |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valor de `true` hace que la compilación falle cuando se produce un error. Un valor de `false` hace que la compilación ignore el error. | Todas las metas excepto `package` |
| `name` | `String` | `build`: Sí, `install`: No, `rm`: Sí | `build`: No predeterminado, `install`: El valor de la propiedad `artifactId` del proyecto Maven | Nombre del paquete sobre el que se va a actuar | Todas las metas excepto `ls` |
| `password` | `String` | Sí | `admin` | La contraseña utilizada para la autenticación con AEM | Todas las metas excepto `package` |
| `serverId` | `String` | No | Identificador de servidor desde el que se recuperan el nombre de usuario y la contraseña para la autenticación | Todas las metas excepto `package` |  |
| `targetURL` | `String` | Sí | `http://localhost:4502/crx/packmgr/service.jsp` | La URL de la API del servicio HTTP del administrador de paquetes de AEM | Todas las metas excepto `package` |
| `timeout` | `int` | No | `5` | Tiempo de espera de conexión para comunicarse con el servicio administrador de paquetes, en segundos | Todas las metas excepto `package` |
| `useProxy` | `boolean` | No | `true` | Un valor de `true` hace que Maven use la primera configuración de proxy activa que se encontró para las solicitudes de proxy al Administrador de paquetes. | Todas las metas excepto `package` |
| `userId` | `String` | Sí | `admin` | El nombre de usuario para autenticarse con AEM | Todas las metas excepto `package` |
| `verbose` | `boolean` | No | `false` | Activa o desactiva el registro detallado | Todas las metas excepto `package` |

### generar {#build}

Crea un paquete de contenido que ya está definido en una instancia de AEM.

>[!NOTE]
>
>No es necesario ejecutar este objetivo dentro de un proyecto Maven.

#### Parámetros {#parameters}

Todos los parámetros del objetivo de compilación se describen en la sección [Parámetros comunes](#common-parameters).

### instalar {#install}

Instala un paquete en el repositorio. La ejecución de esta meta no requiere un proyecto Maven. El objetivo está enlazado a la fase `install` del ciclo de vida de la compilación de Maven.

#### Parámetros {#parameters-1}

Además de los siguientes parámetros, consulte las descripciones en la sección [Parámetros comunes](#common-parameters).

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `artifact` | `String` | No | Valor de la propiedad `artifactId` del proyecto Maven | Una cadena del formulario `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Ninguno | El ID del artefacto que se va a instalar |
| `groupId` | `String` | No | Ninguno | El `groupId` del artefacto que se va a instalar |
| `install` | `boolean` | No | `true` | Determina si se debe desempaquetar el paquete automáticamente cuando se carga |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | Valor de la variable del sistema `localRepository` | El repositorio local de Maven que no se puede configurar con la configuración del complemento, ya que la propiedad del sistema siempre se utiliza |
| `packageFile` | `java.io.File` | No | El artefacto principal que se define para el proyecto Maven | Nombre del archivo del paquete que se va a instalar |
| `packaging` | `String` | No | `zip` | El tipo de paquete del artefacto que se va a instalar |
| `pomRemoteRepositories` | `java.util.List` | Sí | Valor de la propiedad `remoteArtifactRepositories` definida para el proyecto Maven | Este valor no se puede configurar con la configuración del complemento y debe especificarse en el proyecto. |
| `project` | `org.apache.maven.project.MavenProject` | Sí | El proyecto para el que está configurado el complemento | El proyecto Maven, que está implícito porque el proyecto contiene la configuración del complemento |
| `repositoryId` (POM), `repoID` (línea de comandos) | `String` | No | `temp` | El ID del repositorio del que se recupera el artefacto |
| `repositoryUrl` (POM), `repoURL` (línea de comandos) | `String` | No | Ninguno | La dirección URL del repositorio desde el que se recupera el artefacto |
| version | Cadena | No | Ninguno | La versión del artefacto que se va a instalar |

### ls {#ls}

Enumera los paquetes implementados en [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md).

#### Parámetros {#parameters-2}

Todos los parámetros del objetivo ls se describen en la sección [Parámetros comunes](#common-parameters).

### rm {#rm}

Quita un paquete de [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md).

#### Parámetros {#parameters-3}

Todos los parámetros del objetivo rm se describen en la sección [Parámetros comunes](#common-parameters).

### desinstalar {#uninstall}

Desinstala un paquete. El paquete permanece en el servidor en estado desinstalado.

#### Parámetros {#parameters-4}

Todos los parámetros del objetivo de desinstalación se describen en la sección [Parámetros comunes](#common-parameters).


### help {#help}

#### Parámetros {#parameters-6}

| Nombre | Tipo | Requerido | Valor predeterminado | Descripción |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina si se deben mostrar todas las propiedades configurables para cada objetivo |
| `goal` | `String` | No | Ninguno | Estos parámetros definen el nombre del objetivo para el que se va a mostrar ayuda. Si no se especifica ningún valor, se muestra la ayuda para todas las metas. |
| `indentSize` | `int` | No | `2` | El número de espacios que se utilizarán para la sangría de cada nivel (debe ser positivo si está definido) |
| `lineLength` | `int` | No | `80` | Longitud máxima de una línea de visualización (debe ser positiva si se define) |

## Inclusión de una imagen en miniatura o un archivo de propiedades en el paquete {#including-a-thumbnail-image-or-properties-file-in-the-package}

Reemplace los archivos de configuración predeterminados del paquete para personalizar las propiedades del paquete. Por ejemplo, incluya una imagen en miniatura para distinguir el paquete en [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md).

Los archivos de origen se pueden encontrar en cualquier lugar del sistema de archivos. En el archivo POM, defina los recursos de compilación para copiar los archivos de origen en `target/vault-work/META-INF` para incluirlos en el paquete.

El siguiente código POM agrega los archivos de la carpeta `META-INF` del origen del proyecto al paquete:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail and so on) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

El siguiente código POM agrega solo una imagen en miniatura al paquete. La imagen en miniatura debe llamarse `thumbnail.png` y debe encontrarse en la carpeta `META-INF/vault/definition` del paquete. En este ejemplo, el archivo de origen se encuentra en la carpeta `/src/main/content/META-INF/vault/definition` del proyecto:

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

## Uso del tipo de archivo del proyecto AEM para generar proyectos AEM {#using-archetypes}

El último tipo de archivo del proyecto de AEM implementa la estructura de paquetes de prácticas recomendadas para implementaciones locales y de AMS, y se recomienda para todos los proyectos de AEM.

>[!TIP]
>
>Consulte el artículo [Estructura del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) en la documentación de AEM as a Cloud Service y la documentación de [Arquetipo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es). Ambos son totalmente compatibles con AEM 6.5.
