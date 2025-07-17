---
title: Implementación en AEM as a Cloud Service
description: Obtenga información acerca de los aspectos básicos y las prácticas recomendadas de implementación en AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
role: Admin
source-git-commit: d6c5c70e8b6565a20866d392900aef219d3fd09d
workflow-type: tm+mt
source-wordcount: '3440'
ht-degree: 93%

---

# Implementación en AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introducción {#introduction}

Los fundamentos del desarrollo de código son similares en AEM as a Cloud Service en comparación con las soluciones AEM On Premise y Managed Services. Los desarrolladores escriben el código y lo prueban localmente, para a continuación enviarlo a entornos de AEM as a Cloud Service remotos. Se requiere Cloud Manager, que era una herramienta de entrega de contenido opcional para Managed Services. Esta herramienta de envío es ahora el único mecanismo para implementar código en entornos de desarrollo, fase y producción de AEM as a Cloud Service. Para ejecutar una validación y una depuración rápidas de las funcionalidades antes de implementar los entornos mencionados, el código se puede sincronizar de un entorno local a un [Entorno de desarrollo rápido](/help/implementing/developing/introduction/rapid-development-environments.md).

La actualización de la [versión de AEM](/help/implementing/deploying/aem-version-updates.md) siempre es un evento de implementación independiente de la inserción de [código personalizado](#customer-releases). Visto de otra manera, las versiones de código personalizado deben probarse con la versión de AEM que está en producción, ya que es la que se implementa en primer lugar. Las actualizaciones de versión de AEM que se producen posteriormente (que son frecuentes y se aplican automáticamente) están pensadas para ser compatibles con versiones anteriores del código de cliente ya implementado.

El resto de este documento describe cómo los desarrolladores deben adaptar sus prácticas para que funcionen tanto con las actualizaciones de versiones de AEM as a Cloud Service como con las actualizaciones de clientes.

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## Versiones de clientes {#customer-releases}

### Codificación con la versión de AEM correcta {#coding-against-the-right-aem-version}

Para las soluciones de AEM anteriores, la versión de AEM más reciente cambiaba con poca frecuencia (aproximadamente anualmente con Service Packs trimestrales), y los clientes actualizaban las instancias de producción a la última versión de inicio rápido a su propio tiempo, haciendo referencia al Jar de la API. Sin embargo, las aplicaciones de AEM as a Cloud Service se actualizan automáticamente a la última versión de AEM con mayor frecuencia, por lo que el código personalizado para versiones internas debe crearse con la última versión de AEM.

Al igual que para las versiones de AEM existentes que no se basan en la nube, se admite un desarrollo local sin conexión basado en un inicio rápido específico y se espera que normalmente sea la herramienta preferida para la depuración.

>[!NOTE]
>Existen diferencias operativas sutiles entre el comportamiento de la aplicación en un equipo local y el de Adobe Cloud. Estas diferencias arquitectónicas deben respetarse durante el desarrollo local y podrían dar lugar a un comportamiento diferente al implementarse en la infraestructura en la nube. Debido a estas diferencias, es importante realizar pruebas exhaustivas en entornos de desarrollo y fase antes de implementar un nuevo código personalizado en producción.

Para desarrollar un código personalizado para una versión interna, debe descargarse e instalarse la versión correspondiente del [SDK de AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md). Para obtener información adicional acerca del uso de las herramientas de Dispatcher de AEM as a Cloud Service, consulte [Dispatcher en la nube](/help/implementing/dispatcher/disp-overview.md).

El siguiente vídeo proporciona información general de alto nivel sobre cómo implementar los códigos en AEM as a Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/34039?quality=9&captions=spa)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Implementación de paquetes de contenido mediante Cloud Manager y el Administrador de paquetes {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Implementaciones mediante Cloud Manager {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

Los clientes implementan código personalizado en entornos de nube a través de Cloud Manager. Cloud Manager transforma los paquetes de contenido ensamblados localmente en un artefacto que se ajusta al Modelo de funciones de Sling, que es el modo en que se describe una aplicación AEM as a Cloud Service al ejecutarse en un entorno de nube. Como resultado, al consultar los paquetes en [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) en entornos de Cloud, el nombre incluye “cp2fm” y los paquetes transformados tienen todos los metadatos eliminados. No se puede interactuar con ellos, lo que significa que no se pueden descargar, replicar ni abrir. Para obtener documentación detallada sobre el convertidor, consulte [&#128279;](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)
sling-org-apache-sling-feature-cpconverter en GitHub.

Los paquetes de contenido escritos para aplicaciones AEM as a Cloud Service deben tener una clara separación entre contenido inmutable y mutable. Cloud Manager solo instala el contenido mutable, lo que también genera el siguiente mensaje:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

El resto de esta sección describe la composición y las implicaciones de los paquetes inmutables y mutables.

### Paquetes de contenido inmutable {#immutabe-content-packages}

Todo el contenido y el código que persiste en el repositorio inmutable deben registrarse en Git e implementarse mediante Cloud Manager. En otras palabras, a diferencia de las soluciones AEM actuales, el código nunca se implementa directamente en una instancia de AEM en ejecución. Este flujo de trabajo garantiza que el código que se ejecuta para una versión determinada en cualquier entorno de Cloud sea idéntico, lo que elimina el riesgo de variación no intencional del código en la producción. Por ejemplo, la configuración de OSGI debe confirmarse con el control de código fuente en lugar de administrarse durante la ejecución a través del administrador de configuración de la consola web de AEM.

Como los cambios de aplicación debido al patrón de implementación están habilitados mediante un conmutador, no pueden depender de los cambios en el repositorio mutable con la excepción de los usuarios de servicio, sus ACL, los tipos de nodos y los cambios de definición de índice.

Para los clientes con bases de código existentes, es fundamental pasar por el ejercicio de reestructuración de repositorios descrito en la documentación de AEM para garantizar que el contenido que anteriormente estaba bajo /etc se mueva a la ubicación correcta.

Se aplican algunas restricciones adicionales a estos paquetes de código; por ejemplo, [los enlaces de instalación](https://jackrabbit.apache.org/filevault/installhooks.html) no son compatibles.

## Configuración OSGi {#osgi-configuration}

Como se ha mencionado anteriormente, la configuración OSGI debe confirmarse en el control de código fuente en lugar de a través de la consola web. Las técnicas para hacerlo incluyen las siguientes:

* Realizar los cambios necesarios en el entorno de AEM local del desarrollador con el administrador de configuración de la consola web de AEM y a continuación exportar los resultados al proyecto de AEM en el sistema de archivos local
* Crear la configuración OSGI manualmente en el proyecto AEM del sistema de archivos local, haciendo referencia al administrador de configuración de la consola de AEM para los nombres de propiedades.

Obtenga más información sobre la configuración OSGI en [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Contenido mutable {#mutable-content}

A veces, puede resultar útil preparar los cambios de contenido en el control de código fuente para que Cloud Manager pueda implementarlos cada vez que se actualiza un entorno. Por ejemplo, puede ser razonable inicializar ciertas estructuras de carpetas raíz. O bien, alinee los cambios en plantillas editables para habilitar directivas y componentes que se actualizaron durante la implementación de la aplicación.

Existen dos estrategias para describir el contenido que Cloud Manager implementa en el repositorio mutable, los paquetes de contenido mutable y las instrucciones de `repoinit`

### Paquetes de contenido mutable {#mutable-content-packages}

El contenido, como las jerarquías de rutas de carpetas, los usuarios de servicios y los controles de acceso (ACL), se suelen confirmar en un proyecto de AEM basado en arquetipos Maven. Las técnicas incluyen la exportación desde AEM o la escritura directamente como XML. Durante el proceso de compilación e implementación, Cloud Manager empaqueta el paquete de contenido mutable resultante. El contenido mutable se instala en tres momentos diferentes durante la fase de implementación de la canalización:

Antes del inicio de la nueva versión de la aplicación:

* Definiciones de índice (agregar, modificar, eliminar)

Durante el inicio de la nueva versión de la aplicación, pero antes del cambio:

* Usuarios de servicio (agregar)
* ACL de usuario de servicio (agregar)
* Tipos de nodo (agregar)

Después de cambiar a una nueva versión de la aplicación:

* El resto del contenido se puede definir mediante el almacén Jackrabbit. Por ejemplo:
   * Carpetas (agregar, modificar, quitar)
   * Plantillas editables (agregar, modificar, quitar)
   * Configuración según el contexto (cualquier elemento en `/conf`) (agregar, modificar, eliminar)
   * Scripts (los paquetes pueden activar Instalar vínculos en varias etapas del proceso de instalación del paquete). Consulte la [documentación de Jackrabbit Filevault](https://jackrabbit.apache.org/filevault/installhooks.html) acerca de instalar vínculos. Tenga en cuenta que CS de AEM actualmente utiliza la versión 3.4.0 de Filevault, que limita instalar vínculos a usuarios que son administradores, usuarios del sistema y miembros del grupo de administradores.

Es posible limitar la instalación de contenido mutable a la creación o publicación incrustando paquetes en una carpeta install.author o install.publish en `/apps`. La reestructuración para reflejar esta separación se realizó en AEM 6.5 y los detalles sobre la reestructuración recomendada del proyecto se encuentran en la [documentación de AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=es).

>[!NOTE]
>Los paquetes de contenido se implementan en todos los tipos de entorno (des., fase, prod.). No es posible limitar la implementación a un entorno específico. Esta limitación se aplica para garantizar la opción de una ejecución de prueba de ejecución automatizada. El contenido específico de un entorno requiere una instalación manual mediante el [administrador de paquetes](/help/implementing/developing/tools/package-manager.md).

Además, no hay ningún mecanismo para restablecer los cambios del paquete de contenido mutable después de haberlos aplicado. Si los clientes detectan un problema, pueden optar por solucionarlo en su próxima versión de código o, como último recurso, restaurar todo el sistema a un punto en el tiempo antes de la implementación.

Cualquier paquete de terceros incluido debe validarse como compatible con AEM as a Cloud Service; de lo contrario, su inclusión dará como resultado un error de implementación.

Como se mencionó anteriormente, los clientes con bases de código existentes deben ajustarse al ejercicio de reestructuración de repositorios necesario por los cambios de repositorio de la versión 6.5 descritos en la [documentación de AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=es).

## RepoInit {#repoinit}

En los siguientes casos, es preferible utilizar el método de codificación manual para la creación explícita de instrucciones de contenido `repoinit` en configuraciones de fábrica OSGI:

* Crear/eliminar/deshabilitar usuarios de servicios
* Crear/eliminar grupos
* Crear/eliminar usuarios
* Agregar ACL

  >[!NOTE]
  >
  >La definición de ACL requiere que las estructuras de nodos ya estén presentes. Por lo tanto, puede que sea necesario crear instrucciones de ruta anteriores.

* Agregar ruta (por ejemplo, para estructuras de carpetas raíz)
* Agregar CND (definiciones de tipos de nodos)

Es preferible un informe para estos casos de uso de modificación de contenido compatibles debido a las ventajas siguientes:

* `Repoinit` crea recursos al inicio para que la lógica pueda dar por sentada la existencia de esos recursos. En el enfoque del paquete de contenido mutable, los recursos se crean después del inicio, por lo que el código de la aplicación que se basa en ellos puede fallar.
* `Repoinit` es un conjunto de instrucciones relativamente seguro, ya que controla explícitamente la acción que se va a llevar a cabo. Además, las únicas operaciones admitidas son aditivas, a excepción de algunos casos relacionados con la seguridad que permiten eliminar usuarios, usuarios de servicios y grupos. Por el contrario, la eliminación de algo en el enfoque del paquete de contenido mutable es explícita; al definir un filtro, se elimina cualquier elemento presente cubierto por un filtro. Sin embargo, hay que tener cuidado porque con cualquier contenido hay escenarios en los que la presencia de contenido nuevo puede alterar el comportamiento de la aplicación.
* `Repoinit` realiza operaciones atómicas y rápidas. Por el contrario, los paquetes de contenido mutables pueden depender en gran medida del rendimiento según las estructuras cubiertas por un filtro. Incluso si actualiza un solo nodo, se puede crear una instantánea de un árbol grande.
* Es posible validar las instrucciones `repoinit` en un entorno de desarrollo local durante la ejecución, ya que se ejecutan cuando se registre la configuración de OSGi.
* Las instrucciones `Repoinit` son atómicas y explícitas y se omitirán si el estado ya coincide.

Cuando Cloud Manager implementa la aplicación, ejecuta estas instrucciones, independientemente de la instalación de cualquier paquete de contenido.

Para crear instrucciones de `repoinit`, siga este procedimiento:

1. Agregar la configuración OSGi para el PID de fábrica `org.apache.sling.jcr.repoinit.RepositoryInitializer` en una carpeta de configuración del proyecto. Utilice un nombre descriptivo para la configuración como **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. Agregue instrucciones `repoinit` a la propiedad script de la configuración. La sintaxis y las opciones están documentadas en la [Documentación de Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html). Tenga en cuenta que debe haber una creación explícita de una carpeta principal antes de sus carpetas secundarias. Por ejemplo, una creación explícita de `/content` antes de `/content/myfolder` y de `/content/myfolder/mysubfolder`. Para que las ACL se establezcan en estructuras de bajo nivel, se recomienda configurarlas en un nivel superior y trabajar con una restricción `rep:glob`. Por ejemplo, `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Valide en el entorno de desarrollo local durante la ejecución.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Para las ACL definidas para nodos debajo de `/apps` o `/libs` la `repoinit`ejecución de se iniciará en un repositorio en blanco. Los paquetes se instalan después de `repoinit`, por lo que las instrucciones no pueden depender en nada de lo definido en los paquetes, sino que se deben definir las condiciones previas como las estructuras principales que hay debajo.

>[!TIP]
>
>En el caso de las ACL, la creación de estructuras profundas puede resultar engorrosa. Por lo tanto, es más razonable definir una ACL en un nivel superior y restringir donde se supone que actúa a través de una restricción `rep:glob`.

Puede encontrar más información sobre `repoinit` en la [Documentación de Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Administrador de paquetes con definición para paquetes de contenido mutable {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Administrador de paquetes: migración de paquetes de contenido mutable"
>abstract="Explore el uso de Administrador de paquetes para casos de uso en los que un paquete de contenido debe instalarse de forma &quot;única&quot;. La instalación incluye importar contenido específico desde la producción hasta el montaje para depurar un problema de producción, transferir un paquete de contenido pequeño del entorno local a entornos de AEM Cloud, etc."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es" text="Herramienta de transferencia de contenido"

Hay casos de uso en los que un paquete de contenido debe instalarse con definición. Por ejemplo, importar contenido específico de la producción a ensayo para depurar un problema de producción. Para estos escenarios, el [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) se puede utilizar en entornos de AEM as a Cloud Service.

Dado que el Administrador de paquetes es un concepto de tiempo de ejecución, no es posible instalar contenido o código en el repositorio inmutable, por lo que estos paquetes de contenido solo deben consistir en contenido mutable (principalmente `/content` o `/conf`). Si el paquete de contenido incluye contenido mixto (tanto mutable como inmutable), solo se instalará el contenido mutable.

>[!IMPORTANT]
>
>La interfaz de usuario del Administrador de paquetes puede devolver el mensaje de error **Indefinido** si un paquete tarda más de diez minutos en instalarse.
>
>Esto no se debe a un error en la instalación, sino a un tiempo de espera que Cloud Service tiene para todas las solicitudes.
>
>No vuelva a intentar realizar la instalación si aparece un error de este tipo. La instalación continúa correctamente en el fondo. Si reinicia la instalación, podrían producirse conflictos debido a varios procesos de importación simultáneos.

Cualquier paquete de contenido instalado mediante Cloud Manager (mutable e inmutable) aparecerá en estado inmovilizado en la interfaz de usuario del Administrador de paquetes de AEM. Estos paquetes no se pueden volver a instalar, volver a crear ni descargar, y aparecerán en la lista con el sufijo **&quot;cp2fm&quot;**, que indica que la instalación fue administrada por Cloud Manager.

### Inclusión de paquetes de terceros {#including-third-party}

Es habitual que los clientes incluyan paquetes generados previamente de fuentes de terceros, como proveedores de software, tales como los socios de traducción de Adobe. La recomendación es alojar estos paquetes en un repositorio remoto y hacer referencia a ellos en `pom.xml`. Este método es posible para repositorios públicos y también para repositorios privados con protección por contraseña, tal como se describe en los [repositorios Maven protegidos por contraseña](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Si no es posible almacenar el paquete en un repositorio remoto, los clientes pueden ubicarlo en un repositorio Maven local, basado en el sistema de archivos, que se asigna a SCM como parte del proyecto y al que hace referencia todo lo que dependa de él. Se hace referencia a este según lo que dependa de este. El repositorio se declararía en el elemento POM del proyecto, como se ilustra a continuación:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Cualquier paquete de terceros incluido debe cumplir a las directrices de empaquetado y codificación de AEM as a Cloud descritas en este artículo; de lo contrario, su inclusión dará como resultado un error de implementación.

El siguiente fragmento `POM.xml` de Maven muestra cómo los paquetes de terceros pueden integrarse en el paquete “Contenedor” del proyecto, normalmente denominado **&#39;all&#39;**, a través de **la configuración del complemento filevault-package-maven-plugin** de Maven.

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

## Cómo funcionan las implementaciones dinámicas {#how-rolling-deployments-work}

Al igual que las actualizaciones de AEM, las versiones de los clientes se implementan mediante una estrategia de implementación dinámica para eliminar el tiempo de inactividad del clúster de creación en las circunstancias adecuadas. A continuación se describe la secuencia general de eventos, en la que los nodos con las versiones antigua y nueva del código de cliente ejecutan la misma versión del código de la AEM.

* Los nodos con la versión antigua están activos y se crea una versión candidata para la nueva versión, que está disponible.
* Si hay definiciones de índice nuevas o actualizadas, se procesan los índices correspondientes. Tenga en cuenta que los nodos con la versión antigua siempre utilizarán los índices antiguos, mientras que los nodos con la nueva versión siempre utilizarán los índices nuevos.
* Los nodos con la versión nueva se inician mientras que las versiones anteriores siguen sirviendo tráfico.
* Los nodos con la versión antigua se siguen ejecutando y sirviendo mientras se comprueba la preparación de los nodos con la nueva versión mediante comprobaciones de estado.
* Los nodos con la versión nueva que estén listos aceptarán tráfico y reemplazarán los nodos con la versión antigua, los cuales se desactivan.
* Con el tiempo, los nodos con la versión antigua se sustituyen por nodos con la nueva versión hasta que solo quedan nodos con versiones nuevas, lo que completa la implementación.
* Se implementa cualquier contenido mutable nuevo o modificado.

## Índices {#indexes}

Los índices nuevos o modificados provocarán un paso adicional de indexación o reindexación antes de que la versión nueva pueda entrar en el tráfico. Encontrará detalles sobre la administración de índices en AEM as a Cloud Service en [Búsqueda de contenido e indexación](/help/operations/indexing.md). Puede comprobar el estado de indexación de las páginas de compilación en Cloud Manager y recibir una notificación cuando la nueva versión esté lista para admitir tráfico.

>[!NOTE]
>
>El tiempo necesario para una implementación móvil varía según el tamaño del índice. El motivo es que la nueva versión no puede aceptar tráfico hasta que se genere el nuevo índice.

En este momento, AEM as a Cloud Service no funciona con herramientas de administración de índices como la herramienta ACS Commons Ensure Oak Index.

## Replicación {#replication}

El mecanismo de publicación es compatible con versiones anteriores de las [API de Java de replicación de AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es).

Para desarrollar y probar la replicación con el inicio rápido de AEM listo para la nube, las funcionalidades de replicación clásicas deben usarse con la configuración de Autor/Publicación. Si el punto de entrada de la interfaz de usuario de AEM Author se elimina de la nube, los usuarios acceden a `http://localhost:4502/etc/replication` para la configuración.

## Código compatible con hacia atrás para implementaciones móviles {#backwards-compatible-code-for-rolling-deployments}

Como se ha detallado anteriormente, la estrategia de implementación gradual de AEM as a Cloud Service implica que tanto las versiones anteriores como las nuevas pueden estar funcionando al mismo tiempo. Por lo tanto, tenga cuidado con los cambios de código que no sean compatibles con la versión anterior de AEM que aún está en funcionamiento.

Además, la versión antigua debe probarse para verificar la compatibilidad con cualquier estructura de contenido mutable nueva aplicada por la nueva versión en caso de revertir, ya que el contenido mutable no se elimina.

### Usuarios de servicio y cambios de ACL {#service-users-and-acl-changes}

Cambiar los usuarios del servicio o las ACL que acceden al contenido o al código podría provocar errores en las versiones de AEM anteriores, lo que da como resultado acceso a ese contenido o código con usuarios de servicios obsoletos. Para solucionar este comportamiento, la recomendación es hacer cambios distribuidos en al menos dos versiones, y la primera versión actúa como vínculo antes de limpiarla en la versión siguiente.

### Cambios en el índice {#index-changes}

Si se realizan cambios en los índices, es importante que la versión antigua siga utilizando sus índices hasta que finalice, mientras que la nueva versión utiliza su propio conjunto modificado de índices. El desarrollador debe seguir las técnicas de administración de índices descritas en [Búsqueda de contenido e indexación](/help/operations/indexing.md).

### Codificación conservadora para retrocesos {#conservative-coding-for-rollbacks}

Si se informa o se detecta un error después de la implementación, es posible que se requiera una reversión a la versión antigua. Asegúrese de que el código nuevo sea compatible con cualquier estructura nueva creada por esa versión nueva, ya que las nuevas estructuras (cualquier contenido mutable) no se revierten. Si el código antiguo no es compatible, es necesario aplicar correcciones en las versiones posteriores del cliente.

## Entornos de desarrollo rápido (RDE) {#rde}

Los [entornos de desarrollo rápido](/help/implementing/developing/introduction/rapid-development-environments.md) (RDE) permiten a los desarrolladores implementar y revisar cambios con mayor velocidad, pues minimizan la cantidad de tiempo necesario para probar funciones que ya han demostrado funcionar en un entorno de desarrollo local.

A diferencia de los entornos de desarrollo normales, que implementan código mediante la canalización de Cloud Manager, estos utilizan herramientas de línea de comandos para sincronizar el código de un entorno de desarrollo local a un RDE. Una vez que los cambios se hayan probado correctamente en un RDE, impleméntelos en un entorno de desarrollo de nube normal a través de la canalización de Cloud Manager, que coloca el código a través de las puertas de calidad adecuadas.

## Ejecutar modos {#runmodes}

En las soluciones de AEM existentes, los clientes tienen la opción de ejecutar instancias con modos de ejecución arbitrarios y aplicar la configuración OSGI o instalar paquetes OSGI a esas instancias específicas. Los modos de ejecución definidos normalmente incluyen el *servicio* (creación y publicación) y el entorno (RDE, des., fase, prod.).

AEM as a Cloud Service, por otro lado, tiene más opiniones sobre qué modos de ejecución están disponibles y cómo se pueden asignar a ellos los paquetes OSGI y la configuración OSGI:

* Los modos de ejecución de la configuración OSGI deben hacer referencia al RDE, al desarrollo, a la fase, la producción para el entorno o la creación, publicación del servicio. Se admite una combinación de `<service>.<environment_type>`, mientras que estos entornos deben usarse en este orden en particular (por ejemplo, `author.dev` o `publish.prod`). Se debe hacer referencia a los tokens OSGI directamente desde el código en lugar de usar el método `getRunModes` que ya no incluirá el `environment_type` en el tiempo de ejecución. Para obtener más información, consulte [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Los modos de ejecución de los paquetes OSGI están limitados al servicio (autor, publicación). Los paquetes OSGI en el modo previo a la ejecución deben instalarse en el paquete de contenido en `install.author` o `install.publish`.

AEM as a Cloud Service no permite utilizar modos de ejecución para instalar contenido para entornos o servicios específicos. Si un entorno de desarrollo debe estar preconfigurado con datos o HTML que no se encuentre en los entornos de ensayo o producción, se puede utilizar el administrador de paquetes.

Las configuraciones de modo de ejecución admitidas son las siguientes:

* **config** (*de forma predeterminada, se aplica a todos los servicios de AEM*)
* **config.author** (*Se aplica a todos los servicios de AEM Author*)
* **config.author.dev** (*Se aplica al servicio de creación AEM desarrollo*)
* **config.author.rde** (*se aplica al servicio Creación de RDE de AEM*)
* **config.author.stage** (*Se aplica al servicio de creación AEM ensayo*)
* **config.author.prod** (*Se aplica al servicio de creación AEM producción*)
* **config.publish** (*Se aplica al servicio AEM publicación*)
* **config.publish.dev** (*Se aplica al servicio de publicación AEM desarrollo*)
* **config.publish.rde** (*se aplica al servicio Publicación de RDE de AEM*)
* **config.publish.stage** (*Se aplica al servicio de publicación AEM ensayo*)
* **config.publish.prod** (*Se aplica al servicio de publicación de AEM producción*)
* **config.dev** (*Se aplica al servicio de AEM desarrollo*)
* **config.rde** (*se aplica a los servicios de RDE*)
* **config.stage** (*Se aplica al servicio de AEM ensayo*)
* **config.prod** (*Se aplica al servicio de AEM producción*)

Se utiliza la configuración OSGI que tiene los modos de ejecución más coincidentes.

Al desarrollar localmente, el parámetro de inicio de modo de ejecución, `-r`, se utiliza para especificar la configuración OSGI del modo de ejecución.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configuración de tareas de mantenimiento en el control de origen {#maintenance-tasks-configuration-in-source-control}

Las configuraciones de la tarea de mantenimiento deben mantenerse en el control de origen, ya que la pantalla **Herramientas > Operaciones** no estará disponible en los entornos de Cloud. Esta ventaja garantiza la persistencia intencionada de los cambios en lugar de su aplicación reactiva y olvido. Consulte [Tareas de mantenimiento en AEM as a Cloud Service](/help/operations/maintenance.md) para obtener más información.
