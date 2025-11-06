---
title: Plantillas editables
description: Obtenga información sobre cómo se utilizan las plantillas editables al crear una página, y definir su contenido inicial, contenido estructurado, políticas de creación y diseño.
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 4%

---

# Plantillas editables {#editable-templates}

Obtenga información sobre cómo se utilizan las plantillas editables al crear una página, y definir su contenido inicial, contenido estructurado, políticas de creación y diseño.

## Información general {#overview}

Al crear una página, debe seleccionar una plantilla. La plantilla de página se utiliza como base para la nueva página. La plantilla puede definir la estructura de la página resultante, cualquier contenido inicial y los componentes que se pueden utilizar (propiedades de diseño).

* Las plantillas editables permiten a los autores crear y utilizar plantillas.
* Las plantillas editables se pueden utilizar para crear páginas editables con
   * [Editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md) y
   * [Editor universal](/help/sites-cloud/authoring/universal-editor/templates.md)

Las plantillas de página utilizadas para crear páginas editables con el editor universal utilizan un subconjunto limitado de funcionalidades de plantilla editables. Por lo tanto, el resto de este documento se centra en plantillas editables utilizadas para crear páginas editables con el editor de páginas.

## Plantillas editables y páginas editadas con el editor de páginas {#page-editor}

Al crear plantillas para crear páginas editables con el editor de páginas, normalmente se identifican autores especializados.

* Estos autores especializados se denominan **autores de plantillas**
* Los autores de plantillas deben ser miembros del grupo `template-authors`.
* Las plantillas editables conservan una conexión dinámica con cualquier página creada a partir de ellas. Esto garantiza que cualquier cambio en la plantilla se refleje en las propias páginas.
* Las plantillas editables hacen que el componente de página sea más genérico, por lo que el componente de página principal se puede utilizar sin personalización.

Con las plantillas editables, las partes que componen una página están aisladas dentro de los componentes. Puede configurar las combinaciones necesarias de componentes en una interfaz de usuario, lo que elimina la necesidad de desarrollar un nuevo componente de página para cada variación de página.

Este documento:

* Ofrece información general sobre la creación de una plantilla editable
* Describe las tareas de administrador/desarrollador necesarias para crear plantillas editables
* Describe los fundamentos técnicos de las plantillas editables
* Describe cómo AEM evalúa la disponibilidad de una plantilla

>[!NOTE]
>
>Este documento supone que ya está familiarizado con la creación y edición de plantillas. Consulte el documento de creación [Plantillas para crear páginas editables con el editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md), que detalla las capacidades de las plantillas editables tal como se exponen al autor de la plantilla.

>[!TIP]
>
>[El tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) profundiza en cómo usar plantillas editables implementando un ejemplo y es muy útil para comprender cómo configurar una plantilla en un nuevo proyecto

## Crear una nueva plantilla editable {#creating-a-new-template}

La creación de plantillas editables se realiza principalmente con la [consola y el editor de plantillas](/help/sites-cloud/authoring/page-editor/templates.md) por un autor de plantillas. En esta sección se ofrece una descripción general de este proceso y se incluye una descripción de lo que sucede a nivel técnico.

Al crear una plantilla editable, debe hacer lo siguiente:

1. Crear una [carpeta para las plantillas](#template-folders). Esto no es obligatorio, pero es una práctica recomendada.
1. Seleccione un [tipo de plantilla](#template-type). Esto se ha copiado para crear la [definición de plantilla](#template-definitions).

   >[!NOTE]
   >
   >Se proporciona una selección de tipos de plantillas listas para usarse. También puede [crear sus propios tipos de plantilla específicos del sitio](#creating-template-types) si es necesario.

1. Configure la estructura, las políticas de contenido, el contenido inicial y el diseño de la nueva plantilla.

   **Estructura**

   * La estructura permite definir componentes y contenido para la plantilla.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminar de ninguna página resultante.
   * Si desea que los autores de páginas puedan añadir y quitar componentes, agregue un sistema de párrafos a la plantilla.
   * Los componentes se pueden volver a desbloquear y bloquear para permitirle definir el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantillas, consulte [Plantillas para crear páginas editables con el editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de la estructura, consulte [Estructura](#structure) en este documento.

   **Políticas**

   * Las políticas de contenido definen las propiedades de diseño de un componente.

      * Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas.

   * Se aplican a la plantilla (y a las páginas creadas con la plantilla).

   Para obtener más información sobre cómo define las directivas un autor de plantillas, consulte [Plantillas para crear páginas editables con el editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de las directivas, consulte [Políticas de contenido](#content-policies) en este documento.

   **Contenido inicial**

   * El contenido inicial define el contenido que aparecerá cuando se cree una página por primera vez en función de la plantilla.
   * Los autores de la página pueden editar el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantillas, consulte [Plantillas para crear páginas editables con el editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-initial-content-author).

   Para obtener detalles técnicos sobre el contenido inicial, consulte [Contenido inicial](#initial-content) en este documento.

   **Diseño**

   * Puede definir el diseño de la plantilla para una amplia gama de dispositivos.
   * El diseño interactivo para las plantillas funciona igual que para la creación de páginas.

   Para obtener más información sobre cómo define el diseño de la plantilla un autor de plantillas, consulte [Plantillas para crear páginas que se pueden editar con el editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-layout-template-author).

   Para obtener detalles técnicos sobre el diseño de la plantilla, consulte [Diseño](#layout) en este documento.

1. Habilite la plantilla y déjela para árboles de contenido específicos.

   * Una plantilla se puede habilitar o deshabilitar para que esté disponible o no disponible para los autores de páginas.
   * Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

   Para obtener más información sobre cómo un autor de plantillas habilita una plantilla, consulte [Plantillas para crear páginas editables con el editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author).

   Para obtener detalles técnicos sobre cómo habilitar una plantilla, consulte [Habilitar y permitir una plantilla](#enabling-and-allowing-a-template-for-use)e en este documento

1. Úselo para crear páginas de contenido.

   * Cuando se utiliza una plantilla para crear una página, no hay ninguna diferencia visible ni indicación entre las plantillas estáticas y editables.
   * Para el autor de la página, el proceso es transparente.

   Para obtener más información sobre cómo un autor de páginas usa plantillas para crear una página, consulte [Creación y organización de páginas](/help/sites-cloud/authoring/sites-console/organizing-pages.md#templates).

   Para obtener detalles técnicos sobre la creación de páginas con plantillas editables, consulte [Páginas de contenido resultante](#resultant-content-pages) en este documento.

>[!TIP]
>
>Nunca introduzca en una plantilla información que deba internacionalizarse. Para fines de internalización, se recomiendan las [características de localización de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=es).

>[!NOTE]
>
>Las plantillas son herramientas útiles para optimizar el flujo de trabajo de creación de páginas. Sin embargo, demasiadas plantillas pueden saturar a los autores y hacer que la creación de páginas sea confusa. Una buena regla general es mantener el número de plantillas por debajo de 100.
>
>Adobe no recomienda tener más de 1000 plantillas debido a posibles impactos en el rendimiento.

>[!NOTE]
>
>La biblioteca de cliente del editor supone la presencia del área de nombres `cq.shared` en las páginas de contenido y, si no existe, se producirá el error de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>Todas las páginas de contenido de muestra contienen `cq.shared`, por lo que cualquier contenido basado en ellas incluye automáticamente `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de ejemplo, debe asegurarse de incluir el área de nombres `cq.shared`.
>
>Consulte [Uso de bibliotecas del lado del cliente](/help/implementing/developing/introduction/clientlibs.md) para obtener más información.

## Carpetas de plantilla {#template-folders}

Para organizar las plantillas, puede utilizar las siguientes carpetas:

* `global`
* Específico del sitio

>[!NOTE]
>
>Aunque puede anidar las carpetas, cuando el usuario las vea en la consola **Templates**, se presentarán como una estructura plana.

En una instancia estándar de AEM, la carpeta `global` ya existe en la consola de plantillas. Contiene plantillas predeterminadas y actúa como alternativa en caso de que no se encuentre ninguna política ni ningún tipo de plantilla en la carpeta actual. Puede agregar las plantillas predeterminadas a esta carpeta o crear una carpeta (recomendado).

>[!NOTE]
>
>Se recomienda crear una carpeta que contenga las plantillas personalizadas y no utilizar la carpeta `global`.

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

* Mediante programación o con CRXDE Lite
* Usando el [Explorador de configuración](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## Uso del CRXDE Lite {#using-crxde-lite}

1. Se puede crear una nueva carpeta (en /conf) para su instancia mediante programación o con CRXDE Lite.

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
   * Valor: título (de la carpeta) que desea que aparezca en la consola **Plantillas**.

1. Además de los permisos y privilegios de creación estándar (por ejemplo, `content-authors`), ahora debe asignar grupos y definir los derechos de acceso (ACL) necesarios para que los autores puedan crear plantillas en la nueva carpeta.

   El grupo `template-authors` es el grupo predeterminado que se debe asignar. Consulte la sección [ACL y grupos](#acls-and-groups) para obtener más información.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Uso del explorador de configuración {#using-the-configuration-browser}

1. Vaya a **Navegación global** > **Herramientas** > [**Explorador de configuración**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

   Las carpetas existentes se muestran a la izquierda, incluida la carpeta `global`.

1. Haga clic en **Crear**.
1. En el cuadro de diálogo **Crear configuración** deben configurarse los siguientes campos:

   * **Título**: proporcione un título para la carpeta de configuración
   * **Plantillas editables**: Marque esta opción para permitir plantillas editables dentro de esta carpeta

1. Haga clic en **Crear**

>[!NOTE]
>
>En el [Explorador de configuración](/help/implementing/developing/introduction/configurations.md#using-configuration-browser), puede editar la carpeta global y activar la opción **Plantillas editables** si desea crear plantillas dentro de esta carpeta; sin embargo, esta no es una práctica recomendada.

### ACL y grupos {#acls-and-groups}

Una vez creadas las carpetas de plantilla (ya sea mediante CRXDE o con el Explorador de configuración), se deben definir ACL para los grupos adecuados para las carpetas de plantilla para garantizar la seguridad adecuada.

Las carpetas de plantillas para el [tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) se pueden usar como ejemplo.

#### El grupo de autores de plantillas {#the-template-authors-group}

El grupo `template-authors` es el grupo que se usa para administrar el acceso a las plantillas y viene de serie con AEM, pero está vacío. Los usuarios deben agregarse al grupo para el proyecto o sitio.

>[!CAUTION]
>
>El grupo `template-authors` es exclusivo para usuarios que deben poder crear nuevas plantillas.
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
   <td>Autores de plantillas<br /> </td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en el espacio <code>/conf</code> específico del sitio</td>
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
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en el espacio <code>/conf</code> específico del sitio</td>
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

Este grupo predeterminado de `template-authors` solo cubre las configuraciones de proyecto, en las que se permite a todos los miembros de `template-authors` acceder a todas las plantillas y crearlas. Para configuraciones más complejas, donde se necesitan varios grupos de autores de plantillas para separar el acceso a las plantillas, se deben crear grupos de autores de plantillas más personalizados. Sin embargo, los permisos para los grupos de autores de plantillas seguirían siendo los mismos.

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

   * Se proporcionan ejemplos adicionales como parte del [tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* Los desarrolladores suelen definir los tipos de plantillas.

Los tipos de plantilla predeterminados se almacenan en:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>No debe cambiar nada en la ruta de acceso `/libs`. Esto se debe a que el contenido de `/libs` se puede sobrescribir en cualquier momento mediante una actualización a AEM.

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

1. Cree una plantilla como lo haría con cualquier plantilla de página. Vea [Plantillas para crear páginas editables con el editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md#creating-a-new-template-template-author). Esto servirá de base para el tipo de plantilla.
1. Con CRXDE Lite, copie la plantilla creada desde el nodo `templates` al nodo `template-types` en la [carpeta de plantillas](#template-folders).
1. Elimine la plantilla del nodo `templates` en la [carpeta de plantillas](#template-folders).
1. En la copia de la plantilla que se encuentra bajo el nodo `template-types`, elimine todas las propiedades `cq:template` y `cq:templateType` de todos los nodos `jcr:content`.

También puede desarrollar su propio tipo de plantilla con una plantilla editable de ejemplo como base, disponible en GitHub.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto aem-sites-example-custom-template-type en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definiciones de plantilla {#template-definitions}

Las definiciones para plantillas editables se almacenan en [carpetas definidas por el usuario](#template-folders) (recomendado) o, alternativamente, en `global`. Por ejemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

El nodo raíz de la plantilla es del tipo `cq:Template` con una estructura básica de:

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

### jcr:content {#jcr-content}

Este nodo contiene propiedades para la plantilla:

* **Nombre**: `jcr:title`
* **Nombre**: `status`
   * &quot;**Tipo**: `String`
   * **Valor**: `draft`, `enabled` o `disabled`

### Estructura {#structure}

Define la estructura de la página resultante:

* Se combina con el contenido inicial (`/initial`) al crear una página.
* Los cambios realizados en la estructura se reflejan en cualquier página creada con la plantilla.
* El nodo `root` ( `structure/jcr:content/root`) define la lista de componentes disponibles en la página resultante.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover ni eliminar de ninguna página resultante.
   * Después de desbloquear un componente, la propiedad `editable` se establece en `true`.
   * Después de desbloquear un componente que ya contiene contenido, este contenido se mueve a la rama `initial`.

* El nodo `cq:responsive` contiene definiciones para el diseño interactivo.

### Contenido inicial {#initial-content}

Define el contenido inicial que tendrá una nueva página al crearla:

* Contiene un nodo `jcr:content` que se copia en las páginas nuevas.
* Se combina con la estructura (`/structure`) al crear una página.
* Las páginas existentes no se actualizarán si el contenido inicial cambia después de la creación.
* El nodo `root` contiene una lista de componentes para definir lo que está disponible en la página resultante.
* Si el contenido se añade a un componente en modo de estructura y dicho componente se desbloquea posteriormente (o a la inversa), este contenido se utiliza como contenido inicial.

### Diseño {#layout}

Al [editar una plantilla, puede definir el diseño](/help/sites-cloud/authoring/page-editor/templates.md), usa [diseño interactivo estándar](/help/sites-cloud/administering/responsive-layout.md), que el autor de contenido puede [configurar en la página](/help/sites-cloud/authoring/page-editor/responsive-layout.md).

### Políticas de contenido {#content-policies}

Las políticas de contenido definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Se aplican a la plantilla (y a las páginas creadas con la plantilla). Las políticas de contenido se pueden crear y seleccionar en el editor de plantillas.

* La propiedad `cq:policy`, en el nodo `root`
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Proporciona una referencia relativa a la directiva de contenido para el sistema de párrafos de la página.

* La propiedad `cq:policy`, en los nodos explícitos de componente en `root`, proporciona vínculos a las directivas de los componentes individuales.

* Las definiciones de directivas reales se almacenan en:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Las rutas de las definiciones de directivas dependen de la ruta del componente. `cq:policy` contiene una referencia relativa a la propia configuración.

### Políticas de la página {#page-policies}

Las directivas de página le permiten definir la [directiva de contenido](#content-policies) para la página (parsys principal), en la plantilla o en las páginas resultantes.

### Habilitar y permitir el uso de una plantilla {#enabling-and-allowing-a-template-for-use}

1. **Habilitar la plantilla**

   Para poder utilizar una plantilla, debe habilitarse mediante lo siguiente:

   * [Habilitando la plantilla](/help/sites-cloud/authoring/page-editor/templates.md) desde la consola **Plantillas**.

   * Estableciendo la propiedad status en el nodo `jcr:content`.

      * Por ejemplo, en:
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina la propiedad:

         * Nombre: estado
         * Tipo: cadena
         * Valor: `enabled`

1. **Plantillas permitidas**

   * [Defina las rutas de plantilla permitidas en **Propiedades de página**](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author) de la página o página raíz apropiada de una subrama.
   * Establezca la propiedad:
     `cq:allowedTemplates`
En el nodo `jcr:content` de la rama requerida.

   Por ejemplo, con un valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de contenido resultantes {#resultant-content-pages}

Páginas creadas a partir de plantillas editables:

* Se crean con un subárbol que se combina de `structure` y `initial` en la plantilla

* Tener referencias a información contenida en la plantilla y el tipo de plantilla. Esto se logra con un nodo `jcr:content` con las propiedades:

   * `cq:template`: proporciona la referencia dinámica a la plantilla real; permite que los cambios realizados en la plantilla se reflejen en las páginas reales.

   * `cq:templateType`: proporciona una referencia al tipo de plantilla.

![Cómo se interrelacionan las plantillas, el contenido y los componentes](assets/templates-content-components.png)

El diagrama anterior muestra cómo se interrelacionan las plantillas, el contenido y los componentes:

* Controlador - `/content/<my-site>/<my-page>` - La página resultante que hace referencia a la plantilla. El contenido controla todo el proceso. Según las definiciones, accede a la plantilla y a los componentes adecuados.
* Configuración - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - La plantilla [y las directivas de contenido relacionadas](#template-definitions) definen la configuración de la página.
* Modelo - Paquetes OSGi - Los [paquetes OSGI](/help/implementing/deploying/configuring-osgi.md) implementan la funcionalidad.
* Ver - `/apps/<my-site>/components` - Tanto en el entorno de creación como de publicación, los componentes procesan el contenido.

Al procesar una página:

* **Plantillas**:

   * Se hace referencia a la propiedad `cq:template` de su nodo `jcr:content` para obtener acceso a la plantilla que corresponde a esa página.

* **Componentes**:

   * El componente de página combinará el árbol `structure/jcr:content` de la plantilla con el árbol `jcr:content` de la página.
      * El componente de página solo permitirá al autor editar los nodos de la estructura de la plantilla que se han marcado como editables (y los secundarios).
      * Al procesar un componente en una página, la ruta relativa de ese componente se toma del nodo `jcr:content`; a continuación, se buscará la misma ruta de acceso en el nodo `policies/jcr:content` de la plantilla.
         * La propiedad `cq:policy` de este nodo señala a la directiva de contenido real (es decir, contiene la configuración de diseño para ese componente).
            * Esto permite tener varias plantillas que reutilizan las mismas configuraciones de directiva de contenido.

### Disponibilidad de la plantilla {#template-availability}

Al crear una página en la interfaz de administración del sitio, la lista de plantillas disponibles depende de la ubicación de la nueva página y de las restricciones de colocación especificadas en cada plantilla.

Las siguientes propiedades determinan si se permite utilizar una plantilla `T` para colocar una nueva página como elemento secundario de la página `P`. Cada una de estas propiedades es una cadena de varios valores que contiene cero o más expresiones regulares que se utilizan para la coincidencia con rutas:

* La propiedad `cq:allowedTemplates` del subnodo `jcr:content` de `P` o un antecesor de `P`.

* La propiedad `allowedPaths` de `T`.

* La propiedad `allowedParents` de `T`.

* La propiedad `allowedChildren` de la plantilla de `P`.

La evaluación funciona de la siguiente manera:

* Se comparó la primera propiedad `cq:allowedTemplates` que no está vacía al ascender la jerarquía de páginas que comienza por `P` con la ruta de acceso de `T`. Si ninguno de los valores coincide, `T` se rechaza.

* Si `T` tiene una propiedad `allowedPaths` que no está vacía, pero ninguno de los valores coincide con la ruta de acceso de `P`, se rechaza `T`.

* Si ambas propiedades están vacías o no existen, se rechaza `T` a menos que pertenezca a la misma aplicación que `P`. `T` pertenece a la misma aplicación que `P` solo si el nombre del segundo nivel de la ruta de acceso de `T` es el mismo que el nombre del segundo nivel de la ruta de acceso de `P`. Por ejemplo, la plantilla `/apps/wknd/templates/foo` pertenece a la misma aplicación que la página `/content/wknd`.

* Si `T` tiene una propiedad `allowedParents` que no está vacía, pero ninguno de los valores coincide con la ruta de acceso de `P`, se rechaza `T`.

* Si la plantilla de `P` tiene una propiedad `allowedChildren` que no está vacía, pero ninguno de los valores coincide con la ruta de acceso de `T`, se rechaza `T`.

* En todos los demás casos, se permite `T`.

El diagrama siguiente muestra el proceso de evaluación de la plantilla:

![Proceso de evaluación de plantilla](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM ofrece varias propiedades para controlar las plantillas permitidas en **Sitios**. Sin embargo, combinarlas puede dar lugar a reglas muy complejas difíciles de rastrear y administrar.
>
>Por lo tanto, Adobe recomienda empezar de forma sencilla definiendo:
>
>* solo la propiedad `cq:allowedTemplates`
>
>* solo en la raíz del sitio
>
>Para ver un ejemplo, vea el contenido del [tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md): `/content/wknd/jcr:content`
>
>Las propiedades `allowedPaths`, `allowedParents` y `allowedChildren` también se pueden colocar en las plantillas para definir reglas más sofisticadas. Sin embargo, cuando es posible, es *mucho* más fácil definir más propiedades de `cq:allowedTemplates` en subsecciones del sitio si es necesario restringir aún más las plantillas permitidas.
>
>Una ventaja adicional es que un autor puede actualizar las propiedades de `cq:allowedTemplates` en la ficha **Avanzadas** de **Propiedades de página**. Las demás propiedades de la plantilla no se pueden actualizar mediante la interfaz de usuario (estándar), por lo que se necesitaría un desarrollador para mantener las reglas y una implementación de código para cada cambio.

#### Limitación de plantillas utilizadas en páginas secundarias {#limiting-templates-used-in-child-pages}

Para limitar qué plantillas se pueden usar para crear páginas secundarias en una página determinada, use la propiedad `cq:allowedTemplates` del nodo `jcr:content` de la página para especificar la lista de plantillas que se permitirán como secundarias. Cada valor de la lista debe ser una ruta absoluta a una plantilla para una página secundaria permitida, por ejemplo, `/apps/wknd/templates/page-content`.

Puede usar la propiedad `cq:allowedTemplates` en el nodo `jcr:content` de la plantilla para aplicar esta configuración a todas las páginas creadas que usen esta plantilla.

Si desea agregar más restricciones, por ejemplo, con respecto a la jerarquía de plantillas, puede utilizar las propiedades `allowedParents/allowedChildren` en la plantilla. A continuación, puede especificar explícitamente que las páginas creadas a partir de una plantilla T tengan que ser páginas principales o secundarias de páginas creadas a partir de una plantilla T.
