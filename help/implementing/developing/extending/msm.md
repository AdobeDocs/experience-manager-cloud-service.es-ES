---
title: Ampliación del Administrador de varios sitios
description: Obtenga información sobre cómo ampliar la funcionalidad del Administrador de varios sitios.
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 2%

---


# Ampliación del Administrador de varios sitios {#extending-the-multi-site-manager}

Este documento le ayuda a comprender cómo ampliar la funcionalidad del Administrador de varios sitios y abarca los siguientes temas.

* Obtenga información acerca de los miembros principales de la API de Java de MSM
* Cree una nueva acción de sincronización que se pueda utilizar en una configuración de despliegue
* Modificar el idioma y los códigos de país predeterminados

>[!TIP]
>
>Esta página es más fácil de entender en el contexto del documento [Reutilización del contenido: Administrador de varios sitios.](/help/sites-cloud/administering/msm/overview.md)

>[!CAUTION]
>
>El Administrador de varios sitios y su API se utilizan al crear un sitio web y, como tal, solo están pensados para su uso en un entorno de creación.

## Información general sobre la API de Java {#overview-of-the-java-api}

Multi Site Management consta de los siguientes paquetes:

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

Los objetos de API de MSM principales interactúan de la siguiente manera (consulte también la sección [Términos utilizados](/help/sites-cloud/administering/msm/overview.md#terms-used)):

![Objetos principales de la API de MSM](assets/msm-api-interaction.png)

* **`Blueprint`** - A `Blueprint` (como en [configuración de modelo](/help/sites-cloud/administering/msm/overview.md#source-blueprints-and-blueprint-configurations)) especifica las páginas desde las que una live copy puede heredar contenido.

  ![Modelo](assets/msm-blueprint-interaction.png)

   * El uso de una configuración de modelo ( `Blueprint`) es opcional, pero:

      * Permite al autor utilizar la variable **Despliegue** en el origen para insertar explícitamente modificaciones en live copies que hereden de este origen.
      * Permite al autor utilizar **Crear sitio**, que permite al usuario seleccionar idiomas fácilmente y configurar la estructura de la live copy.
      * Define la configuración de despliegue predeterminada para cualquier Live Copies resultante.

* **`LiveRelationship`** - El `LiveRelationship` especifica la conexión (relación) entre un recurso de la rama de live copy y su recurso de origen/modelo equivalente.

   * Las relaciones se utilizan para realizar la herencia y el despliegue.
   * `LiveRelationship` Los objetos de proporcionan acceso (referencias) a las configuraciones de despliegue ( `RolloutConfig`), `LiveCopy`, y `LiveStatus` objetos relacionados con la relación.

   * Por ejemplo, se crea una Live Copy en `/content/copy/us` desde el origen/modelo en `/content/wknd/language-masters`. Los recursos `/content/wknd/language-masters/en/jcr:content` y `/content/copy/us/en/jcr:content` formar una relación.

* **`LiveCopy`** - A `LiveCopy` contiene los detalles de configuración de las relaciones (`LiveRelationship`) entre los recursos de live copy y sus recursos de origen/modelo.

   * Utilice el `LiveCopy` para acceder a la ruta de la página, la ruta de la página de origen/modelo, las configuraciones de despliegue y si las páginas secundarias también se incluyen en la `LiveCopy`.

   * A `LiveCopy` El nodo se crea cada vez que **Crear sitio** o **Crear Live Copy** se utiliza.

* **`LiveStatus`** - `LiveStatus` proporcionan acceso al estado de tiempo de ejecución de un objeto `LiveRelationship`. Se utiliza para consultar el estado de sincronización de una Live Copy.

* **`LiveAction`** - A `LiveAction` es una acción que se ejecuta en cada recurso implicado en el despliegue.

   * `LiveAction`Las solo se generan mediante `RolloutConfig`s.

* **`LiveActionFactory`** - A `LiveActionFactory` crea `LiveAction` objetos dados a `LiveAction` configuración. Las configuraciones se almacenan como recursos en el repositorio.

* **`RolloutConfig`** - El `RolloutConfig` contiene una lista de `LiveActions`, que se utilizará cuando se active. El `LiveCopy` hereda el `RolloutConfig` y el resultado está presente en la variable `LiveRelationship`.

   * La configuración de una Live Copy por primera vez también utiliza una `RolloutConfig` (que déclencheur el `LiveAction`s).

## Creación de una nueva acción de sincronización {#creating-a-new-synchronization-action}

Puede crear acciones de sincronización personalizadas para utilizarlas con las configuraciones de despliegue. Esto puede resultar útil cuando la variable [acciones instaladas](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) no cumplen los requisitos específicos de su aplicación.

Para ello, cree dos clases:

* Una implementación de la [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) que realiza la acción.
* Un componente OSGi que implementa la variable [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) y crea instancias de su `LiveAction` clase

El `LiveActionFactory` crea instancias del `LiveAction` para una configuración determinada:

* `LiveAction` Las clases incluyen los métodos siguientes:

   * `getName` - Devuelve el nombre de la acción

      * El nombre se utiliza para hacer referencia a la acción, por ejemplo, en las configuraciones de despliegue.

   * `execute` - Realiza las tareas de la acción

* `LiveActionFactory` Las clases incluyen los siguientes miembros:

   * `LIVE_ACTION_NAME` - Un campo que contiene el nombre del asociado `LiveAction`

      * Este nombre debe coincidir con el valor devuelto por el `getName` método del `LiveAction` clase.

   * `createAction` : crea una instancia de `LiveAction`

      * El opcional `Resource` se puede utilizar para proporcionar información de configuración.

   * `createsAction` - Devuelve el nombre del asociado `LiveAction`

### Acceso al nodo de configuración de LiveAction {#accessing-the-liveaction-configuration-node}

Utilice el `LiveAction` nodo de configuración en el repositorio para almacenar información que afecta al comportamiento en tiempo de ejecución del `LiveAction` ejemplo. El nodo en el repositorio que almacena el `LiveAction` La configuración de está disponible para `LiveActionFactory` durante la ejecución. Por lo tanto, puede agregar propiedades al nodo de configuración a y utilizarlas en su `LiveActionFactory` según sea necesario.

Por ejemplo, una `LiveAction` necesita almacenar el nombre del autor del modelo. Una propiedad del nodo de configuración incluye el nombre de la propiedad de la página de modelo que almacena la información. En tiempo de ejecución, la variable `LiveAction` recupera el nombre de propiedad de la configuración y, a continuación, obtiene el valor de propiedad.

El parámetro del [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) El método es un `Resource` objeto. Esta `Resource` representa el objeto `cq:LiveSyncAction` para esta acción activa en la configuración de despliegue.

Consulte el documento [Creación de una configuración de despliegue](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) para obtener más información.

Como de costumbre, al utilizar un nodo de configuración, debe adaptarlo a un `ValueMap` objeto:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Acceder a los nodos de destino, a los nodos de origen y a LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

Los siguientes objetos se proporcionan como parámetros del `execute` método del `LiveAction` objeto:

* A [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) objeto que representa el origen de live copy
* A `Resource` que representa el destino de live copy.
* El [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) objeto para live copy
   * El `autoSave` indica si su `LiveAction` debe guardar los cambios realizados en el repositorio
   * El `reset` Este valor indica el modo de restablecimiento del despliegue.

A partir de estos objetos puede obtener toda la información acerca de la `LiveCopy`. También puede utilizar la variable `Resource` objetos que obtener `ResourceResolver`, `Session`, y `Node` objetos. Estos objetos son útiles para manipular el contenido del repositorio:

En la primera línea del siguiente código, el origen es el `Resource` objeto de la página de origen:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>El `Resource` los argumentos pueden ser `null` o `Resources` objetos que no se adaptan a `Node` objetos, como [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/NonExistingResource.html) objetos.

## Creación de una nueva configuración de despliegue {#creating-a-new-rollout-configuration}

Puede crear una configuración de despliegue cuando las configuraciones de despliegue instaladas no cumplan con los requisitos de la aplicación. Siga estos dos pasos:

* [Creación de la configuración de despliegue](#create-the-rollout-configuration)
* [Añadir acciones de sincronización a la configuración de lanzamiento](#add-synchronization-actions-to-the-rollout-configuration)

La nueva configuración de despliegue está disponible al establecer configuraciones de despliegue en una página de modelo o Live Copy.

>[!TIP]
>
>Consulte también la [prácticas recomendadas para personalizar despliegues](/help/sites-cloud/administering/msm/best-practices.md#customizing-rollouts).

### Creación de la configuración de despliegue {#create-the-rollout-configuration}

Para crear una nueva configuración de despliegue:

1. Abrir CRXDE Lite en `https://<host>:<port>/crx/de`.

1. Vaya a `/apps/msm/<your-project>/rolloutconfigs`, la versión personalizada del proyecto de `/libs/msm/wcm/rolloutconfigs`.

   * Si esta es su primera configuración, esto `/libs` La rama debe utilizarse como plantilla para crear la nueva rama en `/apps`.

1. En esta ubicación, cree un nodo con las siguientes propiedades:

   * **Nombre**: Nombre del nodo de la configuración de lanzamiento, por ejemplo `contentCopy` o `workflow`
   * **Tipo**: `cq:RolloutConfig`

1. Agregue las siguientes propiedades a este nodo:

   * **Nombre**: `jcr:title`
     **Tipo**: `String`
     **Valor**: un título de identificación que aparecerá en la interfaz de usuario

   * **Nombre**: `jcr:description`
     **Tipo**: `String`
     **Valor**: una descripción opcional.

   * **Nombre**: `cq:trigger`
     **Tipo**: `String`
     **Valor**: La [Desplegar Déclencheur](/help/sites-cloud/administering/msm/live-copy-sync-config.md#rollout-triggers) para utilizar
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Haga clic en **Guardar todo**.

### Añadir acciones de sincronización a la configuración de despliegue {#add-synchronization-actions-to-the-rollout-configuration}

Las configuraciones de despliegue se almacenan debajo de [nodo de configuración de despliegue](#create-the-rollout-configuration) que ha creado en la variable `/apps/msm/<your-project>/rolloutconfigs` nodo.

Agregar nodos secundarios de tipo `cq:LiveSyncAction` para agregar acciones de sincronización a la configuración de lanzamiento. El orden de los nodos de acción de sincronización determina el orden en que se producen las acciones.

1. En CRXDE Lite, seleccione su [Configuración de despliegue](#create-the-rollout-configuration) nodo, por ejemplo `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`.

1. Cree un nodo con las siguientes propiedades de nodo:

   * **Nombre**: Nombre del nodo de la acción de sincronización
      * El nombre debe ser el mismo que **Nombre de acción** en la tabla debajo de [Acciones de sincronización](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) como `contentCopy` o `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Añada y configure tantos nodos de acción de sincronización como sea necesario.

1. Reorganice los nodos de acción para que su orden coincida con el orden en que desea que se produzcan.
   * El nodo de acción superior se produce primero.

## Crear y usar una clase LiveActionFactory simple {#creating-and-using-a-simple-liveactionfactory-class}

Siga los procedimientos de esta sección para desarrollar una `LiveActionFactory` y utilizarlo en una configuración de despliegue. Los procedimientos utilizan Maven y Eclipse para desarrollar e implementar el `LiveActionFactory`:

1. [Creación del proyecto de Maven](#create-the-maven-project) e importarlo a Eclipse.
1. [Añadir dependencias](#add-dependencies-to-the-pom-file) al archivo POM.
1. [Implementación de `LiveActionFactory` interfaz](#implement-liveactionfactory) e implemente el paquete OSGi.
1. [Creación de la configuración de despliegue](#create-the-example-rollout-configuration).
1. [Creación de la Live Copy](#create-the-live-copy).

[Proyecto Maven y código fuente de la clase Java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout) está disponible en el repositorio Git público.

### Creación del proyecto Maven {#create-the-maven-project}

El siguiente procedimiento requiere que haya agregado la variable `adobe-public` al archivo de configuración de Maven.

* Para obtener información sobre el perfil público de Adobe, consulte [Obtención del complemento Maven del paquete de contenido](/help/implementing/developing/tools/maven-plugin.md#obtaining-the-content-package-maven-plugin)
* Para obtener más información sobre el archivo de configuración de Maven, consulte [Referencia de configuración](https://maven.apache.org/settings.html).

1. Abra una sesión de terminal o de línea de comandos y cambie el directorio para que apunte a la ubicación de donde crear el proyecto.
1. Introduzca el siguiente comando:

   ```text
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Especifique los siguientes valores en la solicitud interactiva:

   * **`groupId`**: `com.adobe.example.msm`
   * **`artifactId`**: `MyLiveActionFactory`
   * **`version`**: `1.0-SNAPSHOT`
   * **`package`**: `MyPackage`
   * **`appsFolderName`**: `myapp`
   * **`artifactName`**: `MyLiveActionFactory package`
   * **`packageGroup`**: `myPackages`

1. Iniciar Eclipse y [Importe el proyecto Maven.](/help/implementing/developing/tools/eclipse.md#import-the-maven-project-into-eclipse)

### Añadir dependencias al archivo POM {#add-dependencies-to-the-pom-file}

Agregue dependencias para que el compilador Eclipse pueda hacer referencia a las clases que se utilizan en el `LiveActionFactory` código.

1. En el Explorador del proyecto Eclipse, abra el archivo `MyLiveActionFactory/pom.xml`.

1. En el editor, haga clic en `pom.xml` y busque la pestaña `project/dependencyManagement/dependencies` sección.

1. Agregue el siguiente XML dentro de la variable `dependencyManagement` y, a continuación, guarde el archivo.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Abra el archivo POM para el paquete desde **Explorador de proyectos** en `MyLiveActionFactory-bundle/pom.xml`.

1. En el editor, haga clic en `pom.xml` y busque la sección proyecto/dependencias. Agregue el siguiente XML dentro del elemento dependencies y, a continuación, guarde el archivo:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementar LiveActionFactory {#implement-liveactionfactory}

Lo siguiente `LiveActionFactory` clase implementa un `LiveAction` que registra mensajes sobre las páginas de origen y destino y copia el `cq:lastModifiedBy` del nodo de origen al nodo de destino. El nombre de la acción activa es `exampleLiveAction`.

1. En el Explorador del proyecto Eclipse, haga clic con el botón secundario en `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` paquete y haga clic en **Nuevo** -> **Clase**.

1. Para el **Nombre**, introduzca `ExampleLiveActionFactory` y luego haga clic en **Finalizar**.

1. Abra el `ExampleLiveActionFactory.java` , reemplace el contenido por el siguiente código y guarde el archivo.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. Con el terminal o la sesión de comandos, cambie el directorio a `MyLiveActionFactory` (el directorio del proyecto Maven). A continuación, introduzca el siguiente comando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

1. AEM El `error.log` debe indicar que el paquete está iniciado, visible en los registros en `https://<host>:<port>/system/console/status-slinglogs`.

   ```text
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Creación de la configuración de despliegue de ejemplo {#create-the-example-rollout-configuration}

Cree la configuración de despliegue de MSM que utiliza el `LiveActionFactory` que ha creado:

1. Creación y configuración de un [Configuración de despliegue con el procedimiento estándar](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) uso de las propiedades:

   * **Título**: Configuración de despliegue de ejemplo
   * **Nombre**: example plerolloutconfig
   * **cq:déclencheur**: `publish`

### Añadir la acción Live a la configuración de despliegue de ejemplo {#add-the-live-action-to-the-example-rollout-configuration}

Configure la configuración de despliegue que creó en el procedimiento anterior para que utilice el `ExampleLiveActionFactory` clase.

1. Abra CRXDE Lite.

1. Cree el siguiente nodo en `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nombre**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Haga clic en **Guardar todo**.

1. Seleccione el `exampleLiveAction` y agregue una propiedad para indicar a `ExampleLiveAction` que el `cq:LastModifiedBy` La propiedad debe replicarse desde el nodo de origen al nodo de destino.

   * **Nombre**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

1. Haga clic en **Guardar todo**.

### Creación de la Live Copy {#create-the-live-copy}

[Creación de una Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md#creating-a-live-copy-of-a-page) de la rama Inglés/Productos del sitio de referencia de WKND con la configuración de despliegue:

* **Origen**: `/content/wknd/language-masters/en/products`

* **Configuración de despliegue**: Configuración de despliegue de ejemplo

Activar el **Productos** (inglés) de la rama de origen y observe los mensajes de registro que la variable `LiveAction` La clase genera:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

## Cambio de nombres de idiomas y países predeterminados {#changing-language-names-and-default-countries}

AEM utiliza un conjunto predeterminado de códigos de idioma y país.

* El código de idioma predeterminado es el código de dos letras en minúsculas, tal como se define en la norma ISO-639-1.
* El código de país predeterminado es el código de dos letras en minúsculas o mayúsculas, tal como se define en la norma ISO 3166.

MSM utiliza una lista almacenada de códigos de idioma y país para determinar el nombre del país asociado al nombre de la versión de idioma de la página. Si es necesario, puede cambiar los siguientes aspectos de la lista:

* Títulos de idiomas
* Nombres de países
* Países predeterminados para idiomas (para códigos como `en`, `de`, entre otros)

La lista de idiomas se almacena debajo de `/libs/wcm/core/resources/languages` nodo. Cada nodo secundario representa un idioma o un idioma-país:

* El nombre del nodo es el código de idioma (como `en` o `de`) o el código language_country (por ejemplo, `en_us` o `de_ch`).

* El `language` La propiedad del nodo almacena el nombre completo del idioma del código.
* El `country` La propiedad del nodo almacena el nombre completo del país para el código.
* Cuando el nombre del nodo solo consta de un código de idioma (como `en`), la propiedad del país es `*`y un adicional de `defaultCountry` La propiedad almacena el código del idioma-país para indicar el país que se va a utilizar.

![Definición de idioma](assets/msm-language-manager.png)

Para modificar los idiomas:

1. Abra CRXDE Lite.
1. Seleccione el `/apps` y haga clic en **Crear**, entonces **Crear carpeta.**

1. Asigne un nombre a la nueva carpeta `wcm`.

1. Repita el paso anterior para crear el `/apps/wcm/core` árbol de carpetas. Creación de un nodo de tipo `sling:Folder` in `core` llamado `resources`.

1. Haga clic con el botón derecho en `/libs/wcm/core/resources/languages` y haga clic en **Copiar**.
1. Haga clic con el botón derecho en `/apps/wcm/core/resources` y haga clic en **Pegar**. Modifique los nodos secundarios según sea necesario.
1. Haga clic en **Guardar todo**.
1. Clic **Herramientas**, **Operaciones** entonces **Consola web**. Desde esta consola, haga clic en **OSGi**, entonces **Configuración**.
1. Busque y haga clic en **Administrador de idiomas de CQ WCM por día** y cambie el valor de **Lista de idiomas** hasta `/apps/wcm/core/resources/languages`, luego haga clic en **Guardar**.

   ![Administrador de idiomas de CQ WCM por día](assets/msm-language-manager.png)

## Configurar los bloqueos MSM en las propiedades de página {#configuring-msm-locks-on-page-properties}

Al crear una propiedad de página personalizada, es posible que tenga que considerar si la nueva propiedad debe cumplir los requisitos para su despliegue en cualquier Live Copy.

Por ejemplo, si se agregan dos propiedades de página nuevas:

* Correo electrónico de contacto:

   * No es necesario desplegar esta propiedad, ya que será diferente en cada país (o marca, etc.).

* Estilo visual clave:

   * El requisito del proyecto es que esta propiedad se implemente, ya que es (generalmente) común a todos los países (o marcas, etc.).

A continuación, debe asegurarse de que:

* Correo electrónico de contacto:

   * Se excluye de las propiedades desplegadas.
   * Consulte el documento [Configuración de la sincronización de Live Copy](/help/sites-cloud/administering/msm/live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) para obtener más información.

* Estilo visual clave:

   * Asegúrese de que no puede editar esta propiedad a menos que se cancele la herencia.
   * Asegúrese también de que puede restablecer la herencia. Esto se controla haciendo clic en los vínculos de cadena/cadena rota que alternan para indicar el estado de la conexión.

La propiedad dialog controla si una propiedad de página está sujeta a despliegue y, por lo tanto, a cancelación o restablecimiento de la herencia al editar:

* `cq-msm-lockable`

   * Esto creará el símbolo de vínculo de cadena en el cuadro de diálogo.
   * Esto solo permite editar si se cancela la herencia (el vínculo de cadena está roto).
   * Esto solo se aplica al primer nivel secundario del recurso
      * **Tipo**: `String`
      * **Valor**: Contiene el nombre de la propiedad considerada y es comparable al valor de la propiedad `name`
         * Por ejemplo, consulte
           `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

Cuándo `cq-msm-lockable` se ha definido, romper/cerrar la cadena interactuará con MSM de la siguiente manera:

* Si el valor de `cq-msm-lockable` es:

   * **Relativo** (por ejemplo, `myProperty` o `./myProperty`)

      * Romper la cadena añadirá y quitará la propiedad de `cq:propertyInheritanceCancelled`.

   * **Absoluto** (por ejemplo, `/image`)

      * Si se interrumpe la cadena, se cancelará la herencia añadiendo `cq:LiveSyncCancelled` mixin a `./image` y configuración `cq:isCancelledForChildren` hasta `true`.

      * Al cerrar la cadena, se revertirá la herencia.

>[!NOTE]
>
>`cq-msm-lockable` se aplica al primer nivel secundario del recurso que se va a editar y no funciona en ningún antecesor de nivel más profundo, independientemente de si el valor se define como absoluto o relativo.

>[!NOTE]
>
>Al volver a habilitar la herencia, la propiedad de página Live Copy no se sincroniza automáticamente con la propiedad de origen. Puede solicitar manualmente una sincronización si es necesario.
