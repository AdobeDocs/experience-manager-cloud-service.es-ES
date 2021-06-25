---
title: Configuración de OSGi para Adobe Experience Manager as a Cloud Service
description: 'Configuración de OSGi con valores secretos y valores específicos de entorno '
feature: Implementación
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: b28202a4e133f046b50477c07eb5a37271532c90
workflow-type: tm+mt
source-wordcount: '2927'
ht-degree: 0%

---

# Configuración de OSGi para Adobe Experience Manager as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

[](https://www.osgi.org/) OSGies un elemento fundamental de la pila de tecnología de Adobe Experience Manager (AEM). Se utiliza para controlar los paquetes compuestos de AEM y sus configuraciones.

OSGi proporciona los primitivos estandarizados que permiten construir aplicaciones a partir de componentes pequeños, reutilizables y colaborativos. Estos componentes se pueden componer en una aplicación e implementar. Esto permite una administración sencilla de los paquetes OSGi, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi está contenido en uno de los distintos paquetes. Para obtener más información, consulte la [especificación OSGi](https://www.osgi.org/Specifications/HomePage).

Puede administrar los ajustes de configuración de los componentes de OSGi a través de archivos de configuración que formen parte de un proyecto de código AEM.

## Archivos de configuración OSGi {#osgi-configuration-files}

Los cambios de configuración se definen en los paquetes de código del proyecto AEM (`ui.apps`) como archivos de configuración (`.cfg.json`) en carpetas de configuración específicas del modo de ejecución:

`/apps/example/config.<runmode>`

El formato de los archivos de configuración OSGi se basa en JSON utilizando el formato `.cfg.json` definido por el proyecto Apache Sling.

Las configuraciones de OSGi se dirigen a los componentes de OSGi a través de su Identidad Persistente (PID), que de forma predeterminada es el nombre de clase Java™ del componente OSGi. Por ejemplo, para proporcionar la configuración OSGi para un servicio OSGi implementado por:

`com.example.workflow.impl.ApprovalWorkflow.java`

un archivo de configuración OSGi se define en:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

siguiendo el formato de configuración cfg.json OSGi .

>[!NOTE]
>
>Las versiones anteriores de AEM admitían archivos de configuración OSGi utilizando diferentes formatos de archivo como .cfg., .config y como definiciones de recursos de XML sling:OsgiConfig . Estos formatos se sustituyen por el formato de configuración cfg.json OSGi .

## Resolución del modo de ejecución {#runmode-resolution}

Las configuraciones de OSGi específicas se pueden dirigir a instancias de AEM específicas mediante modos de ejecución. Para utilizar el modo de ejecución, cree carpetas de configuración en `/apps/example` (donde por ejemplo es su nombre de proyecto), con el formato:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Se utiliza cualquier configuración OSGi en dichas carpetas si los modos de ejecución definidos en el nombre de la carpeta de configuración coinciden con los modos de ejecución utilizados por AEM.

Por ejemplo, si AEM utiliza los modos de ejecución author y dev, se aplican los nodos de configuración en `/apps/example/config.author/` y `/apps/example/config.author.dev/`, mientras que los nodos de configuración en `/apps/example/config.publish/` y `/apps/example/config.author.stage/` no se aplican.

Si se aplican varias configuraciones para el mismo PID, se aplica la configuración con el mayor número de modos de ejecución coincidentes.

La granularidad de esta regla se encuentra en el nivel de PID. Esto significa que no puede definir algunas propiedades para el mismo PID en `/apps/example/config.author/` y otras más específicas en `/apps/example/config.author.dev/` para el mismo PID. La configuración con el mayor número de modos de ejecución coincidentes será efectiva para todo el PID.

>[!NOTE]
>
>Una `config.preview` carpeta de configuración OSGI **no puede** declararse de la misma manera que una `config.publish` puede declararse una carpeta. En su lugar, el nivel de vista previa hereda su configuración OSGI de los valores del nivel de publicación.

Al desarrollar localmente, se puede pasar un parámetro de inicio de modo de ejecución para dictar qué configuración de OSGI de modo de ejecución se utiliza.

## Tipos de valores de configuración de OSGi {#types-of-osgi-configuration-values}

Existen tres variedades de valores de configuración OSGi que se pueden usar con Adobe Experience Manager como Cloud Service.

1. **Valores** en línea, que son valores que están codificados en la configuración OSGi y almacenados en Git. Por ejemplo:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Valores secretos**, que son valores que no deben almacenarse en Git por motivos de seguridad. Por ejemplo:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Valores** específicos de entorno, que son valores que varían entre entornos de desarrollo y, por lo tanto, no se pueden definir con precisión mediante el modo de ejecución (ya que hay un solo  `dev` modo de ejecución en Adobe Experience Manager como Cloud Service). Por ejemplo:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Tenga en cuenta que un solo archivo de configuración OSGi puede utilizar cualquier combinación de estos tipos de valores de configuración en conjunto. Por ejemplo:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Cómo elegir el tipo de valor de configuración de OSGi apropiado {#how-to-choose-the-appropriate-osgi-configuration-value-type}

El caso común de OSGi utiliza valores de configuración de OSGi en línea. Las configuraciones específicas del entorno se utilizan solo para casos de uso específicos en los que un valor difiere entre entornos de desarrollo.

![](assets/choose-configuration-value-type_res1.png)

Las configuraciones específicas del entorno amplían las configuraciones OSGi tradicionales definidas estáticamente que contienen valores en línea, lo que proporciona la capacidad de administrar los valores de configuración OSGi externamente a través de la API de Cloud Manager. Es importante comprender cuándo se debe utilizar el enfoque común y tradicional de definir valores en línea y almacenarlos en Git, en lugar de abstraer los valores en configuraciones específicas del entorno.

Las siguientes directrices tratan sobre cuándo utilizar configuraciones específicas de entorno secreto y no secreto:

### Cuándo se deben utilizar los valores de configuración en línea {#when-to-use-inline-configuration-values}

Los valores de las configuraciones en línea se consideran el enfoque estándar y deben utilizarse cuando sea posible. Las configuraciones en línea proporcionan las ventajas de:

* Se mantienen, con un gobierno y un historial de versiones en Git
* Los valores están implícitamente vinculados a las implementaciones de código
* No requieren ninguna consideración o coordinación de despliegue adicional

Siempre que defina un valor de configuración OSGi, comience con valores en línea y seleccione únicamente configuraciones secretas o específicas del entorno si es necesario para el caso de uso.

### Cuándo usar valores de configuración específicos de entornos no secretos {#when-to-use-non-secret-environment-specific-configuration-values}

Utilice únicamente configuraciones específicas del entorno (`$[env:ENV_VAR_NAME]`) para valores de configuración no secretos cuando los valores varían para el nivel de vista previa o varían entre entornos de desarrollo. Esto incluye instancias de desarrollo locales y cualquier entorno de desarrollo de Adobe Experience Manager as a Cloud Service. Aparte de establecer valores únicos para el nivel de vista previa, evite utilizar configuraciones específicas de entorno no secreto para Adobe Experience Manager como escenario de Cloud Service o entornos de producción.

* Utilice únicamente configuraciones específicas de entorno no secreto para valores de configuración que difieran entre el nivel de publicación y vista previa, o para valores que difieran entre entornos de desarrollo, incluidas instancias de desarrollo local.
* Además del escenario en el que el nivel de vista previa necesita variar desde el nivel de publicación, utilice los valores en línea estándar en las configuraciones OSGi para los valores no secretos de fase y producción. En relación con esto, no se recomienda utilizar configuraciones específicas del entorno para facilitar la realización de cambios de configuración en tiempo de ejecución en entornos de fase y producción; estos cambios deben introducirse mediante la administración del código fuente.

### Cuándo utilizar valores de configuración específicos de entornos secretos {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager como Cloud Service requiere el uso de configuraciones específicas del entorno (`$[secret:SECRET_VAR_NAME]`) para cualquier valor de configuración OSGi secreto, como contraseñas, claves de API privadas o cualquier otro valor que no se pueda almacenar en Git por motivos de seguridad.

Utilice configuraciones secretas específicas del entorno para almacenar el valor de secretos en todos los entornos de Adobe Experience Manager as a Cloud Service, incluidos los de fase y producción.

## Creación de configuraciones de OSGi {#creating-sogi-configurations}

Existen dos maneras de crear configuraciones de OSGi, como se describe a continuación. El método anterior se utiliza generalmente para configurar componentes OSGi personalizados que tienen propiedades y valores OSGi conocidos por parte del desarrollador, y el último para componentes OSGi proporcionados por AEM.

### Escritura de configuraciones de OSGi {#writing-osgi-configurations}

Los archivos de configuración OSGi con formato JSON se pueden escribir a mano directamente en el proyecto AEM. A menudo, esta es la forma más rápida de crear configuraciones de OSGi para componentes de OSGi conocidos, y especialmente componentes de OSGi personalizados que han sido diseñados y desarrollados por el mismo desarrollador que define las configuraciones. Este método también se puede utilizar para copiar/pegar y actualizar configuraciones para el mismo componente OSGi en varias carpetas de modo de ejecución.

1. En su IDE, abra el proyecto `ui.apps`, busque o cree la carpeta de configuración (`/apps/.../config.<runmode>`) que se dirija a los modos de ejecución que la nueva configuración de OSGi debe aplicar
1. En esta carpeta de configuración, cree un nuevo archivo `<PID>.cfg.json`. El PID es la identidad persistente del componente OSGi y suele ser el nombre de clase completo de la implementación del componente OSGi. Por ejemplo:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
Tenga en cuenta que los nombres de archivo de fábrica de configuración OSGi utilizan la convención de  `<PID>-<factory-name>.cfg.json` nomenclatura
1. Abra el nuevo archivo `.cfg.json` y defina las combinaciones clave/valor para los pares de propiedad y valor OSGi, siguiendo el formato de configuración [JSON OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. Guarde los cambios en el nuevo archivo `.cfg.json`
1. Añadir y confirmar el nuevo archivo de configuración OSGi en Git

### Generación de configuraciones de OSGi mediante el inicio rápido AEM SDK {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

La consola web AEM del SDK de AEM Quickstart Jar se puede utilizar para configurar componentes OSGi y exportar configuraciones de OSGi como JSON. Esto resulta útil para configurar componentes OSGi proporcionados por AEM, cuyas propiedades OSGi y sus formatos de valor pueden no ser bien entendidos por el desarrollador que define las configuraciones OSGi en el proyecto AEM.

>[!NOTE]
>
>La interfaz de usuario de configuración de la Consola Web AEM escribe `.cfg.json` archivos en el repositorio. Por lo tanto, tenga en cuenta esto para evitar un comportamiento inesperado potencial durante el desarrollo local, cuando las configuraciones de OSGi definidas por el proyecto AEM pueden diferir de las configuraciones generadas.

1. Inicie sesión en la consola web AEM del SDK de AEM Quickstart Jar como usuario administrador
1. Vaya a OSGi > Configuración
1. Para configurar, busque el componente OSGi y pulse su título para editar
   ![Configuración de OSGi](./assets/configuring-osgi/configuration.png)
1. Edite los valores de las propiedades de configuración de OSGi a través de la interfaz de usuario web según sea necesario
1. Registre la identidad persistente (PID) en un lugar seguro. Esto se utiliza más adelante para generar el JSON de configuración OSGi
1. Toque Guardar
1. Vaya a OSGi > Impresora de configuración del instalador OSGi
1. Pegue en el PID copiado en el paso 5, asegúrese de que el Formato de serialización está establecido en &quot;OSGi Configurator JSON&quot;
1. Toque Imprimir
1. La configuración OSGi en formato JSON se mostrará en la sección Propiedades de configuración serializadas
   ![Impresora de configuración del instalador OSGi](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. En su IDE, abra el proyecto `ui.apps`, busque o cree la carpeta de configuración (`/apps/.../config.<runmode>`) que se dirija a los modos de ejecución que debe aplicar la nueva configuración de OSGi.
1. En esta carpeta de configuración, cree un nuevo archivo `<PID>.cfg.json`. El PID es el mismo valor que el del paso 5.
1. Pegue las Propiedades de configuración serializadas del paso 10 en el archivo `.cfg.json`.
1. Guarde los cambios en el nuevo archivo `.cfg.json`.
1. Añada y confirme su nuevo archivo de configuración OSGi en Git.


## Formatos de propiedades de configuración de OSGi {#osgi-configuration-property-formats}

### Valores en línea {#inline-values}

Los valores en línea tienen el formato de pares de nombre-valor estándar, siguiendo la sintaxis estándar JSON. Por ejemplo:

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### Valores de configuración específicos de entorno {#environment-specific-configuration-values}

La configuración OSGi debe asignar un marcador de posición para la variable que se pretende definir por entorno:

```
use $[env:ENV_VAR_NAME]
```

Los clientes solo deben utilizar esta técnica para las propiedades de configuración OSGI relacionadas con su código personalizado; no debe utilizarse para anular la configuración OSGI definida por Adobe.

>[!NOTE]
>
>Los marcadores de posición no se pueden usar en [instrucciones de informe](/help/implementing/deploying/overview.md#repoinit).

### Valores de configuración secreta {#secret-configuration-values}

La configuración OSGi debe asignar un marcador de posición para el secreto que se pretende definir por entorno:

```
use $[secret:SECRET_VAR_NAME]
```

### Asignación de nombres a variables {#variable-naming}

Lo siguiente se aplica a los valores de configuración secreta y específica del entorno.

Los nombres de las variables deben seguir las siguientes reglas:

* Longitud mínima: 2
* Longitud máxima: 100
* Debe coincidir con regex: `[a-zA-Z_][a-zA-Z_0-9]*`

Los valores de las variables no deben superar los 2048 caracteres.

>[!NOTE]
>
>Los nombres de variables con el prefijo `INTERNAL_` se reservan mediante Adobe. Se ignorará cualquier variable configurada por el cliente que comience con este prefijo.

### Valores predeterminados {#default-values}

Lo siguiente se aplica a los valores de configuración secreta y específica del entorno.

Si no se establece ningún valor por entorno, durante la ejecución el marcador de posición no se reemplaza y se deja en su lugar porque no se produjo ninguna interpolación. Para evitarlo, se puede proporcionar un valor predeterminado como parte del marcador de posición con la siguiente sintaxis:

```
$[env:ENV_VAR_NAME;default=<value>]
```

Con un valor predeterminado proporcionado, el marcador de posición se reemplaza por el valor por entorno si se proporciona o por el valor predeterminado proporcionado.

### Desarrollo local {#local-development}

Lo siguiente se aplica a los valores de configuración secreta y específica del entorno.

Las variables se pueden definir en el entorno local para que la AEM local las recopile durante la ejecución. Por ejemplo, en Linux®:

```bash
export ENV_VAR_NAME=my_value
```

Se recomienda escribir una secuencia de comandos bash simple que establezca las variables de entorno utilizadas en las configuraciones y que la ejecute antes de comenzar el AEM. Herramientas como [https://direnv.net/](https://direnv.net/) ayudan a simplificar este enfoque. Según el tipo de valores, se pueden registrar en la administración del código fuente si todos los usuarios pueden compartirlos.

Los valores de los secretos se leen a partir de archivos. Por lo tanto, para cada marcador de posición que utilice un secreto se debe crear un archivo de texto que contenga el valor secreto.

Por ejemplo, si se utiliza `$[secret:server_password]`, se debe crear un archivo de texto denominado **server_password**. Todos estos archivos secretos deben almacenarse en el mismo directorio y la propiedad `org.apache.felix.configadmin.plugin.interpolation.secretsdir` del marco debe configurarse con ese directorio local.

### Configuración de autor frente a publicación {#author-vs-publish-configuration}

Si una propiedad OSGI requiere valores diferentes para autor y publicación:

* Se deben utilizar carpetas OSGi separadas `config.author` y `config.publish`, tal como se describe en la sección [Resolución del modo de ejecución](#runmode-resolution).
* Hay dos opciones para crear los nombres de variables independientes que deben usarse:
   * la primera opción, que se recomienda: en todas las carpetas OSGI (como `config.author` y `config.publish`) declaradas para definir valores diferentes, utilice el mismo nombre de variable. Por ejemplo
      `$[env:ENV_VAR_NAME;default=<value>]`, donde el valor predeterminado corresponde al valor predeterminado de ese nivel (autor o publicación). Al configurar la variable de entorno mediante [Cloud Manager API](#cloud-manager-api-format-for-setting-properties) o a través de un cliente, diferencie entre los niveles mediante el parámetro &quot;servicio&quot; como se describe en esta [documentación de referencia de API](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables). El parámetro &quot;service&quot; enlazará el valor de la variable al nivel OSGI apropiado. Puede ser &quot;autor&quot;, &quot;publicación&quot; o &quot;previsualización&quot;.
   * la segunda opción, que es declarar variables distintas con un prefijo como `author_<samevariablename>` y `publish_<samevariablename>`

### Ejemplos de configuración {#configuration-examples}

En los ejemplos siguientes, supongamos que hay tres entornos dev, además de los entornos stage y prod.

**Ejemplo 1**

La intención es que el valor de la propiedad OSGI `my_var1` sea el mismo para stage y prod, pero diferente para cada uno de los tres entornos de desarrollo.

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
{ 
 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

**Ejemplo 2**

La intención es que el valor de la propiedad OSGI `my_var1` difiera para stage, prod y para cada uno de los tres entornos de desarrollo. Por lo tanto, se debe llamar a la API de Cloud Manager para establecer el valor de `my_var1` para cada contenedor de desarrollo.

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
config.stage
</td>
<td>
<pre>
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ 
 "my_var1": "val2",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

**Ejemplo 3**

La intención es que el valor de la propiedad OSGi `my_var1` sea el mismo para stage, production y solo uno de los entornos de desarrollo, pero que difiera para los otros dos entornos de desarrollo. En este caso, se debe llamar a la API de Cloud Manager para que establezca el valor de `my_var1` para cada entorno de desarrollo, incluido el entorno de desarrollo que debe tener el mismo valor que stage y production. No heredará el valor establecido en la carpeta **config**.

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
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

Otra manera de lograr esto sería establecer un valor predeterminado para el token de reemplazo en la carpeta config.dev de manera que sea el mismo valor que en la carpeta **config**.

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
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1": "$[env:my_var1;default=val1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

## Formato de API de Cloud Manager para la configuración de propiedades {#cloud-manager-api-format-for-setting-properties}

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md) sobre cómo se debe configurar la API.
>[!NOTE]
>
>Asegúrese de que la API de Cloud Manager utilizada haya asignado la función &quot;Administrador de implementación - Cloud Service&quot;. Otras funciones no pueden ejecutar todos los comandos siguientes.

### Configuración de valores mediante API {#setting-values-via-api}

Llamar a la API implementa las nuevas variables y valores en un entorno de Cloud, de forma similar a una canalización de implementación de código de cliente típica. Los servicios de autor y publicación se reiniciarán y harán referencia a los nuevos valores, normalmente tardando unos minutos.

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

>[!NOTE]
>Las variables predeterminadas no se establecen mediante API, sino en la propiedad OSGi misma.
>
>Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) para obtener más información.

### Obtención de valores mediante API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables) para obtener más información.

### Eliminación de valores mediante API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Para eliminar una variable, inclúyala con un valor vacío.

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) para obtener más información.

### Obtención de valores mediante la línea de comandos {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### Configuración de valores mediante la línea de comandos {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### Eliminación de valores mediante la línea de comandos {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>Consulte [esta página](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obtener más información sobre cómo configurar valores utilizando el complemento Cloud Manager para la CLI de Adobe I/O.

### Número de variables {#number-of-variables}

Se pueden declarar hasta 200 variables por entorno.

## Consideraciones de implementación para valores de configuración secretos y específicos de entorno {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Debido a que los valores de configuración específicos de entorno y secreto existen fuera de Git y, por lo tanto, no forman parte de los mecanismos formales de implementación de Adobe Experience Manager as a Cloud Service, el cliente debe administrar, administrar e integrar en Adobe Experience Manager as a Cloud Service.

Como se ha mencionado anteriormente, la llamada a la API implementa las nuevas variables y valores en los entornos de Cloud, de forma similar a una canalización de implementación de código de cliente típica. Los servicios de autor y publicación se reiniciarán y harán referencia a los nuevos valores, normalmente tardando unos minutos. Tenga en cuenta que las puertas de calidad y las pruebas que ejecuta Cloud Manager durante una implementación de código normal no se realizan durante este proceso.

Normalmente, los clientes llaman a la API para establecer variables de entorno antes de implementar un código que dependa de ellas en Cloud Manager. En algunas situaciones, es posible que se desee modificar una variable existente después de que el código ya se haya implementado.

>[!NOTE]
>
>Es posible que la API no tenga éxito cuando se está utilizando una canalización, ya sea una actualización de AEM o una implementación de cliente, dependiendo de qué parte de la canalización de extremo a extremo se esté ejecutando en ese momento. La respuesta de error indicará que la solicitud no se realizó correctamente, aunque no indicará el motivo específico.

Puede haber escenarios en los que una implementación programada del código de cliente dependa de variables existentes para tener nuevos valores, lo que no sería apropiado con el código actual. Si esto supone un problema, se recomienda realizar modificaciones de variables de forma aditiva. Para ello, cree nuevos nombres de variables en lugar de cambiar el valor de variables antiguas, de modo que el código antiguo nunca haga referencia al nuevo valor. A continuación, cuando la nueva versión del cliente parezca estable, puede optar por eliminar los valores más antiguos.

Del mismo modo, dado que los valores de una variable no tienen versiones, una reversión del código podría hacer que haga referencia a valores más nuevos que causen problemas. La estrategia de variables aditivas mencionada anteriormente también sería útil aquí.

Esta estrategia de variable aditiva también es útil para escenarios de recuperación ante desastres donde si se necesita reimplementar el código de varios días antes de que se necesite, los nombres y valores de las variables a los que hace referencia seguirán intactos. Esto se basa en una estrategia en la que un cliente espera unos días antes de eliminar esas variables antiguas; de lo contrario, el código anterior no tendría las variables adecuadas a las que hacer referencia.
