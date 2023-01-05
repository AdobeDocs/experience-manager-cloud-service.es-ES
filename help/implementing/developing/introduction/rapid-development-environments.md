---
title: Entornos de desarrollo rápido
description: Aprenda a aprovechar los entornos de desarrollo rápido para iteraciones de desarrollo rápidas en un entorno de nube.
hidefromtoc: true
source-git-commit: 983901387d059a98942b4f7c533770a55dd4ff4a
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 7%

---


# Entornos de desarrollo rápido {#rapid-development-environments}

>[!AVAILABILITY]
>
>Esta función aún no está disponible.

Para implementar cambios, los entornos actuales de Cloud Development requieren el uso de un proceso que emplee reglas de calidad y seguridad de código extensas, llamadas canalización CI/CD. En situaciones en las que se necesitan cambios rápidos e iterativos, el Adobe ha introducido entornos de desarrollo rápido (RDEs).

Los RDE permiten a los desarrolladores implementar y revisar cambios rápidamente, lo que minimiza la cantidad de tiempo necesario para probar las funciones que se ha probado que funcionan en un entorno de desarrollo local.

Una vez que los cambios se han probado en un RDE, se pueden implementar en un entorno de desarrollo de nube normal a través de la canalización de Cloud Manager.

## Introducción {#introduction}

Los RDE se pueden utilizar para configuraciones de código, contenido y Apache o Dispatcher. A diferencia de los entornos habituales de desarrollo de nube, los desarrolladores pueden utilizar herramientas de línea de comandos locales para sincronizar el código creado localmente en un RDE.

Cada programa está aprovisionado con un RDE. En el caso de las cuentas de Sandbox, hibernarán después de unas horas de no uso.

Normalmente, un desarrollador único utilizaría un RDE en un momento determinado para probar y depurar una función específica. Cuando la sesión de desarrollo ha finalizado, el RDE se puede restablecer a un estado predeterminado para el siguiente uso.

<!-- Temporarily hiding this. See CQDOC-19795 for more details

Additional RDEs may be purchased for Production programs -->

## Habilitar RDE en un programa {#enabling-rde-in-a-program}

Siga estos pasos para utilizar Cloud Manager para crear un RDE para su programa.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa al que desea añadir un RDE para mostrar sus detalles.

   * Los RDE se pueden agregar a ambas [programas de simulación de pruebas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) y [programas de producción.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. En la página **Información general del programa**, haga clic en **Agregar entorno** en la tarjeta **Entornos** para agregar un entorno.

   ![Tarjeta Entornos](/help/implementing/cloud-manager/assets/no-environments.png)

   * La opción **Agregar entorno** también está disponible en la pestaña **Entornos**.

      ![Pestaña Entornos](/help/implementing/cloud-manager/assets/environments-tab.png)

   * La opción **Agregar entorno** se puede desactivar debido a la falta de permisos o dependiendo de los recursos con licencia.

1. En el cuadro de diálogo **Agregar entorno** que aparece:

   * Select **Desarrollo rápido** en el **Seleccionar tipo de entorno** encabezado.
      * El número de entornos disponibles/utilizados se muestra entre paréntesis detrás del tipo de entorno.
   * Proporcione un **Nombre** para el entorno.
   * Proporcionar un **Descripción** para el entorno.
   * Seleccione una **Región de nube**.

   ![Cuadro de diálogo Agregar entorno](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Haga clic en **Guardar** para agregar el entorno especificado.

La pantalla **Información general** ahora muestra el nuevo entorno en la tarjeta **Entornos.**

Para obtener más información sobre el uso de Cloud Manager para crear entornos, administrar quién tiene acceso a ellos y asignar dominios personalizados, consulte [la documentación de Cloud Manager.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Instalación de las herramientas de la línea de comandos de RDE {#installing-the-rde-command-line-tools}

Una vez añadido un RDE para el programa mediante Cloud Manager, puede interactuar con él configurando las herramientas de línea de comandos como se describe en los pasos siguientes:

1. Instale las herramientas CLI de Adobe I/O según el procedimiento [here](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Instale el complemento del administrador de nube de herramientas de CLI de Adobe I/O y configúrelas como se describe [here](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. Instale las herramientas CLI de Adobe I/O AEM complemento RDE ejecutando estos comandos:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Configure el complemento de cloud manager para su ID de organización:

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   y reemplace la cadena alfanumérica con su propio ID de organización, que se puede buscar utilizando la estrategia [here](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. A continuación, configure su id de programa:

   `aio config:set cloudmanager_programid 12345`

1. A continuación, configure el id de entorno al que se adjuntará el RDE:

   `aio config:set cloudmanager_environmentid 123456`

1. Una vez que haya terminado de configurar el complemento, inicie sesión realizando

   `aio login`

   La respuesta en un inicio de sesión exitoso debe parecerse a la salida siguiente, pero puede ignorar los valores mostrados.

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

1. Verifique que el inicio de sesión se haya completado correctamente ejecutando

   `aio cloudmanager:list-programs`

   Esto debería incluir todos los programas de la organización configurada.

   Tenga en cuenta que lo anterior requiere que sea miembro de Cloud Manager **Desarrollador: Cloud Service** Perfil de producto. Consulte [esta página](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) para obtener más información.

   Como alternativa, puede confirmar que tiene esta función de desarrollador si puede iniciar sesión en la consola de desarrollador ejecutando este comando:

   `aio cloudmanager:environment:open-developer-console`

## Uso de RDE al desarrollar una nueva función {#using-rde-while-developing-a-new-feature}

Adobe recomienda el siguiente flujo de trabajo para desarrollar una nueva función:

* Cuando se alcanza un hito intermedio y se valida correctamente localmente con el SDK as a Cloud Service de AEM, el código debe comprometerse con una rama de funciones de Git que aún no forme parte de la línea principal, aunque comprometerse con Git sea opcional. Lo que constituye un &quot;hito intermedio&quot; varía en función de los hábitos de equipo. Algunos ejemplos son algunas líneas de código nuevas, medio día de trabajo o completar una subfunción.

* Restablezca el RDE si lo ha utilizado otra función y desea [restablecerlo a un estado predeterminado](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->El restablecimiento tardará unos minutos y se eliminará todo el contenido y el código existentes. Puede utilizar el comando de estado RDE para confirmar que el RDE está listo.

* Mediante la interfaz de línea de comandos RDE, sincronice el código local con el RDE. Las opciones incluyen la instalación de un paquete de contenido, un paquete específico, un archivo de configuración OSGI, un archivo de contenido y un archivo zip de una configuración de Apache/Dispatcher. También es posible hacer referencia a un paquete de contenido remoto. Consulte la [Herramientas de línea de comandos RDE](#rde-cli-commands) para obtener más información. Puede utilizar el comando de estado para validar que la implementación se haya realizado correctamente. Opcionalmente, utilice el Administrador de paquetes para instalar paquetes de contenido.

* Pruebe el código en el RDE. Las URL de creación y publicación están disponibles en Cloud Manager.

* Si el código no se comporta como se espera, utilice técnicas de depuración estándar para comprender el problema y realizar los cambios correspondientes. Sin comprometer las modificaciones del código en git (ya que no se han validado), utilice la CLI local para sincronizar el código con RDE. Continúe iterando hasta que se resuelva el problema.

* Una vez que el código se comporte como se espera, transfiera el código a la rama de características de Git.

* El código sincronizado con RDE no utiliza una canalización de Cloud Manager, por lo que ahora debe utilizar una canalización de no producción de Cloud Manager para implementar la rama de funciones de Git en el entorno de desarrollo de nube. Esto valida que el código pasa las puertas de calidad de Cloud Manager y le permite estar seguro de que el código se implementará correctamente posteriormente mediante la canalización de producción de Cloud Manager.

* Repita los pasos anteriores para cada hito intermedio hasta que todo el código de la función esté listo y se ejecute correctamente tanto en el entorno RDE como en el entorno de desarrollo de nube.

* Implemente el código en producción a través de la canalización de producción de Cloud Manager.

## Uso de RDE para depurar una función existente {#use-rde-to-debug-an-existing-feature}

El flujo de trabajo es similar al desarrollo de una nueva función. La diferencia es que el código que se sincroniza con RDE reflejaría la etiqueta de Git de lo que se insertara en el entorno en el que se ha encontrado el problema. Además, puede resultar útil implementar contenido que coincida con el entorno de flujo ascendente. Esto se puede lograr mediante la exportación e importación de paquetes de contenido.

## Varios desarrolladores que colaboran en el mismo RDE {#multiple-developers-collaborating-on-the-same-rde}

Un RDE admite un solo proyecto a la vez. Dado que el código se sincroniza de un entorno de desarrollo local al entorno RDE, lo más normal es que un desarrollador lo utilice por su cuenta a la vez.

Sin embargo, con una coordinación cuidadosa, es posible que más de un desarrollador valide una función específica o depure un problema específico. La clave es que cada desarrollador mantenga sus proyectos locales sincronizados, de modo que los cambios de código realizados por un desarrollador en particular los absorban otros desarrolladores; de lo contrario, un desarrollador podría sobrescribir inadvertidamente el código del otro. La estrategia recomendada es que cada desarrollador afirme sus cambios a una rama de Git compartida antes de sincronizarlos con RDE, de modo que los demás desarrolladores extraigan los cambios antes de realizar sus propios cambios.

## Herramientas de línea de comandos RDE {#rde-cli-commands}

### Ayuda/Información general {#help}

* Para obtener una lista de comandos, escriba:

   `aio aem:rde`

* Para obtener ayuda detallada sobre un comando, escriba:

   `aio aem rde <command> --help`

### Implementación en RDE {#deploying-to-rde}

Esta sección describe el uso de la CLI de RDE para implementar, instalar o actualizar paquetes, configuraciones de OSGI, paquetes de contenido, archivos de contenido individuales y configuraciones de Apache o Dispatcher.

El patrón general de uso es `aio aem:rde:install <artifact>`.

A continuación se muestran algunos ejemplos:

<u>Implementación de un paquete de contenido</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

La respuesta para una implementación correcta es similar a la siguiente:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Opcionalmente, puede hacer referencia a un repositorio remoto:

`aio aem:rde:install 'https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip'`

<u>Implementación de una configuración OSGI</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

donde la respuesta para una implementación correcta es similar a la siguiente:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>Implementación de un paquete</u>

Para implementar un paquete, utilice:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

donde la respuesta para una implementación correcta es similar a la siguiente:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>Implementación de un archivo de contenido</u>

Para implementar un archivo de contenido, utilice:

`aio aem:rde:install world.txt -p /apps/hello.txt`

donde la respuesta para una implementación correcta es similar a la siguiente:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>Implementación de una configuración de Apache/Dispatcher</u>

Toda la estructura de carpetas debe presentar la forma de un archivo zip para este tipo de configuración. Puede comprimirlo ejecutando este comando desde la raíz de una carpeta de configuración de Dispatcher:

`zip -y -r dispatcher.zip`

a continuación, implemente la configuración mediante este comando:

`aio aem:rde:install -t dispatcher-config dispatcher-wknd-2.1.0.zip`

Una implementación correcta generará una respuesta similar a la siguiente:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

El código implementado en RDE no se somete a una canalización de Cloud Manager y sus puertas de calidad asociadas. Sin embargo, el código sí se somete a algún análisis, que informará de los errores, como se muestra en el siguiente ejemplo de código:

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

El ejemplo de código anterior ilustra el comportamiento si un paquete no se resuelve, en cuyo caso se &quot;configura&quot; y solo se instala si se cumplen sus requisitos (importaciones que faltan, en este caso) mediante la instalación de otro código.

### Comprobación del estado del RDE {#checking-rde-status}

Puede utilizar la CLI de RDE para comprobar si el entorno está listo para implementarse en, ya que las implementaciones se han realizado mediante el complemento RDE.

En ejecución:

`aio aem:rde:status`

devolverá:

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

Si el comando devuelve una nota sobre la implementación de instancias, puede continuar y realizar la siguiente actualización, pero es posible que la última no esté visible en la instancia.

### Mostrar historial de implementación {#show-deployment-history}

Puede comprobar el historial de implementaciones realizadas en RDE ejecutando:

`aio aem:rde:history`

que devuelve una respuesta en forma de:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Eliminación de RDE {#deleting-from-rde}

Puede eliminar configuraciones y paquetes que se hayan implementado anteriormente en RDE a través de las herramientas de CLI. Utilice la variable `status` para obtener una lista de lo que se puede eliminar, que incluye la variable `bsn` para paquetes y `pid` para las configuraciones a las que se hace referencia en el comando delete.

Por ejemplo, si `com.adobe.granite.demo.MyServlet.cfg.json` se ha instalado, la variable `bsn` es solo `com.adobe.granite.demo.MyServlet`, sin la variable **cfg.json** sufijo.

No se admite la eliminación de paquetes de contenido o archivos de contenido. Para eliminarlos, se debe restablecer el RDE, que lo devolverá a un estado predeterminado.

Consulte el ejemplo siguiente para obtener más información:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

## Restablecer {#reset-rde}

Al restablecer el RDE, se eliminan todos los códigos personalizados, las configuraciones y el contenido tanto del autor como de las instancias de publicación. Esto puede resultar útil, por ejemplo, si el RDE se ha utilizado para probar una función específica y desea restablecerla a un estado predeterminado para probar una función diferente.

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code will be deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role in order to be able to use the reset feature. If not, a reset action will result in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

Puede utilizar Cloud Manager para restablecer el RDE siguiendo los pasos siguientes:

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea restablecer el RDE.

1. En la página **Información general**, haga clic en la pestaña **Entornos** en la parte superior de la pantalla.

   ![Pestaña Entornos](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * También puede hacer clic en el botón **Mostrar todo** en la tarjeta **Entornos** para saltar directamente a la pestaña **Entornos**.

      ![Mostrar todas las opciones](/help/implementing/cloud-manager/assets/environment-showall.png)

1. La variable **Entornos** se abre y enumera todos los entornos del programa.

   ![La pestaña de entornos](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Haga clic en el botón de puntos suspensivos del RDE que desea restablecer y, a continuación, seleccione **Restablecer**.

   ![Ver detalles del entorno](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Confirme que desea restablecer el RDE haciendo clic en **Restablecer** en el cuadro de diálogo.

   ![Confirmar restablecimiento](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager confirma mediante una notificación de banner que se ha iniciado el proceso de restablecimiento.

   ![Restablecer notificación de banner](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

Una vez iniciado el proceso de restablecimiento de RDE, normalmente se tarda unos minutos en completar y devolver el entorno a su estado predeterminado. El estado del proceso de restablecimiento se puede ver en cualquier momento en la variable **Estado** de **Entornos** o en el **Entornos** ventana.

![Estado de restablecimiento de RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

También puede restablecer el RDE utilizando el botón de puntos suspensivos directamente desde el **Entornos** en el **Información general** página.

![Restablecer RDE desde la tarjeta Entornos](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Para obtener más información sobre cómo utilizar Cloud Manager para administrar sus entornos, consulte [la documentación de Cloud Manager.](/help/implementing/cloud-manager/manage-environments.md)

## Registro {#logging}

Los niveles de registro se pueden configurar modificando las configuraciones de OSGi. Marque la [documentación](/help/implementing/developing/introduction/logging.md) para obtener más información.

## ¿En qué se diferencian los RDE de los entornos de desarrollo de la nube? {#how-are-rds-different-from-cloud-development-environments}

Aunque el RDE es en muchos aspectos similar a un entorno de desarrollo de nube, hay algunas diferencias arquitectónicas menores para permitir una sincronización rápida del código. El mecanismo para obtener código para RDE es diferente: para RDE, uno sincroniza código de un entorno de desarrollo local, mientras que para entornos de desarrollo de nube, uno implementa código mediante Cloud Manager.

Por estos motivos, se recomienda que, después de validar el código en un entorno RDE, implemente el código en un entorno de desarrollo de nube mediante la canalización que no sea de producción. Finalmente, pruebe el código antes de implementarlo con la canalización de producción.

<!-- Temporarily hiding this. See CQDOC-19795 for more details

## How many RDEs do I need? {#how-many-rds-do-i-need}

The purchase of additional RDEs for Production programs will be possible beginning with late January.

The number of RDEs needed depends on the make-up and processes of an organization. The most flexible model is where an organization purchases a dedicated RDE for each one of their AEM CS developers. In this model, each developer can test their code on the RDE without needing to coordinate with other team members around whether an RDE environment is available.

At the other extreme, a team with a single RDE may use internal processes to coordinate which developer can use the environment at a given time. This can possibly be whenever a developer has hit an intermediate feature milestone and is ready to validate in a Cloud environment where they can quickly make the changes they need.

An intermediate model is one where an organization purchases a number of RDEs that will create a situation in which not every developer will have a dedicated environment, but there is a greater likelihood of an unused RDE being available. One strategy could be to allocate an RDE per scrum team or major feature. Internal processes may be used to coordinate usage of the environments. -->
