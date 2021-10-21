---
title: Implementación en AEM as a Cloud Service
description: 'Implementación en AEM as a Cloud Service '
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: f85a4dd109459e216d23a9da67f67d4ad7aa8709
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 1%

---

# Implementación en AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introducción {#introduction}

The fundamentals of code development are similar in AEM as a Cloud Service compared to the AEM On Premise and Managed Services solutions. Developers write code and test it locally, which is then pushed to remote AEM as a Cloud Service environments. Se requiere Cloud Manager, que era una herramienta de entrega de contenido opcional para Managed Services. Este es ahora el único mecanismo para implementar código en entornos as a Cloud Service AEM.

La actualización de la variable [AEM versión](/help/implementing/deploying/aem-version-updates.md) siempre es un evento de implementación independiente de la extracción [código personalizado](#customer-releases). Visto de otra manera, las versiones de código personalizado deben probarse con la versión AEM que está en producción, ya que eso es lo que se implementará en la parte superior. AEM actualizaciones de la versión que se producen después de eso, que serán frecuentes y se aplicarán automáticamente. Están pensados para ser compatibles con el código de cliente ya implementado.

El resto de este documento describirá cómo los desarrolladores deben adaptar sus prácticas para que funcionen tanto con las actualizaciones de versiones de AEM as a Cloud Service como con las actualizaciones de clientes.

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## Versiones de clientes {#customer-releases}

### Codificación con la versión AEM correcta {#coding-against-the-right-aem-version}

Para las soluciones de AEM anteriores, la versión de AEM más actual cambió con poca frecuencia (aproximadamente anualmente con Service Packs trimestrales) y los clientes actualizarían las instancias de producción a la última versión de inicio rápido a su propio tiempo, haciendo referencia al Jar de API. Sin embargo, AEM aplicaciones as a Cloud Service se actualizan automáticamente a la última versión de AEM con más frecuencia, por lo que el código personalizado para versiones internas debe crearse con la última versión de AEM.

Al igual que para las versiones de AEM existentes que no sean de la nube, se admitirá un desarrollo local sin conexión basado en un inicio rápido específico y se espera que sea la herramienta preferida para la depuración en la mayoría de los casos.

>[!NOTE]
>Existen diferencias operativas sutiles entre el comportamiento de la aplicación en un equipo local y el de Adobe Cloud. Estas diferencias arquitectónicas deben respetarse durante el desarrollo local y podrían llevar a un comportamiento diferente al implementar en la infraestructura de la nube. Debido a estas diferencias, es importante realizar pruebas exhaustivas en entornos de desarrollo y ensayo antes de implementar un nuevo código personalizado en producción.

Para desarrollar código personalizado para una versión interna, la versión correspondiente de la variable [SDK as a Cloud Service AEM](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) debe descargarse e instalarse. Para obtener información adicional sobre el uso de las AEM herramientas as a Cloud Service de Dispatcher, consulte [esta página](/help/implementing/dispatcher/disp-overview.md).

El siguiente vídeo proporciona información general de alto nivel sobre cómo implementar código en AEM as a Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Implementación de paquetes de contenido mediante Cloud Manager y el administrador de paquetes {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Implementaciones a través de Cloud Manager {#deployments-via-cloud-manager}

Los clientes implementan código personalizado en entornos de nube a través de Cloud Manager. Debe tenerse en cuenta que Cloud Manager transforma los paquetes de contenido ensamblados localmente en un artefacto que se ajusta al Modelo de funciones de Sling, que es el modo en que se describe una aplicación as a Cloud Service AEM al ejecutarse en un entorno de nube. Como resultado, al consultar los paquetes en el Administrador de paquetes en entornos en la nube, el nombre incluirá &quot;cp2fm&quot; y los paquetes transformados tendrán todos los metadatos eliminados. No se pueden interactuar con ellos, lo que significa que no se pueden descargar, replicar ni abrir. Puede encontrar documentación detallada sobre el conversor [se encuentra aquí](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

Los paquetes de contenido escritos para AEM aplicaciones as a Cloud Service deben tener una clara separación entre contenido inmutable y mutable, y Cloud Manager solo instalará el contenido mutable, lo que también genera un mensaje como:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

El resto de esta sección describirá la composición y las implicaciones de los paquetes inmutables y mutables.

### Paquetes de contenido inmutables {#immutabe-content-packages}

Todo el contenido y el código que persiste en el repositorio inmutable deben registrarse en Git e implementarse mediante Cloud Manager. En otras palabras, a diferencia de las soluciones AEM actuales, el código nunca se implementa directamente en una instancia de AEM en ejecución. Esto garantiza que el código que se ejecuta para una versión determinada en cualquier entorno de Cloud sea idéntico, lo que elimina el riesgo de variación no intencional del código en la producción. Por ejemplo, la configuración OSGI debe comprometerse con el control de código fuente en lugar de administrarse durante la ejecución a través del administrador de configuración de la consola web de AEM.

Como los cambios de aplicación debido al patrón de implementación Blue-Green están activados por un switch, no pueden depender de los cambios en el repositorio mutable con la excepción de los usuarios de servicio, sus ACL, los tipos de nodos y los cambios de definición de índice.

Para los clientes con bases de código existentes, es fundamental pasar por el ejercicio de reestructuración de repositorios descrito en AEM documentación para garantizar que el contenido que anteriormente estaba bajo /etc se mueva a la ubicación correcta.

Se aplican algunas restricciones adicionales a estos paquetes de código, por ejemplo [instalar enlaces](http://jackrabbit.apache.org/filevault/installhooks.html) no son compatibles.

## Configuración OSGI {#osgi-configuration}

Como se ha mencionado anteriormente, la configuración OSGI debe comprometerse con el control de código fuente en lugar de a través de la consola web. Las técnicas para hacerlo incluyen:

* Making the necessary changes on the developer&#39;s local AEM environment with the AEM web console&#39;s configuration manager and then exporting the results to the AEM project on the local file system
* Crear la configuración OSGI manualmente en el proyecto AEM del sistema de archivos local, haciendo referencia al administrador de configuración de la consola de AEM para los nombres de propiedades.

Obtenga más información sobre la configuración OSGI en [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Mutable Content {#mutable-content}

En algunos casos, puede resultar útil preparar los cambios de contenido en el control de código fuente para que Cloud Manager pueda implementarlos cada vez que se actualiza un entorno. Por ejemplo, puede que sea razonable sembrar ciertas estructuras de carpetas raíz o alinear los cambios en plantillas editables para habilitar las políticas en las de los componentes que la implementación de la aplicación actualizó.

Existen dos estrategias para describir el contenido que Cloud Manager implementará en el repositorio mutable, los paquetes de contenido mutable y las declaraciones de informe.

### Paquetes de contenido mutables {#mutable-content-packages}

El contenido, como las jerarquías de rutas de carpetas, los usuarios de servicios y los controles de acceso (ACL), se suelen comprometer en un proyecto de AEM basado en arquetipos maven. Techniques include exporting from AEM or writing directly as XML. During the build and deployment process, Cloud Manager packages the resulting mutable content package. El contenido mutable se instala en 3 momentos diferentes durante la fase de implementación de la canalización:

Antes del inicio de la nueva versión de la aplicación:

* definiciones de índice (añadir, modificar, eliminar)

During startup of new version of application but ahead of switchover:

* Service Users (add)
* Service User ACLs (add)
* tipos de nodo (añadir)

After switchover to new version of application:

* El resto del contenido se puede definir mediante la bóveda jackrabbit. Por ejemplo:
   * Carpetas (añadir, modificar, quitar)
   * Plantillas editables (añadir, modificar, quitar)
   * Configuración según el contexto (cualquier elemento de `/conf`) (añadir, modificar, quitar)
   * Scripts (los paquetes pueden déclencheur Instalar enlaces en varias etapas del proceso de instalación del paquete. Consulte la [Documentación de Jackrabbit filevault](http://jackrabbit.incubator.apache.org/filevault/installhooks.html) acerca de los enlaces de instalación. Tenga en cuenta que AEM CS actualmente utiliza Filevault versión 3.4.0, que limita los enlaces de instalación a los usuarios administradores, usuarios del sistema y miembros del grupo de administradores).

Es posible limitar la instalación de contenido mutable a la creación o publicación incrustando paquetes en una carpeta install.author o install.publish en `/apps`. La reestructuración para reflejar esta separación se llevó a cabo en el AEM 6.5 y en el [AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>Los paquetes de contenido se implementan en todos los tipos de entorno (dev, stage, prod). No es posible limitar la implementación a un entorno específico. Esta limitación se aplica para garantizar la opción de una ejecución de prueba de ejecución automatizada. El contenido específico de un entorno requiere la instalación manual mediante el Administrador de paquetes.

Además, no hay ningún mecanismo para revertir los cambios del paquete de contenido mutable después de haberlos aplicado. Si los clientes detectan un problema, pueden optar por solucionarlo en su próxima versión de código o, como último recurso, restaurar todo el sistema a un punto en el tiempo antes de la implementación.

Cualquier paquete de terceros incluido debe validarse como compatible con AEM servicio as a Cloud Service; de lo contrario, su inclusión dará como resultado un error de implementación.

Como se ha mencionado anteriormente, los clientes con bases de código existentes deben ajustarse al ejercicio de reestructuración de repositorios que requieren los cambios de repositorios de la versión 6.5 descritos en la [AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## Informe {#repoinit}

En los siguientes casos, es preferible utilizar el método de codificación manual para la creación explícita de contenido `repoinit` en configuraciones de fábrica OSGI:

* Crear/eliminar/deshabilitar usuarios de servicios
* Crear/eliminar grupos
* Crear/eliminar usuarios
* Añadir ACL

   >[!NOTE]
   >
   >La definición de ACL requiere que las estructuras de nodos ya estén presentes. Por lo tanto, puede que sea necesario crear instrucciones de ruta anteriores.

* Agregar ruta (por ejemplo, para estructuras de carpetas raíz)
* Agregar CND (definiciones de nodos)

Es preferible un informe para estos casos de uso de modificación de contenido compatible debido a las siguientes ventajas:

* Report crea recursos al inicio para que la lógica pueda dar por sentada la existencia de esos recursos. En el enfoque del paquete de contenido mutable, los recursos se crean después del inicio, por lo que el código de la aplicación que se basa en ellos puede fallar.
* El informe es un conjunto de instrucciones relativamente seguro, ya que controla explícitamente la acción que se va a realizar. Además, las únicas operaciones admitidas son aditivas, a excepción de algunos casos relacionados con la seguridad que permiten eliminar usuarios, usuarios de servicios y grupos. Por el contrario, la eliminación de algo en el enfoque del paquete de contenido mutable es explícita; al definir un filtro, se eliminará cualquier elemento presente cubierto por un filtro. Sin embargo, se debe tener precaución ya que con cualquier contenido hay escenarios en los que la presencia de contenido nuevo puede alterar el comportamiento de la aplicación.
* Repoinit realiza operaciones atómicas y rápidas. Por el contrario, los paquetes de contenido mutables pueden depender en gran medida del rendimiento según las estructuras cubiertas por un filtro. Incluso si actualiza un solo nodo, se puede crear una instantánea de un árbol grande.
* Es posible validar las instrucciones de informe en un entorno de desarrollo local durante la ejecución, ya que se ejecutarán cuando se registre la configuración de OSGi.
* Las instrucciones de informe son atómicas y explícitas y se omitirán si el estado ya coincide.

Cuando Cloud Manager implementa la aplicación, ejecuta estas instrucciones, independientemente de la instalación de cualquier paquete de contenido.

Para crear instrucciones de informe, siga el siguiente procedimiento:

1. Añadir la configuración OSGi para el PID de fábrica `org.apache.sling.jcr.repoinit.RepositoryInitializer` en una carpeta de configuración del proyecto. Utilice un nombre descriptivo para la configuración como **org.apache.sling.jcr.repository.RepositoryInitializer~initstructure**.
1. Agregue instrucciones de informe a la propiedad script de la configuración. La sintaxis y las opciones están documentadas en [Documentación de Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html). Tenga en cuenta que debe haber una creación explícita de una carpeta principal antes de sus carpetas secundarias. Por ejemplo, una creación explícita de `/content` before `/content/myfolder`antes de `/content/myfolder/mysubfolder`. Para que las ACL se establezcan en estructuras de bajo nivel, se recomienda configurarlas en un nivel superior y trabajar con un `rep:glob` restricción.  Por ejemplo `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Valide en el entorno de desarrollo local durante la ejecución.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>For ACLs defined for nodes underneath `/apps` or `/libs` the repoinit execution will start on a blank repository. Los paquetes se instalan después de la notificación, por lo que las instrucciones no pueden depender de nada definido en los paquetes, sino que deben definir las condiciones previas como las estructuras principales debajo.

>[!TIP]
>
>For ACLs the creation of deep structures might be cumbersome, therefore is more reasonable to define an ACL on a higher level and constrain where it is supposed to act via a rep:glob restriction.

More detail about about repoinit can be found in the [Sling documentation](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Administrador de paquetes &quot;one offs&quot; para paquetes de contenido mutable {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Package Manager - Migrating Mutable Content Packages"
>abstract="Explore el uso del administrador de paquetes para casos de uso en los que un paquete de contenido debe instalarse como &quot;único&quot; que incluye la importación de contenido específico de la producción a la puesta en escena para depurar un problema de producción, la transferencia de paquetes de contenido pequeño del entorno local a entornos de AEM Cloud y más."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#cloud-migration" text="Herramienta de transferencia de contenido"

There are use cases where a content package should be installed as a &quot;one off&quot;. For example importing specific content from production on to staging in order to debug a production issue. Para estos escenarios, el Administrador de paquetes se puede utilizar en AEM entornos as a Cloud Service.

Since Package Manager is a runtime concept, it is not possible to install content or code into the immutable repository, so these content packages should only consist of mutable content (mainly `/content` or `/conf`). Si el paquete de contenido incluye contenido mixto (tanto mutable como inmutable), solo se instalará el contenido mutable.

>[!IMPORTANT]
>
>La interfaz de usuario del administrador de paquetes puede devolver un **undefined** mensaje de error si un paquete tarda más de 10 minutos en instalarse. No vuelva a intentar realizar la instalación si esto sucede, ya que continúa correctamente en segundo plano y algunos conflictos podrían introducirse en varios procesos de importación simultáneos.

Cualquier paquete de contenido instalado mediante Cloud Manager (mutable e inmutable) aparecerá en estado congelado en AEM interfaz de usuario del Administrador de paquetes. These packages cannot be reinstalled, rebuilt or even downloaded, and will listed with a **&quot;cp2fm&quot;** suffix, indicating their installation was managed by Cloud Manager.

### Including Third Party Packages {#including-third-party}

Es habitual que los clientes incluyan paquetes pregenerados de fuentes de terceros, como proveedores de software como los socios de traducción de Adobe. La recomendación es alojar estos paquetes en un repositorio remoto y hacer referencia a ellos en el `pom.xml`. Esto es posible para repositorios públicos y también para repositorios privados con protección de contraseña, como se describe en [repositorios maven protegidos por contraseña](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Si no es posible almacenar el paquete en un repositorio remoto, los clientes pueden ubicarlo en un repositorio Maven local, basado en file system, que está comprometido con SCM como parte del proyecto y al que se hace referencia en función de su dependencia. El repositorio sería declarado en los pomas del proyecto que se ilustran a continuación:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Cualquier paquete de terceros incluido debe adherirse a las directrices de empaquetado y codificación del servicio as a Cloud Service de AEM descritas en este artículo; de lo contrario, su inclusión dará como resultado un error de implementación.

El siguiente fragmento Maven POM XML muestra cómo los paquetes de terceros pueden incrustarse en el paquete “Contenedor” del proyecto, normalmente denominado **“todo”**, a través de la configuración del complemento **filevault-package-maven-plugin** Maven.

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <subPackages>
           
          <!-- Include the application's ui.apps and ui.content packages -->
          ...
 
          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <!-- Set the version for all dependencies, including 3rd party packages, in the project's Reactor POM -->
          <subPackage>
              <groupId>com.adobe.cq</groupId>
              <artifactId>core.wcm.components.all</artifactId>
              <filter>true</filter>
          </subPackage>
 
 
          <subPackage>
              <groupId>com.3rdparty.groupId</groupId>
              <artifactId>core.3rdparty.artifactId</artifactId>
              <filter>true</filter>
          </subPackage>
      <subPackages>
  </configuration>
</plugin>
...
```

## Cómo funcionan las implementaciones móviles {#how-rolling-deployments-work}

Al igual que las actualizaciones de AEM, las versiones de los clientes se implementan mediante una estrategia de implementación móvil para eliminar el downtime del clúster de creación en las circunstancias adecuadas. La secuencia general de eventos es la que se describe a continuación, donde **Azul** es la versión antigua del código de cliente y **Verde** es la nueva versión. Tanto Blue como Green ejecutan la misma versión de AEM código.

* La versión azul está activa y hay un candidato a la versión para Verde creado y disponible
* Si hay definiciones de índice nuevas o actualizadas, se procesan los índices correspondientes. Tenga en cuenta que la implementación azul siempre usará los índices antiguos, mientras que el verde siempre usará los nuevos índices.
* El verde empieza mientras que el azul sigue sirviendo
* El azul se está ejecutando y sirve mientras se comprueba la disponibilidad de Green mediante controles de estado
* Los nodos verdes que están listos aceptan tráfico y reemplazan a los nodos azules, que se reducen
* Con el tiempo, los nodos azules se reemplazan por nodos verdes hasta que solo permanezca verde, completando así la implementación
* Se implementa cualquier contenido mutable nuevo o modificado

## Índices {#indexes}

Los índices nuevos o modificados provocarán un paso adicional de indexación o reindexación antes de que la nueva versión (verde) pueda entrar en el tráfico. Los detalles sobre la administración de índices en AEM as a Cloud Service se pueden encontrar en [este artículo](/help/operations/indexing.md). Puede comprobar el estado del trabajo de indexación en la página de compilación de Cloud Manager y recibirá una notificación cuando la nueva versión esté lista para recibir tráfico.

>[!NOTE]
>
>El tiempo necesario para una implementación móvil variará según el tamaño del índice, ya que la versión verde no puede aceptar tráfico hasta que se haya generado el nuevo índice.

En este momento, AEM as a Cloud Service no funciona con herramientas de administración de índices como ACS Commons Asegúrese de la herramienta Oak Index.

## Replicación {#replication}

El mecanismo de publicación es compatible con el [API de Java de replicación de AEM](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html).

Para desarrollar y probar con la replicación con la nube lista AEM inicio rápido, las funcionalidades de replicación clásicas deben usarse con la configuración de Autor/Publicación. En el caso de que el punto de entrada de la interfaz de usuario de AEM Author se haya eliminado para la nube, los usuarios irían a `http://localhost:4502/etc/replication` para la configuración.

## Código compatible con versiones anteriores para implementaciones móviles {#backwards-compatible-code-for-rolling-deployments}

Como se ha detallado anteriormente, la estrategia de implementación gradual de AEM as a Cloud Service implica que tanto las versiones anteriores como las nuevas pueden estar funcionando al mismo tiempo. Por lo tanto, tenga cuidado con los cambios de código que no sean compatibles con la versión anterior de AEM que aún está en funcionamiento.

Además, la versión antigua debe probarse para verificar la compatibilidad con cualquier estructura de contenido mutable nueva aplicada por la nueva versión en caso de revertir, ya que el contenido mutable no se elimina.

### Usuarios de servicio y cambios de ACL {#service-users-and-acl-changes}

Cambiar los usuarios del servicio o las ACLs necesarias para acceder al contenido o al código podría provocar errores en las versiones AEM anteriores, lo que daría como resultado acceso a ese contenido o código con usuarios de servicios obsoletos. Para solucionar este comportamiento, se recomienda hacer cambios distribuidos en al menos 2 versiones, y la primera versión actúa como puente antes de limpiarla en la versión siguiente.

### Cambios en el índice {#index-changes}

Si se realizan cambios en los índices, es importante que la versión azul siga utilizando sus índices hasta que finalice, mientras que la versión verde utiliza su propio conjunto modificado de índices. El desarrollador debe seguir las técnicas de administración de índices descritas [en este artículo](/help/operations/indexing.md).

### Codificación conservadora para retrocesos {#conservative-coding-for-rollbacks}

If a failure is reported or detected after the deployment, it is possible that a rollback to the Blue version will be required. Sería aconsejable garantizar que el código azul sea compatible con cualquier estructura nueva creada por la versión verde, ya que las nuevas estructuras (cualquier contenido mutable) no se revertirán. If the old code is not compatible, fixes will need to be applied in subsequent customer releases.

## Modos de ejecución {#runmodes}

En las soluciones de AEM existentes, los clientes tienen la opción de ejecutar instancias con modos de ejecución arbitrarios y aplicar la configuración OSGI o instalar paquetes OSGI a esas instancias específicas. Los modos de ejecución definidos normalmente incluyen la variable *service* (autor y publicación) y el entorno (dev, stage, prod).

AEM as a Cloud Service, por otro lado, tiene más opiniones sobre qué modos de ejecución están disponibles y cómo se pueden asignar a ellos los paquetes OSGI y la configuración OSGI:

* Los modos de ejecución de la configuración OSGI deben hacer referencia a dev, stage, prod para el entorno o el autor, publicar para el servicio. Una combinación de `<service>.<environment_type>` se admite, mientras que estos se deben utilizar en este orden concreto (por ejemplo `author.dev` o `publish.prod`). Se debe hacer referencia a los tokens OSGI directamente desde el código en lugar de usar la variable `getRunModes` que ya no incluirá el `environment_type` en tiempo de ejecución. Para obtener más información, consulte [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Los modos de ejecución de los paquetes OSGI están limitados al servicio (autor, publicación). Los paquetes OSGI en modo de ejecución deben instalarse en el paquete de contenido en `install/author` o `install/publish`.

Al igual que las soluciones de AEM existentes, no hay forma de utilizar modos de ejecución para instalar solo contenido para entornos o servicios específicos. Si se desea sembrar un entorno de desarrollo con datos o HTML que no estén en fase o producción, se puede utilizar el administrador de paquetes.

The supported runmode configurations are:

* **config** (*El valor predeterminado se aplica a todos los AEM Services*)
* **config.author** (*Se aplica a todos los servicios de AEM Author*)
* **config.author.dev** (*Se aplica al servicio de creación AEM desarrollo*)
* **config.author.stage** (*Applies to AEM Staging Author service*)
* **config.author.prod** (*Se aplica a AEM servicio de creación de producción*)
* **config.publish** (*Se aplica al servicio AEM Publish*)
* **config.publish.dev** (*Se aplica al servicio de publicación AEM desarrollo*)
* **config.publish.stage** (*Se aplica al servicio de publicación AEM ensayo*)
* **config.publish.prod** (*Se aplica a AEM servicio Publicación de producción*)
* **config.dev** (*Se aplica a AEM servicios de desarrollo)
* **config.stage** (*Applies to AEM Staging services)
* **config.prod** (*Se aplica a AEM servicios de producción)

Se utiliza la configuración OSGI que tiene los modos de ejecución más coincidentes.

Al desarrollar localmente, se puede pasar un parámetro de inicio de modo de ejecución para dictar qué configuración de OSGI de modo de ejecución se utilizará.

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Maintenance Tasks Configuration in Source Control {#maintenance-tasks-configuration-in-source-control}

Maintenance Task configurations must be persisted in source control since the **Tools > Operations** screen will no longer be available in Cloud environments. Esto tiene la ventaja de garantizar que los cambios se mantengan intencionalmente en lugar de aplicarse de forma reactiva y tal vez olvidados. Please reference the [Maintenance Task article](/help/operations/maintenance.md) for additional information.
