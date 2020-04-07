---
title: Registro
description: Obtenga información sobre cómo configurar los parámetros globales para el servicio de registro central, la configuración específica para los servicios individuales o cómo solicitar el registro de datos.
translation-type: tm+mt
source-git-commit: 73813dd87e3eebfe26673640125ea64916e14789

---


# Registro{#logging}

AEM como servicio de nube le oferta la posibilidad de configurar:

* parámetros globales para el servicio de registro central
* registro de datos de solicitud; una configuración de registro especializada para información de solicitud
* ajustes específicos para los servicios individuales; por ejemplo, un archivo de registro y un formato individuales para los mensajes de registro

Para el desarrollo local, las entradas de registro se escriben en los archivos locales de la `/crx-quickstart/logs` carpeta.

En los entornos de Cloud, los desarrolladores pueden descargar registros a través de Cloud Manager o utilizar una herramienta de línea de comandos para reducir los registros.

>[!NOTE]
>
>El inicio de sesión en AEM como servicio de nube se basa en los principios de Sling. Consulte [Registro de Sling](https://sling.apache.org/site/logging.html) para obtener más información.

## Registro global {#global-logging}

[La Configuración](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) de registro de Apache Sling se utiliza para configurar el registrador raíz. Esto define la configuración global para iniciar sesión en AEM como un servicio de nube:

* el nivel de registro
* la ubicación del archivo de registro central
* el número de versiones que deben conservarse
* rotación de versiones; bien el tamaño máximo o bien un intervalo de tiempo
* el formato que se utilizará al escribir los mensajes de registro

## Registros y escritores para servicios individuales {#loggers-and-writers-for-individual-services}

Además de la configuración de registro global, AEM como servicio de nube le permite configurar opciones específicas para un servicio individual:

* el nivel de registro específico
* la ubicación del archivo de registro individual
* el número de versiones que deben conservarse
* rotación de versiones; bien el tamaño máximo o el intervalo de tiempo
* el formato que se utilizará al escribir los mensajes de registro
* el registrador (el servicio OSGi que proporciona los mensajes de registro)

Esto le permite canal los mensajes de registro de un único servicio en un archivo independiente. Esto puede resultar especialmente útil durante el desarrollo o la realización de pruebas; por ejemplo, cuando necesita un nivel de registro mayor para un servicio específico.

AEM como servicio de nube utiliza lo siguiente para escribir mensajes de registro en el archivo:

1. Un servicio **** OSGi (registrador) escribe un mensaje de registro.
1. Un **registrador** toma este mensaje y lo formatea según sus especificaciones.
1. Un **escritor** de registro escribe todos estos mensajes en el archivo físico que ha definido.

Estos elementos están vinculados por los siguientes parámetros para los elementos apropiados:

* **Registrador (registrador)**

   Defina los servicios que generan los mensajes.

* **Archivo de registro (registrador)**

   Defina el archivo físico para almacenar los mensajes de registro.

   Se utiliza para vincular un registrador con un grabador de registros. El valor debe ser idéntico al mismo parámetro en la configuración del Escritor de registros para la conexión que se va a realizar.

* **Archivo de registro (escritor de registro)**

   Defina el archivo físico en el que se escribirán los mensajes de registro.

   Debe ser idéntico al mismo parámetro en la configuración del Escritor de registro, o no se realizará la coincidencia. Si no hay coincidencia, se creará un Writer implícito con la configuración predeterminada (rotación diaria del registro).

### Registradores y escritores estándar {#standard-loggers-and-writers}

Algunos registradores y escritores se incluyen en un AEM estándar como instalación de Cloud Service.

El primero es un caso especial, ya que controla tanto los archivos `request.log` como los `access.log` :

* El Registrador:

   * Registrador De Datos De Solicitud Personalizable Apache Sling

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Escriba mensajes sobre el contenido de la solicitud en `request.log`.

* Vínculos a:

   * Registrador de solicitudes Apache Sling

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Escribe los mensajes en `request.log` o `access.log`.

Se pueden personalizar si es necesario, aunque la configuración estándar es adecuada para la mayoría de las instalaciones.

Los otros pares siguen la configuración estándar:

* El Registrador:

   * Configuración del registrador de Apache Sling

      (org.apache.sling.commons.log.LogManager.Factory.config)

   * Escribe `Information` mensajes en `logs/error.log`.

* Vínculos al escritor:

   * Configuración del escritor de registro de Apache Sling

      (org.apache.sling.commons.log.LogManager.Factory.writer)

* El Registrador:

   * Configuración del registrador de registros Sling de Apache(org.apache.sling.commons.log.LogManager.Factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Escribe `Warning` mensajes en `../logs/error.log` para el servicio `org.apache.pdfbox`.

* No se vincula a un escritor específico, por lo que creará y utilizará un escritor implícito con la configuración predeterminada (rotación diaria del registro).

## Configuración del nivel de registro {#setting-the-log-level}

Para cambiar los niveles de registro de los entornos de nube, se debe modificar la configuración de OSGI de registro de Sling, seguida de una reimplementación completa. Dado que esto no es instantáneo, tenga cuidado de habilitar los registros detallados en entornos de producción que reciben mucho tráfico. En el futuro, es posible que haya mecanismos para cambiar más rápidamente el nivel de registro.

> [!NOTE]
> 
> Para realizar los cambios de configuración que se indican a continuación, debe crearlos en un entorno de desarrollo local y, a continuación, colocarlos en una instancia de AEM como servicio de nube. Para obtener más información sobre cómo hacerlo, consulte [Implementación en AEM como un servicio](/help/implementing/deploying/overview.md)de nube.

### Activación del nivel de registro DEBUG {#activating-the-debug-log-level}

> [!WARNING]
>
> Al activar el nivel de registro DEBUG globalmente, se generará una gran cantidad de información que será difícil de pasar. Se recomienda habilitarlo solo para los servicios que requieren depuración. Para obtener más información, consulte [Registros y escritores de servicios](logging.md#loggers-and-writers-for-individual-services)individuales.

El nivel de registro predeterminado es INFO, es decir, los mensajes DEBUG no se registran.
Para activar el nivel de registro DEBUG, establezca la variable

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

para depurar. No deje el registro en el nivel de registro DEBUG más tiempo del necesario, ya que genera muchos registros.
Una línea en el archivo de depuración normalmente inicio con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

Los niveles de registro son los siguientes:

| 0 | Error fatal | Error en la acción y el instalador no puede continuar. |
|---|---|---|
| 1 | Error | Error en la acción. La instalación continúa, pero una parte de CRX no se instaló correctamente y no funcionará. |
| 2 | Advertencia | La acción se ha realizado correctamente, pero se han encontrado problemas. CRX puede funcionar correctamente o no. |
| 3 | Información | La acción se ha realizado correctamente. |

### Creación de sus propios registradores y escritores {#creating-your-own-loggers-and-writers}

Puede definir su propio par Logger/Writer:

1. Cree una nueva instancia de la Configuración de fábrica [Apache Sling Logging Logger Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

   1. Especifique el archivo de registro.
   1. Especifique el registrador.
   1. Configure los demás parámetros según sea necesario.

1. Cree una nueva instancia de la Configuración de fábrica [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

   1. Especifique el archivo de registro: debe coincidir con el especificado para el registrador.
   1. Configure los demás parámetros según sea necesario.

### Crear un archivo de registro personalizado {#create-a-custom-log-file}

>[!NOTE]
>
>Al trabajar con Adobe Experience Manager, existen varios métodos para administrar la configuración de dichos servicios.

En determinadas circunstancias, es posible que desee crear un archivo de registro personalizado con un nivel de registro diferente. Puede hacerlo en el repositorio:

1. Si aún no existe, cree una nueva carpeta de configuración ( `sling:Folder`) para el proyecto `/apps/<*project-name*>/config`.
1. En `/apps/<*project-name*>/config`, cree un nodo para la nueva configuración del registrador de registros de Sling de Apache:

   * Nombre: `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (ya que es un Logger)

      Donde `<*identifier*>` se reemplaza por texto libre que debe introducir para identificar la instancia (no puede omitir esta información).

      Por ejemplo, `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * Tipo: `sling:OsgiConfig`
   >[!NOTE]
   >
   >Aunque no es un requisito técnico, es aconsejable hacer `<*identifier*>` único.

1. Establezca las siguientes propiedades en este nodo:

   * Nombre: `org.apache.sling.commons.log.file`

      Tipo: Cadena

      Valor: especifique el archivo de registro; por ejemplo, `logs/myLogFile.log`

   * Nombre: `org.apache.sling.commons.log.names`

      Tipo: Cadena[] (String + Multi)

      Valor: especifique los servicios OSGi para los que el registrador debe registrar los mensajes; por ejemplo, todo lo siguiente:

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * Nombre: `org.apache.sling.commons.log.level`

      Tipo: Cadena

      Valor: especifique el nivel de registro requerido ( `debug`, `info`, `warn` o `error`); por ejemplo `debug`

   * Configure los demás parámetros según sea necesario:

      * Nombre: `org.apache.sling.commons.log.pattern`

         Tipo: `String`

         Valor: especifique el patrón del mensaje de registro según sea necesario; por ejemplo,

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` admite hasta seis argumentos.

   >{0} Marca de tiempo del tipo `java.util.Date`
   >
   >{1} el marcador de registro{2} el nombre del subproceso actual{3} el nombre del registrador{4} el nivel de registro{5} el mensaje de registro

   >Si la llamada de registro incluye un `Throwable` seguimiento de pila se anexa al mensaje.

   >[!CAUTION]
   org.apache.sling.commons.log.names debe tener un valor.

   >[!NOTE]
   Las rutas de escritura de registros son relativas a la `crx-quickstart` ubicación.
   Por lo tanto, un archivo de registro especificado como:
   `logs/thelog.log`

   >escribe a:
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   Y un archivo de registro especificado como:
   `../logs/thelog.log`

   >escribe en un directorio:
   ` <*cq-installation-dir*>/logs/`
&quot;(es decir, junto a ` `&lt;*cq-installation-dir*>/`crx-quickstart/`)

1. Este paso solo es necesario cuando se requiere un nuevo Writer (es decir, con una configuración diferente a la predeterminada Writer).

   >[!CAUTION]
   Solo se requiere una nueva configuración del grabador de registros cuando el valor predeterminado existente no es adecuado.

   >Si no se configura ningún Writer explícito, el sistema generará automáticamente un Writer implícito basado en el valor predeterminado.

   En `/apps/<*project-name*>/config`, cree un nodo para la nueva `Apache Sling Logging Writer` Configuración:

   * Nombre: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (ya que es un escritor)

      Al igual que con el Registrador, `<*identifier*>` se reemplaza por texto libre que debe introducir para identificar la instancia (no puede omitir esta información). Por ejemplo, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * Tipo: `sling:OsgiConfig`
   >[!NOTE]
   Aunque no es un requisito técnico, es aconsejable hacer `<*identifier*>` único.

   Establezca las siguientes propiedades en este nodo:

   * Nombre: `org.apache.sling.commons.log.file`

      Tipo: `String`

      Valor: especifique el archivo de registro para que coincida con el archivo especificado en el registrador;

      para este ejemplo, `../logs/myLogFile.log`.

   * Configure los demás parámetros según sea necesario:

      * Nombre: `org.apache.sling.commons.log.file.number`

         Tipo: `Long`

         Valor: especifique el número de archivos de registro que desea conservar; por ejemplo, `5`

      * Nombre: `org.apache.sling.commons.log.file.size`

         Tipo: `String`

         Valor: especificar según sea necesario para controlar la rotación de archivos por tamaño/fecha; por ejemplo, `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` controla la rotación del archivo de registro configurando:
   * un tamaño máximo de archivo
   * una programación de fecha y hora
   para indicar cuándo se creará un archivo nuevo (y se cambiará el nombre del archivo existente según el patrón de nombre).
   * Se puede especificar un límite de tamaño con un número. Si no se proporciona ningún indicador de tamaño, se toma como el número de bytes o puede agregar uno de los indicadores de tamaño - `KB`, `MB`, o `GB` (se omiten las mayúsculas y minúsculas).
   * Se puede especificar una programación de fecha y hora como un `java.util.SimpleDateFormat` patrón. Esto define el período de tiempo después del cual se rotará el archivo; también el sufijo anexado al archivo rotado (para identificación).
   El valor predeterminado es &#39;.&#39;aaaa-MM-dd (para rotación diaria del registro).
   Por ejemplo, a la medianoche del 20 de enero de 2010 (o cuando el primer mensaje de registro después de esto sea preciso), ../logs/error.log cambiará su nombre a ../logs/error.log.2010-01-20. El registro para el 21 de enero se enviará a (nuevo y vacío) ../logs/error.log hasta que se pase a la siguiente modificación del día.
       | `&#39;.&#39;aaaa-MM`|Rotación al comienzo de cada mes|
    |—|—|
    | `&#39;.&#39;aaaa-ww`|La rotación al primer día de cada semana (depende de la configuración regional). |
       | `&#39;.&#39;aaaa-MM-dd`|Rotación diaria a medianoche. |
       | `&#39;.&#39;aaaa-MM-dd-a`|Rotación a medianoche y mediodía de cada día. |
       | `&#39;.&#39;aaaa-MM-dd-HH`|Rotación en la parte superior de cada hora. |
       | `&#39;.&#39;aaaa-MM-dd-HH-mm`|Rotación al principio de cada minuto. |
     
     Nota: Al especificar una fecha/hora:
       1. Debe &quot;escapar&quot; el texto literal dentro de un par de comillas simples (&#39; &#39;);
       esto sirve para evitar que ciertos caracteres se interpreten como letras de patrón.
       1. Utilice únicamente caracteres permitidos para un nombre de archivo válido en cualquier lugar de la opción.
   

1. Lea el nuevo archivo de registro con la herramienta elegida.

   El archivo de registro creado por este ejemplo será `../crx-quickstart/logs/myLogFile.log`.

La consola de Felix también proporciona información sobre la compatibilidad con el registro de Sling en `../system/console/slinglog`; por ejemplo `https://localhost:4502/system/console/slinglog`.draf