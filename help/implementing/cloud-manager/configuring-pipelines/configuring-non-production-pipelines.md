---
title: Adición de una canalización que no es de producción
description: Obtenga información sobre cómo añadir una canalización que no sea de producción para probar la calidad del código antes de implementarla en entornos de producción.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 7663af90b17e4b9d9567041c3bed8e20465c87d9
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 20%

---


# Adición de una canalización que no es de producción {#configuring-non-production-pipelines}

Después de configurar un programa y crear al menos un entorno en la interfaz de usuario de Cloud Manager, puede agregar canalizaciones que no sean de producción. Estas canalizaciones le permiten probar la calidad del código antes de implementarlo en entornos de producción.

Un usuario debe tener la función **[Administrador de implementación](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar canalizaciones que no sean de producción.

>[!NOTE]
>
>Puede [editar la configuración de canalización](managing-pipelines.md) después de la configuración inicial.

## Adición de una nueva canalización que no es de producción {#adding-non-production-pipeline}

Después de configurar un programa y crear al menos un entorno en la interfaz de usuario de Cloud Manager, puede agregar canalizaciones que no sean de producción. Utilice estas canalizaciones para probar la calidad del código antes de implementarlo en entornos de producción.

**Para agregar una nueva canalización que no sea de producción:**

1. Inicie sesión en Cloud Manager en [experiece.adobe.com](https://experience.adobe.com).
1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización que desee.
1. En la consola **Mis programas**, haga clic en un programa.
1. En el panel lateral izquierdo, haga clic en **Canalizaciones**.
1. En la página **Canalizaciones**, cerca de la esquina superior derecha, haga clic en **Agregar canalización** > **Agregar canalización que no sea de producción**.

   ![Agregar canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. En la ficha **Configuración** del cuadro de diálogo **Agregar canalización que no sea de producción**, seleccione una de las siguientes canalizaciones que no sean de producción que desee crear:

   * **Canalización de calidad de código**: crea una canalización que crea el código en una rama GIT, ejecuta pruebas unitarias y evalúa la calidad del código sin implementarlo en un entorno.
   * **Canalización de implementación**: crea una canalización que genera el código, ejecuta pruebas unitarias, evalúa la calidad del código y se implementa en un entorno que no es de producción.

   ![Cuadro de diálogo Agregar canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. En la sección **Configuración de canalización**, en el campo **Nombre de canalización que no es de producción**, escriba una descripción para la canalización que no es de producción.
1. En la sección **Opciones de implementación**, seleccione uno de los siguientes déclencheur de implementación que desee usar:

   * **Manual**: Le permite iniciar manualmente la canalización.
   * **Cambios en Git**: Inicia la canalización cuando se añaden confirmaciones a la rama de Git configurada. Con esta opción, aún puede iniciar la canalización manualmente, según sea necesario.

1. Seleccione el **Comportamiento de errores de métricas importantes** que desee usar.

   * **Preguntar cada vez**: esta es la configuración predeterminada y requiere intervención manual en caso de que se produzca algún error importante.
   * **Fallo inmediatamente**: si se selecciona, la canalización se cancela siempre que se produzca un fallo importante. Básicamente, emula a un usuario rechazando manualmente cada error.
   * **Continuar inmediatamente**: si se selecciona, la canalización se ejecuta automáticamente cada vez que se produzca un error importante. Básicamente, emula al usuario que aprueba manualmente cada error.

1. Haga clic en **Continuar**.

1. Los pasos restantes que utilice para completar la configuración de la canalización que no sea de producción dependen del tipo de código fuente que elija utilizar.
En la ficha **Código Source** del cuadro de diálogo **Agregar canalización que no sea de producción**, seleccione qué tipo de código debe procesar la canalización que no sea de producción.

   * **[Estoy usando código de pila completa](#full-stack-code)**
   * **[Estoy usando implementación dirigida](#targeted-deployment)**

   Consulte [Canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información sobre los tipos de canalizaciones.


### Estoy utilizando código de pila completa {#full-stack-code}

Una canalización de código de pila completa implementa simultáneamente generaciones de código back-end y front-end que contienen una o más aplicaciones de servidor de AEM junto con la configuración HTTPD/Dispatcher.

>[!NOTE]
>
>Si existe una canalización de código de pila completa para el entorno seleccionado, esta selección está deshabilitada.

Para finalizar la configuración de la canalización de no producción de código de pila completa, haga lo siguiente:

1. En la sección **Código Source**, defina las siguientes opciones.

   * **Entornos de implementación aptos**: solo disponible cuando edita una canalización que no es de producción. Si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.
   * **Repositorio**: en la lista desplegable, elija el repositorio Git que la canalización usa como origen. Cloud Manager genera código a partir del repositorio que elija aquí.

     >[!TIP]
     > 
     >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para poder aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: en la lista desplegable, elija desde qué rama del repositorio seleccionado se debe generar la canalización. El valor predeterminado es `main`. La canalización utiliza la rama elegida como origen para la compilación y la implementación. Si es necesario, haga clic en **Actualizar** para actualizar la lista de ramas disponibles para el repositorio seleccionado. Utilice esta opción si una rama creada recientemente no aparece en la lista.
   * **Estrategia de compilación**
      * **Compilación completa**: genera todos los módulos del repositorio cada vez
      * BETA **Smart Build**: genera solo módulos que han cambiado desde la última confirmación.<br>Obtenga más información acerca de [cómo usar Smart Build en una canalización que no es de producción](#about-smart-build-non-production-pipeline).

        >[!IMPORTANT]
        >
        >La generación inteligente solo está disponible para canalizaciones de calidad de código y canalizaciones de implementación de código de pila completa de desarrollo.

   * **Ignorar configuración de nivel web**: cuando está marcada, la canalización no implementa la configuración del nivel web.

1. En la sección **Canalización**, si la canalización es una canalización de implementación, puede elegir ejecutar una fase de prueba. Marque las opciones que desee habilitar en esta fase. Si no se selecciona ninguna de las opciones, la fase de prueba no se muestra durante la ejecución de la canalización.

   * **Prueba funcional del producto** - Ejecute [pruebas funcionales del producto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) en el entorno de desarrollo.
   * **Pruebas funcionales personalizadas** - Ejecute [pruebas funcionales personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) en el entorno de desarrollo.
   * **Pruebas de IU personalizadas** - Ejecutar [pruebas de IU personalizadas](/help/implementing/cloud-manager/ui-testing.md) para aplicaciones personalizadas.
   * **Auditoría de experiencias** - Ejecutar [Auditoría de experiencias](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Canalización de pila completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Haga clic en **Guardar**.

La canalización se ha guardado y ahora puede [administrar sus canalizaciones]&#x200B;(canalización de administración)
lines.md) en la tarjeta **Canalizaciones** de la página **Información general del programa**.

### Estoy utilizando la implementación dirigida {#targeted-deployment}

Una implementación de destino implementa código solo para partes seleccionadas de la aplicación de AEM. En una implementación de este tipo, puede elegir **Incluir** uno de los siguientes tipos de código:

![Opciones de implementación de destino](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment1.png)

<!--
* **Config** - Configure settings for various features in your AEM environment.
  * See [Using Config Pipelines](/help/operations/config-pipeline.md) for a list of supported configurations, which include log forwarding, purge-related maintenance tasks, and various CDN configurations, and to manage them in your repository so they are deployed properly.
  * When running a targeted deployment pipeline, configurations are deployed, provided they are saved to the environment, repository, and branch you defined in the pipeline.
  * At any time, there can only be one config pipeline per environment.
* **Configure Edge Delivery Services config pipeline** - Edge Delivery Configuration Pipelines do not have separate development, staging, and production environments. In AEM as a Cloud Service, changes move through development, stage, and production tiers. In contrast, an Edge Delivery Configuration Pipeline applies its configuration directly to all Edge Delivery Sites domains registered in Cloud Manager. To learn more, see [Add an Edge Delivery Pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
-->


* **Código front-end**: configure JavaScript y CSS para el front-end de su aplicación AEM.
   * Con las canalizaciones front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo se puede acelerar.
   * Consulte el documento [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber cómo funciona este proceso, así como algunas consideraciones que deben tenerse en cuenta para aprovechar al máximo este proceso.
* **Configuración de nivel web**: configure las propiedades de Dispatcher para almacenar, procesar y enviar páginas web al cliente.
   * Consulte el documento [Canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) para obtener más información.
   * Si existe una canalización de código de nivel web para el entorno seleccionado, esta selección está deshabilitada.
   * Si una canalización de pila completa ya se implementa en un entorno, aún puede crear una canalización de configuración de capa web para ese mismo entorno. Cuando lo haga, Cloud Manager ignorará la configuración del nivel web en la canalización de pila completa.

     >[!NOTE]
     >
     >Las canalizaciones de configuración de nivel web no son compatibles con los repositorios privados. Consulte [Agregar repositorios privados en Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obtener detalles y la lista completa de limitaciones.

<!--
The steps to complete the creation of your non-production, targeted deployment pipeline are the same once you choose a deployment type.

1. Choose which deployment type you require.

![Targeted deployment options](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Define the **Eligible Deployment Environments**.

   * If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
-->

1. En la sección **Código Source**, defina las siguientes opciones:

   * **Repositorio**: esta opción define desde qué repositorio GIT la canalización que no es de producción debe recuperar el código.

     >[!TIP]
     > 
     >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para poder aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código. Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo. Encuentra las ramas coincidentes que puede seleccionar.
   * **Ubicación del código**: esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.

<!--
   * **Pipeline** - For front-end non-production pipelines, you have the option to enable **[Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)**.
   
   ![Config pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)
-->

1. Si habilitó la auditoría de experiencias, haga clic en **Continuar** para avanzar a la pestaña **Auditoría de experiencias**, donde puede definir las rutas que siempre se deben incluir en la auditoría de experiencias.

   * Si habilitó **Auditoría de experiencias**, consulte el documento [Auditoría de experiencias](/help/implementing/cloud-manager/reports/report-experience-audit.md) para obtener detalles sobre cómo configurar.
   * Si no lo ha hecho, omita este paso.

1. Haga clic en **Guardar** para guardar la canalización.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.


## Acerca del uso de Smart Build en una canalización que no es de producción{#about-smart-build-non-production-pipeline}

**Smart Build** en Cloud Manager es una estrategia de compilación optimizada para canalizaciones que no son de producción. La versión inteligente reduce los tiempos de compilación al almacenar en caché los módulos y reconstruir solo los módulos que han cambiado desde la última ejecución correcta. Los módulos no modificados se reutilizan desde la caché, mientras que solo se reconstruyen los módulos modificados y sus dependencias, lo que mejora la eficacia de los flujos de trabajo de desarrollo iterativos.

Actualmente, Smart Build solo está disponible para lo siguiente:

* Código de calidad de las canalizaciones.
* Desarrollo de canalizaciones de implementación de pila completa.

>[!NOTE]
>
>La primera ejecución después de habilitar Smart Build se comporta como una compilación completa porque la caché está vacía.

Se recomienda Smart Build cuando se dispone de lo siguiente:

* Está desarrollando y comprometiendo activamente cambios incrementales frecuentes.
* El proyecto contiene varios módulos Maven.
* Las compilaciones completas están tardando un tiempo considerable.

Smart Build no siempre es ideal cuando se tiene lo siguiente:

* Su compilación se basa en gran medida en complementos que realizan operaciones fuera del gráfico de dependencias de Maven.
* Se requiere una validación de regeneración completa en cada ejecución.

### Comprender el rendimiento de compilación{#smart-build-performance}

La mejora del rendimiento obtenida mediante el uso de Smart Build depende de varios factores, entre los que se incluyen los siguientes:

* Número de módulos del proyecto.
* La frecuencia y el ámbito del código cambian.
* La distribución de dependencias entre módulos.

Generalmente, los proyectos con muchos módulos independientes pueden ver la mayor mejora.

### Exclusión de caché por módulo{#smart-build-cache-optout}

Smart Build proporciona un control detallado que le permite deshabilitar el almacenamiento en caché para módulos específicos. Esta capacidad es útil cuando se utilizan ciertos módulos:

* Use complementos, como `exec-maven-plugin` o `maven-antrun-plugin`.
* Realizar operaciones de archivo no rastreadas por dependencias de Maven.
* El contenido almacenado en caché produce resultados incoherentes.

### Deshabilitar el almacenamiento en caché de un módulo{#smart-build-disable-caching}

Puede agregar la siguiente propiedad al `pom.xml` del módulo afectado:

```xml
<properties>
  <maven.build.cache.enabled>false</maven.build.cache.enabled>
</properties>
```

Esta sintaxis fuerza al módulo a reconstruir en cada ejecución de canalización, mientras que otros módulos siguen beneficiándose del almacenamiento en caché.

### Limitaciones y consideraciones al utilizar Smart Build{#smart-build-limitations}

Tenga en cuenta lo siguiente al utilizar Smart Build:

* La generación inteligente se basa en el análisis de dependencias de Maven.
* Los cambios fuera del gráfico de dependencias no pueden almacenar en déclencheur las regeneraciones.
* Es posible que algunos complementos no sean totalmente compatibles con el almacenamiento en caché.
* Puede volver a **Compilación completa** en cualquier momento editando la canalización que no sea de producción.

Si encuentra un comportamiento de compilación inesperado, considere la posibilidad de deshabilitar el almacenamiento en caché para módulos específicos o cambiar temporalmente su estrategia de compilación a **Compilación completa**.

### Solución de problemas de Smart Build{#smart-build-troubleshoot}

| Problema | Soluciones sugeridas |
| --- | --- |
| Los resultados de la compilación son incoherentes | · Deshabilite el almacenamiento en caché para los módulos afectados.<br>· Compruebe el comportamiento de los complementos (especialmente los complementos `exec`/`antrun`). |
| Sin mejora de rendimiento | · Asegúrese de que se han producido varias ejecuciones (calentamiento de la caché).<br>· Compruebe si la mayoría de los módulos cambian con frecuencia. |
| Artefactos inesperados o cambios que faltan | · Revise si los cambios están fuera del seguimiento de dependencias de Maven.<br>· Use **Compilación completa** para la verificación. |

Consulte [Agregar una canalización que no sea de producción](#adding-non-production-pipeline) para habilitar Smart Build.











<!--
## Add a non-production pipeline {#adding-non-production-pipeline}

Once you have set up your program and have at least one environment using the Cloud Manager UI, you are ready to add a non-production pipeline by following these steps.

1. Sign into Cloud Manager at [experiece.adobe.com](https://experience.adobe.com).
1. In the **Quick access** section, click **Experience Manager**.
1. In the left side panel, click **Cloud Manager**.
1. Select an organization that you want.
1. On the **My Programs** console, click a program. 

1. Access the **Pipelines** card from the Cloud Manager home screen. Click **+Add** and select **Add Non-Production Pipeline**. 

   ![Add non-production pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. On the **Configuration** tab of the **Add Non-Production Pipeline** dialog, select the type of non-production pipeline you with to add.

   * **Code Quality Pipeline** - Create a pipeline that builds your code, runs unit tests, and evaluates code quality but does NOT deploy.
   * **Deployment Pipeline** - Create a pipeline that builds your code, runs unit tests, evaluates code quality, and deploys to an environment.

   ![Add Non-Production pipeline dialog](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Provide a **Non-Production Pipeline Name** to identify your pipeline along with the following additional information.

   * **Deployment Trigger** - You have the following options when defining the deployment triggers to start the pipeline.
   
     * **Manual** - Use this option to start the pipeline manually.
     * **On Git Changes** - This option starts the CI/CD pipeline whenever commits are added to the configured Git branch. With this option, you can still start the pipeline manually as required.

1. If you choose to create a **Deployment Pipeline**, you must also define the **Important Metric Failures Behavior**.

   * **Ask every time** - This behavior is the default setting and requires manual intervention on any important failure.
   * **Fail Immediately** - If selected, the pipeline is canceled whenever an important failure occurs. It is essentially emulating a user manually rejecting each failure.
   * **Continue Immediately** - If selected, the pipeline procedes automatically whenever an important failure occurs. It is essentially emulating a user manually approving each failure.

1. Click **Continue**.

1. On the **Source Code** tab of the **Add Non-Production Pipeline** dialog, you must select which type of code the pipeline should process.

   * **[Full Stack Code](#full-stack-code)**
   * **[Targeted deployment](#targeted-deployment)**

See [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) for more information about the types of pipelines.

The steps to complete the creation of your non-production pipeline vary depending on the type of source code you selected. Follow the links above to jump to the next section of this document so you can complete the configuration of your pipeline.

### Full Stack Code {#full-stack-code}

A full-stack code pipeline simultaneously deploys back-end and front-end code builds containing one or more AEM server applications along with HTTPD/Dispatcher configuration.

>[!NOTE]
>
>If a full-stack code pipeline exists for the selected environment, this selection is disabled.

To finish the configuration of the full-stack code non-production pipeline, follow these steps.

1. On the **Source Code** tab, you must define the following options.

   * **Eligible Deployment Environments** - If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
   * **Repository** - This option defines from which git repo that the pipeline should retrieve the code.

   >[!TIP]
   > 
   >See [Adding and Managing Repositories](/help/implementing/cloud-manager/managing-code/managing-repositories.md) so you can learn how to add and manage repositories in Cloud Manager.

   * **Git Branch** - This option defines from which branch in the selected pipeline should retrieve the code.
     * Enter the first few characters of the branch name and the auto-complete feature of this field. It helps you find the matching branches that you can select.
   * **Ignore Web Tier Configuration** - When checked, the pipeline does not deploy your web tier configuration.
   * **Pipeline** - If your pipeline is a deployment pipeline, you can choose to run a testing phase. Check the options that you want to enable in this phase. If none of the options are selected, the testing phase is not displayed during the pipeline's run.

     * **Product Functional Testing** - Execute [product functional tests](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) against the development environment.
     * **Custom Functional Testing** - Execute [custom functional tests](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) against the development environment.
     * **Custom UI Testing** - Execute [custom UI tests](/help/implementing/cloud-manager/ui-testing.md) for custom applications.
     * **Experience Audit** - Execute [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Full-stack pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Click **Save**.

The pipeline is saved and you can now [manage your pipelines](managing-pipelines.md) on the **Pipelines** card on the **Program Overview** page.

-->



## Excluir paquetes de Dispatcher {#exclude-dispatcher-packages}

Si desea que los paquetes de Dispatcher se creen en su canalización pero no se carguen en el almacenamiento de la compilación, deshabilite la publicación. Esto puede acortar el tiempo de ejecución de la canalización.

Agregue la siguiente configuración al archivo del proyecto `pom.xml` para deshabilitar la publicación de paquetes de Dispatcher. Establezca una variable de entorno en el contenedor de compilación de Cloud Manager para marcar cuándo se deben ignorar los paquetes de Dispatcher. La canalización lee este indicador e ignora en consecuencia.

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
