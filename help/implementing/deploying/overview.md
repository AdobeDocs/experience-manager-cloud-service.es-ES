---
title: Implementación en AEM as a Cloud Service
description: 'Implementación en AEM as a Cloud Service '
translation-type: tm+mt
source-git-commit: 450d78be9472c854a13ba35965ac10f806aba3d9
workflow-type: tm+mt
source-wordcount: '3210'
ht-degree: 1%

---


# Implementación en AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introducción {#introduction}

Los aspectos fundamentales del desarrollo de código son similares en AEM como Cloud Service en comparación con las soluciones AEM in situ y Managed Services. Los desarrolladores escriben código y lo prueban localmente, que luego se envía a AEM remotos como entornos de Cloud Service. Cloud Manager, que era una herramienta opcional de envío de contenido para Managed Services, es obligatorio. Ahora es el único mecanismo para implementar código para AEM como entornos de Cloud Service.

La actualización de la versión [](/help/implementing/deploying/aem-version-updates.md) AEM siempre es un evento de implementación independiente de la inserción de código [](#customer-releases)personalizado. Visto de otra manera, las versiones de código personalizado deben probarse con la versión AEM que está en producción, ya que eso es lo que se implementará en la parte superior. AEM actualizaciones de versiones posteriores, que serán frecuentes y se aplicarán automáticamente. Están pensados para ser compatibles con versiones anteriores del código de cliente ya implementado.

El resto de este documento describe cómo los desarrolladores deben adaptar sus prácticas para que funcionen tanto con AEM como con las actualizaciones de versiones de los Cloud Service como con las actualizaciones de los clientes.

>[!NOTE]
>Se recomienda que los clientes con bases de código existentes realicen el proceso de reestructuración del repositorio descrito en la documentación [de](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)AEM.

## Versiones de clientes {#customer-releases}

### Codificación con la versión AEM correcta {#coding-against-the-right-aem-version}

Para soluciones de AEM anteriores, la versión de AEM más reciente cambió con poca frecuencia (aproximadamente anualmente con Service Packs trimestrales) y los clientes actualizarían las instancias de producción a la última versión de inicio rápido a su propio tiempo, haciendo referencia a la API Jar. Sin embargo, AEM como aplicaciones Cloud Service se actualizan automáticamente a la versión más reciente de AEM con más frecuencia, por lo que el código personalizado para versiones internas debe crearse con la versión AEM más reciente.

Al igual que en las versiones de AEM existentes que no son de nube, se admitirá un desarrollo local sin conexión basado en un inicio rápido específico y se espera que sea la herramienta de elección para la depuración en la mayoría de los casos.

>[!NOTE]
>Existen diferencias operativas sutiles entre el comportamiento de la aplicación en un equipo local y el de Adobe Cloud. Estas diferencias arquitectónicas deben respetarse durante el desarrollo local y podrían conducir a un comportamiento diferente al implementarlas en la infraestructura de nube. Debido a estas diferencias, es importante realizar pruebas exhaustivas en entornos de desarrollo y etapa antes de desarrollar un nuevo código personalizado en producción.

Para desarrollar código personalizado para una versión interna, se debe descargar e instalar la versión pertinente del [AEM como SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) Cloud Service. Para obtener información adicional sobre el uso del AEM como herramientas de despachante de Cloud Service, consulte [esta página](/help/implementing/dispatcher/disp-overview.md).

El siguiente vídeo proporciona información general de alto nivel sobre cómo implementar código para AEM como Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

>[!NOTE]
>Se recomienda que los clientes con bases de código existentes realicen el proceso de reestructuración del repositorio descrito en la documentación [de](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)AEM.

## Implementación de paquetes de contenido mediante Cloud Manager y Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Implementaciones mediante Cloud Manager {#deployments-via-cloud-manager}

Los clientes implementan código personalizado en entornos de nube a través de Cloud Manager. Debe tenerse en cuenta que Cloud Manager transforma los paquetes de contenido ensamblados localmente en un artefacto conforme al Modelo de funciones de Sling, que es la forma en que se describe un AEM como una aplicación Cloud Service cuando se ejecuta en un entorno en la nube. Como resultado, al consultar los paquetes en el Administrador de paquetes en entornos de nube, el nombre incluirá &quot;cp2fm&quot; y los paquetes transformados tendrán todos los metadatos eliminados. No se pueden interactuar con ellos, lo que significa que no se pueden descargar, replicar ni abrir. Encontrará documentación detallada sobre el convertidor [aquí](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

Los paquetes de contenido escritos para AEM como aplicaciones de Cloud Service deben tener una separación clara entre el contenido inmutable y el mutable, y Cloud Manager lo aplicará fallando en la compilación, generando un mensaje como:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

El resto de esta sección describirá la composición y las implicaciones de los paquetes inmutables y mutables.

### Paquetes de contenido inmutables {#immutabe-content-packages}

Todo el contenido y el código que se mantienen en el repositorio inmutable deben registrarse en Git e implementarse a través de Cloud Manager. En otras palabras, a diferencia de las soluciones AEM actuales, el código nunca se implementa directamente en una instancia de AEM en ejecución. Esto garantiza que el código que se ejecuta para una versión determinada en cualquier entorno de la nube sea idéntico, lo que elimina el riesgo de variación no intencionada del código en la producción. Por ejemplo, la configuración OSGI debe asignarse al control de código fuente en lugar de gestionarse en tiempo de ejecución mediante el administrador de configuración de la consola web de AEM.

Dado que los cambios de la aplicación debidos al patrón de implementación Blue-Green están activados por un conmutador, no pueden depender de los cambios en el repositorio mutable con excepción de los usuarios de servicio, sus ACL, los tipos de nodos y los cambios de definición de índice.

Para los clientes con bases de código existentes, es fundamental pasar por el proceso de reestructuración del repositorio descrito en AEM documentación para garantizar que el contenido que anteriormente se encontraba bajo /etc se traslade a la ubicación correcta.

## Configuración de OSGI {#osgi-configuration}

Como se mencionó anteriormente, la configuración OSGI debe estar asignada al control de código fuente en lugar de hacerlo a través de la consola web. Las técnicas para hacerlo incluyen:

* Realizar los cambios necesarios en el entorno de AEM local del desarrollador con el administrador de configuración de la consola web de AEM y luego exportar los resultados al proyecto de AEM en el sistema de archivos local
* Creación manual de la configuración OSGI en el proyecto de AEM en el sistema de archivos local, haciendo referencia al administrador de configuración de la consola de AEM para los nombres de propiedad.

Obtenga más información sobre la configuración OSGI en [Configuración de OSGi para AEM como Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Contenido mutable {#mutable-content}

En algunos casos, puede resultar útil preparar cambios de contenido en el control de código fuente para que Cloud Manager pueda implementarlo cada vez que se actualice un entorno. Por ejemplo, puede que sea razonable crear ciertas estructuras de carpetas raíz o alinear los cambios en plantillas editables para habilitar las directivas en las de los componentes que la implementación de la aplicación ha actualizado.

Existen dos estrategias para describir el contenido que Cloud Manager implementará en el repositorio mutable, los paquetes de contenido mutable y las sentencias de informe.

### Paquetes de contenido mutable {#mutable-content-packages}

El contenido, como las jerarquías de rutas de carpeta, los usuarios de servicios y los controles de acceso (ACL), se suelen asignar a un proyecto de AEM basado en arquetipos determinado. Las técnicas incluyen exportar desde AEM o escribir directamente como XML. Durante el proceso de compilación e implementación, Cloud Manager empaqueta el paquete de contenido mutable resultante. El contenido mutable se instala en 3 momentos diferentes durante la fase de implementación de la canalización:

Antes del inicio de la nueva versión de la aplicación:

* definiciones de índice (agregar, modificar, eliminar)

Durante el inicio de la nueva versión de la aplicación, pero antes del cambio:

* Usuarios de servicio (agregar)
* ACL de usuario de servicio (agregar)
* tipos de nodo (agregar)

Después de cambiar a la nueva versión de la aplicación:

* Todos los demás contenidos definibles mediante bóveda jackrabbit. Por ejemplo:
   * Carpetas (agregar, modificar, quitar)
   * Plantillas editables (agregar, modificar, eliminar)
   * Configuración según el contexto (cualquier elemento en `/conf`) (agregar, modificar, eliminar)
   * Secuencias de comandos (los paquetes pueden activar los enlaces de instalación en varias etapas del proceso de instalación del paquete)

Es posible limitar la instalación de contenido mutable a la creación o publicación incrustando paquetes en una carpeta install.author o install.publish en `/apps`. Los detalles se pueden encontrar en [AEM documentación](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html) sobre la reestructuración recomendada del proyecto.

>[!NOTE]
>Los paquetes de contenido se implementan en todos los tipos de entorno (dev, stage, prod). No es posible limitar la implementación a un entorno específico. Esta limitación se ha establecido para garantizar la opción de una serie de pruebas de ejecución automatizada. El contenido específico de un entorno requiere la instalación manual mediante el Administrador de paquetes.

Además, no hay ningún mecanismo para revertir los cambios del paquete de contenido mutable después de que se hayan aplicado. Si los clientes detectan un problema, pueden optar por corregirlo en su próxima versión de código o como último recurso, restaurar todo el sistema a un punto en el tiempo antes de la implementación.

Todos los paquetes de terceros incluidos deben validarse como AEM compatibles con el servicio de Cloud Service; de lo contrario, su inclusión provocará un error de implementación.

Como se ha mencionado anteriormente, los clientes con bases de código existentes deben ajustarse al proceso de reestructuración del repositorio descrito en [AEM documentación](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html).

## Informe {#repoinit}

En los siguientes casos, es preferible utilizar el método de codificación manual de las sentencias de creación de contenido explícito en las configuraciones de fábrica de OSGI: `repoinit`

* Crear/eliminar/deshabilitar usuarios de servicios
* Crear/eliminar grupos
* Crear/eliminar usuarios
* Añadir ACL

   >[!NOTE]
   >
   >La definición de ACL requiere que las estructuras de nodos ya estén presentes. Por lo tanto, puede que sea necesario crear las sentencias de ruta anteriores.

* Añadir ruta (por ejemplo, para estructuras de carpetas raíz)
* Añadir CND (definiciones de tipo de nodo)

Es preferible un informe para estos casos de uso de modificación de contenido compatible debido a las siguientes ventajas:

* El informe crea recursos al inicio para que la lógica pueda dar por sentada la existencia de esos recursos. En el enfoque de paquete de contenido mutable, los recursos se crean después del inicio, por lo que el código de la aplicación que se basa en ellos puede fallar.
* El informe es un conjunto de instrucciones relativamente seguro, ya que controla explícitamente la acción que se va a realizar. Además, las únicas operaciones admitidas son aditivas, a excepción de algunos casos relacionados con la seguridad que permiten la eliminación de usuarios, usuarios de servicios y grupos. Por el contrario, la eliminación de algo en el enfoque del paquete de contenido mutable es explícita;  al definir un filtro, se eliminará todo lo que esté cubierto por un filtro. Sin embargo, se debe tener precaución ya que con cualquier contenido hay escenarios en los que la presencia de contenido nuevo puede alterar el comportamiento de la aplicación.
* El informe realiza operaciones atómicas y rápidas. Por el contrario, los paquetes de contenido mutable pueden depender en gran medida del rendimiento según las estructuras cubiertas por un filtro. Incluso si se actualiza un solo nodo, se puede crear una instantánea de un árbol grande.
* Es posible validar las sentencias de informe en un entorno de desarrollo local durante la ejecución, ya que se ejecutarán cuando se registre la configuración de OSGi.
* Las instrucciones de informe son atómicas y explícitas y se omitirán si el estado ya coincide.

Cuando Cloud Manager implementa la aplicación, ejecuta estas sentencias, independientemente de la instalación de cualquier paquete de contenido.

Para crear sentencias de informe, siga el procedimiento siguiente:

1. Añada la configuración de OSGi para el PID de fábrica `org.apache.sling.jcr.repoinit.RepositoryInitializer` en una carpeta de configuración del proyecto. Utilice un nombre descriptivo para la configuración como **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. Añada sentencias de informe a la propiedad script de la configuración. La sintaxis y las opciones se documentan en la documentación [de](https://sling.apache.org/documentation/bundles/repository-initialization.html)Sling. Tenga en cuenta que debe haber una creación explícita de una carpeta principal antes que sus carpetas secundarias. Por ejemplo, una creación explícita de `/content` before `/content/myfolder`, before `/content/myfolder/mysubfolder`. Para que las ACL se establezcan en estructuras de bajo nivel, se recomienda establecerlas en un nivel superior y trabajar con una `rep:glob` restricción.  Por ejemplo `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Validar en el entorno de desarrollo local durante la ejecución.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Para las ACL definidas para nodos debajo `/apps` o `/libs` la ejecución del informe se inicio en un repositorio en blanco. Los paquetes se instalan después de la notificación, por lo tanto las sentencias no pueden basarse en nada definido en los paquetes, sino que deben definir las condiciones previas como las estructuras principales debajo.

>[!TIP]
>
>Para las ACL, la creación de estructuras profundas puede ser complicada, por lo tanto es más razonable definir una ACL en un nivel superior y restringir donde se supone que debe actuar a través de una restricción rep:glob.

Encontrará más información sobre los informes en la documentación de [Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Administrador de paquetes &quot;one offs&quot; para paquetes de contenido mutable {#package-manager-oneoffs-for-mutable-content-packages}

Hay casos de uso en los que un paquete de contenido debe instalarse como &quot;uno de descuento&quot;. Por ejemplo, importar contenido específico de la producción a ensayo para depurar un problema de producción. En estos casos, el Administrador de paquetes se puede utilizar en AEM como entornos de Cloud Service.

Dado que Package Manager es un concepto de tiempo de ejecución, no es posible instalar contenido o código en el repositorio inmutable, por lo que estos paquetes de contenido solo deben constar de contenido mutable (principalmente `/content` o `/conf`). Si el paquete de contenido incluye contenido mixto (tanto mutable como inmutable), solo se instalará el contenido mutable.

Todos los paquetes de contenido instalados a través de Cloud Manager (tanto mutables como inmutables) aparecerán en estado de congelación en la interfaz de usuario AEM Package Manager. Estos paquetes no se pueden volver a instalar, reconstruir o incluso descargar, y se mostrarán con un sufijo **&quot;cp2fm&quot;** , que indica que la instalación ha sido administrada por Cloud Manager.

### Inclusión de paquetes de terceros {#including-third-party}

Es común que los clientes incluyan paquetes precompilados de fuentes de terceros, como proveedores de software como los socios de traducción de Adobe. La recomendación es alojar estos paquetes en un repositorio remoto y hacer referencia a ellos en el `pom.xml`. Esto es posible para repositorios públicos y también para repositorios privados con protección de contraseña, como se describe en repositorios [protegidos con](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)contraseña.

Si no es posible almacenar el paquete en un repositorio remoto, los clientes pueden colocarlo en un repositorio Maven local basado en file systems, que se ha comprometido con SCM como parte del proyecto y al que se hace referencia por cualquier elemento que dependa de él. El repositorio se declararía en los pomas del proyecto que se ilustran a continuación:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Todos los paquetes de terceros incluidos deben atenerse al AEM como directrices de programación y empaquetado de servicio Cloud Service descritas en este artículo; de lo contrario, su inclusión dará lugar a un error de implementación.

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

Al igual que las actualizaciones de AEM, las versiones de los clientes se implementan mediante una estrategia de implementación móvil para eliminar el tiempo de inactividad del clúster de creación en las circunstancias correctas. La secuencia general de eventos es la que se describe a continuación, donde **Blue** es la versión antigua del código del cliente y **Green** es la nueva versión. Tanto Blue como Green están ejecutando la misma versión de AEM código.

* La versión azul está activa y un candidato para la versión verde está compilado y disponible
* Si hay definiciones de índice nuevas o actualizadas, se procesan los índices correspondientes. Tenga en cuenta que la implementación azul siempre usará los índices antiguos, mientras que el verde siempre usará los nuevos índices.
* El verde empieza mientras que el azul sigue sirviendo
* El azul funciona y sirve mientras se comprueba si Green está listo a través de controles de salud
* Los nodos verdes que están listos aceptan tráfico y reemplazan a los nodos azules, que se reducen
* Con el tiempo, los nodos azules se reemplazan por nodos verdes hasta que solo permanece verde, completando así la implementación
* Se implementa cualquier contenido mutable nuevo o modificado

## Índices {#indexes}

Los índices nuevos o modificados provocarán un paso adicional de indexación o reindexación antes de que la nueva versión (verde) pueda asumir el tráfico. En [este artículo](/help/operations/indexing.md)se pueden encontrar detalles sobre la administración de índices en AEM como Cloud Service. Puede comprobar el estado del trabajo de indexación en la página de compilación del Administrador de nube y recibirá una notificación cuando la nueva versión esté lista para recibir tráfico.

>[!NOTE]
>
>El tiempo necesario para una implementación móvil variará según el tamaño del índice, ya que la versión verde no puede aceptar tráfico hasta que se haya generado el nuevo índice.

En este momento, AEM como Cloud Service no funciona con herramientas de gestión de índices como ACS Commons Asegúrese de la herramienta Índice de Robos.

## Replicación {#replication}

El mecanismo de publicación es compatible con las APIs [de Java de replicación](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html)AEM.

Para desarrollar y probar con la replicación con el inicio rápido AEM listo para la nube, las capacidades de replicación clásicas deben usarse con una configuración de creación/publicación. En el caso de que el punto de entrada de la interfaz de usuario de AEM Author se haya eliminado para la nube, los usuarios irán a `http://localhost:4502/etc/replication` para configurarlo.

## Código compatible con versiones anteriores para implementaciones móviles {#backwards-compatible-code-for-rolling-deployments}

Como se ha indicado anteriormente, AEM como estrategia de despliegue continuo de un Cloud Service implica que tanto las versiones antiguas como las nuevas pueden estar funcionando al mismo tiempo. Por lo tanto, tenga cuidado con los cambios de código que no son compatibles con la versión anterior de AEM que aún está en funcionamiento.

Además, la versión anterior debe probarse para comprobar la compatibilidad con cualquier estructura de contenido mutable nueva que la nueva versión aplique en el evento de revertir, ya que no se elimina el contenido mutable.

### Usuarios de servicio y cambios de ACL {#service-users-and-acl-changes}

Cambiar los usuarios de servicios o las ACL necesarias para acceder al contenido o al código podría provocar errores en las versiones anteriores de AEM, lo que daría como resultado el acceso a dicho contenido o código con usuarios de servicios obsoletos. Para solucionar este comportamiento, una recomendación es que los cambios se extiendan al menos en 2 versiones, y que la primera versión actúe como puente antes de limpiarla en la versión siguiente.

### Cambios de índice {#index-changes}

Si se realizan cambios en los índices, es importante que la versión azul siga utilizando sus índices hasta que se termine, mientras que la versión verde utiliza su propio conjunto modificado de índices. El desarrollador debe seguir las técnicas de gestión de índices descritas [en este artículo](/help/operations/indexing.md).

### Codificación conservadora para retrocesos {#conservative-coding-for-rollbacks}

Si se notifica o detecta un error después de la implementación, es posible que se requiera una reversión a la versión azul. Sería aconsejable garantizar que el código azul sea compatible con cualquier estructura nueva creada por la versión verde, ya que las nuevas estructuras (cualquier contenido mutable) no se revertirán. Si el código antiguo no es compatible, las correcciones deberán aplicarse en versiones posteriores de clientes.

## Modos de ejecución {#runmodes}

En las soluciones de AEM existentes, los clientes tienen la opción de ejecutar instancias con modos de ejecución arbitrarios y aplicar la configuración OSGI o instalar paquetes OSGI a esas instancias específicas. Los modos de ejecución que se definen normalmente incluyen el *servicio* (autor y publicación) y el entorno (dev, stage, prod).

AEM como Cloud Service, por otro lado, tiene más opiniones sobre qué modos de ejecución están disponibles y cómo pueden asignarse a ellos los paquetes OSGI y la configuración OSGI:

* Los modos de ejecución de la configuración OSGI deben hacer referencia a dev, stage, prod para el entorno o autor, publicar para el servicio. Se admite una combinación de `<service>.<environment_type>` estos elementos, que deben utilizarse en este orden concreto (por ejemplo `author.dev` o `publish.prod`). Se debe hacer referencia a los tokens OSGI directamente desde el código en lugar de utilizar el `getRunModes` método, que ya no incluirá los tokens `environment_type` en tiempo de ejecución. Para obtener más información, consulte [Configuración de OSGi para AEM como Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Los modos de ejecución de paquetes OSGI están limitados al servicio (autor, publicación). Los paquetes OSGI en modo por ejecución deben instalarse en el paquete de contenido en `install/author` o `install/publish`.

Al igual que las soluciones de AEM existentes, no hay forma de utilizar los modos de ejecución para instalar solo contenido para entornos o servicios específicos. Si se deseaba crear un entorno dev con datos o HTML que no se encuentra en el escenario o en la producción, se podría utilizar el administrador de paquetes.

Las configuraciones de modo de ejecución admitidas son:

* **config** (*el valor predeterminado se aplica a todos los servicios* AEM)
* **config.author** (*se aplica a todos los servicios* de AEM Author)
* **config.author.dev** (*se aplica a AEM servicio* Dev Author)
* **config.author.stage** (*se aplica a AEM servicio* de creación de ensayo)
* **config.author.prod** (*se aplica a AEM servicio* Production Author)
* **config.publish** (*se aplica al servicio* AEM Publish)
* **config.publish.dev** (*se aplica a AEM servicio* Dev Publish)
* **config.publish.stage** (*se aplica a AEM servicio* de publicación de ensayo)
* **config.publish.prod** (*se aplica a AEM servicio* Producción Publish)
* **config.dev** (*Se aplica a AEM servicios Dev)
* **config.stage** (*Se aplica a AEM servicios de ensayo)
* **config.prod** (*Se aplica a AEM servicios de producción)

Se utiliza la configuración OSGI que tiene los modos de ejecución más coincidentes.

Cuando se desarrolla localmente, se puede pasar un parámetro de inicio runmode para dictar qué configuración OSGI de modo de ejecución se utilizará.

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configuración de Tareas de mantenimiento en el control de código fuente {#maintenance-tasks-configuration-in-source-control}

Las configuraciones de Tarea de mantenimiento deben mantenerse en el control de código fuente, ya que la pantalla **Herramientas > Operaciones** ya no estará disponible en entornos de nube. Esto tiene la ventaja de garantizar que los cambios se mantengan intencionalmente en lugar de aplicarse de manera reactiva y tal vez olvidarse. Consulte el artículo [de Tarea de](/help/operations/maintenance.md) mantenimiento para obtener información adicional.
