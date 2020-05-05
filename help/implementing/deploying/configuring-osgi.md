---
title: Configuración de OSGi para AEM como servicio de nube
description: 'Configuración de OSGi con valores secretos y valores específicos de Entorno '
translation-type: tm+mt
source-git-commit: 743a8b4c971bf1d3f22ef12b464c9bb0158d96c0

---


# Configuraciones de OSGi {#osgi-configurations}

[OSGi](https://www.osgi.org/) es un elemento fundamental en la pila de tecnología de Adobe Experience Manager (AEM). Se utiliza para controlar los paquetes compuestos de AEM y sus configuraciones.

OSGi proporciona los primitivos estandarizados que permiten construir aplicaciones a partir de componentes pequeños, reutilizables y de colaboración. Estos componentes se pueden componer en una aplicación y se pueden implementar. Esto permite administrar fácilmente los paquetes OSGi, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi está contenido en uno de los distintos paquetes. Para obtener más información, consulte la especificación [OSGi](https://www.osgi.org/Specifications/HomePage).

Puede administrar la configuración de los componentes de OSGi mediante archivos de configuración que formen parte de un proyecto de código de AEM.

## Archivos de configuración OSGi {#osgi-configuration-files}

Los cambios de configuración se definen en los paquetes de código (`ui.apps`) del proyecto AEM como archivos de configuración (`.cfg.json`) en carpetas de configuración específicas del modo de ejecución:

`/apps/example/config.<runmode>`

El formato de los archivos de configuración OSGi se basa en JSON utilizando el `.cfg.json` formato definido por el proyecto Apache Sling.

Las configuraciones de OSGi destinatario los componentes de OSGi a través de su Identidad persistente (PID), que se establece de forma predeterminada en el nombre de clase Java del componente OSGi. Por ejemplo, para proporcionar la configuración OSGi para un servicio OSGi implementado por:

`com.example.workflow.impl.ApprovalWorkflow.java`

un archivo de configuración OSGi se define en:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

siguiendo el formato [de configuración]cfg.json OSGi (siguiendo el formato de configuración cfg.json OSGi).

> [!NOTE]
>
> Las versiones anteriores de AEM admitían archivos de configuración OSGi utilizando diferentes formatos de archivo como .cfg., .config y como definiciones de recursos XML sling:OsgiConfig. Estos formatos se sustituyen por el formato de configuración de OSGi cfg.json.

## Resolución de modo de ejecución {#runmode-resolution}

Las configuraciones de OSGi específicas se pueden dirigir a instancias específicas de AEM mediante modos de ejecución. Para utilizar el modo de ejecución, cree carpetas de configuración en `/apps/example` (donde el ejemplo es el nombre del proyecto), en el formato:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Se utilizará cualquier configuración OSGi en dichas carpetas si los modos de ejecución definidos en el nombre de la carpeta de configuración coinciden con los modos de ejecución utilizados por AEM.

Por ejemplo, si AEM utiliza el autor y el desarrollador de los modos de ejecución, se aplicarán los nodos de configuración en `/apps/example/config.author/` y `/apps/example/config.author.dev/` , mientras que los nodos de configuración en `/apps/example/config.publish/` y no `/apps/example/config.author.stage/` se aplicarán.

Si se aplican varias configuraciones para el mismo PID, se aplica la configuración con el mayor número de modos de ejecución coincidentes.

La granularidad de esta regla se encuentra en un nivel PID. Esto significa que no puede definir algunas propiedades para el mismo PID en `/apps/example/config.author/` y otras más específicas en `/apps/example/config.author.dev/` para el mismo PID.  La configuración con el mayor número de modos de ejecución coincidentes será efectiva para todo el PID.

Cuando se desarrolla localmente, se puede pasar un parámetro de inicio runmode para dictar qué configuración OSGI de modo de ejecución se utilizará.

## Tipos de valores de configuración OSGi {#types-of-osgi-configuration-values}

Existen tres variedades de valores de configuración OSGi que se pueden utilizar con AEM como un servicio en la nube.

1. **Valores** en línea, que son valores que están codificados en la configuración OSGi y almacenados en Git. Por ejemplo:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Valores** secretos, que son valores que no deben almacenarse en Git por motivos de seguridad. Por ejemplo:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Los valores** específicos de Entorno, que son valores que varían entre los entornos de desarrollo, y por lo tanto no se pueden definir correctamente como objetivos en el modo de ejecución (ya que hay un solo `dev` modo de ejecución en AEM como servicio de nube). Por ejemplo:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Tenga en cuenta que un solo archivo de configuración OSGi puede utilizar cualquier combinación de estos tipos de valores de configuración en forma conjunta. Por ejemplo:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Cómo elegir el tipo de valor de configuración de OSGi adecuado {#how-to-choose-the-appropriate-osgi-configuration-value-type}

El caso común para OSGi utiliza valores de configuración OSGi en línea. Las configuraciones específicas del Entorno se utilizan solamente para casos de uso específicos en los que un valor difiere entre entornos de desarrollo.

![](assets/choose-configuration-value-type.png)

Las configuraciones específicas de Entorno amplían las configuraciones OSGi tradicionales y definidas estáticamente que contienen valores en línea, lo que permite administrar los valores de configuración OSGi externamente mediante la API de Cloud Manager. Es importante comprender cuándo se debe utilizar el enfoque común y tradicional de definir valores en línea y almacenarlos en Git, en lugar de abstraer los valores en configuraciones específicas del entorno.

La siguiente guía indica cuándo utilizar configuraciones no secretas y específicas de entornos secretos:

### Cuándo utilizar los valores de configuración en línea {#when-to-use-inline-configuration-values}

Los valores de configuración en línea se consideran el método estándar y deben utilizarse cuando sea posible. Las configuraciones en línea proporcionan los beneficios de:

* Se mantienen, con un historial de gobernanza y versiones en Git
* Los valores están implícitamente vinculados a implementaciones de código
* No requieren ninguna consideración o coordinación de despliegue adicional

Siempre que se define un valor de configuración OSGi, se realiza un inicio con valores en línea, cualquier configuración sólo selecciona configuraciones secretas o específicas de entorno si es necesario para el caso de uso.

### Cuándo utilizar valores de configuración no secretos específicos del Entorno {#when-to-use-non-secret-environment-specific-configuration-values}

Utilice únicamente configuraciones específicas de entorno (`$[env:ENV_VAR_NAME]`) para valores de configuración no secretos cuando los valores varíen entre los entornos de desarrollo. Esto incluye instancias de desarrollo local y cualquier AEM como entornos de desarrollo de servicios en la nube. Evite utilizar configuraciones no secretas específicas de entorno para AEM como una etapa de servicio en la nube o entornos de producción.

* Utilice únicamente configuraciones no secretas específicas de entorno para valores de configuración que difieran entre entornos de desarrollo, incluidas las instancias de desarrollo local.
* En su lugar, utilice los valores en línea estándar en las configuraciones OSGi para valores no secretos de fase y producción.  En relación con esto, no se recomienda utilizar configuraciones específicas de entorno para facilitar la realización de cambios de configuración en tiempo de ejecución a entornos de fase y producción; estos cambios deben introducirse mediante la administración del código fuente.

### Cuándo utilizar valores de configuración específicos de entorno secreto {#when-to-use-secret-environment-specific-configuration-values}

AEM como servicio de nube requiere el uso de configuraciones específicas de entorno (`$[secret:SECRET_VAR_NAME]`) para cualquier valor de configuración OSGi secreto, como contraseñas, claves de API privadas o cualquier otro valor que no pueda almacenarse en Git por motivos de seguridad.

Utilice configuraciones secretas específicas del entorno para almacenar el valor de los secretos en todos los entornos de AEM como servicios en la nube, incluidos el escenario y la producción.

### Añadir una nueva configuración en el repositorio {#adding-a-new-configuration-to-the-repository}

#### Qué necesita saber {#what-you-need-to-know}

Para agregar una nueva configuración al repositorio, debe saber lo siguiente:

1. Identidad **persistente** (PID) del servicio.

   Haga referencia al campo **Configuraciones** de la consola web. El nombre se muestra entre corchetes después del nombre del paquete (o en Información **de** configuración hacia la parte inferior de la página).

   Por ejemplo, cree un nodo `com.day.cq.wcm.core.impl.VersionManagerImpl.` para configurar **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Indica si se requiere un modo de ejecución específico. Cree la carpeta:

   * `config` - para todos los modos de ejecución
   * `config.author` - para el entorno del autor
   * `config.publish` - para el entorno de publicación
   * `config.<run-mode>` - según proceda

1. Indica si es necesaria una **configuración** o una configuración **de fábrica** .
1. Parámetros individuales que se van a configurar; incluyendo cualquier definición de parámetro existente que deba volver a crearse.

   Haga referencia al campo de parámetro individual en la consola web. El nombre se muestra entre corchetes para cada parámetro.

   Por ejemplo, crear una propiedad
   `versionmanager.createVersionOnActivation` para configurar **Crear versión en la Activación**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. ¿Ya existe una configuración en `/libs`? Para lista de todas las configuraciones de su instancia, utilice la herramienta de **Consulta** de CRXDE Lite para enviar la siguiente consulta SQL:

   `select * from sling:OsgiConfig`

   Si es así, esta configuración se puede copiar en ` /apps/<yourProject>/`y, a continuación, personalizar en la nueva ubicación.

## Creación de la configuración en el repositorio {#creating-the-configuration-in-the-repository}

Para agregar la nueva configuración al repositorio:

1. Utilice CRXDE Lite para desplazarse a:

   ` /apps/<yourProject>`

1. Si aún no existe, cree la `config` carpeta ( `sling:Folder`):

   * `config` - aplicable a todos los modos de ejecución
   * `config.<run-mode>` - específica para un modo de ejecución particular

1. En esta carpeta, cree un nodo:

   * Tipo: `sling:OsgiConfig`
   * Nombre: la identidad persistente (PID);

      por ejemplo, el uso de AEM WCM Version Manager `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >Al realizar una configuración de fábrica, anexe `-<identifier>` al nombre.
   >
   >Como en: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Donde `<identifier>` se reemplaza por texto libre que (debe) introducir para identificar la instancia (no puede omitir esta información); por ejemplo:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Para cada parámetro que desee configurar, cree una propiedad en este nodo:

   * Nombre: el nombre del parámetro como se muestra en la consola web; el nombre se muestra entre corchetes al final de la descripción del campo. Por ejemplo, para `Create Version on Activation` uso `versionmanager.createVersionOnActivation`
   * Tipo: según proceda.
   * Valor: según sea necesario.
   Solo necesita crear propiedades para los parámetros que desea configurar; otros seguirán teniendo los valores predeterminados establecidos por AEM.

1. Guarde todos los cambios.

   Los cambios se aplican en cuanto se actualiza el nodo reiniciando el servicio (como sucede con los cambios realizados en la consola web).

>[!CAUTION]
>
>No debe cambiar nada en la `/libs` ruta.

>[!CAUTION]
>
>La ruta completa de una configuración debe ser correcta para que se lea al inicio.


## Formato de propiedad de configuración en el control de código fuente {#configuration-property-format-in-source-control}

La creación de una nueva propiedad de configuración OSGI se describe en la sección anterior para [Añadir una nueva configuración al repositorio](#creating-the-configuration-in-the-repository) . Siga estos pasos y modifique la sintaxis como se describe en las subsecciones siguientes:

### Valores en línea {#inline-values}

Como es de esperar, los valores en línea tienen el formato de pares de nombre-valor estándar, siguiendo la sintaxis estándar JSON. Por ejemplo:

```json
 {

 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500

}
```

### Valores de configuración específicos de Entorno {#environment-specific-configuration-values}

La configuración de OSGi debe asignar un marcador de posición para la variable que se va a definir por entorno:

```
use $[env:ENV_VAR_NAME]
```

Los clientes solo deben utilizar esta técnica para las propiedades de configuración OSGI relacionadas con su código personalizado; no debe utilizarse para anular la configuración OSGI definida por Adobe.

### Valores de configuración secreta {#secret-configuration-values}

La configuración OSGi debe asignar un marcador de posición para el secreto que se va a definir por entorno:

```
use $[secret:SECRET_VAR_NAME]
```

### Asignación de nombres a variables {#variable-naming}

Lo siguiente se aplica tanto a los valores de configuración secreta como a los específicos del entorno.

Los nombres de las variables deben seguir las siguientes reglas:

* longitud mínima: 2
* longitud máxima: 100
* debe coincidir con regex: `[a-zA-Z_][a-zA-Z_0-9]*`

Los valores de las variables no deben superar los 2048 caracteres.

### Valores predeterminados {#default-values}

Lo siguiente se aplica tanto a los valores de configuración secreta como a los específicos del entorno.

Si no se establece ningún valor por entorno, en tiempo de ejecución el marcador de posición no se reemplazará ni se dejará en su lugar, ya que no se produjo ninguna interpolación. Para evitarlo, se puede proporcionar un valor predeterminado como parte del marcador de posición con la siguiente sintaxis:

```
$[env:ENV_VAR_NAME;default=<value>]
```

Con un valor predeterminado proporcionado, el marcador de posición se reemplazará por el valor por entorno, si se proporciona, o por el valor predeterminado proporcionado.

### Desarrollo local {#local-development}

Lo siguiente se aplica tanto a los valores de configuración secreta como a los específicos del entorno.

Las variables se pueden definir en el entorno local para que el AEM local las recoja durante la ejecución. Por ejemplo, en Linux:

```bash
export ENV_VAR_NAME=my_value
```

Se recomienda escribir una secuencia de comandos bash simple que defina las variables de entorno utilizadas en las configuraciones y que la ejecute antes de iniciar AEM. Herramientas como [https://direnv.net/](https://direnv.net/) ayudan a simplificar este enfoque. Según el tipo de valores, se pueden registrar en la administración de código fuente, si todos los usuarios pueden compartirlos.

Los valores de los secretos se leen de los archivos. Por lo tanto, para cada marcador de posición que utilice un secreto debe crearse un archivo de texto que contenga el valor secreto.

Por ejemplo, si `$[secret:server_password]` se utiliza, se debe crear un archivo de texto llamado **server_password** . Todos estos archivos secretos deben almacenarse en el mismo directorio y la propiedad framework `org.apache.felix.configadmin.plugin.interpolation.secretsdir` debe configurarse con ese directorio local.

### Configuración de creación vs. publicación {#author-vs-publish-configuration}

Si una propiedad OSGI requiere valores diferentes para el autor y para la publicación:

* se deben utilizar carpetas separadas `config.author` y `config.publish` OSGi, tal como se describe en la sección [Resolución del](#runmode-resolution)modo de ejecución.
* se deben utilizar nombres de variables independientes. Se recomienda utilizar un prefijo como author_<variablename> y publish_<variablename> donde los nombres de las variables son los mismos

### Ejemplos de configuración {#configuration-examples}

En los ejemplos siguientes, supongamos que hay tres entornos dev, además de los entornos de etapa y prod.

**Ejemplo 1**

La intención es que el valor de la propiedad OSGI `my_var1` sea el mismo para stage y prod, pero difiere para cada uno de los 3 entornos dev.

<table>
<tr>
<td>
<b>Carpeta</b>
</td>
<td>
<b>Contenido de myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**Ejemplo 2**

La intención es que el valor de la propiedad OSGI `my_var1` difiera para stage, prod y para cada uno de los 3 entornos dev. Por lo tanto, será necesario llamar a la API de Cloud Manager para establecer el valor `my_var1` para cada env de desarrollo.

