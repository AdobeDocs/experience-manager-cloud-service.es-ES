---
title: Entornos de desarrollo rápido
description: Aprenda a utilizar entornos de desarrollo rápido para iteraciones de desarrollo rápido en un entorno de nube.
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '4990'
ht-degree: 3%

---

# Entornos de desarrollo rápido {#rapid-development-environments}

Para implementar cambios, los entornos de desarrollo de nube actuales requieren el uso de un proceso que emplea amplias reglas de calidad y seguridad de código denominadas canalización CI/CD. Para situaciones en las que se necesitan cambios rápidos e iterativos, Adobe ha introducido Entornos de Desarrollo Rápido (RDE, por sus siglas en inglés).

Los RDE permiten a los desarrolladores implementar y revisar cambios rápidamente, minimizando la cantidad de tiempo necesario para probar características que han demostrado funcionar en un entorno de desarrollo local.

Una vez que los cambios se han probado en un RDE, pueden implementarse en un entorno de desarrollo de nube normal a través de la canalización de Cloud Manager.

>[!NOTE]
> Póngase en contacto con los desarrolladores de RDE en nuestro [canal de Discord](https://discord.com/channels/1131492224371277874/1245304281184079872). Siéntase libre de hacer cualquier pregunta o dar comentarios con respecto a los temas de RDE.

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


Puede ver vídeos adicionales que muestran [cómo configurarlo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html), [cómo utilizarlo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) y el [ciclo de vida de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) mediante RDE.

## Introducción {#introduction}

Los RDE se pueden utilizar para configuraciones de código, contenido y Apache o Dispatcher. A diferencia de los entornos de desarrollo de nube normales, los desarrolladores pueden utilizar herramientas de línea de comandos locales para sincronizar el código creado localmente en un RDE.

Cada programa está aprovisionado con un RDE. Si hay cuentas de zona protegida, hibernan después de unas horas de no uso.

Una vez creados, los RDE se establecen en la versión de Adobe Experience Manager AEM () más reciente disponible. Un restablecimiento de RDE, que se puede realizar con Cloud Manager AEM, ciclos el RDE y lo establece en la última versión disponible de la versión de la aplicación de la versión de la aplicación de la versión de la aplicación de la versión de la aplicación de datos (RDE).

Normalmente, un solo desarrollador utilizaría un RDE en un momento determinado para probar y depurar una función específica. Cuando se completa la sesión de desarrollo, el RDE se puede restablecer a un estado predeterminado para el siguiente uso.

Los RDE adicionales pueden tener licencia para programas de Producción (que no sean de zonas protegidas).

## Habilitar RDE en un programa {#enabling-rde-in-a-program}

Siga estos pasos para poder usar Cloud Manager para crear un RDE para su programa.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa al que desee agregar un RDE para mostrar sus detalles.

   * Los RDE se pueden agregar a [programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) y a [programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).

1. En la página **Información general del programa**, haga clic en **Agregar entorno** en la tarjeta **Entornos** para agregar uno.

   ![Tarjeta Entornos](/help/implementing/cloud-manager/assets/no-environments.png)

   * La opción **Agregar entorno** también está disponible en la pestaña **Entornos**.

     ![Pestaña Entornos](/help/implementing/cloud-manager/assets/environments-tab.png)

   * La opción **Agregar entorno** se puede desactivar debido a la falta de permisos o dependiendo de los recursos con licencia.

1. En el cuadro de diálogo **Agregar entorno** que aparece:

   * Seleccione **Desarrollo rápido** en el encabezado **Seleccionar tipo de entorno**.
      * El número de entornos disponibles/utilizados se muestra entre paréntesis detrás del tipo de entorno.
   * Proporcione un **Nombre** para el entorno.
   * Proporcione una **descripción** opcional para el entorno.
   * Seleccione una **Región de nube**.

   ![Cuadro de diálogo Agregar entorno](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Haga clic en **Guardar** para agregar el entorno especificado.

La pantalla **Información general** ahora muestra su nuevo entorno en la tarjeta **Entornos**.

AEM Tras la creación, los RDE se establecen en la versión de la versión de la aplicación disponible más reciente Un restablecimiento de RDE, que también se puede realizar con Cloud Manager AEM, ejecuta un ciclo de RDE y lo establece en la última versión disponible de la versión de la aplicación de la versión de la versión de la versión de la versión de la versión de la aplicación de datos (RDE).

Para obtener más información sobre cómo usar Cloud Manager para crear entornos, administrar quién tiene acceso a ellos y asignar dominios personalizados, consulte [la documentación de Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Instalación de las herramientas de línea de comandos de RDE {#installing-the-rde-command-line-tools}

Después de agregar un RDE para el programa mediante Cloud Manager, puede interactuar con él configurando las herramientas de línea de comandos como se describe en los pasos siguientes:

>[!IMPORTANT]
>
>Asegúrese de tener instalada la versión 20 de [Node y NPM](https://nodejs.org/es/download/) para CLI de Adobe I/O y los complementos relacionados para que funcionen correctamente.


1. Instale las herramientas CLI de Adobe I/O según este [procedimiento](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Instale el complemento RDE de herramientas de CLI de Adobe I/O AEM:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Inicie sesión con el cliente aio.

   ```
   aio login
   ```

   La información de inicio de sesión (token) se almacena en la configuración de aio global y, por lo tanto, solo admite un inicio de sesión y una organización. Si desea utilizar varios RDE que necesiten diferentes inicios de sesión u organizaciones, siga el siguiente ejemplo de introducción a contextos.

   <details><summary>Siga este ejemplo para configurar un contexto local para uno de sus inicios de sesión de RDE</summary>
   Para almacenar la información de inicio de sesión localmente en un archivo .aio en el directorio actual dentro de un contexto específico, siga estos pasos. Un contexto también es una forma inteligente de configurar un entorno o script de CI/CD.  Para utilizar esta función, asegúrese de utilizar al menos la versión 10.3.1 de aio-cli. Actualícelo con npm install -g @adobe/aio-cli

   Vamos a crear un contexto llamado &quot;mycontext&quot; que luego establecemos como el contexto predeterminado usando el complemento auth antes de llamar al comando login.

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```

   >[!NOTE]
   > El comando de inicio de sesión con la opción `--no-open` generará una dirección URL en el terminal en lugar de abrir el explorador predeterminado. Así podrás copiarlo y abrirlo con una ventana de **incógnito** de tu navegador. De este modo, la sesión que haya iniciado en la ventana normal del explorador permanecerá sin cambios y podrá asegurarse de utilizar el inicio de sesión y la organización específicos necesarios para su contexto.

   El primer comando crea una nueva configuración de contexto de inicio de sesión, denominada `mycontext`, en el archivo de configuración `.aio` local (el archivo se crea si es necesario). El segundo comando establece el contexto `mycontext` como el contexto &quot;actual&quot;, es decir, el predeterminado.

   Con esta configuración en su lugar, el comando login almacena automáticamente los tokens de inicio de sesión en el contexto `mycontext`, por lo que lo mantiene local.

   Se pueden administrar varios contextos manteniendo las configuraciones locales en varias carpetas. Alternativamente, también es posible configurar varios contextos dentro de un solo archivo de configuración y cambiar entre ellos cambiando el contexto &quot;actual&quot;.
   </details>

1. Configure el complemento RDE para utilizar su organización, programa y entorno. El siguiente comando setup proporcionará al usuario de forma interactiva una lista de los programas de su organización y mostrará los entornos RDE de ese programa para elegir.

   ```
   aio aem:rde:setup
   ```

   El paso de configuración se puede omitir si se pretende utilizar un entorno con scripts, en cuyo caso se pueden incluir los valores de organización, programa y entorno en cada comando. [Vea los comandos rojos que aparecen a continuación para obtener más información](#rde-cli-commands).

### La configuración interactiva {#installing-the-rde-command-line-tools-interactive}

El comando setup preguntará si la configuración proporcionada debe almacenarse local o globalmente.

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

Elija `no` para
* almacene la organización, el programa y el entorno globalmente en su configuración de aio.
* trabajar sólo con un único RDE.

Elija `yes` para
* almacene la organización, el programa y el entorno localmente en el directorio actual, en un archivo de `.aio`. Esto resulta práctico si desea enviar el archivo al control de versiones para que otros usuarios que clonen el repositorio de Git puedan utilizarlo.
* trabaje con muchos RDE, de modo que cambiar a otro directorio use esa configuración en su lugar.
* utilice la configuración de en un contexto de programación como un script, que puede hacer referencia a ella.


Una vez seleccionada la configuración local o global, el comando setup intentará leer el ID de organización de su inicio de sesión actual y, a continuación, leer los programas de la organización. Si no se encuentra la organización, puede introducirla manualmente junto con algunas directrices.

```
Selected only organization: XYXYXYXYXYXYXYXXYY
retrieving programs of your organization ...
```

Una vez recuperados los programas, el usuario puede seleccionar de la lista y también escribir para filtrar.
Cuando se seleccionó el programa, se muestra una lista de entornos RDE entre los que elegir.
Si solo hay un programa o entorno RDE disponible, se selecciona automáticamente.

Para ver el contexto del entorno actual, ejecute:

```aio aem rde setup --show```

El comando responderá con un resultado similar al siguiente:

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### Procedimiento de configuración manual en un entorno no interactivo {#manual-setup}

En los entornos en los que ningún usuario puede ejecutar de forma interactiva el comando setup como se ha descrito anteriormente (como CI/CD o secuencias de comandos), los tres parámetros para la organización, el programa y el entorno se pueden configurar manualmente según los pasos siguientes.


<details>
  <summary>Amplíe para encontrar detalles sobre cómo configurar manualmente</summary>

1. Configure su ID de organización y sustituya la cadena alfanumérica por su propio ID de organización.

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * Puede buscar su propio identificador de organización con el método documentado en [Ver su identificador de organización](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. A continuación, configure su ID de programa:

   `aio config:set cloudmanager_programid 12345`

1. A continuación, configure el ID de entorno al que se va a adjuntar el RDE:

   `aio config:set cloudmanager_environmentid 123456`

1. Cuando haya terminado de configurar el complemento, inicie sesión realizando las siguientes acciones

   `aio login`

   Estos pasos requieren que sea miembro del perfil de producto **Desarrollador - Cloud Service** de Cloud Manager. Consulte [Asignar integrantes del equipo a perfiles de producto de Cloud Manager - Asignar el perfil de producto del desarrollador](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) para obtener más información.

Para obtener más información y demostración, vea el tutorial en vídeo [cómo configurar un RDE (06:24)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html).
</details>

## Uso de RDE al desarrollar una nueva función {#using-rde-while-developing-a-new-feature}

Adobe recomienda el siguiente flujo de trabajo para desarrollar una nueva función:

* Cuando se alcance un hito intermedio y se valide correctamente localmente con AEM as a Cloud Service SDK, confirme el código a una rama de características de Git. La rama aún no debe formar parte de la línea principal, aunque comprometerse con Git es opcional. Lo que constituye un &quot;hito intermedio&quot; varía en función de los hábitos del equipo. Algunos ejemplos son unas pocas líneas de código nuevas, medio día de trabajo o completar una subfunción.

* Restablezca el RDE si lo ha utilizado otra característica y desea [restablecerlo a un estado predeterminado](#reset-rde). <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->El restablecimiento tarda unos minutos y se elimina todo el contenido y código existentes. Puede utilizar el comando Estado de RDE para confirmar que el RDE está listo. AEM El RDE vuelve con la versión de lanzamiento más reciente de la versión de la.

  >[!IMPORTANT]
  >
  > AEM AEM Si los entornos de ensayo y producción no reciben actualizaciones automáticas de versiones de la versión de la versión y están detrás de la versión de la versión de la versión más reciente de la versión, es posible que el código que se ejecuta en el RDE no coincida con el modo en que funciona en el ensayo y la producción. En ese caso, es especialmente importante realizar pruebas exhaustivas del código en el ensayo antes de implementarlo en la producción.


* Mediante la interfaz de línea de comandos de RDE, sincronice el código local con RDE. Las opciones incluyen instalar un paquete de contenido, un paquete específico, un archivo de configuración OSGI, un archivo de contenido y un archivo zip de una configuración de Apache/Dispatcher. También es posible hacer referencia a un paquete de contenido remoto. Consulte [Herramientas de línea de comandos RDE](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands) para obtener más información. Puede utilizar el comando status para validar que la implementación se realizó correctamente. De forma opcional, utilice el Administrador de paquetes para instalar paquetes de contenido.

* Pruebe el código en el RDE. Las direcciones URL de autor y Publish están disponibles en Cloud Manager.

* Si el código no se comporta como se espera, utilice técnicas de depuración estándar para comprender el problema y realizar los cambios correspondientes. Sin confirmar las modificaciones de código en Git (ya que no se han validado), utilice la CLI local para sincronizar el código con RDE. Siga iterando hasta que se resuelva el problema.

* Una vez que el código se comporte según lo esperado, confírmelo en la rama de características de Git.

* El código sincronizado con RDE no utiliza una canalización de Cloud Manager, por lo que ahora debe utilizar una canalización que no sea de producción de Cloud Manager para implementar la rama de características de Git en el entorno de desarrollo de la nube. Esto valida que el código pasa las puertas de calidad de Cloud Manager y le permite estar seguro de que el código se implementará correctamente más adelante mediante la canalización de producción de Cloud Manager.

* Repita los pasos anteriores para cada hito intermedio hasta que todo el código de la función esté listo y se ejecute correctamente en el entorno de RDE y de desarrollo en la nube.

* Implemente el código en producción mediante la canalización de producción de Cloud Manager.

## Usar RDE para depurar una función existente {#use-rde-to-debug-an-existing-feature}

El flujo de trabajo es similar al desarrollo de una nueva función. La diferencia es que el código que se sincroniza con RDE reflejaría la etiqueta Git de lo que se haya insertado en el entorno en el que se ha encontrado el problema. Además, puede resultar útil implementar contenido que coincida con el entorno de flujo ascendente. Esto se puede lograr mediante la exportación e importación de paquetes de contenido.

## Varios desarrolladores que colaboran en el mismo RED {#multiple-developers-collaborating-on-the-same-rde}

Un RDE admite un solo proyecto a la vez. Dado que el código se sincroniza desde un entorno de desarrollo local al entorno de RDE, es más natural que un desarrollador lo utilice por su cuenta en un momento determinado.

Sin embargo, con una coordinación cuidadosa, es posible que más de un desarrollador valide una función específica o depure un problema específico. La clave es que cada desarrollador mantenga sus proyectos locales sincronizados para que los demás desarrolladores absorban los cambios de código realizados por un desarrollador en particular; de lo contrario, un desarrollador podría sobrescribir de forma involuntaria el código del otro. La estrategia recomendada es que cada desarrollador confirme sus cambios en una rama de Git compartida antes de sincronizarse con RDE, de modo que los demás desarrolladores extraigan los cambios antes de realizar sus propios cambios.

## Comandos de herramientas de línea de comandos RDE {#rde-cli-commands}

### Ayuda/Información general {#help}

* Para obtener una lista de comandos, escriba:

  `aio aem:rde`

* Para obtener ayuda detallada sobre un comando, escriba:

  `aio aem rde <command> --help`

### Indicadores globales {#global-flags}

* Para una salida menos detallada, utilice el indicador quiet:

  `aio aem rde <command> --quiet`

  Esto elimina ciertos elementos, como los giros y las barras de progreso, y limita la necesidad de que el usuario introduzca datos.

* Para JSON en lugar de para la salida del registro de la consola, utilice el indicador json:

  `aio aem rde <command> --json`

  Devuelve un JSON válido al suprimir cualquier salida de la consola. Consulte los ejemplos de JSON más adelante.

* Para evitar configurar la información de conexión de RDE mediante el comando setup o cualquier creación de configuración de aio, utilice los tres indicadores para organización, programa y entorno:

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  Esto todavía requiere que se realice un ```aio login```.

### Implementación en RDE {#deploying-to-rde}

En esta sección se describe el uso de la CLI de RDE para implementar, instalar o actualizar paquetes, configuraciones de OSGI, paquetes de contenido, archivos de contenido individuales y configuraciones de Apache o Dispatcher.

El patrón de uso general es `aio aem:rde:install <artifact>`.

Puede encontrar algunos ejemplos a continuación:

#### Implementación de un paquete de contenido {#deploy-content-package}

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

La respuesta para una implementación correcta es similar a la siguiente:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Opcionalmente, puede hacer referencia a un repositorio remoto:

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

De forma predeterminada, los artefactos se implementan en los niveles de creación y publicación, pero el indicador &quot;-s&quot; se puede utilizar para dirigirse a un nivel específico.

AEM Se puede implementar cualquier paquete de datos, como paquetes con código, contenido o un [paquete de contenedor](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) (también denominado paquete &quot;todo&quot;).

>[!IMPORTANT]
>
>La configuración de Dispatcher para el proyecto WKND no se implementa mediante la instalación del paquete de contenido anterior. Impleméntelo por separado siguiendo los pasos de &quot;Implementación de una configuración de Apache/Dispatcher&quot;.

#### Implementación de una configuración OSGI {#deploy-OSGI-config}

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

Donde la respuesta para una implementación correcta es similar a la siguiente:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

#### Implementación de un paquete {#deploy-bundle}

Para implementar un paquete, utilice:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

Donde la respuesta para una implementación correcta es similar a la siguiente:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

#### Implementación de un archivo de contenido {#deploy-content-file}

Para implementar un archivo de contenido, utilice:

`aio aem:rde:install world.txt -p /apps/hello.txt`

Donde la respuesta para una implementación correcta es similar a la siguiente:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

#### Implementación de una configuración de Apache/Dispatcher {#deploy-apache-config}

Toda la estructura de carpetas debe estar en forma de archivo zip para este tipo de configuración.

AEM Desde el módulo `dispatcher` de un proyecto de, puede comprimir la configuración de Dispatcher ejecutando el siguiente comando de Maven:

`mvn clean package`

O utilizando el siguiente comando zip del directorio `src` del módulo `dispatcher`:

`zip -y -r dispatcher.zip .`

A continuación, implemente la configuración mediante este comando:

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>El comando anterior supone que está implementando las configuraciones de Dispatcher del proyecto [WKND](https://github.com/adobe/aem-guides-wknd). Asegúrese de reemplazar `X.X.X` con el número de versión del proyecto WKND correspondiente o el número de versión específico del proyecto al implementar la configuración de Dispatcher del proyecto.

>[!NOTE]
>
>RDE admite la configuración de Dispatcher en &quot;modo flexible&quot;, pero no la configuración de Dispatcher en &quot;modo heredado&quot;. Consulte [Documentación de Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para obtener información sobre los dos modos. También puede consultar la documentación sobre [la migración al modo flexible](/help/implementing/dispatcher/validation-debug.md#migrating), si aún no lo ha hecho.

Una implementación correcta genera una respuesta similar a la siguiente:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

El código implementado en RDE no se somete a una canalización de Cloud Manager y a sus puertas de calidad asociadas. Sin embargo, el código pasa por algún análisis, que informa de los errores, como se muestra en el ejemplo de código siguiente:

```
$ aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar
...
#19: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D74FR1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
Logs:
The analyser found the following errors for author :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
The analyser found the following errors for publish :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
```

El ejemplo de código anterior ilustra el comportamiento si un paquete no se resuelve. En cuyo caso, se &quot;almacena en zona intermedia&quot; y solo se instala si sus requisitos (importaciones que faltan, en este caso) se satisfacen mediante la instalación de otro código.

#### Implementación de la configuración relacionada con la canalización (configuraciones yaml) {#deploy-config-pipeline}

Las configuraciones específicas del entorno (uno o más archivos yaml) descritas en el artículo [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md) se pueden implementar de la siguiente manera:

`aio aem:rde:install -t env-config ./my-config-folder`
donde my-config-folder es la carpeta principal que contiene las configuraciones de yaml.

También es posible instalar un archivo zip que contenga el árbol de carpetas de configuración:

`aio aem:rde:install -t env-config config.zip`

Tenga en cuenta que la matriz envTypes del archivo yaml debe incluir el valor *red*, como en el ejemplo siguiente:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["rde"]
```

### Implementación de código front-end basado en temas de sitio y plantillas de sitio {#deploying-themes-to-rde}

Los RDE admiten código front-end basado en [temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md) y [plantillas de sitio](/help/sites-cloud/administering/site-creation/site-templates.md). Con RDE, esto se hace usando una directiva de línea de comandos para implementar paquetes front-end, en lugar de la [canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) de Cloud Manager que se usa para otros tipos de entornos.

Como de costumbre, cree su paquete front-end utilizando npm:

`npm run build`

Debe generar una carpeta `dist/`, de modo que la carpeta del paquete front-end debe contener un archivo `package.json` y una carpeta `dist`:

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```
Ahora está listo para implementar el paquete front-end en RDE apuntando a la carpeta de paquetes front-end:

```
aio aem:rde:install -t frontend ./path-to-frontend-pkg-folder/
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

También puede comprimir el archivo `package.json` y la carpeta `dist` e implementar ese archivo zip:

`zip -r frontend-pkg.zip ./path-to-frontend-pkg-folder/dist ./path-to-frontend-pkg-folder/package.json`

```
aio aem:rde:install -t frontend frontend-pkg.zip
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

>[!NOTE]
>
>El nombre de los archivos del paquete front-end debe cumplir las siguientes convenciones de nomenclatura:
> * carpeta &quot;dist&quot;, para la carpeta npm build output package
> * archivo &quot;package.json&quot;, para el paquete de dependencias npm

>[!TIP]
>
> Si creó su RDE antes de abril de 2023 y experimentó el error &quot;UNEXPECTED_API_ERROR&quot; al intentar la función de front-end por primera vez, intente eliminar su entorno y crearlo de nuevo.

### Comprobación del estado de RDE {#checking-rde-status}

Puede utilizar la CLI de RDE para comprobar si el entorno está listo para implementarse en, ya que las implementaciones se han realizado mediante el complemento de RDE.

En ejecución:

`aio aem:rde:status`

Devuelve lo siguiente:

```
Info for cm-p12345-e987654
Environment: Ready
- Bundles Author:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Bundles Publish:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Configurations Author:
 com.adobe.granite.demo.MyServlet
- Configurations Publish:
 com.adobe.granite.demo.MyServlet
```

Si el comando devuelve una nota sobre la implementación de instancias, aún puede continuar y realizar la siguiente actualización, pero es posible que la última aún no esté visible en la instancia.

### Mostrar historial de implementación {#show-deployment-history}

Puede comprobar el historial de implementaciones realizadas en RDE ejecutando:

`aio aem:rde:history`

Que devuelve una respuesta en forma de:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Eliminando de RDE {#deleting-from-rde}

Puede eliminar configuraciones y paquetes que se hayan implementado previamente en RDE mediante la herramienta CLI. Utilice el comando `status` para obtener una lista de lo que se puede eliminar, que incluye `bsn` para paquetes y `pid` para configuraciones a las que se hace referencia en el comando eliminar.

Por ejemplo, si se ha instalado `com.adobe.granite.demo.MyServlet.cfg.json`, `bsn` es solo `com.adobe.granite.demo.MyServlet`, sin el sufijo **cfg.json**.

No se admite la eliminación de paquetes de contenido o archivos de contenido. Para eliminarlos, el RDE debe restablecerse, lo que lo devuelve a un estado predeterminado.

Consulte el ejemplo siguiente para obtener más información:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

Para obtener más información y demostración, vea el tutorial en vídeo [cómo usar comandos RDE (10:01)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html).

## Registros {#rde-logging}

Al igual que otros tipos de entornos, los niveles de registro se pueden establecer modificando las configuraciones de OSGi, aunque, como se ha descrito anteriormente, el modelo de implementación para RDE implica una línea de comandos en lugar de una implementación de Cloud Manager. Consulte la [documentación de registro](/help/implementing/developing/introduction/logging.md) para obtener más información sobre cómo ver, descargar e interpretar los registros.

La CLI de RDE también tiene su propio comando de registro que se puede utilizar para configurar rápidamente qué clases y paquetes deben registrarse y en qué nivel de registro. Estas configuraciones pueden verse como efímeras, ya que no modifican las propiedades OSGI en el control de versiones. Esta función se centra en rastrear registros en tiempo real, en lugar de buscar registros del pasado distante.

El siguiente ejemplo ilustra cómo rastrear el nivel de creación, con un paquete establecido en un nivel de registro de depuración y dos paquetes (separados por espacios) establecidos en un nivel de depuración de información. La salida que incluye un paquete **auth** está resaltada.

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

>[!TIP]
>
>Si ve el error `RDECLI:UNEXPECTED_API_ERROR` al reproducir con los comandos de registro para el servicio de creación, restablezca el entorno e inténtelo de nuevo. Este error se producirá si la operación de restablecimiento más reciente se realizó antes de finales de mayo de 2024.
>
>```
>aio aem:rde:reset
>```

Consulte `aio aem:rde:logs --help` para ver el conjunto completo de opciones de línea de comandos.

Las funciones incluyen:

* declarar niveles de registro en un nivel por paquete o clase
* personalizar el formato de salida del registro
* hasta cuatro configuraciones de registro actuales, cada una en su propio terminal
* resaltar registros específicos

Tenga en cuenta que los registros se almacenan en la memoria en el RDE y estos registros se reciclan y, por lo tanto, se descartan si no se siguen o si la red es demasiado lenta.


## Restablecer {#reset-rde}

Al restablecer el editor de texto enriquecido, se eliminan todos los códigos personalizados, las configuraciones y el contenido de las instancias de autor y publicación. Este restablecimiento es útil, por ejemplo, si el RDE se ha utilizado para probar una función específica y desea restablecerla a un estado predeterminado para que pueda probar una función diferente.

AEM Un restablecimiento establece el RDE a la última versión disponible de la.

El restablecimiento se puede realizar mediante [Cloud Manager](#reset-the-rde-cloud-manager) o a través de la [línea de comandos](#reset-the-rde-command-line). El restablecimiento tarda unos minutos y todo el contenido y el código existentes se eliminan del editor de código.

>[NOTA!]
>
>Se le debe asignar la función de desarrollador de Cloud Manager para utilizar la función de restablecimiento. Si no es así, una acción de restablecimiento producirá un error.

### Restablecer el RDE a través de la línea de comandos {#reset-the-rde-command-line}

Puede restablecer el RDE y devolverlo a un estado predeterminado ejecutando:

`aio aem:rde:reset`

Esto generalmente toma unos minutos y reportará ```Environment reset.``` cuando se realice correctamente o ```Failed to reset the environment.``` si hay errores. Para obtener un resultado estructurado, consulte el capítulo sobre el resultado ```--json``` que aparece a continuación.

Utilice el [comando status](#checking-rde-status) para comprobar si el entorno está listo de nuevo.

### Restablecer el RDE en Cloud Manager {#reset-the-rde-cloud-manager}

Puede utilizar Cloud Manager para restablecer su RDE siguiendo los pasos siguientes:

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea restablecer el RDE.

1. En la página **Información general**, haga clic en la pestaña **Entornos** en la parte superior de la pantalla.

   ![Pestaña Entornos](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * También puede hacer clic en el botón **Mostrar todo** en la tarjeta **Entornos** para ir directamente a la pestaña **Entornos**.

     ![Mostrar todas las opciones](/help/implementing/cloud-manager/assets/environment-showall.png)

1. Se abre la ventana **Entornos** y se enumeran todos los entornos del programa.

   ![La pestaña de entornos](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Haga clic en el botón de los tres puntos del RDE que desee restablecer y, a continuación, seleccione **Restablecer**.

   ![Ver detalles del entorno](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Confirme que desea restablecer el RDE haciendo clic en **Restablecer** en el cuadro de diálogo.

   ![Confirmar restablecimiento](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager confirma mediante una notificación tipo banner que se ha iniciado el proceso de restablecimiento.

   ![Restablecer notificación de banner](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

Una vez iniciado el proceso de restablecimiento de RDE, normalmente se tarda unos minutos en completar y devolver el entorno a su estado predeterminado. El estado del proceso de restablecimiento se puede ver en cualquier momento en la columna **Status** de la tarjeta **Environments** o en la ventana **Environments**.

![Estado de restablecimiento de RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

También puede restablecer el RDE usando el botón de puntos suspensivos directamente desde la tarjeta **Entornos** en la página **Información general**.

![Restablecer RDE desde la tarjeta Entornos](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Para obtener más información sobre cómo usar Cloud Manager para administrar sus entornos, consulte [la documentación de Cloud Manager](/help/implementing/cloud-manager/manage-environments.md).

## Comandos compatibles con la salida JSON {#json-commands}

La mayoría de los comandos admiten el indicador global ```--json```, que suprime la salida de la consola y devuelve un json válido para procesarlo en los scripts. A continuación se muestran algunos comandos admitidos, con ejemplos de la salida json.

### Estado {#status}

<details>
  <summary>Amplíe para ver ejemplos de estado</summary>

#### Un RDE limpio {#clean-rde}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Modification in progress | Deployment in progress | Upload in progress | Ready (instances are currently deploying) | Ready",
  "author": {
    "osgiBundles": [],
    "osgiConfigs": []
  },
  "publish": {
    "osgiBundles": [],
    "osgiConfigs": []
  }
}
```

#### Un RDE con algunos paquetes instalados {#rde-installed-bundles}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "author": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  },
  "publish": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  }
}
```

</details>

### Instalar {#install}

<details>
  <summary>Amplíe para ver ejemplos de instalación</summary>

```$ aio aem rde install ~/Downloads/hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "4",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:30:44.578Z",
        "processed": "2024-05-21T12:31:07.886468Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### Eliminar {#delete}

<details>
  <summary>Amplíe para ver los ejemplos de eliminación</summary>

```$ aio aem rde delete com.adobe.granite.hotdev.demo-1.0.0.SNAPSHOT --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "84",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:16.889Z",
        "processed": "2024-05-21T11:49:18.188420Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    },
    {
      "updateId": "85",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:23.857Z",
        "processed": "2024-05-21T11:49:25.237930Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### Historia {#history}

<details>
  <summary>Amplíe para ver ejemplos de historial</summary>

```$ aio aem rde history --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "items": [
    {
      "updateId": "112",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:07.934Z",
        "processed": "2024-05-21T12:53:09.118766Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "111",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:00.824Z",
        "processed": "2024-05-21T12:53:02.101560Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "110",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:52:12.123Z",
        "processed": "2024-05-21T12:52:31.026147Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507"
    }
  ]
}
```

</details>

### Restablecer {#reset}

<details>
  <summary>Amplíe para ver ejemplos de restablecimiento</summary>

#### Fuego y olvido, sin esperas {#fire-no-wait}

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### Esperar a la finalización, restablecido correctamente {#wait-success}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```

#### Esperar a la finalización, error al restablecer {#wait-failed}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset_failed"
}
```

</details>

### Reiniciar {#restart}

<details>
  <summary>Amplíe para ver ejemplos de reinicio</summary>

```$ aio aem rde restart --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "restarted"
}
```

</details>

## Ejecutar modos {#runmodes}

La configuración OSGI específica de RDE se puede aplicar utilizando sufijos en el nombre de la carpeta, como en los ejemplos siguientes:

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

Consulte la [documentación sobre el modo de ejecución](/help/implementing/deploying/overview.md#runmodes) para obtener información general sobre los modos de ejecución.

>[!NOTE]
>
>La configuración OSGI de RDE es única, ya que hereda los valores de cualquier propiedad OSGI declarada por el modo de ejecución `dev` del paquete.

Los RDE son distintos de otros entornos en los que el contenido se puede instalar en una carpeta install.rde (o install.author.rde o install.publish.rde) en /apps. Esto permite enviar contenido a Git y enviarlo al editor de texto enriquecido (RDE) mediante las herramientas de la línea de comandos.

## Rellenar con contenido {#populating-content}

Cuando se restablece un RDE, se elimina todo el contenido y, por lo tanto, si lo desea, se debe realizar una acción explícita para añadir contenido. Como práctica recomendada, considere la posibilidad de combinar un conjunto de contenido para utilizarlo como contenido de prueba para validar o depurar funciones en el editor de experiencias visuales. Existen varias estrategias posibles para rellenar el RDE con ese contenido:

1. Sincronizar el paquete de contenido explícitamente con RDE mediante las herramientas de la línea de comandos

1. Coloque y confirme el contenido de muestra en Git dentro de una carpeta install.rde en /apps y, a continuación, sincronice el paquete de contenido general con RDE mediante las herramientas de la línea de comandos.

1. Use la [herramienta de copia de contenido](/help/implementing/developing/tools/content-copy.md) para copiar un conjunto de contenido definido desde entornos de producción, ensayo o desarrollo, o desde otro RDE.

1. Uso del Administrador de paquetes

Se encuentra limitado a 1 GB al sincronizar paquetes de contenido.


## ¿En qué se diferencian los RDE de los entornos de desarrollo en la nube? {#how-are-rds-different-from-cloud-development-environments}

Aunque el RDE es similar en muchos aspectos a un entorno de desarrollo en la nube, existen algunas diferencias arquitectónicas menores que permiten una sincronización rápida del código. El mecanismo para obtener código en RDE es diferente: para RDE, se sincroniza código de un entorno de desarrollo local, mientras que para los entornos de desarrollo en la nube, se implementa código a través de Cloud Manager.

Por estos motivos, se recomienda que, después de validar el código en un entorno RDE, implemente el código en un entorno de desarrollo de nube mediante la canalización que no sea de producción. Finalmente, pruebe el código antes de implementarlo con la canalización de producción.

Tenga en cuenta también las siguientes consideraciones:

* Los RDE no incluyen un nivel de previsualización
* Actualmente, los RDE no son compatibles con el canal de prelanzamiento.


## ¿Cuántos RDE necesito? {#how-many-rds-do-i-need}

Hay disponible un RDE para cada solución con licencia y el Adobe también ofrece RDE adicionales, que se pueden licenciar para programas de Producción (que no sean de zona protegida).

El número de RDE necesarios depende de la composición y los procesos de una organización. El modelo más flexible es donde una organización compra un RDE dedicado para cada uno de sus desarrolladores de AEM Cloud Service. En este modelo, cada desarrollador puede probar su código en RDE sin coordinarse con otros integrantes del equipo para saber si hay un entorno RDE disponible.

En el otro extremo, un equipo con un solo RDE puede utilizar procesos internos para coordinar qué desarrolladores pueden utilizar el entorno en un momento determinado. Esto puede suceder posiblemente cada vez que un desarrollador ha alcanzado un hito de característica intermedia y está listo para validarlo en un entorno de nube donde puede realizar rápidamente los cambios que necesita.

Un modelo intermedio es aquel en el que una organización compra varios RDE, de modo que existe una mayor probabilidad de que esté disponible un RDE no utilizado. Una estrategia podría ser asignar un RDE por equipo de depuración o función principal. Se pueden utilizar procesos internos para coordinar el uso de los entornos.

## ¿En qué se diferencia un entorno de desarrollo rápido (RDE) de AEM Forms Cloud Service de otros entornos? {#how-are-forms-rds-different-from-cloud-development-environments}

Los desarrolladores de Forms pueden utilizar el entorno de desarrollo rápido de AEM Forms Cloud Service para desarrollar rápidamente Forms adaptable, flujos de trabajo y personalizaciones, como la personalización de componentes principales, integraciones con sistemas de terceros y mucho más. El entorno de desarrollo rápido (RDE) de AEM Forms Cloud Service no es compatible con las API de comunicación. Tampoco es compatible con las funciones y capacidades que requieren el documento de registro, como la generación de un documento de registro al enviar un formulario adaptable. Las siguientes funciones de AEM Forms no están disponibles en un entorno de desarrollo rápido (RDE):

* Configurar un documento de registro para un formulario adaptable
* Generar un documento de registro al enviar un formulario adaptable o con un paso del flujo de trabajo
* Enviar documento de registro como archivo adjunto con la acción de envío Correo electrónico o con el paso Correo electrónico en un flujo de trabajo
* Usar Adobe Sign en un formulario adaptable o en un paso del flujo de trabajo
* API de comunicación

>[!NOTE]
>
> No hay diferencia entre la interfaz de usuario del entorno de desarrollo rápido (RDE) y otros entornos de Cloud Service para Forms. Todas las opciones relacionadas con el documento de registro, como seleccionar una plantilla de documento de registro para un formulario adaptable, siguen apareciendo en la interfaz de usuario. Estos entornos no tienen API de comunicación ni capacidades de documento de registro para probar estas opciones. Por lo tanto, cuando elige cualquier opción que requiera API de comunicación o capacidades de documento de registro, no se realiza ninguna acción y se muestra un mensaje de error.

## Tutorial de RDE

Para obtener más información sobre RDE en AEM as a Cloud Service, vea el tutorial en vídeo que muestra [cómo configurarlo, cómo utilizarlo y el ciclo de vida de desarrollo (01:25)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html).

# Solución de problemas {#troubleshooting}

## Localización de averías de RDE (#rde-troublehooting)

### AEM Cómo obtener la versión más reciente de un RDE existente. {#get-latest-aem-version}

Una vez creados, los RDE se establecen en la versión de Adobe Experience Manager AEM () más reciente disponible. Un [restablecimiento de RDE](#reset-rde), que se puede realizar mediante Cloud Manager AEM o el comando `aio aem:rde:reset`, efectúa un ciclo de RDE y lo establece en la última versión disponible de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la versión más reciente disponible.

## solución de problemas del complemento aio RDE {#aio-rde-plugin-troubleshooting}

### Errores relacionados con permisos insuficientes {#insufficient-permissions}

Para usar el complemento RDE, se requiere que sea miembro del perfil de producto de **Desarrollador - Cloud Service** de Cloud Manager. Consulte [Asignar integrantes del equipo a perfiles de producto de Cloud Manager - Asignar el perfil de producto del desarrollador](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) para obtener más información.

También puede confirmar que tiene esta función de desarrollador si puede iniciar sesión en la consola de desarrollador ejecutando este comando:

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>Si ve el error `Warning: cloudmanager:* is not a aio command.`, debe instalar [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) ejecutando el siguiente comando:
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

Compruebe que el inicio de sesión se haya completado correctamente ejecutando

`aio cloudmanager:list-programs`

Esto debería enumerar todos los programas de la organización configurada y confirmar que tiene asignada la función correcta.

### Uso del contexto obsoleto &quot;aio-cli-plugin-cloudmanager&quot; {#aio-rde-plugin-troubleshooting-deprecatedcontext}

Debido al historial de &quot;aio-cli-plugin-aem-rde&quot;, se utilizó el nombre de contexto &quot;aio-cli-plugin-cloudmanager&quot; durante un tiempo. El complemento rojo ahora utiliza la forma IMS de tratar con la información contextual, lo que significa que hay opciones para almacenar la información contextual global o localmente, así como para establecer de forma predeterminada todas las llamadas aio a un valor predeterminado configurado si así lo desea. El contexto predeterminado configurado se almacena localmente y permite a los desarrolladores realizar un seguimiento y utilizar contextos individuales y su información dentro de una carpeta. Para obtener más información, lea [el ejemplo anterior para configurar un contexto local](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools).

Los desarrolladores que utilizan ambos complementos, el aio-cli-plugin-cloudmanager y el aio-cli-plugin-aem-red y desean mantener toda la información en el mismo contexto tienen dos opciones en este momento:

#### Siga usando el contexto &quot;aio-cli-plugin-cloudmanager&quot;

El contexto aún se puede utilizar, se mostrará una advertencia de obsolescencia en el complemento RDE. Esta advertencia se puede omitir usando el modo ```--quiet```. Las versiones más recientes del complemento RDE ya no ofrecerán la alternativa de leer el contexto &quot;aio-cli-plugin-cloudmanager&quot;. Para seguir usándolo, simplemente configure el contexto predeterminado en &quot;aio-cli-plugin-cloudmanager&quot;, vea [el ejemplo anterior para configurar un contexto local](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools).

#### Utilice cualquier otro nombre de contexto también para el complemento Cloud Manager

Los complementos de Cloud Manager ofrecen un parámetro para definir el contexto que se va a utilizar. Todavía no admite la configuración de contexto predeterminada de IMS. Para ello, configure el complemento RDE con [el ejemplo para configurar un contexto local](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools) e indique al complemento de Cloud Manager que utilice &#39;myContext&#39; como ```--imsContextName=myContext``` en cada llamada a él.
