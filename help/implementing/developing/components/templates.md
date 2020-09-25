---
title: Plantillas de página
description: Las plantillas de página se utilizan al crear una página que se utilizará como base para la nueva página
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '3221'
ht-degree: 8%

---


# Plantillas de página {#page-templates}

Al crear una página, debe seleccionar una plantilla. La plantilla de página se utiliza como base para la nueva página. Una plantilla define la estructura de la página resultante, todo el contenido inicial y los componentes que se pueden utilizar (propiedades de diseño). Esto tiene varias ventajas:

* Las plantillas de página permiten a los autores especializados [crear y editar plantillas](/help/sites-cloud/authoring/features/templates.md).
   * Estos autores especializados se denominan autores **de plantillas**
   * Los autores de plantillas deben ser miembros del `template-authors` grupo.
* Las plantillas de página mantienen una conexión dinámica con cualquier página creada a partir de ellas. Esto garantiza que cualquier cambio en la plantilla se refleje en las páginas mismas.
* Las plantillas de página hacen que el componente de página sea más genérico para que el componente de página principal se pueda utilizar sin personalización.

Con las plantillas de página, los artículos que crean una página se aislan dentro de los componentes. Puede configurar las combinaciones necesarias de componentes en una interfaz de usuario, eliminando así la necesidad de desarrollar un nuevo componente de página para cada variación de página.

Este documento:

* Proporciona información general sobre cómo crear una plantilla de página
* Describe las tareas de administrador y desarrollador necesarias para crear plantillas editables
* Describe los fundamentos técnicos de las plantillas editables
* Describe cómo AEM evalúa la disponibilidad de una plantilla

>[!NOTE]
>
>Este documento supone que ya está familiarizado con la creación y edición de plantillas. Consulte el documento de creación [Creación de plantillas](/help/sites-cloud/authoring/features/templates.md)de página, que detalla las funciones de las plantillas editables tal y como están expuestas al autor de la plantilla.

>[!TIP]
>
>[El tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md) WKND profundiza en cómo utilizar las plantillas de página mediante la implementación de un ejemplo y resulta muy útil para comprender cómo configurar una plantilla en un nuevo proyecto

## Creating a New Template {#creating-a-new-template}

La creación de plantillas de página se realiza principalmente con la consola de [plantilla y el editor](/help/sites-cloud/authoring/features/templates.md) de plantillas. En esta sección se ofrece una visión general de este proceso y se ofrece una descripción de lo que ocurre a nivel técnico.

Al crear una nueva plantilla editable, realiza estas acciones:

1. Cree una [carpeta para las plantillas](#template-folders). Esto no es obligatorio, pero se recomienda una práctica recomendada.
1. Seleccione un tipo [de](#template-type)plantilla. Se copia para crear la definición [de](#template-definitions)plantilla.

   >[!NOTE]
   >
   >Se proporciona una selección de tipos de plantilla lista para usar. También puede [crear sus propios tipos](#creating-template-types) de plantilla específicos del sitio si es necesario.

1. Configure la estructura, las políticas de contenido, el contenido inicial y el diseño de la nueva plantilla.

   **Estructura**

   * La estructura permite definir componentes y contenido para la plantilla.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminarse de ninguna página resultante.
   * Si desea que los autores de la página puedan añadir y quitar componentes, añada un sistema de párrafos a la plantilla.
   * Los componentes pueden volver a desbloquearse y bloquearse para que pueda definir el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantilla, consulte [Creación de plantillas](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)de página.

   Para obtener información técnica sobre la estructura, consulte [Estructura](#structure) en este documento.

   **Políticas**

   * Las políticas de contenido definen las propiedades de diseño de un componente.

      * Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas.
   * Esto se aplica a la plantilla (y a las páginas creadas con la plantilla).

   Para obtener más información sobre cómo define el autor de una plantilla las políticas, consulte [Creación de plantillas](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)de página.

   Para obtener información técnica sobre las políticas, consulte Políticas [de contenido](#content-policies) en este documento.

   **Contenido inicial**

   * El contenido inicial define el contenido que aparecerá cuando se cree una página por primera vez en función de la plantilla.
   * A continuación, los autores de las páginas pueden editar el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantilla, consulte [Creación de plantillas](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author)de página.

   Para obtener detalles técnicos sobre el contenido inicial, consulte Contenido [](#initial-content) inicial en este documento.

   **Diseño**

   * Puede definir el diseño de la plantilla para una amplia gama de dispositivos.
   * El diseño interactivo para las plantillas funciona tal como lo hace para la creación de páginas.

   Para obtener más información sobre cómo define el diseño de plantilla un autor de plantilla, consulte [Creación de plantillas](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author)de página.

   Para obtener información técnica sobre el diseño de la plantilla, consulte [Diseño](#layout) en este documento.

1. Habilite la plantilla y, a continuación, déjela para árboles de contenido específicos.

   * Una plantilla puede habilitarse o deshabilitarse para que esté disponible o no esté disponible para los autores de la página.
   * Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

   Para obtener más información sobre cómo el autor de una plantilla habilita una plantilla, consulte [Creación de plantillas](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author)de página.

   Para obtener información técnica sobre cómo habilitar una plantilla, consulte [Activación y autorización de una plantilla para](#enabling-and-allowing-a-template-for-use)uso en este documento

1. Utilícelo para crear páginas de contenido.

   * Al utilizar una plantilla para crear una página nueva, no existe ninguna diferencia visible ni ninguna indicación entre las plantillas estáticas y las editables.
   * Para el autor de la página, el proceso es transparente.

   Para obtener más información sobre cómo el autor de una página utiliza plantillas para crear una página, consulte [Creación y organización de páginas](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Para obtener información técnica sobre la creación de páginas con plantillas editables, consulte [Páginas](#resultant-content-pages) de contenido resultantes en este documento.

>[!NOTE]
>
>La biblioteca de cliente del editor asume la presencia de la `cq.shared` Área de nombres en las páginas de contenido y, si no se encuentra, se `Uncaught TypeError: Cannot read property 'shared' of undefined` producirá el error de JavaScript.
>
>Todas las páginas de contenido de muestra contienen `cq.shared`, por lo que cualquier contenido basado en ellas incluye `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de muestra, debe asegurarse de incluir la `cq.shared` Área de nombres.

<!--See [Using Client-Side Libraries](/help/sites-developing/clientlibs.md) for further information.-->

>[!CAUTION]
>
>No introduzca nunca en una plantilla información que deba internacionalizarse.

## Carpetas de plantilla {#template-folders}

Para organizar las plantillas, puede utilizar las siguientes carpetas:

* `global`
* Específico del sitio

>[!NOTE]
>
>Aunque puede anidar las carpetas, cuando el usuario las vista en la consola **Plantillas** , se presentan como una estructura plana.

En una instancia estándar de AEM, la carpeta `global` ya existe en la consola de plantillas. Contiene plantillas predeterminadas y actúa como alternativa en caso de que no se encuentre ninguna política ni ningún tipo de plantilla en la carpeta actual. Puede agregar las plantillas predeterminadas a esta carpeta o crear una nueva carpeta (recomendado).

>[!NOTE]
>
>Se recomienda crear una nueva carpeta para albergar las plantillas personalizadas y no utilizar la `global` carpeta.

>[!CAUTION]
>
>Las carpetas deben ser creadas por un usuario con `admin` derechos.

Los tipos de plantilla y las directivas se heredan en todas las carpetas según el siguiente orden de prioridad:

1. La carpeta actual
1. Principal(s) de la carpeta actual
1. `/conf/global`
1. `/apps`
1. `/libs`

Se crea una lista de todas las entradas permitidas. Si alguna configuración se superpone ( `path`/ `label`), solo se presenta al usuario la instancia más cercana a la carpeta actual.

Para crear una nueva carpeta, puede hacer lo siguiente:

* Programáticamente o con CRXDE Lite
* Uso del navegador de configuración

## Uso de CRXDE Lite {#using-crxde-lite}

1. Se puede crear una nueva carpeta (en /conf) para su instancia mediante programación o con CRXDE Lite.

   Debe utilizarse la siguiente estructura:

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
   * Valor: Título (para la carpeta) que desea que aparezca en la consola **Plantillas** .

1. Además de los permisos y privilegios de creación estándar (p. ej. `content-authors`) ahora debe asignar grupos y definir los derechos de acceso requeridos (ACL) para que los autores puedan crear plantillas en la nueva carpeta.

   El grupo `template-authors` es el grupo predeterminado que se debe asignar. Consulte la sección [ACL y grupos](#acls-and-groups) para obtener más información.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Uso del navegador de configuración {#using-the-configuration-browser}

1. Vaya a Navegación **** global -> **Herramientas** > Navegador **** de configuración.

   Las carpetas existentes se muestran a la izquierda, incluida la `global` carpeta.

1. Haga clic en **Crear**.
1. En el cuadro de diálogo **Crear configuración** se deben configurar los campos siguientes:

   * **Título**: Proporcionar un título para la carpeta de configuración
   * **Plantillas** editables: Haga clic para permitir plantillas editables dentro de esta carpeta

1. Haga clic en **Crear**

>[!NOTE]
>
>En el navegador de configuración, puede editar la carpeta global y activar la opción Plantillas **** editables si desea crear plantillas dentro de esta carpeta, aunque no se recomienda hacerlo.

### ACL y grupos {#acls-and-groups}

Una vez creadas las carpetas de plantilla (ya sea a través de CRXDE o con el navegador de configuración), las ACL deben definirse para los grupos adecuados para las carpetas de plantilla a fin de garantizar una seguridad adecuada.

Las carpetas de plantillas del tutorial [](/help/implementing/developing/introduction/develop-wknd-tutorial.md) WKND pueden utilizarse como ejemplo.

#### El grupo de autores de plantillas {#the-template-authors-group}

El `template-authors` grupo es el grupo que se utiliza para administrar el acceso a las plantillas y viene estándar con AEM, pero está vacío. Los usuarios deben agregarse al grupo para el proyecto o sitio.

>[!CAUTION]
>
>El `template-authors` grupo es solo para usuarios que deben poder crear nuevas plantillas.
>
>La edición de plantillas es muy potente y, si no se realiza correctamente, las plantillas existentes se pueden romper. Por lo tanto, esta función debe centrarse y incluir únicamente a usuarios cualificados.

En la tabla siguiente se detallan los permisos necesarios para editar plantillas.

<table>
 <tbody>
  <tr>
   <th>Ruta</th>
   <th>Función/Grupo</th>
   <th>Permisos   <br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores de plantilla<br /> </td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en un espacio específico del sitio <code>/conf</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las plantillas al procesar una página</td>
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
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en un espacio específico del sitio <code>/conf</code></td>
  </tr>
  <tr>
   <td>Usuario Web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las directivas al procesar una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los creadores de contenido deben activar las directivas de una plantilla de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autor de plantillas</td>
   <td>read</td>
   <td>El autor de la plantilla crea una nueva plantilla basada en uno de los tipos de plantilla predefinidos.</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

Este `template-authors` grupo predeterminado solo cubre la configuración del proyecto, donde todos `template-authors` los miembros pueden acceder a todas las plantillas y crearlas. Para configuraciones más complejas, donde se necesitan varios grupos de autores de plantillas para separar el acceso a las plantillas, se deben crear más grupos de autores de plantillas personalizadas. Sin embargo, los permisos para los grupos de autores de plantillas seguirían siendo los mismos.

## Template Type {#template-type}

Al crear una nueva plantilla, debe especificar un tipo de plantilla:

* Los tipos de plantilla proporcionan plantillas para una plantilla. Al crear una nueva plantilla, se utiliza la estructura y el contenido inicial del tipo de plantilla seleccionado para crearlos en la nueva plantilla.

   * El tipo de plantilla se copia para crear la plantilla.
   * Una vez que se ha producido la copia, la única conexión entre la plantilla y el tipo de plantilla es una referencia estática con fines informativos.

* Los tipos de plantilla le permiten definir:

   * Tipo de recurso del componente de página.
   * La directiva del nodo raíz, que define los componentes permitidos en el editor de plantillas.
   * Se recomienda definir los puntos de interrupción para la cuadrícula adaptable y la configuración del emulador móvil en el tipo de plantilla.

* AEM ofrece una pequeña selección de tipos de plantilla predeterminados, como Página HTML5 y Página de formulario adaptable.

   * Se proporcionan ejemplos adicionales como parte del tutorial de [WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* Los desarrolladores suelen definir los tipos de plantilla.

Los tipos de plantilla predeterminados se almacenan en:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>No debe cambiar nada en la `/libs` ruta. Esto se debe a que el contenido de `/libs` se puede sobrescribir en cualquier momento mediante una actualización a AEM.

Los tipos de plantilla específicos del sitio deben almacenarse en la ubicación comparable de:

* `/apps/settings/wcm/template-types`

Las definiciones de los tipos de plantillas personalizadas deben almacenarse en carpetas definidas por el usuario (recomendadas) o bien en `global`. Por ejemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Los tipos de plantilla deben respetar la estructura de carpetas correcta (por ejemplo: `/settings/wcm/...`), de lo contrario no se encontrarán los tipos de plantilla.

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating a new editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

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

Si ha creado una plantilla que puede servir de base para otras plantillas, puede copiar esta plantilla como un tipo de plantilla.

1. Cree una plantilla como lo haría con cualquier plantilla de página [como se documenta aquí](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), que servirá como base para el tipo de plantilla.
1. Con CRXDE Lite, copie la plantilla recién creada del `templates` nodo en el `template-types` nodo situado debajo de la carpeta [de](#template-folders)plantillas.
1. Elimine la plantilla del `templates` nodo situado debajo de la carpeta [de la](#template-folders)plantilla.
1. En la copia de la plantilla que se encuentra bajo el `template-types` nodo, elimine todas `cq:template` las propiedades y `cq:templateType``jcr:content` .

También puede desarrollar su propio tipo de plantilla utilizando como base una plantilla editable de ejemplo, disponible en GitHub.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra un proyecto de tipo aem-sites-example-custom-template en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definiciones de plantilla {#template-definitions}

Las definiciones de las plantillas editables se almacenan en carpetas [definidas por el](#template-folders) usuario (recomendadas) o de forma alternativa en `global`. Por ejemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

El nodo raíz de la plantilla es del tipo `cq:Template` con una estructura de esqueleto de:

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
   * ``**Tipo**: `String`
   * **Valor**: `draft`, `enabled` o `disabled`

### Estructura {#structure}

Define la estructura de la página resultante:

* Se combina con el contenido inicial ( `/initial`) al crear una página nueva.
* Los cambios realizados en la estructura se reflejarán en cualquier página creada con la plantilla.
* El nodo `root` ( `structure/jcr:content/root`) define la lista de los componentes que estarán disponibles en la página resultante.
   * Los componentes definidos en la estructura de plantilla no se pueden mover ni eliminar de ninguna página resultante.
   * Una vez desbloqueado el componente, la `editable` propiedad se establece en `true`.
   * Una vez desbloqueado un componente que ya contiene contenido, este contenido se moverá a la `initial` rama.

* El `cq:responsive` nodo contiene definiciones para el diseño interactivo.

### Contenido inicial {#initial-content}

Define el contenido inicial que tendrá una página nueva al crearla:

* Contiene un `jcr:content` nodo que se copia en cualquier página nueva.
* Se combina con la estructura ( `/structure`) al crear una página nueva.
* Las páginas existentes no se actualizarán si se cambia el contenido inicial después de la creación.
* El `root` nodo contiene una lista de componentes para definir lo que estará disponible en la página resultante.
* Si se agrega contenido a un componente en modo de estructura y dicho componente se desbloquea posteriormente (o viceversa), este contenido se utiliza como contenido inicial.

### Diseño {#layout}

Al [editar una plantilla puede definir el diseño](/help/sites-cloud/authoring/features/templates.md), con el diseño [interactivo](/help/sites-cloud/authoring/features/responsive-layout.md)estándar.

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Content Policies {#content-policies}

Las políticas de contenido definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Esto se aplica a la plantilla (y a las páginas creadas con la plantilla). Las directivas de contenido se pueden crear y seleccionar en el editor de plantillas.

* La propiedad `cq:policy`, en el `root` nodo
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Proporciona una referencia relativa a la directiva de contenido para el sistema de párrafos de la página.

* La propiedad `cq:policy`, en los nodos explícitos del componente debajo de `root`, proporciona vínculos a las políticas de los componentes individuales.

* Las definiciones de directiva reales se almacenan en:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Las rutas de las definiciones de políticas dependen de la ruta del componente. `cq:policy` contiene una referencia relativa a la configuración misma.

### Políticas de la página {#page-policies}

Las políticas de página permiten definir la directiva [de](#content-policies) contenido para la página (parsys principal), ya sea en la plantilla o en las páginas resultantes.

### Habilitar y permitir el uso de una plantilla {#enabling-and-allowing-a-template-for-use}

1. **Habilitar la plantilla**

   Para poder usar una plantilla, debe habilitarla:

   * [Activación de la plantilla](/help/sites-cloud/authoring/features/templates.md) desde la consola **Plantillas** .

   * Definición de la propiedad status en el `jcr:content` nodo.

      * Por ejemplo, en:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina la propiedad:

         * Nombre: status
         * Tipo: Cadena
         * Value: `enabled`

1. **Plantillas permitidas**

   * [Defina las rutas de plantilla permitidas en las Propiedades **de**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) página de la página o página raíz adecuada de una subrama.
   * Establezca la propiedad:
      `cq:allowedTemplates`
En el 
`jcr:content` nodo de la rama requerida.
   Por ejemplo, con un valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de contenido resultantes {#resultant-content-pages}

Páginas creadas a partir de plantillas editables:

* Se crean con un subárbol que se combina desde `structure` y `initial` en la plantilla

* Tenga referencias a la información contenida en la plantilla y el tipo de plantilla. Esto se logra con un `jcr:content` nodo con las propiedades:

   * `cq:template` - Proporciona la referencia dinámica a la plantilla real; permite que los cambios realizados en la plantilla se reflejen en las páginas reales.

   * `cq:templateType` - Proporciona una referencia al tipo de plantilla.

![Interrelación entre plantillas, contenido y componentes](assets/templates-content-components.png)

El diagrama anterior muestra cómo las plantillas, el contenido y los componentes se interrelacionan:

* Controlador: `/content/<my-site>/<my-page>` : la página resultante que hace referencia a la plantilla. El contenido controla todo el proceso. De acuerdo con las definiciones, accede a la plantilla y los componentes correspondientes.
* Configuración: `/conf/<my-folder>/settings/wcm/templates/<my-template>` : la [plantilla y las directivas](#template-definitions) de contenido relacionadas definen la configuración de la página.
* Modelo: paquetes OSGi: los paquetes [OSGI](/help/implementing/deploying/configuring-osgi.md) implementan la funcionalidad.
* Vista: `/apps/<my-site>/components` : tanto en los entornos de creación como de publicación, los componentes representan el contenido.

Al procesar una página:

* **Plantillas**:

   * Se hará referencia a la `cq:template` propiedad de su `jcr:content` nodo para acceder a la plantilla que corresponde a esa página.

* **Componentes**:

   * El componente de página combinará el `structure/jcr:content` árbol de la plantilla con el `jcr:content` árbol de la página.
      * El componente de página solo permitirá al autor editar los nodos de la estructura de plantilla que se han marcado como editables (así como cualquier elemento secundario).
      * Cuando se procesa un componente en una página, la ruta relativa de dicho componente se toma del `jcr:content` nodo; se buscará la misma ruta bajo el `policies/jcr:content` nodo de la plantilla.
         * La `cq:policy` propiedad de este nodo apunta a la directiva de contenido real (es decir, contiene la configuración de diseño para ese componente).
            * Esto le permite tener varias plantillas que reutilizan las mismas configuraciones de directiva de contenido.

### Disponibilidad de la plantilla {#template-availability}

Al crear una nueva página en la interfaz de administración del sitio, la lista de las plantillas disponibles depende de la ubicación de la nueva página y de las restricciones de colocación especificadas en cada plantilla.

Las siguientes propiedades determinan si `T` se permite utilizar una plantilla para que una nueva página se coloque como elemento secundario de la página `P`. Cada una de estas propiedades es una cadena de varios valores que contiene cero o más Expresiones regulares que se utilizan para hacer coincidir con rutas:

* La `cq:allowedTemplates` propiedad del `jcr:content` subnodo de `P` o un antecesor de `P`.

* La `allowedPaths` propiedad de `T`.

* La `allowedParents` propiedad de `T`.

* La `allowedChildren` propiedad de la plantilla de `P`.

La evaluación funciona de la siguiente manera:

* La primera propiedad no vacía `cq:allowedTemplates` encontrada al ascender la jerarquía de páginas empezando por `P` se compara con la ruta de `T`. Si ninguno de los valores coincide, `T` se rechaza.

* Si `T` tiene una propiedad no vacía `allowedPaths` , pero ninguno de los valores coincide con la ruta de `P`, `T` se rechaza.

* Si las dos propiedades anteriores están vacías o no existen, `T` se rechaza a menos que pertenezcan a la misma aplicación que `P`. `T` pertenece a la misma aplicación que `P` si el nombre del segundo nivel de la ruta de `T` acceso es el mismo que el nombre del segundo nivel de la ruta de `P`. Por ejemplo, la plantilla `/apps/geometrixx/templates/foo` pertenece a la misma aplicación que la página `/content/geometrixx`.

* Si `T` tiene una propiedad no vacía `allowedParents` , pero ninguno de los valores coincide con la ruta de `P`, `T` se rechaza.

* Si la plantilla de `P` tiene una propiedad no vacía `allowedChildren` , pero ninguno de los valores coincide con la ruta de `T`, `T` se rechaza.

* En todos los demás casos, `T` se permite.

El diagrama siguiente muestra el proceso de evaluación de la plantilla:

![Proceso de evaluación de plantilla](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM oferta varias propiedades para controlar las plantillas permitidas en **Sitios**. Sin embargo, combinarlos puede llevar a reglas muy complejas que son difíciles de rastrear y administrar.
>
>Por lo tanto, Adobe recomienda que el inicio sea sencillo, definiendo:
>
>* solo la `cq:allowedTemplates` propiedad
   >
   >
* solo en la raíz del sitio
>
>
Para ver un ejemplo, consulte el contenido del tutorial [](/help/implementing/developing/introduction/develop-wknd-tutorial.md) WKND: `/content/wknd/jcr:content`
>
>Las propiedades `allowedPaths`, `allowedParents`y `allowedChildren` también se pueden colocar en las plantillas para definir reglas más sofisticadas. Sin embargo, cuando es posible, es *mucho* más sencillo definir más `cq:allowedTemplates` propiedades en las subsecciones del sitio si es necesario restringir aún más las plantillas permitidas.
>
>Una ventaja adicional es que un autor puede actualizar las `cq:allowedTemplates` propiedades en la ficha **Avanzadas** de las Propiedades de la **página**. Las demás propiedades de plantilla no se pueden actualizar con la IU (estándar), por lo que sería necesario que un desarrollador mantuviera las reglas y una implementación de código para cada cambio.

#### Limitación de plantillas utilizadas en páginas secundarias {#limiting-templates-used-in-child-pages}

Para limitar qué plantillas se pueden utilizar para crear páginas secundarias en una página determinada, utilice la `cq:allowedTemplates` propiedad del `jcr:content` nodo de la página para especificar la lista de las plantillas que se permitirán como páginas secundarias. Cada valor de la lista debe ser una ruta absoluta a una plantilla para una página secundaria permitida, por ejemplo `/apps/wknd/templates/page-content`.

Puede utilizar la `cq:allowedTemplates` `jcr:content` propiedad en el nodo de la plantilla para que esta configuración se aplique a todas las páginas creadas recientemente que utilicen esta plantilla.

Si desea agregar más restricciones, por ejemplo en relación con la jerarquía de plantillas, puede utilizar las `allowedParents/allowedChildren` propiedades de la plantilla. A continuación, puede especificar explícitamente que las páginas creadas a partir de una plantilla T deben ser páginas principales/secundarias de páginas creadas a partir de una plantilla T.
