---
title: Implementación en AEM as a Cloud Service
description: Implementación en AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: 8e9ff8f77ac4920f87adcba0258cfccb15f9a5b9
workflow-type: tm+mt
source-wordcount: '3415'
ht-degree: 1%

---

# Implementación en AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introducción {#introduction}

Los fundamentos del desarrollo de código son similares en AEM as a Cloud Service en comparación con las soluciones AEM On Premise y Managed Services. Los desarrolladores escriben el código y lo prueban localmente, que luego se inserta en entornos as a Cloud Service AEM remotos. Se requiere Cloud Manager, que era una herramienta de entrega de contenido opcional para Managed Services. Este es ahora el único mecanismo para implementar código en entornos as a Cloud Service AEM.

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

Los clientes implementan código personalizado en entornos de nube a través de Cloud Manager. Debe tenerse en cuenta que Cloud Manager transforma los paquetes de contenido ensamblados localmente en un artefacto que se ajusta al Modelo de funciones de Sling, que es el modo en que se describe una aplicación as a Cloud Service AEM al ejecutarse en un entorno de nube. Como resultado, al consultar los paquetes en [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) en entornos de Cloud, el nombre incluye &quot;cp2fm&quot; y los paquetes transformados tienen todos los metadatos eliminados. No se pueden interactuar con ellos, lo que significa que no se pueden descargar, replicar ni abrir. Puede encontrar documentación detallada sobre el conversor [se encuentra aquí](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

Los paquetes de contenido escritos para AEM aplicaciones as a Cloud Service deben tener una clara separación entre contenido inmutable y mutable, y Cloud Manager solo instalará el contenido mutable, lo que también genera un mensaje como:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

El resto de esta sección describirá la composición y las implicaciones de los paquetes inmutables y mutables.

### Paquetes de contenido inmutables {#immutabe-content-packages}

Todo el contenido y el código que persiste en el repositorio inmutable deben registrarse en Git e implementarse mediante Cloud Manager. En otras palabras, a diferencia de las soluciones AEM actuales, el código nunca se implementa directamente en una instancia de AEM en ejecución. Esto garantiza que el código que se ejecuta para una versión determinada en cualquier entorno de Cloud sea idéntico, lo que elimina el riesgo de variación no intencional del código en la producción. Por ejemplo, la configuración OSGI debe comprometerse con el control de código fuente en lugar de administrarse durante la ejecución a través del administrador de configuración de la consola web de AEM.

Como los cambios de aplicación debido al patrón de implementación Blue-Green están activados por un switch, no pueden depender de los cambios en el repositorio mutable con la excepción de los usuarios de servicio, sus ACL, los tipos de nodos y los cambios de definición de índice.

Para los clientes con bases de código existentes, es fundamental pasar por el ejercicio de reestructuración de repositorios descrito en AEM documentación para garantizar que el contenido que anteriormente estaba bajo /etc se mueva a la ubicación correcta.

Se aplican algunas restricciones adicionales a estos paquetes de código, por ejemplo [instalar enlaces](https://jackrabbit.apache.org/filevault/installhooks.html) no son compatibles.

## Configuración OSGi {#osgi-configuration}

Como se ha mencionado anteriormente, la configuración OSGI debe comprometerse con el control de código fuente en lugar de a través de la consola web. Las técnicas para hacerlo incluyen:

* Realización de los cambios necesarios en el entorno de AEM local del desarrollador con el administrador de configuración de la consola web de AEM y exportación de los resultados al proyecto de AEM en el sistema de archivos local
* Crear la configuración OSGI manualmente en el proyecto AEM del sistema de archivos local, haciendo referencia al administrador de configuración de la consola de AEM para los nombres de propiedades.

Obtenga más información sobre la configuración OSGI en [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Contenido mutable {#mutable-content}

En algunos casos, puede resultar útil preparar los cambios de contenido en el control de código fuente para que Cloud Manager pueda implementarlos cada vez que se actualiza un entorno. Por ejemplo, puede que sea razonable sembrar ciertas estructuras de carpetas raíz o alinear los cambios en plantillas editables para habilitar las políticas en las de los componentes que la implementación de la aplicación actualizó.

Existen dos estrategias para describir el contenido que Cloud Manager implementará en el repositorio mutable, los paquetes de contenido mutable y las declaraciones de informe.

### Paquetes de contenido mutables {#mutable-content-packages}

El contenido, como las jerarquías de rutas de carpetas, los usuarios de servicios y los controles de acceso (ACL), se suelen comprometer en un proyecto de AEM basado en arquetipos maven. Las técnicas incluyen la exportación desde AEM o la escritura directamente como XML. Durante el proceso de compilación e implementación, Cloud Manager empaqueta el paquete de contenido mutable resultante. El contenido mutable se instala en 3 momentos diferentes durante la fase de implementación de la canalización:

Antes del inicio de la nueva versión de la aplicación:

* definiciones de índice (añadir, modificar, eliminar)

Durante el inicio de la nueva versión de la aplicación, pero antes del cambio:

* Usuarios de servicio (añadir)
* ACL de usuario de servicio (añadir)
* tipos de nodo (añadir)

Después de cambiar a una nueva versión de la aplicación:

* El resto del contenido se puede definir mediante la bóveda jackrabbit. Por ejemplo:
   * Carpetas (añadir, modificar, quitar)
   * Plantillas editables (añadir, modificar, quitar)
   * Configuración según el contexto (cualquier elemento de `/conf`) (añadir, modificar, quitar)
   * Scripts (los paquetes pueden déclencheur Instalar enlaces en varias etapas del proceso de instalación del paquete. <!-- MISDIRECTED REQUEST, 421 ERROR, CAN'T FIND CORRECT PATH See the [Jackrabbit filevault documentation](https://jackrabbit.incubator.apache.org/filevault/installhooks.html) about install hooks. --> Tenga en cuenta que AEM CS actualmente utiliza Filevault versión 3.4.0, que limita los enlaces de instalación a los usuarios administradores, usuarios del sistema y miembros del grupo de administradores).

Es posible limitar la instalación de contenido mutable a la creación o publicación incrustando paquetes en una carpeta install.author o install.publish en `/apps`. La reestructuración para reflejar esta separación se llevó a cabo en el AEM 6.5 y en el [AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=es)

>[!NOTE]
>Los paquetes de contenido se implementan en todos los tipos de entorno (dev, stage, prod). No es posible limitar la implementación a un entorno específico. Esta limitación se aplica para garantizar la opción de una ejecución de prueba de ejecución automatizada. El contenido específico de un entorno requiere una instalación manual mediante [Administrador de paquetes.](/help/implementing/developing/tools/package-manager.md)

Además, no hay ningún mecanismo para revertir los cambios del paquete de contenido mutable después de haberlos aplicado. Si los clientes detectan un problema, pueden optar por solucionarlo en su próxima versión de código o, como último recurso, restaurar todo el sistema a un punto en el tiempo antes de la implementación.

Cualquier paquete de terceros incluido debe validarse como compatible con AEM servicio as a Cloud Service; de lo contrario, su inclusión dará como resultado un error de implementación.

Como se ha mencionado anteriormente, los clientes con bases de código existentes deben ajustarse al ejercicio de reestructuración de repositorios que requieren los cambios de repositorios de la versión 6.5 descritos en la [AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=es)

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
>Para ACL definidos para nodos inferiores `/apps` o `/libs` la ejecución del informe se iniciará en un repositorio en blanco. Los paquetes se instalan después de la notificación, por lo que las instrucciones no pueden depender de nada definido en los paquetes, sino que deben definir las condiciones previas como las estructuras principales debajo.

>[!TIP]
>
>Para las ACL, la creación de estructuras profundas puede ser engorrosa, por lo tanto es más razonable definir una ACL en un nivel superior y restringir donde se supone que debe actuar a través de una restricción rep:glob.

Puede encontrar más información sobre el informe en la [Documentación de Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Administrador de paquetes &quot;one offs&quot; para paquetes de contenido mutable {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Administrador de paquetes: migración de paquetes de contenido mutable"
>abstract="Explore el uso del administrador de paquetes para casos de uso en los que un paquete de contenido debe instalarse como &quot;único&quot; que incluye la importación de contenido específico de la producción a la puesta en escena para depurar un problema de producción, la transferencia de paquetes de contenido pequeño del entorno local a entornos de AEM Cloud y más."
>abstract="Explore el uso del administrador de paquetes para casos de uso en los que un paquete de contenido debe instalarse como &quot;único&quot;, lo que incluye la importación de contenido específico de la producción en el entorno de ensayo para depurar un problema de producción, la transferencia de paquetes de contenido pequeño del entorno local a entornos de AEM Cloud y más."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#cloud-migration" text="Herramienta de transferencia de contenido"

Hay casos de uso en los que un paquete de contenido debe instalarse como &quot;único&quot;. Por ejemplo, importar contenido específico de la producción a ensayo para depurar un problema de producción. Para estos escenarios, [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) se puede utilizar en AEM entornos as a Cloud Service.

Dado que el Administrador de paquetes es un concepto de tiempo de ejecución, no es posible instalar contenido o código en el repositorio inmutable, por lo que estos paquetes de contenido solo deben consistir en contenido mutable (principalmente `/content` o `/conf`). Si el paquete de contenido incluye contenido mixto (tanto mutable como inmutable), solo se instalará el contenido mutable.

>[!IMPORTANT]
>
>La interfaz de usuario del Administrador de paquetes puede devolver un valor **undefined** mensaje de error si un paquete tarda más de 10 minutos en instalarse.
>
>Esto no se debe a un error en la instalación, sino a un tiempo de espera que el Cloud Service tiene para todas las solicitudes.
>
>No vuelva a intentar realizar la instalación si aparece un error de este tipo. La instalación continúa correctamente en segundo plano. Si reinicia la instalación, varios procesos de importación simultáneos podrían introducir algunos conflictos.

Cualquier paquete de contenido instalado mediante Cloud Manager (mutable e inmutable) aparecerá en estado congelado en AEM interfaz de usuario del Administrador de paquetes. Estos paquetes no se pueden volver a instalar, volver a crear ni descargar, y aparecerán en la lista con una **&quot;cp2fm&quot;** , indicando que la instalación fue administrada por Cloud Manager.

### Inclusión de paquetes de terceros {#including-third-party}

Es habitual que los clientes incluyan paquetes pregenerados de fuentes de terceros, como proveedores de software como los socios de traducción de Adobe. La recomendación es alojar estos paquetes en un repositorio remoto y hacer referencia a ellos en el `pom.xml`. Esto es posible para repositorios públicos y también para repositorios privados con protección de contraseña, como se describe en [repositorios maven protegidos por contraseña](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Si no es posible almacenar el paquete en un repositorio remoto, los clientes pueden ubicarlo en un repositorio Maven local, basado en file system, que está comprometido con SCM como parte del proyecto y al que se hace referencia en función de su dependencia. El repositorio se declararía en el pom del proyecto como se ilustra a continuación:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Cualquier paquete de terceros incluido debe adherirse a las directrices de empaquetado y codificación del servicio as a Cloud Service de AEM descritas en este artículo; de lo contrario, su inclusión dará como resultado un error de implementación.

El siguiente Maven `POM.xml` Un fragmento de código muestra cómo los paquetes de terceros pueden incrustarse en el paquete &quot;Contenedor&quot; del proyecto, normalmente denominado **&#39;all&#39;**, a través de la variable **filevault-package-maven-plugin** Configuración del complemento Maven.

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          ...

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

Si se informa o se detecta un error después de la implementación, es posible que se requiera una reversión a la versión azul. Sería aconsejable garantizar que el código azul sea compatible con cualquier estructura nueva creada por la versión verde, ya que las nuevas estructuras (cualquier contenido mutable) no se revertirán. Si el código antiguo no es compatible, será necesario aplicar correcciones en las versiones posteriores del cliente.

## Modos de ejecución {#runmodes}

En las soluciones de AEM existentes, los clientes tienen la opción de ejecutar instancias con modos de ejecución arbitrarios y aplicar la configuración OSGI o instalar paquetes OSGI a esas instancias específicas. Los modos de ejecución definidos normalmente incluyen la variable *service* (autor y publicación) y el entorno (rde, dev, stage, prod).

AEM as a Cloud Service, por otro lado, tiene más opiniones sobre qué modos de ejecución están disponibles y cómo se pueden asignar a ellos los paquetes OSGI y la configuración OSGI:

* Los modos de ejecución de la configuración OSGI deben hacer referencia a RDE, dev, stage, prod para el entorno o autor, publicar para el servicio. Una combinación de `<service>.<environment_type>` se admite, mientras que estos se deben utilizar en este orden concreto (por ejemplo `author.dev` o `publish.prod`). Se debe hacer referencia a los tokens OSGI directamente desde el código en lugar de usar la variable `getRunModes` que ya no incluirá el `environment_type` en tiempo de ejecución. Para obtener más información, consulte [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Los modos de ejecución de los paquetes OSGI están limitados al servicio (autor, publicación). Los paquetes OSGI en modo de ejecución deben instalarse en el paquete de contenido en `install/author` o `install/publish`.

Al igual que las soluciones de AEM existentes, no hay forma de utilizar modos de ejecución para instalar solo contenido para entornos o servicios específicos. Si se desea sembrar un entorno de desarrollo con datos o HTML que no estén en fase o producción, se puede utilizar el administrador de paquetes.

Las configuraciones de modo de ejecución admitidas son:

* **config** (*El valor predeterminado se aplica a todos los servicios AEM*)
* **config.author** (*Se aplica a todos los servicios de AEM Author*)
* **config.author.dev** (*Se aplica al servicio de creación AEM desarrollo*)
* **config.author.rde** (*Se aplica a AEM servicio de creación de RDE*)
* **config.author.stage** (*Se aplica al servicio de creación AEM ensayo*)
* **config.author.prod** (*Se aplica a AEM servicio de creación de producción*)
* **config.publish** (*Se aplica al servicio AEM Publish*)
* **config.publish.dev** (*Se aplica al servicio de publicación AEM desarrollo*)
* **config.publish.rde** (*Se aplica a AEM servicio de publicación RDE*)
* **config.publish.stage** (*Se aplica al servicio de publicación AEM ensayo*)
* **config.publish.prod** (*Se aplica a AEM servicio Publicación de producción*)
* **config.dev** (*Se aplica a AEM servicios de desarrollo*)
* **config.rde** (*Se aplica a los servicios RDE*)
* **config.stage** (*Se aplica a AEM servicios de ensayo*)
* **config.prod** (*Se aplica a AEM servicios de producción*)

Se utiliza la configuración OSGI que tiene los modos de ejecución más coincidentes.

Al desarrollar localmente, un parámetro de inicio de modo de ejecución, `-r`, se utiliza para especificar la configuración OSGI del modo de ejecución.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configuración de tareas de mantenimiento en el control de código fuente {#maintenance-tasks-configuration-in-source-control}

Las configuraciones de la tarea de mantenimiento deben persistir en el control de código fuente, ya que la variable **Herramientas > Operaciones** La pantalla ya no estará disponible en los entornos de Cloud. Esto tiene la ventaja de garantizar que los cambios se mantengan intencionalmente en lugar de aplicarse de forma reactiva y tal vez olvidados. Consulte la [Artículo de la tarea de mantenimiento](/help/operations/maintenance.md) para obtener más información.
