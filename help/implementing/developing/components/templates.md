---
title: Plantillas de página
description: Las plantillas de página se utilizan al crear una página que se utilizará como base para la nueva página
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: f5aa9229ff06fdcff5474594269ebcf9daf09e41
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 10%

---

# Plantillas de página {#page-templates}

Al crear una página, debe seleccionar una plantilla. La plantilla de página se utiliza como base para la nueva página. Una plantilla define la estructura de la página resultante, todo el contenido inicial y los componentes que se pueden utilizar (propiedades de diseño). Esto tiene varias ventajas:

* Las plantillas de página permiten que los autores especializados [crear y editar plantillas](/help/sites-cloud/authoring/features/templates.md).
   * A estos autores especializados se les llama **autores de plantillas**
   * Los autores de plantillas deben ser miembros del `template-authors` grupo.
* Las plantillas de página mantienen una conexión dinámica con cualquier página creada a partir de ellas. Esto garantiza que cualquier cambio en la plantilla se refleje en las propias páginas.
* Las plantillas de página hacen que el componente de página sea más genérico, de modo que el componente de página principal se pueda utilizar sin personalización.

Con las plantillas de página, los elementos que crean una página están aislados dentro de los componentes. Puede configurar las combinaciones necesarias de componentes en una interfaz de usuario, eliminando así la necesidad de desarrollar un nuevo componente de página para cada variación de página.

Este documento:

* Proporciona información general sobre la creación de una plantilla de página
* Describe las tareas de administrador/desarrollador necesarias para crear plantillas editables
* Describe los fundamentos técnicos de las plantillas editables
* Describe cómo AEM evalúa la disponibilidad de una plantilla

>[!NOTE]
>
>Este documento supone que ya está familiarizado con la creación y edición de plantillas. Consulte el documento de creación [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md), que detalla las capacidades de las plantillas editables tal y como se exponen al autor de la plantilla.

>[!TIP]
>
>[Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) profundiza en cómo utilizar las plantillas de página mediante la implementación de un ejemplo y resulta muy útil para comprender cómo configurar una plantilla en un nuevo proyecto

## Creación de una plantilla nueva {#creating-a-new-template}

La creación de plantillas de página se realiza principalmente con la variable [consola de plantillas y editor de plantillas](/help/sites-cloud/authoring/features/templates.md) por un autor de plantillas. Esta sección ofrece información general sobre este proceso y a continuación una descripción de lo que ocurre a nivel técnico.

Al crear una nueva plantilla editable, realiza estas acciones:

1. Cree un [carpeta de las plantillas](#template-folders). Esto no es obligatorio, pero se recomienda una práctica recomendada.
1. Seleccione un [tipo de plantilla](#template-type). Esto se copia para crear la variable [definición de plantilla](#template-definitions).

   >[!NOTE]
   >
   >Se proporciona una selección de tipos de plantillas listas para usar. También puede [crear sus propios tipos de plantilla específicos del sitio](#creating-template-types) si es necesario.

1. Configure la estructura, las políticas de contenido, el contenido inicial y el diseño de la nueva plantilla.

   **Estructura**

   * La estructura permite definir componentes y contenido para la plantilla.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminarse de ninguna página resultante.
   * Si desea que los autores de la página puedan añadir y quitar componentes, añada un sistema de párrafos a la plantilla.
   * Los componentes pueden volver a desbloquearse y bloquearse para que pueda definir el contenido inicial.

   Para obtener más información sobre cómo define un autor de plantillas la estructura, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de la estructura, consulte [Estructura](#structure) en este documento.

   **Políticas**

   * Las políticas de contenido definen las propiedades de diseño de un componente.

      * Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas.
   * Esto se aplica a la plantilla (y a las páginas creadas con la plantilla).

   Para obtener más información sobre cómo define las políticas un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos sobre las directivas, consulte [Políticas de contenido](#content-policies) en este documento.

   **Contenido inicial**

   * El contenido inicial define el contenido que aparecerá cuando se cree una página por primera vez en función de la plantilla.
   * Los autores de páginas pueden editar el contenido inicial.

   Para obtener más información sobre cómo define un autor de plantillas la estructura, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   Para obtener información técnica sobre el contenido inicial, consulte [Contenido inicial](#initial-content) en este documento.

   **Diseño**

   * Puede definir el diseño de la plantilla para una amplia gama de dispositivos.
   * El diseño interactivo para las plantillas funciona tal como lo hace para la creación de páginas.

   Para obtener más información sobre cómo define un autor de plantillas el diseño de la plantilla, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   Para obtener información técnica sobre el diseño de la plantilla, consulte [Diseño](#layout) en este documento.

1. Habilite la plantilla y luego déjela para árboles de contenido específicos.

   * Una plantilla se puede habilitar o deshabilitar para que esté disponible o no disponible para los autores de páginas.
   * Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

   Para obtener más información sobre cómo un autor de plantillas habilita una plantilla, consulte [Creación de plantillas de página](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   Para obtener información técnica sobre cómo activar una plantilla, consulte [Activación y autorización de una plantilla para nosotros](#enabling-and-allowing-a-template-for-use)e en este documento

1. Utilícelo para crear páginas de contenido.

   * Al utilizar una plantilla para crear una página nueva, no existe ninguna diferencia visible ni ninguna indicación entre las plantillas estáticas y las editables.
   * Para el autor de la página, el proceso es transparente.

   Para obtener más información sobre cómo un autor de páginas utiliza plantillas para crear una página, consulte [Creación y organización de páginas](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Para obtener información técnica sobre la creación de páginas con plantillas editables, consulte [Páginas de contenido resultantes](#resultant-content-pages) en este documento.

>[!TIP]
>
>No introduzca nunca en una plantilla información que deba internacionalizarse. Para fines de internalización, la variable [características de localización de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=es) se recomienda.

>[!NOTE]
>
>Las plantillas son herramientas útiles para optimizar el flujo de trabajo de creación de páginas. Sin embargo, demasiadas plantillas pueden saturar a los autores y hacer que la creación de páginas sea confusa. Una buena regla general es mantener el número de plantillas por debajo de 100.
>
>Adobe no recomienda tener más de 1000 plantillas debido a posibles impactos en el rendimiento.

>[!NOTE]
>
>La biblioteca de cliente del editor asume la presencia de la variable `cq.shared` espacio de nombres en páginas de contenido y si no hay el error de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` será el resultado.
>
>Todas las páginas de contenido de ejemplo contienen `cq.shared`, por lo que cualquier contenido basado en ellos se incluye automáticamente `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de muestra, debe asegurarse de incluir la variable `cq.shared` espacio de nombres.
>
>Consulte [Uso de bibliotecas del lado del cliente](/help/implementing/developing/introduction/clientlibs.md) para obtener más información.



## Carpetas de plantilla {#template-folders}

Para organizar las plantillas, puede utilizar las siguientes carpetas:

* `global`
* Específico del sitio

>[!NOTE]
>
>Aunque puede anidar sus carpetas, cuando el usuario las vea en la **Plantillas** se presentan como una estructura plana.

En una instancia estándar de AEM, la carpeta `global` ya existe en la consola de plantillas. Contiene plantillas predeterminadas y actúa como alternativa en caso de que no se encuentre ninguna política ni ningún tipo de plantilla en la carpeta actual. Puede añadir las plantillas predeterminadas a esta carpeta o crear una nueva carpeta (recomendado).

>[!NOTE]
>
>Se recomienda crear una nueva carpeta que contenga las plantillas personalizadas y no utilizar la variable `global` carpeta.

>[!CAUTION]
>
>Las carpetas deben ser creadas por un usuario con `admin` derechos.

Los tipos de plantilla y las directivas se heredan en todas las carpetas según el siguiente orden de prioridad:

1. La carpeta actual
1. Principales de la carpeta actual
1. `/conf/global`
1. `/apps`
1. `/libs`

Se crea una lista de todas las entradas permitidas. Si alguna configuración se superpone ( `path`/ `label`), solo se presenta al usuario la instancia más cercana a la carpeta actual.

Para crear una carpeta nueva, puede hacer lo siguiente:

* Programado o con CRXDE Lite
* Al usar la variable [Explorador de configuración](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

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
   * Valor: El título (para la carpeta) que desea que aparezca en la **Plantillas** consola.

1. Además de los permisos y privilegios de creación estándar (por ejemplo, `content-authors`) ahora debe asignar grupos y definir los derechos de acceso (ACL) necesarios para que sus autores puedan crear plantillas en la nueva carpeta.

   La variable `template-authors` grupo es el grupo predeterminado que debe asignarse. Consulte la sección [ACL y grupos](#acls-and-groups) para obtener más información.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Uso del explorador de configuración {#using-the-configuration-browser}

1. Vaya a **Navegación global** -> **Herramientas** > [**Explorador de configuración**.](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   Las carpetas existentes se muestran a la izquierda, incluido el `global` carpeta.

1. Haga clic en **Crear**.
1. En el **Crear configuración** es necesario configurar los siguientes campos:

   * **Título**: Proporcionar un título para la carpeta de configuración
   * **Plantillas editables**: Haga clic para permitir plantillas editables dentro de esta carpeta

1. Haga clic en **Crear**

>[!NOTE]
>
>En el [Navegador de configuración,](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) puede editar la carpeta global y activar el **Plantillas editables** si desea crear plantillas dentro de esta carpeta, esta no es la práctica recomendada.

### ACL y grupos {#acls-and-groups}

Una vez creadas las carpetas de plantillas (a través de CRXDE o con el navegador de configuración), las ACL deben definirse para los grupos adecuados para las carpetas de plantillas para garantizar la seguridad adecuada.

Las carpetas de plantillas para la variable [Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) se puede usar como ejemplo.

#### El grupo de autores de plantillas {#the-template-authors-group}

La variable `template-authors` grupo es el grupo que se utiliza para administrar el acceso a las plantillas y viene estándar con AEM, pero está vacío. Los usuarios deben agregarse al grupo para el proyecto o sitio.

>[!CAUTION]
>
>La variable `template-authors` solo es para usuarios que deben poder crear nuevas plantillas.
>
>La edición de plantillas es muy potente y, si no se realiza correctamente, se pueden romper las plantillas existentes. Por lo tanto, esta función debe centrarse y solo incluir a usuarios cualificados.

La siguiente tabla detalla los permisos necesarios para la edición de plantillas.

<table>
 <tbody>
  <tr>
   <th>Ruta </th>
   <th>Función/Grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores de plantillas<br /> </td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en sitios específicos <code>/conf</code> espacio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
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
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en sitios específicos <code>/conf</code> espacio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
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
   <td>read</td>
   <td>El autor de plantillas crea una nueva plantilla basada en uno de los tipos de plantilla predefinidos.</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

Esta opción predeterminada `template-authors` El grupo solo cubre la configuración del proyecto, donde todas las `template-authors` los miembros pueden acceder y crear todas las plantillas. Para configuraciones más complejas, donde se necesitan varios grupos de autores de plantillas para separar el acceso a las plantillas, se deben crear más grupos de autores de plantillas personalizadas. Sin embargo, los permisos para los grupos de autores de plantillas seguirían siendo los mismos.

## Tipo de plantilla {#template-type}

Al crear una plantilla nueva, debe especificar un tipo de plantilla:

* Los tipos de plantilla proporcionan plantillas para una plantilla. Al crear una plantilla nueva, la estructura y el contenido inicial del tipo de plantilla seleccionado se utilizan para crear la plantilla nueva.

   * El tipo de plantilla se copia para crear la plantilla.
   * Una vez que se ha producido la copia, la única conexión entre la plantilla y el tipo de plantilla es una referencia estática con fines informativos.

* Los tipos de plantilla le permiten definir:

   * Tipo de recurso del componente de página.
   * La directiva del nodo raíz, que define los componentes permitidos en el editor de plantillas.
   * Se recomienda definir los puntos de interrupción para la cuadrícula adaptable y la configuración del emulador móvil en el tipo de plantilla.

* AEM ofrece una pequeña selección de tipos de plantillas listos para usar, como Página HTML5 y Página de formulario adaptable.

   * Se proporcionan ejemplos adicionales como parte del [Tutorial de WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* Los desarrolladores suelen definir los tipos de plantilla.

Los tipos de plantilla predeterminados se almacenan en:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>No debe cambiar nada en la variable `/libs` ruta. Esto se debe a que el contenido de `/libs` se puede sobrescribir en cualquier momento mediante una actualización a AEM.

Los tipos de plantilla específicos del sitio se deben almacenar en una ubicación comparable de:

* `/apps/settings/wcm/template-types`

Las definiciones de los tipos de plantillas personalizadas deben almacenarse en carpetas definidas por el usuario (recomendadas) o, alternativamente, en `global`. Por ejemplo:

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

1. Cree una plantilla como lo haría con cualquier plantilla de página [tal como se documenta aquí](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), que servirá de base para su tipo de plantilla.
1. Con el CRXDE Lite , copie la plantilla recién creada del `templates` al nodo `template-types` en el nodo [carpeta de plantillas](#template-folders).
1. Elimine la plantilla de la sección `templates` en el nodo [carpeta de plantillas](#template-folders).
1. En la copia de la plantilla que se encuentra en el `template-types` nodo, eliminar todo `cq:template` y `cq:templateType` propiedades de todas `jcr:content` nodos.

También puede desarrollar su propio tipo de plantilla utilizando una plantilla editable de ejemplo como base, disponible en GitHub.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra un proyecto de tipo aem-sites-example-custom-template en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definiciones de plantillas {#template-definitions}

Se almacenan las definiciones de las plantillas editables [carpetas definidas por el usuario](#template-folders) (recomendado) o alternativamente en `global`. Por ejemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

El nodo raíz de la plantilla es del tipo `cq:Template` con una estructura esquelética de:

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
* La variable `root` ( `structure/jcr:content/root`) define la lista de componentes que estarán disponibles en la página resultante.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover ni eliminar de ninguna página resultante.
   * Una vez desbloqueado el componente, se desbloquea la variable `editable` la propiedad se establece en `true`.
   * Una vez desbloqueado un componente que ya contiene contenido, este contenido se moverá al `initial` rama.

* La variable `cq:responsive` contiene definiciones para el diseño interactivo.

### Contenido inicial {#initial-content}

Define el contenido inicial que tendrá una página nueva al crearla:

* Contiene un `jcr:content` que se copia en cualquier página nueva.
* Se combina con la estructura ( `/structure`) al crear una página nueva.
* Las páginas existentes no se actualizarán si el contenido inicial se cambia después de la creación.
* La variable `root` contiene una lista de componentes para definir qué estará disponible en la página resultante.
* Si el contenido se añade a un componente en modo de estructura y ese componente se desbloquea posteriormente (o viceversa), este contenido se utiliza como contenido inicial.

### Diseño {#layout}

When [editar una plantilla, puede definir el diseño](/help/sites-cloud/authoring/features/templates.md), utiliza [diseño adaptable estándar](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Políticas de contenido {#content-policies}

Las políticas de contenido definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Esto se aplica a la plantilla (y a las páginas creadas con la plantilla). Las políticas de contenido se pueden crear y seleccionar en el editor de plantillas.

* La propiedad `cq:policy`, en el `root` node
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Proporciona una referencia relativa a la política de contenido para el sistema de párrafos de la página.

* La propiedad `cq:policy`, en los nodos explícitos del componente debajo de `root`, proporcione vínculos a las políticas de los componentes individuales.

* Las definiciones de directiva reales se almacenan en:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Las rutas de las definiciones de políticas dependen de la ruta del componente. `cq:policy` contiene una referencia relativa a la configuración misma.

### Políticas de la página {#page-policies}

Las políticas de página permiten definir la variable [política de contenido](#content-policies) para la página (parsys principal), en la plantilla o en las páginas resultantes.

### Activación y autorización de una plantilla para su uso {#enabling-and-allowing-a-template-for-use}

1. **Habilitar la plantilla**

   Para poder utilizar una plantilla, debe habilitarla:

   * [Activación de la plantilla](/help/sites-cloud/authoring/features/templates.md) de la variable **Plantillas** consola.

   * Configuración de la propiedad de estado en la variable `jcr:content` nodo .

      * Por ejemplo, en:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina la propiedad:

         * Nombre: status
         * Tipo: Cadena
         * Valor: `enabled`

1. **Plantillas permitidas**

   * [Defina las rutas de acceso de plantilla permitidas en el **Propiedades de página**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) de la página o página raíz adecuada de una subrama.
   * Establezca la propiedad:
      `cq:allowedTemplates`
En el 
`jcr:content` nodo de la rama requerida.
   Por ejemplo, con un valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de contenido resultantes {#resultant-content-pages}

Páginas creadas a partir de plantillas editables:

* Se crean con un subárbol que se combina a partir de `structure` y `initial` en la plantilla

* Tienen referencias a información contenida en la plantilla y el tipo de plantilla. Esto se logra con un `jcr:content` con las propiedades:

   * `cq:template` - Proporciona la referencia dinámica a la plantilla real; permite que los cambios realizados en la plantilla se reflejen en las páginas reales.

   * `cq:templateType` : Proporciona una referencia al tipo de plantilla.

![Interrelación de plantillas, contenido y componentes](assets/templates-content-components.png)

El diagrama anterior muestra cómo las plantillas, el contenido y los componentes se interrelacionan:

* Controlador - `/content/<my-site>/<my-page>` - La página resultante que hace referencia a la plantilla. El contenido controla todo el proceso. Según las definiciones, accede a la plantilla y los componentes adecuados.
* Configuración - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - El [plantilla y políticas de contenido relacionadas](#template-definitions) defina la configuración de página.
* Modelo: paquetes OSGi: [Paquetes OSGI](/help/implementing/deploying/configuring-osgi.md) implemente la funcionalidad .
* Ver - `/apps/<my-site>/components` : en los entornos de autor y publicación, el contenido se representa mediante componentes.

Al procesar una página:

* **Plantillas**:

   * La variable `cq:template` propiedad de su `jcr:content` se hará referencia al nodo para acceder a la plantilla que corresponde a esa página.

* **Componentes**:

   * El componente de página combinará el `structure/jcr:content` árbol de la plantilla con la variable `jcr:content` de la página.
      * El componente de página solo permite al autor editar los nodos de la estructura de la plantilla que se han marcado como editables (así como los secundarios).
      * Al procesar un componente en una página, la ruta relativa de ese componente se toma de la `jcr:content` nodo; la misma ruta debajo de `policies/jcr:content` de la plantilla se buscará.
         * La variable `cq:policy` La propiedad de este nodo apunta a la política de contenido real (es decir, contiene la configuración de diseño para ese componente).
            * Esto le permite tener varias plantillas que reutilizan las mismas configuraciones de directiva de contenido.

### Disponibilidad de la plantilla {#template-availability}

Al crear una página nueva en la interfaz de administración del sitio, la lista de plantillas disponibles depende de la ubicación de la nueva página y las restricciones de colocación especificadas en cada plantilla.

Las siguientes propiedades determinan si una plantilla `T` se permite para que una nueva página se coloque como un elemento secundario de la página `P`. Cada una de estas propiedades es una cadena de varios valores que contiene cero o más expresiones regulares que se utilizan para hacer coincidir con rutas:

* La variable `cq:allowedTemplates` propiedad de la variable `jcr:content` subnodo de `P` o un antecesor de `P`.

* La variable `allowedPaths` propiedad de `T`.

* La variable `allowedParents` propiedad de `T`.

* La variable `allowedChildren` propiedad de la plantilla de `P`.

La evaluación funciona de la siguiente manera:

* El primer no vacío `cq:allowedTemplates` propiedad encontrada al ascender la jerarquía de páginas comenzando por `P` se compara con la ruta de `T`. Si ninguno de los valores coincide, `T` se rechaza.

* If `T` tiene un no vacío `allowedPaths` , pero ninguno de los valores coincide con la ruta de `P`, `T` se rechaza.

* Si ambas propiedades anteriores están vacías o no existen, `T` se rechaza a menos que pertenezca a la misma aplicación que `P`. `T` pertenece a la misma aplicación que `P` if y only si el nombre del segundo nivel de la ruta de acceso de `T` es el mismo que el nombre del segundo nivel de la ruta de `P`. Por ejemplo, la plantilla `/apps/wknd/templates/foo` pertenece a la misma aplicación que la página `/content/wknd`.

* If `T` tiene un no vacío `allowedParents` , pero ninguno de los valores coincide con la ruta de `P`, `T` se rechaza.

* Si la plantilla de `P` tiene un no vacío `allowedChildren` , pero ninguno de los valores coincide con la ruta de `T`, `T` se rechaza.

* En todos los demás casos, `T` está permitido.

El diagrama siguiente muestra el proceso de evaluación de la plantilla:

![Proceso de evaluación de plantilla](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM ofrece varias propiedades para controlar las plantillas permitidas en **Sitios**. Sin embargo, combinarlas puede llevar a reglas muy complejas que son difíciles de rastrear y administrar.
>
>Por lo tanto, Adobe recomienda que comience con sencillez, definiendo:
>
>* solo la variable `cq:allowedTemplates` property
>
>* solo en la raíz del sitio
>
>Para ver un ejemplo, consulte la [Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) contenido: `/content/wknd/jcr:content`
>
>Las propiedades `allowedPaths`, `allowedParents`y `allowedChildren` también se puede colocar en las plantillas para definir reglas más sofisticadas. Sin embargo, cuando es posible, es *many* más sencillo de definir `cq:allowedTemplates` propiedades en subsecciones del sitio si es necesario restringir aún más las plantillas permitidas.
>
>La ventaja adicional es que la variable `cq:allowedTemplates` un autor puede actualizar las propiedades en la variable **Avanzadas** de la pestaña **Propiedades de página**. Las demás propiedades de la plantilla no se pueden actualizar mediante la interfaz de usuario (estándar), por lo que sería necesario que un desarrollador mantuviera las reglas y una implementación de código para cada cambio.

#### Limitación de plantillas utilizadas en páginas secundarias {#limiting-templates-used-in-child-pages}

Para limitar las plantillas que se pueden usar para crear páginas secundarias en una página determinada, use la variable `cq:allowedTemplates` propiedad de `jcr:content` de la página para especificar la lista de plantillas que se permitirán como páginas secundarias. Cada valor de la lista debe ser una ruta absoluta a una plantilla para una página secundaria permitida, por ejemplo `/apps/wknd/templates/page-content`.

Puede usar la variable `cq:allowedTemplates` en la plantilla  `jcr:content` para que esta configuración se aplique a todas las páginas recién creadas que utilicen esta plantilla.

Si desea agregar más restricciones, por ejemplo con respecto a la jerarquía de plantillas, puede usar la variable `allowedParents/allowedChildren` propiedades de la plantilla. A continuación, puede especificar explícitamente que las páginas creadas a partir de una plantilla T deben ser páginas principales o secundarias de páginas creadas a partir de una plantilla T.
