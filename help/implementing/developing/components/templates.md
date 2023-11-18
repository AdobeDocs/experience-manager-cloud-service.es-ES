---
title: Plantillas de página
description: Las plantillas de página se utilizan para crear una página que se utiliza como base para la nueva página
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '3279'
ht-degree: 8%

---

# Plantillas de página {#page-templates}

Al crear una página, debe seleccionar una plantilla. La plantilla de página se utiliza como base para la nueva página. La plantilla define la estructura de la página resultante, cualquier contenido inicial y los componentes que se pueden utilizar (propiedades de diseño). Esto tiene varias ventajas:

* Las plantillas de página permiten a los autores especializados [crear y editar plantillas](/help/sites-cloud/authoring/features/templates.md).
   * Estos autores especializados se denominan **autores de plantillas**
   * Los autores de plantillas deben ser miembros de `template-authors` grupo.
* Las plantillas de página conservan una conexión dinámica con cualquier página creada a partir de ellas. Esto garantiza que cualquier cambio en la plantilla se refleje en las propias páginas.
* Las plantillas de página hacen que el componente de página sea más genérico, por lo que el componente de página principal se puede utilizar sin personalización.

Con las plantillas de página, las partes que componen una página están aisladas dentro de los componentes. Puede configurar las combinaciones necesarias de componentes en una interfaz de usuario, lo que elimina la necesidad de desarrollar un nuevo componente de página para cada variación de página.

Este documento:

* Ofrece información general sobre la creación de una plantilla de página
* Describe las tareas de administrador/desarrollador necesarias para crear plantillas editables
* Describe los fundamentos técnicos de las plantillas editables
* AEM Describe cómo evalúa la disponibilidad de una plantilla de manera

>[!NOTE]
>
>Este documento supone que ya está familiarizado con la creación y edición de plantillas. Consulte el documento de creación [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md), que detalla las capacidades de las plantillas editables tal como se exponen al autor de la plantilla.

>[!TIP]
>
>[El tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) profundiza en cómo utilizar las plantillas de página implementando un ejemplo y resulta bastante útil para comprender cómo configurar una plantilla en un nuevo proyecto

## Creación de una nueva plantilla {#creating-a-new-template}

La creación de plantillas de página se realiza principalmente con [consola de plantillas y editor de plantillas](/help/sites-cloud/authoring/features/templates.md) por un autor de plantillas. En esta sección se ofrece una descripción general de este proceso y se incluye una descripción de lo que sucede a nivel técnico.

Al crear una plantilla editable, debe hacer lo siguiente:

1. Crear un [carpeta para las plantillas](#template-folders). Esto no es obligatorio, pero es una práctica recomendada.
1. Seleccione una [tipo de plantilla](#template-type). Esto se copia para crear el [definición de plantilla](#template-definitions).

   >[!NOTE]
   >
   >Se proporciona una selección de tipos de plantillas listas para usarse. También puede [crear sus propios tipos de plantillas específicas del sitio](#creating-template-types) si es necesario.

1. Configure la estructura, las políticas de contenido, el contenido inicial y el diseño de la nueva plantilla.

   **Estructura**

   * La estructura permite definir componentes y contenido para la plantilla.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminar de ninguna página resultante.
   * Si desea que los autores de páginas puedan añadir y quitar componentes, agregue un sistema de párrafos a la plantilla.
   * Los componentes pueden volver a desbloquearse y bloquearse para que pueda definir el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de la estructura, consulte [Estructura](#structure) en este documento.

   **Políticas**

   * Las políticas de contenido definen las propiedades de diseño de un componente.

      * Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas.

   * Se aplican a la plantilla (y a las páginas creadas con la plantilla).

   Para obtener más información sobre cómo define las directivas un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de las directivas, consulte [Políticas de contenido](#content-policies) en este documento.

   **Contenido inicial**

   * El contenido inicial define el contenido que aparecerá cuando se cree una página por primera vez en función de la plantilla.
   * Los autores de la página pueden editar el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   Para obtener detalles técnicos sobre el contenido inicial, consulte [Contenido inicial](#initial-content) en este documento.

   **Diseño**

   * Puede definir el diseño de la plantilla para una amplia gama de dispositivos.
   * El diseño interactivo para las plantillas funciona tal como lo hace para la creación de páginas.

   Para obtener más información sobre cómo define el diseño de la plantilla un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   Para obtener más información técnica sobre el diseño de la plantilla, consulte [Diseño](#layout) en este documento.

1. Habilite la plantilla y déjela para árboles de contenido específicos.

   * Una plantilla se puede habilitar o deshabilitar para que esté disponible o no disponible para los autores de páginas.
   * Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

   Para obtener más información sobre cómo un autor de plantillas habilita una plantilla, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   Para obtener detalles técnicos sobre la activación de una plantilla, consulte [Activación y autorización de una plantilla](#enabling-and-allowing-a-template-for-use)e en este documento

1. Úselo para crear páginas de contenido.

   * Cuando se utiliza una plantilla para crear una página, no hay ninguna diferencia visible ni indicación entre las plantillas estáticas y editables.
   * Para el autor de la página, el proceso es transparente.

   Para obtener más información sobre cómo un autor de páginas utiliza plantillas para crear una página, consulte [Crear y organizar páginas](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Para obtener más información técnica sobre la creación de páginas con plantillas editables, consulte [Páginas de contenido resultantes](#resultant-content-pages) en este documento.

>[!TIP]
>
>Nunca introduzca en una plantilla información que deba internacionalizarse. Para fines de internalización, la variable [Funciones de localización de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=es) se recomiendan.

>[!NOTE]
>
>Las plantillas son herramientas útiles para optimizar el flujo de trabajo de creación de páginas. Sin embargo, demasiadas plantillas pueden saturar a los autores y hacer que la creación de páginas sea confusa. Una buena regla general es mantener el número de plantillas por debajo de 100.
>
>Adobe no recomienda tener más de 1000 plantillas debido a posibles impactos en el rendimiento.

>[!NOTE]
>
>La biblioteca de cliente del editor supone la presencia de `cq.shared` en las páginas de contenido y, si no hay ningún error de JavaScript, `Uncaught TypeError: Cannot read property 'shared' of undefined` resultará.
>
>Todas las páginas de contenido de muestra contienen `cq.shared`, de modo que cualquier contenido basado en ellos incluye automáticamente `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de ejemplo, debe asegurarse de incluir la variable `cq.shared` namespace.
>
>Consulte [Uso de bibliotecas del lado del cliente](/help/implementing/developing/introduction/clientlibs.md) para obtener más información.



## Carpetas de plantilla {#template-folders}

Para organizar las plantillas, puede utilizar las siguientes carpetas:

* `global`
* Específico del sitio

>[!NOTE]
>
>Aunque puede anidar las carpetas, cuando el usuario las vea en la **Plantillas** consola se presentan como una estructura plana.

En una instancia estándar de AEM, la carpeta `global` ya existe en la consola de plantillas. Contiene plantillas predeterminadas y actúa como alternativa en caso de que no se encuentre ninguna política ni ningún tipo de plantilla en la carpeta actual. Puede agregar las plantillas predeterminadas a esta carpeta o crear una carpeta (recomendado).

>[!NOTE]
>
>Se recomienda crear una carpeta para guardar las plantillas personalizadas y no utilizar el `global` carpeta.

>[!CAUTION]
>
>Las carpetas debe crearlas un usuario con `admin` derechos.

Los tipos de plantilla y las directivas se heredan en todas las carpetas según el siguiente orden de prioridad:

1. La carpeta actual
1. Página principal de la carpeta actual
1. `/conf/global`
1. `/apps`
1. `/libs`

Se crea una lista de todas las entradas permitidas. Si alguna configuración se superpone ( `path`/ `label`), solo se presenta al usuario la instancia más cercana a la carpeta actual.

Para crear una carpeta, puede hacer lo siguiente:

* Mediante programación o con el CRXDE Lite
* Uso del [Explorador de configuración](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## Uso del CRXDE Lite {#using-crxde-lite}

1. Se puede crear una nueva carpeta (en /conf) para su instancia mediante programación o con el CRXDE Lite.

   Se debe utilizar la siguiente estructura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. A continuación, puede definir las siguientes propiedades en el nodo raíz de la carpeta:

   `<your-folder-name> [sling:Folder]`

   * Nombre: `jcr:title`
   * Tipo: `String`
   * Valor: el título (de la carpeta) que desea que aparezca en la **Plantillas** consola.

1. Además de los permisos y privilegios estándar de creación (por ejemplo, `content-authors`Ahora debe asignar grupos y definir los derechos de acceso (ACL) necesarios para que los autores puedan crear plantillas en la nueva carpeta.

   El `template-authors` group es el grupo predeterminado que se debe asignar. Consulte la sección [ACL y grupos](#acls-and-groups) para obtener más información.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Uso del explorador de configuración {#using-the-configuration-browser}

1. Ir a **Navegación global** > **Herramientas** > [**Explorador de configuración**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

   Las carpetas existentes se muestran a la izquierda, incluida la `global` carpeta.

1. Haga clic en **Crear**.
1. En el **Crear configuración** diálogo se deben configurar los siguientes campos:

   * **Título**: proporcione un título para la carpeta de configuración
   * **Plantillas editables**: Marque para permitir plantillas editables dentro de esta carpeta

1. Haga clic en **Crear**

>[!NOTE]
>
>En el [Explorador de configuración,](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) puede editar la carpeta global y activar el **Plantillas editables** si desea crear plantillas dentro de esta carpeta, sin embargo, esta no es la práctica recomendada.

### ACL y grupos {#acls-and-groups}

Una vez creadas las carpetas de plantilla (ya sea mediante CRXDE o con el Explorador de configuración), se deben definir ACL para los grupos adecuados para las carpetas de plantilla para garantizar la seguridad adecuada.

Las carpetas de plantilla para la [Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) se puede utilizar como ejemplo.

#### El grupo de autores de plantillas {#the-template-authors-group}

El `template-authors` AEM group es el grupo que se utiliza para administrar el acceso a las plantillas y viene de serie con la opción de acceso a las plantillas, pero está vacío. Los usuarios deben agregarse al grupo para el proyecto o sitio.

>[!CAUTION]
>
>El `template-authors` El grupo solo es para usuarios que deben poder crear nuevas plantillas.
>
>La edición de plantillas es muy potente y, si no se realiza correctamente, las plantillas existentes pueden romperse. Por lo tanto, esta función debe centrarse y solo incluir usuarios cualificados.

La siguiente tabla detalla los permisos necesarios para editar plantillas.

<table>
 <tbody>
  <tr>
   <th>Ruta</th>
   <th>Rol/grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Template Autores<br /> </td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en sitios específicos <code>/conf</code> espacio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
   <td>El usuario web anónimo debe leer las plantillas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>replicateLos autores de contenido deben activar las plantillas de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en sitios específicos <code>/conf</code> espacio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
   <td>El usuario web anónimo debe leer las directivas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los autores de contenido deben activar las políticas de una plantilla de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autor de plantillas</td>
   <td>leer</td>
   <td>El autor de la plantilla crea una nueva plantilla basada en uno de los tipos de plantilla predefinidos.</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

Este valor predeterminado `template-authors` grupo solo abarca las configuraciones de proyecto, donde todas las `template-authors` los miembros pueden acceder a todas las plantillas y crearlas. Para configuraciones más complejas, donde se necesitan varios grupos de autores de plantillas para separar el acceso a las plantillas, se deben crear grupos de autores de plantillas más personalizados. Sin embargo, los permisos para los grupos de autores de plantillas seguirían siendo los mismos.

## Tipo de plantilla {#template-type}

Al crear una plantilla, debe especificar un tipo de plantilla:

* Los tipos de plantilla proporcionan plantillas para una plantilla de forma eficaz. Al crear una plantilla, se utiliza la estructura y el contenido inicial del tipo de plantilla seleccionado para crear la nueva plantilla.

   * El tipo de plantilla se copia para crearla.
   * Una vez realizada la copia, la única conexión entre la plantilla y el tipo de plantilla es una referencia estática con fines informativos.

* Los tipos de plantilla permiten definir lo siguiente:

   * El tipo de recurso del componente de página.
   * La directiva del nodo raíz, que define los componentes permitidos en el editor de plantillas.
   * Se recomienda definir los puntos de interrupción para la cuadrícula adaptable y la configuración del emulador móvil en en el tipo de plantilla.

* AEM proporciona una pequeña selección de tipos de plantillas listas para usar, como Página de HTML5 y Página de formulario adaptable.

   * Se proporcionan ejemplos adicionales como parte de la variable [Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* Los desarrolladores suelen definir los tipos de plantillas.

Los tipos de plantilla predeterminados se almacenan en:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>No debe cambiar nada en el `/libs` ruta. Esto se debe al contenido de `/libs` AEM se puede sobrescribir en cualquier momento mediante una actualización de la dirección de correo electrónico de.

Los tipos de plantilla específicos del sitio deben almacenarse en la ubicación comparable de:

* `/apps/settings/wcm/template-types`

Las definiciones de los tipos de plantillas personalizadas deben almacenarse en carpetas definidas por el usuario (recomendado) o, alternativamente, en `global`. Por ejemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Los tipos de plantilla deben respetar la estructura de carpetas correcta (es decir, `/settings/wcm/...`); de lo contrario, no se encontrarán los tipos de plantilla.

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating an editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### Creación de tipos de plantilla {#creating-template-types}

Si ha creado una plantilla que puede servir de base a otras plantillas, puede copiar esta plantilla como un tipo de plantilla.

1. Cree una plantilla como lo haría con cualquier plantilla de página [como se documenta aquí](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), que servirá de base para el tipo de plantilla.
1. Con el CRXDE Lite, copie la plantilla recién creada desde el `templates` nodo a `template-types` nodo bajo el [carpeta de plantillas](#template-folders).
1. Elimine la plantilla del `templates` nodo bajo el [carpeta de plantillas](#template-folders).
1. En la copia de la plantilla que se encuentra debajo de `template-types` nodo, eliminar todo `cq:template` y `cq:templateType` propiedades de todos `jcr:content` nodos.

También puede desarrollar su propio tipo de plantilla con una plantilla editable de ejemplo como base, disponible en GitHub.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-sites-example-custom-template-type en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definiciones de plantilla {#template-definitions}

Se almacenan las definiciones de las plantillas editables [carpetas definidas por el usuario](#template-folders) (recomendado) o alternativamente en `global`. Por ejemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

El nodo raíz de la plantilla es del tipo `cq:Template` con una estructura esquemática de:

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Los elementos principales son:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:contenido {#jcr-content}

Este nodo contiene propiedades para la plantilla:

* **Nombre**: `jcr:title`
* **Nombre**: `status`
   * ``**Tipo**: `String`
   * **Valor**: `draft`, `enabled` o `disabled`

### Estructura {#structure}

Define la estructura de la página resultante:

* Se combina con el contenido inicial ( `/initial`) al crear una página.
* Los cambios realizados en la estructura se reflejan en cualquier página creada con la plantilla.
* El `root` ( `structure/jcr:content/root`) define la lista de componentes disponibles en la página resultante.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover ni eliminar de ninguna página resultante.
   * Después de desbloquear un componente, `editable` La propiedad se establece en `true`.
   * Después de desbloquear un componente que ya contiene contenido, este se mueve a `initial` Rama.

* El `cq:responsive` El nodo contiene definiciones para el diseño interactivo.

### Contenido inicial {#initial-content}

Define el contenido inicial que tendrá una nueva página al crearla:

* Contiene un `jcr:content` que se copia en cualquier página nueva.
* Se combina con la estructura ( `/structure`) al crear una página.
* Las páginas existentes no se actualizarán si el contenido inicial cambia después de la creación.
* El `root` El nodo contiene una lista de componentes para definir qué está disponible en la página resultante.
* Si el contenido se añade a un componente en modo de estructura y dicho componente se desbloquea posteriormente (o viceversa), este contenido se utiliza como contenido inicial.

### Diseño {#layout}

Cuándo [edición de una plantilla puede definir el diseño](/help/sites-cloud/authoring/features/templates.md), esto utiliza [diseño interactivo estándar](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Políticas de contenido {#content-policies}

Las políticas de contenido definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Se aplican a la plantilla (y a las páginas creadas con la plantilla). Las políticas de contenido se pueden crear y seleccionar en el editor de plantillas.

* La propiedad `cq:policy`, en el `root` nodo
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Proporciona una referencia relativa a la directiva de contenido para el sistema de párrafos de la página.

* La propiedad `cq:policy`, en los nodos explícitos de componente en `root`, proporcione vínculos a las directivas para los componentes individuales.

* Las definiciones de directivas reales se almacenan en:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Las rutas de las definiciones de directivas dependen de la ruta del componente. `cq:policy` contiene una referencia relativa a la propia configuración.

### Políticas de la página {#page-policies}

Las políticas de página permiten definir la variable [política de contenido](#content-policies) para la página (parsys principal), en la plantilla o en las páginas resultantes.

### Habilitar y permitir el uso de una plantilla {#enabling-and-allowing-a-template-for-use}

1. **Habilitar la plantilla**

   Para poder utilizar una plantilla, debe habilitarse mediante lo siguiente:

   * [Activación de la plantilla](/help/sites-cloud/authoring/features/templates.md) desde el **Plantillas** consola.

   * Estableciendo la propiedad status en `jcr:content` nodo.

      * Por ejemplo, en:
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina la propiedad:

         * Nombre: estado
         * Tipo: cadena
         * Valor: `enabled`

1. **Plantillas permitidas**

   * [Defina las rutas de plantilla permitidas en la variable **Propiedades de página**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) de la página adecuada o de la página raíz de una subrama.
   * Establezca la propiedad:
     `cq:allowedTemplates`
En el `jcr:content` de la rama requerida.

   Por ejemplo, con un valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de contenido resultantes {#resultant-content-pages}

Páginas creadas a partir de plantillas editables:

* Se crean con un subárbol que se combina con `structure` y `initial` en la plantilla

* Tener referencias a información contenida en la plantilla y el tipo de plantilla. Esto se logra con una `jcr:content` nodo con las propiedades:

   * `cq:template` : Proporciona la referencia dinámica a la plantilla real; permite que los cambios realizados en la plantilla se reflejen en las páginas reales.

   * `cq:templateType` : Proporciona una referencia al tipo de plantilla.

![Interrelación entre plantillas, contenido y componentes](assets/templates-content-components.png)

El diagrama anterior muestra cómo se interrelacionan las plantillas, el contenido y los componentes:

* Controlador - `/content/<my-site>/<my-page>` : La página resultante que hace referencia a la plantilla. El contenido controla todo el proceso. Según las definiciones, accede a la plantilla y a los componentes adecuados.
* Configuración - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - El [plantilla y políticas de contenido relacionadas](#template-definitions) defina la configuración de página.
* Modelo - Paquetes OSGi - El [Paquetes OSGI](/help/implementing/deploying/configuring-osgi.md) implemente la funcionalidad.
* Ver - `/apps/<my-site>/components` : Tanto en el entorno de creación como en el de publicación, el contenido se procesa mediante componentes.

Al procesar una página:

* **Plantillas**:

   * El `cq:template` propiedad de su `jcr:content` se hace referencia al nodo para acceder a la plantilla que corresponde a esa página.

* **Componentes**:

   * El componente de página combinará las variables `structure/jcr:content` árbol de la plantilla con el `jcr:content` árbol de la página.
      * El componente de página solo permitirá al autor editar los nodos de la estructura de la plantilla que se han marcado como editables (y los secundarios).
      * Al procesar un componente en una página, la ruta relativa de ese componente se toma del `jcr:content` nodo; la misma ruta bajo el `policies/jcr:content` A continuación, se buscará en el nodo de la plantilla.
         * El `cq:policy` La propiedad de este nodo señala a la directiva de contenido real (es decir, contiene la configuración de diseño para ese componente).
            * Esto permite tener varias plantillas que reutilizan las mismas configuraciones de directiva de contenido.

### Disponibilidad de la plantilla {#template-availability}

Al crear una página en la interfaz de administración del sitio, la lista de plantillas disponibles depende de la ubicación de la nueva página y de las restricciones de colocación especificadas en cada plantilla.

Las siguientes propiedades determinan si una plantilla `T` se puede usar para que una nueva página se coloque como elemento secundario de la página `P`. Cada una de estas propiedades es una cadena de varios valores que contiene cero o más expresiones regulares que se utilizan para la coincidencia con rutas:

* El `cq:allowedTemplates` propiedad del `jcr:content` subnodo de `P` o un antecesor de `P`.

* El `allowedPaths` propiedad de `T`.

* El `allowedParents` propiedad de `T`.

* El `allowedChildren` propiedad de la plantilla de `P`.

La evaluación funciona de la siguiente manera:

* La primera no vacía `cq:allowedTemplates` se encontró la propiedad al ascender la jerarquía de páginas que empieza por `P` se compara con la ruta de `T`. Si ninguno de los valores coincide, `T` se ha rechazado.

* If `T` tiene un no vacío `allowedPaths` , pero ninguno de los valores coincide con la ruta de `P`, `T` se ha rechazado.

* Si ambas propiedades anteriores están vacías o no existen, `T` se rechaza a menos que pertenezca a la misma aplicación que `P`. `T` pertenece a la misma aplicación que `P` if y only si el nombre del segundo nivel de la ruta de `T` es el mismo que el nombre del segundo nivel de la ruta de `P`. Por ejemplo, la plantilla `/apps/wknd/templates/foo` pertenece a la misma aplicación que la página `/content/wknd`.

* If `T` tiene un no vacío `allowedParents` , pero ninguno de los valores coincide con la ruta de `P`, `T` se ha rechazado.

* Si la plantilla de `P` tiene un no vacío `allowedChildren` , pero ninguno de los valores coincide con la ruta de `T`, `T` se ha rechazado.

* En todos los demás casos, `T` está permitido.

El diagrama siguiente muestra el proceso de evaluación de la plantilla:

![Proceso de evaluación de plantilla](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM ofrece varias propiedades para controlar las plantillas permitidas en **Sites**. Sin embargo, combinarlas puede dar lugar a reglas muy complejas difíciles de rastrear y administrar.
>
>Por lo tanto, Adobe recomienda empezar de forma sencilla definiendo:
>
>* solo el `cq:allowedTemplates` propiedad
>
>* solo en la raíz del sitio
>
>Para ver un ejemplo, consulte la [Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) contenido: `/content/wknd/jcr:content`
>
>Las propiedades `allowedPaths`, `allowedParents`, y `allowedChildren` también se puede colocar en las plantillas para definir reglas más sofisticadas. Sin embargo, cuando es posible, lo es *mucho* más fácil de definir `cq:allowedTemplates` propiedades en las subsecciones del sitio si es necesario restringir aún más las plantillas permitidas.
>
>Una ventaja adicional es que el `cq:allowedTemplates` Las propiedades puede actualizarlas un autor en el **Avanzadas** de la pestaña **Propiedades de página**. Las demás propiedades de la plantilla no se pueden actualizar mediante la interfaz de usuario (estándar), por lo que se necesitaría un desarrollador para mantener las reglas y una implementación de código para cada cambio.

#### Limitación de plantillas utilizadas en páginas secundarias {#limiting-templates-used-in-child-pages}

Para limitar qué plantillas se pueden utilizar para crear páginas secundarias en una página determinada, utilice la variable `cq:allowedTemplates` propiedad de `jcr:content` de la página para especificar la lista de plantillas que pueden utilizarse como páginas secundarias. Cada valor de la lista debe ser una ruta absoluta a una plantilla para una página secundaria permitida, por ejemplo `/apps/wknd/templates/page-content`.

Puede usar el complemento `cq:allowedTemplates` propiedad en la plantilla  `jcr:content` para que esta configuración se aplique a todas las páginas recién creadas que utilicen esta plantilla.

Si desea agregar más restricciones, por ejemplo con respecto a la jerarquía de plantillas, puede utilizar la variable `allowedParents/allowedChildren` propiedades en la plantilla. A continuación, puede especificar explícitamente que las páginas creadas a partir de una plantilla T tengan que ser páginas principales o secundarias de páginas creadas a partir de una plantilla T.
