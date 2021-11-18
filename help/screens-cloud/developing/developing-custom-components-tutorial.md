---
title: Desarrollo de un componente personalizado para pantallas as a Cloud Service
description: El siguiente tutorial recorre los pasos para crear un componente personalizado para AEM Screens. AEM Screens reutiliza muchos patrones de diseño y tecnologías existentes de otros productos AEM. El tutorial resalta las diferencias y las consideraciones especiales al desarrollar para AEM Screens.
source-git-commit: 0ca86e127569e8f6eb92654e4224a4d5da72ebf4
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 2%

---


# Desarrollo de un componente personalizado para AEM Screens as a Cloud Service{#developing-a-custom-component-for-aem-screens}

El siguiente tutorial recorre los pasos para crear un componente personalizado para AEM Screens. AEM Screens reutiliza muchos patrones de diseño y tecnologías existentes de otros productos AEM. El tutorial resalta las diferencias y las consideraciones especiales al desarrollar para AEM Screens.

## Información general {#overview}

Este tutorial está diseñado para desarrolladores que utilicen AEM Screens por primera vez. En este tutorial, se ha creado un componente &quot;Hello World&quot; sencillo para un canal de secuencia en AEM Screens. Un cuadro de diálogo permite a los autores actualizar el texto mostrado.


## Requisitos previos {#prerequisites}

Para completar este tutorial, es necesario lo siguiente:

1. Último paquete de funciones de Screens

1. Reproductor de AEM Screens

1. Entorno de desarrollo local

Los pasos del tutorial y las capturas de pantalla se realizan mediante **CRXDE-Lite**. También se pueden utilizar IDE para completar el tutorial. Más información sobre el uso de un IDE para desarrollar [con AEM se puede encontrar aquí.](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html#eclipse-ide)


## Configuración del proyecto {#project-setup}

El código fuente de un proyecto de Screens se administra normalmente como un proyecto Maven de varios módulos. Para acelerar el tutorial, se generó un proyecto previamente utilizando la variable [AEM tipo de archivo del proyecto 13](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype). Más detalles sobre [crear un proyecto con el tipo de archivo del proyecto Maven AEM se puede encontrar aquí](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html#maven-multimodule).

1. Descargue e instale los siguientes paquetes utilizando [Administrador de paquetes CRX](http://localhost:4502/crx/packmgr/index.jsp):

[Obtener archivo](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)

   [Obtener archivo](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)
   **Opcionalmente** si trabaja con Eclipse u otro IDE, descargue el siguiente paquete fuente. Implemente el proyecto en una instancia de AEM local mediante el comando Maven:

   **`mvn -PautoInstallPackage clean install`**

   Inicio de HelloWorld SRC Screens de We.Retail Run Project

[Obtener archivo](/help/screens-cloud/developing/assets/src-screens-weretail-run.zip)

1. En [Administrador de paquetes CRX](http://localhost:4502/crx/packmgr/index.jsp) compruebe que están instalados los dos paquetes siguientes:

   1. **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**
   1. **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**

   ![Screens Los paquetes de We.Retail Run Ui.Apps y Ui.Content instalados a través del administrador de paquetes CRX](assets/crx-packages.png)

   Screens Los paquetes de We.Retail Run Ui.Apps y Ui.Content instalados a través del administrador de paquetes CRX

1. La variable **screens-weretail-run.ui.apps** el paquete instala código debajo de `/apps/weretail-run`.

   Este paquete contiene el código responsable de procesar los componentes personalizados del proyecto. Este paquete incluye código de componente y cualquier JavaScript o CSS que se necesite. Este paquete también incrusta **screens-weretail-run.core-0.0.1-SNAPSHOT.jar** que contiene cualquier código Java que necesite el proyecto.

   >[!NOTE]
   >
   >En este tutorial no se escribe ningún código Java. Si se necesita una lógica empresarial más compleja, se puede crear e implementar Java back-end mediante el paquete Core Java.

   ![Representación del código ui.apps en el CRXDE Lite](/help/screens-cloud/developing/assets/uipps-contents.png)

   Representación del código ui.apps en el CRXDE Lite

   La variable **helloworld** actualmente es solo un marcador de posición. Durante el tutorial, se añadirá una funcionalidad que permitirá a un autor actualizar el mensaje que muestra el componente.

1. La variable **screens-weretail-run.ui.content** instala el código debajo de:

   * `/conf/we-retail-run`
   * `/content/dam/we-retail-run`
   * `/content/screens/we-retail-run`

   Este paquete contiene el contenido inicial y la estructura de configuración necesaria para el proyecto. **`/conf/we-retail-run`** contiene todas las configuraciones para el proyecto de ejecución de We.Retail. **`/content/dam/we-retail-run`** incluye el inicio de recursos digitales para el proyecto. **`/content/screens/we-retail-run`** contiene la estructura de contenido de Screens. El contenido debajo de todas estas rutas se actualiza principalmente en AEM. Para promover la coherencia entre entornos (local, Dev, Stage, Prod), a menudo se guarda una estructura de contenido base en el control de código fuente.

1. **Vaya al proyecto AEM Screens > Ejecución de We.Retail :**

   En el menú Inicio de AEM > Haga clic en el icono Screens . Compruebe que se pueda ver el proyecto de ejecución de We.Retail.

   ![we-retaiul-run-starter](/help/screens-cloud/developing/assets/we-retaiul-run-starter.png)

## Crear el componente Hello World {#hello-world-cmp}

El componente Hello World es un componente sencillo que permite al usuario introducir un mensaje para que se muestre en la pantalla. El componente se basa en la variable [Plantilla de componente de AEM Screens: https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template).

AEM Screens tiene algunas restricciones interesantes que no son necesariamente ciertas para los componentes tradicionales de WCM Sites.

* La mayoría de los componentes de Screens necesitan ejecutarse en pantalla completa en los dispositivos de señalización digital de destino
* La mayoría de los componentes de Screens deben incrustarse en los canales de secuencia para generar diapositivas
* La creación debería permitir la edición de componentes individuales en un canal de secuencia, por lo que su representación a pantalla completa no está en duda

1. En **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp` (o IDE de su elección) navegue hasta `/apps/weretail-run/components/content/helloworld.`

   Agregue las siguientes propiedades al `helloworld` componente:

   ```
       jcr:title="Hello World"
       sling:resourceSuperType="foundation/components/parbase"
       componentGroup="We.Retail Run - Content"
   ```

   ![Propiedades para /apps/weretail-run/components/content/helloworld](/help/screens-cloud/developing/assets/2018-04-28_at_4_23pm.png)

   Propiedades para /apps/weretail-run/components/content/helloworld

   La variable **helloworld** amplía el **foundation/components/parbase** para que se pueda utilizar correctamente dentro de un canal de secuencia.

1. Cree un archivo debajo de `/apps/weretail-run/components/content/helloworld` named `helloworld.html.`

   Rellene el archivo con lo siguiente:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/helloworld.html
   
   */-->
   
   <!--/* production: preview authoring mode + unspecified mode (i.e. on publish) */-->
   <sly data-sly-test.production="${wcmmode.preview || wcmmode.disabled}" data-sly-include="production.html" />
   
   <!--/* edit: any other authoring mode, i.e. edit, design, scaffolding, etc. */-->
   <sly data-sly-test="${!production}" data-sly-include="edit.html" />
   ```

   Los componentes de Screens requieren dos renderizaciones diferentes en función de las cuales [modo de creación](https://helpx.adobe.com/experience-manager/6-4/sites/authoring/using/author-environment-tools.html#PageModes) se está utilizando:

   1. **Producción**: Modo de vista previa o publicación (wcmmode=disabled)
   1. **Editar**: se utiliza para todos los demás modos de creación, es decir, edición, diseño, andamiaje, desarrollador...

   `helloworld.html`actúa como conmutador, comprobando qué modo de creación está activo actualmente y redirigiéndose a otro script HTL. Una convención común que utilizan los componentes de pantalla es tener una `edit.html` secuencia de comandos para el modo de edición y `production.html` secuencia de comandos para el modo Producción.

1. Cree un archivo debajo de `/apps/weretail-run/components/content/helloworld` named `production.html.`

   Rellene el archivo con lo siguiente:

   ```xml
   <!--/*
    /apps/weretail-run/components/content/helloworld/production.html
   
   */-->
   
   <div data-duration="${properties.duration}" class="cmp-hello-world">
    <h1 class="cmp-hello-world__message">${properties.message}</h1>
   </div>
   ```

   Arriba está el marcado de producción para el componente Hello World. A `data-duration` se incluye ya que el componente se utiliza en un canal de secuencia. La variable `data-duration` el canal de secuencia utiliza el atributo para saber durante cuánto tiempo se va a mostrar un elemento de secuencia.

   El componente procesa un `div` y `h1` etiqueta con texto. `${properties.message}` es una parte del script HTL que mostrará el contenido de una propiedad JCR denominada `message`. Posteriormente se crea un cuadro de diálogo que permite al usuario introducir un valor para la variable `message` texto de propiedad.

   Tenga en cuenta también que la notación BEM (Modificador de elemento de bloque) se utiliza con el componente. BEM es una convención de codificación CSS que facilita la creación de componentes reutilizables. BEM es la notación utilizada por [Componentes principales AEM](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/wiki/CSS-coding-conventions). Puede encontrar más información en: [https://getbem.com/](https://getbem.com/)

1. Cree un archivo debajo de `/apps/weretail-run/components/content/helloworld` named `edit.html.`

   Rellene el archivo con lo siguiente:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/edit.html
   
   */-->
   
   <!--/* if message populated */-->
   <div
    data-sly-test.message="${properties.message}"
    class="aem-Screens-editWrapper cmp-hello-world">
    <p class="cmp-hello-world__message">${message}</p>
   </div>
   
   <!--/* empty place holder */-->
   <div data-sly-test="${!message}"
        class="aem-Screens-editWrapper cq-placeholder cmp-hello-world"
        data-emptytext="${'Hello World' @ i18n, locale=request.locale}">
   </div>
   ```

   Arriba está el marcado de edición para el componente Hola a todos. El primer bloque muestra una versión de edición del componente si se ha rellenado el mensaje de diálogo.

   El segundo bloque se representa si no se ha introducido ningún mensaje de diálogo. La variable `cq-placeholder` y `data-emptytext` procesar la etiqueta ***Hello World*** como titular de lugar en ese caso. La cadena de la etiqueta se puede internacionalizar con i18n para admitir la creación en varias configuraciones regionales.

1. **Copie el cuadro de diálogo Imagen de Screens para utilizarlo para el componente Hola a todos.**

   Es más fácil empezar desde un cuadro de diálogo existente y luego realizar modificaciones.

   1. Copie el cuadro de diálogo desde: `/libs/screens/core/components/content/image/cq:dialog`
   1. Pegue el cuadro de diálogo debajo de `/apps/weretail-run/components/content/helloworld`

   ![copy-image-dialog](/help/screens-cloud/developing/assets/copy-image-dialog.gif)

1. **Actualice el cuadro de diálogo Hola mundo para incluir una pestaña para el mensaje.**

   Actualice el cuadro de diálogo para que coincida con lo siguiente. La estructura del nodo JCR del cuadro de diálogo final se presenta a continuación en XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
       jcr:primaryType="nt:unstructured"
       jcr:title="Hello World"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content
           jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/coral/foundation/tabs"
           size="L">
           <items jcr:primaryType="nt:unstructured">
               <message
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Message"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <message
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                   fieldDescription="Message for component to display"
                                   fieldLabel="Message"
                                   name="./message"/>
                           </items>
                       </column>
                   </items>
               </message>
               <sequence
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Sequence"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <duration
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield"
                                   defaultValue=""
                                   fieldDescription="Amount of time the image will be shown in the sequence, in milliseconds"
                                   fieldLabel="Duration (ms)"
                                   min="0"
                                   name="./duration"/>
                           </items>
                       </column>
                   </items>
               </sequence>
           </items>
       </content>
   </jcr:root>
   ```

   El campo de texto del mensaje se guarda en una propiedad denominada `message` y que el campo numérico de Duración se guardará en una propiedad denominada `duration`. Se hace referencia a estas dos propiedades en `/apps/weretail-run/components/content/helloworld/production.html` por HTL como `${properties.message}` y `${properties.duration}`.

   ![Hello World: cuadro de diálogo completado](/help/screens-cloud/developing/assets/2018-04-29_at_5_21pm.png)

   Hello World: cuadro de diálogo completado

## Creación de bibliotecas del lado del cliente {#clientlibs}

Las bibliotecas del lado del cliente proporcionan un mecanismo para organizar y administrar los archivos CSS y JavaScript necesarios para una implementación de AEM.

Los componentes de AEM Screens se representan de forma diferente en el modo de edición frente al modo de producción/previsualización. Se crearán dos bibliotecas de cliente, una para el modo de edición y otra para la vista previa/producción.

1. Cree una carpeta para bibliotecas del lado del cliente para el componente Hello World.

   Bajo `/apps/weretail-run/components/content/helloworld`crear una nueva carpeta con el nombre `clientlibs`.

   ![2018-04-30_at_1046am](/help/screens-cloud/developing/assets/2018-04-30_at_1046am.png)

1. Debajo de la variable `clientlibs` carpeta crear un nuevo nodo denominado `shared` de tipo `cq:ClientLibraryFolder.`

   ![2018-04-30_at_1115am](/help/screens-cloud/developing/assets/2018-04-30_at_1115am.png)

1. Agregue las siguientes propiedades a la biblioteca de cliente compartida:

   * `allowProxy` | Boolean | `true`

   * `categories`| String[] | `cq.screens.components`

   ![Propiedades para /apps/weretail-run/components/content/helloworld/clientlibs/shared](/help/screens-cloud/developing/assets/2018-05-03_at_1026pm.png)

   Propiedades para /apps/weretail-run/components/content/helloworld/clientlibs/shared

   La propiedad categories es una cadena que identifica la biblioteca del cliente. La categoría cq.screens.components se utiliza en los modos Edición y Vista previa/Producción. Por lo tanto, cualquier CSS/JS definido en la clientlib compartida se carga en todos los modos.

   Se recomienda no exponer nunca ninguna ruta directamente a /apps en un entorno de producción. La propiedad allowProxy garantiza que se haga referencia a la biblioteca de cliente CSS y JS con el prefijo of/etc.clientlibs.

1. Crear archivo con el nombre `css.txt` debajo de la carpeta compartida.

   Rellene el archivo con lo siguiente:

   ```
   #base=css
   
   styles.less
   ```

1. Crear una carpeta con el nombre `css` debajo del `shared` carpeta. Añada un archivo con el nombre `style.less` debajo del `css` carpeta. La estructura de las bibliotecas de cliente debería tener este aspecto:

   ![2018-04-30_at_3_11pm](/help/screens-cloud/developing/assets/2018-04-30_at_3_11pm.png)

   En lugar de escribir CSS directamente, este tutorial utiliza LESS. [LESS](https://lesscss.org/) es un precompilador CSS popular que admite variables, mezclas y funciones CSS. AEM bibliotecas de cliente admiten de forma nativa la compilación de LESS. Se pueden utilizar sass u otros precompiladores, pero deben compilarse fuera de AEM.

1. Rellenar `/apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less` con lo siguiente:

   ```css
   /**
       Shared Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less
   
   **/
   
   .cmp-hello-world {
       background-color: #fff;
   
    &__message {
     color: #000;
     font-family: Helvetica;
     text-align:center;
    }
   }
   ```

1. Copie y pegue el `shared` carpeta de biblioteca de cliente para crear una nueva biblioteca de cliente denominada `production`.

   ![Copiar la biblioteca de cliente compartida para crear una nueva biblioteca de cliente de producción](/help/screens-cloud/developing/assets/copy-clientlib.gif)

   Copiar la biblioteca de cliente compartida para crear una nueva biblioteca de cliente de producción

1. Actualice el `categories` propiedad de la clientlibrary de producción que se va a `cq.screens.components.production.`

   Esto garantiza que los estilos solo se carguen cuando se encuentran en el modo de vista previa/producción.

   ![Propiedades para /apps/weretail-run/components/content/helloworld/clientlibs/production](/help/screens-cloud/developing/assets/2018-04-30_at_5_04pm.png)

   Propiedades para /apps/weretail-run/components/content/helloworld/clientlibs/production

1. Rellenar `/apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less` con lo siguiente:

   ```css
   /**
       Production Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less
   
   **/
   .cmp-hello-world {
   
       height: 100%;
       width: 100%;
       position: fixed;
   
    &__message {
   
     position: relative;
     font-size: 5rem;
     top:25%;
    }
   }
   ```

   Los estilos anteriores mostrarán el mensaje centrado en el medio de la pantalla, pero solo en el modo de producción.

Una tercera categoría clientlibrary: `cq.screens.components.edit` se puede utilizar para añadir al componente estilos específicos de solo edición.

| Categoría de Clientlib | Uso |
|---|---|
| `cq.screens.components` | Estilos y secuencias de comandos que se comparten entre los modos de edición y producción |
| `cq.screens.components.edit` | Estilos y secuencias de comandos que solo se utilizan en el modo de edición |
| `cq.screens.components.production` | Estilos y secuencias de comandos que solo se utilizan en el modo de producción |

## Crear una página de diseño {#design-page}

Uso de AEM Screens [Plantillas de página estáticas](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/page-templates-static.html) y [Configuración de diseño](https://helpx.adobe.com/experience-manager/6-4/sites/authoring/using/default-components-designmode.html) para cambios globales. Las configuraciones de diseño se utilizan frecuentemente para configurar los componentes permitidos para Parsys en un canal. Una práctica recomendada es almacenar estas configuraciones de una forma específica de la aplicación.

Debajo se crea una página de diseño de ejecución de We.Retail que almacenará todas las configuraciones específicas del proyecto de ejecución de We.Retail.

1. En **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs` vaya a `/apps/settings/wcm/designs`
1. Cree un nuevo nodo debajo de la carpeta de diseños, con el nombre `we-retail-run` con un tipo de `cq:Page`.
1. Debajo de la variable `we-retail-run` página, agregue otro nodo denominado `jcr:content` de tipo `nt:unstructured`. Agregue las siguientes propiedades al `jcr:content` nodo:

   | Nombre | Tipo | Value |
   |---|---|---|
   | jcr:title | String | Ejecución de We.Retail |
   | sling:resourceType | Cadena | wcm/core/components/designer |
   | cq:doctype | Cadena | html_5 |

   ![Página de diseño en /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1219pm.png)

   Página de diseño en /apps/settings/wcm/designs/we-retail-run

## Crear un canal de secuencia {#create-sequence-channel}

El componente Hello World está diseñado para utilizarse en un canal de secuencia. Para probar el componente, se crea un nuevo canal de secuencia.

1. En el menú Inicio de AEM, vaya a **Pantallas** > **Ru de We.Retail** n > y seleccione **Canales**.

1. Haga clic en el **Crear** botón

   1. Choose **Crear entidad**

   ![2018-04-30_at_5_18pm](/help/screens-cloud/developing/assets/2018-04-30_at_5_18pm.png)

1. En el asistente Crear :

1. Paso de plantilla: elija **Canal de secuencia**

   1. Paso Propiedades
   * Ficha Básico > Título = **Canal inactivo**
   * Pestaña Canal > marcar **Hacer que el canal esté en línea**

   ![canal inactivo](/help/screens-cloud/developing/assets/idle-channel.gif)

1. Abra las propiedades de página del canal inactivo. Actualizar el campo Diseño para que apunte a `/apps/settings/wcm/designs/we-retail-run,`la página de diseño creada en la sección anterior.

   ![Configuración de diseño /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1240pm.png)

   Configuración de diseño apuntando a /apps/settings/wcm/designs/we-retail-run

1. Edite el canal inactivo recién creado para abrirlo.

1. Cambie el modo de página a **Diseño** Modo

   1. Haga clic en el **llave** Icono en Parsys para configurar los componentes permitidos

   1. Seleccione el **Pantallas** y **Ejecución de We.Retail: contenido** grupo.

   ![2018-04-30_at_5_43pm](assets/2018-04-30_at_5_43pm.png)

1. Cambie el modo de página a **Editar**. El componente Hello World ahora se puede añadir a la página y combinarse con otros componentes de canal de secuencia.

   ![2018-04-30_at_5_53pm](assets/2018-04-30_at_5_53pm.png)

1. En **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs/we-retail-run/jcr%3Acontent/sequencechannel/par` vaya a `/apps/settings/wcm/designs/we-retail-run/jcr:content/sequencechannel/par`. Observe que `components` ahora la propiedad incluye `group:Screens`, `group:We.Retail Run - Content`.

   ![Configuración de diseño en /apps/settings/wcm/designs/we-retail run](/help/screens-cloud/developing/assets/2018-05-07_at_1_14pm.png)

   Configuración de diseño en /apps/settings/wcm/designs/we-retail run

## Plantilla para controladores personalizados {#custom-handlers}

Si el componente personalizado utiliza recursos externos como recursos (imágenes, vídeos, fuentes, iconos, etc.), representaciones de recursos específicas o bibliotecas del lado del cliente (css, js, etc.), estos no se añaden automáticamente a la configuración sin conexión, ya que solo agrupamos el marcado del HTML de forma predeterminada.

Para permitirle personalizar y optimizar los recursos exactos que se descargan en el reproductor, ofrecemos un mecanismo de extensión para los componentes personalizados que expone sus dependencias a la lógica de almacenamiento en caché sin conexión en Screens.

La sección siguiente muestra la plantilla para los controladores de recursos sin conexión personalizados y los requisitos mínimos en la `pom.xml` para ese proyecto específico.

```java
package …;

import javax.annotation.Nonnull;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceUtil;
import org.apache.sling.api.resource.ValueMap;

import com.adobe.cq.screens.visitor.OfflineResourceHandler;

@Service(value = OfflineResourceHandler.class)
@Component(immediate = true)
public class MyCustomHandler extends AbstractResourceHandler {

 @Reference
 private …; // OSGi services injection

 /**
  * The resource types that are handled by the handler.
  * @return the handled resource types
  */
 @Nonnull
 @Override
 public String[] getSupportedResourceTypes() {
     return new String[] { … };
 }

 /**
  * Accept the provided resource, visit and traverse it as needed.
  * @param resource The resource to accept
  */
 @Override
 public void accept(@Nonnull Resource resource) {
     ValueMap properties = ResourceUtil.getValueMap(resource);
     
     /* You can directly add explicit paths for offline caching using the `visit`
        method of the visitor. */
     
     // retrieve a custom property from the component
     String myCustomRenditionUrl = properties.get("myCustomRenditionUrl", String.class);
     // adding that exact asset/rendition/path to the offline manifest
     this.visitor.visit(myCustomRenditionUrl);
     
     
     /* You can delegate handling for dependent resources so they are also added to
        the offline cache using the `accept` method of the visitor. */
     
     // retrieve a referenced dependent resource
     String referencedResourcePath = properties.get("myOtherResource", String.class);
     ResourceResolver resolver = resource.getResourceResolver();
     Resource referencedResource = resolver.getResource(referencedResourcePath);
     // let the handler for that resource handle it
     if (referencedResource != null) {
         this.visitor.accept(referencedResource);
     }
   }
}
```

El siguiente código proporciona los requisitos mínimos en la variable `pom.xml` para ese proyecto específico:

```css
   <dependencies>
        …
        <!-- Felix annotations -->
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.9.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- Screens core bundle with OfflineResourceHandler/AbstractResourceHandler -->
        <dependency>
            <groupId>com.adobe.cq.screens</groupId>
            <artifactId>com.adobe.cq.screens</artifactId>
            <version>1.5.90</version>
            <scope>provided</scope>
        </dependency>
        …
      </dependencies>
```

## En resumen {#putting-it-all-together}

El siguiente vídeo muestra el componente terminado y cómo se puede añadir a un canal de secuencia. A continuación, el canal se agrega a la visualización Ubicación y, finalmente, se asigna a un reproductor Screens.

>[!VIDEO](https://video.tv.adobe.com/v/22385?quaity=9)

## Código finalizado {#finished-code}

A continuación se muestra el código terminado del tutorial. La variable **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip** y **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip** son los paquetes AEM compilados. El **SRC-screens-weretail-run-0.0.1.zip **es el código fuente no compilado que se puede implementar mediante Maven.

[Obtener archivo](/help/screens-cloud/developing/assets/screens-weretail-runuiapps-001-snapshot.zip)

[Obtener archivo](/help/screens-cloud/developing/assets/screens-weretail-runuicontent-001-snapshot.zip)

[Obtener archivo](/help/screens-cloud/developing/assets/screens-weretail-run.zip)
