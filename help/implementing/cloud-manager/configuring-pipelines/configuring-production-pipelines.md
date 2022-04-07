---
title: Configuración de canalizaciones de producción
description: Aprenda a configurar canalizaciones de producción para crear e implementar su código en entornos de producción.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 9804d9b71f082c3d4788667fdc3993af3b673588
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 0%

---

# Configuración de una canalización de producción {#configure-production-pipeline}

Aprenda a configurar canalizaciones de producción para crear e implementar su código en entornos de producción.

Un usuario debe tener la variable **[Administrador de implementación](/help/onboarding/learn-concepts/cloud-manager-introduction.md#role-based-permissions)** para configurar las canalizaciones de producción.

>[!NOTE]
>
>No se puede configurar una canalización de producción hasta que se complete la creación del programa, un repositorio de Git tenga al menos una rama y se cree un conjunto de entornos de producción y ensayo.

Antes de comenzar a implementar el código, debe configurar la configuración de la canalización desde la [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Puede [editar configuración de canalización](managing-pipelines.md) después de la configuración inicial.

## Adición de una nueva canalización de producción {#adding-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno usando la variable [!UICONTROL Cloud Manager] En la interfaz de usuario de , puede añadir una canalización de producción siguiendo estos pasos.

>[!TIP]
>
>Antes de configurar una canalización front-end, consulte la [AEM Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para obtener una guía completa a través de la herramienta de creación rápida AEM sitios fácil de usar. Este recorrido le ayudará a optimizar el desarrollo front-end de su sitio AEM, lo que le permitirá personalizar rápidamente su sitio sin AEM conocimiento del back-end.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la **Canalizaciones** de la **Información general del programa** página y haga clic en **Agregar** para seleccionar **Agregar canalización de producción**.

   ![La tarjeta canalizaciones de la descripción general del Administrador de programas](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. La variable **Agregar canalización de producción** se abre. Proporcione un **Nombre de canalización** para identificar la canalización junto con las siguientes opciones. Haga clic en **Continuar**.

   **Déclencheur de implementación** : dispone de las siguientes opciones al definir los déclencheur de implementación para iniciar la canalización.

   * **Manual** - Utilice esta opción para iniciar manualmente la canalización.
   * **Cambios en Git** - Esta opción inicia la canalización CI/CD cada vez que se añaden confirmaciones a la rama git configurada. Con esta opción, aún puede iniciar la canalización manualmente según sea necesario.

   **Comportamiento de errores de métricas importantes** - Durante la configuración o edición de la canalización, la variable **Administrador de implementación** tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad. Las opciones disponibles son:

   * **Pregunte cada vez** - Esta es la configuración predeterminada y requiere intervención manual en caso de que se produzca algún error importante.
   * **Fallo Inmediatamente** - Si se selecciona, la canalización se cancelará siempre que se produzca un fallo importante. Básicamente, esto emula a un usuario rechazando manualmente cada error.
   * **Continuar inmediatamente** - Si se selecciona, la canalización se realizará automáticamente cada vez que se produzca un error importante. Básicamente, esto está emulando a un usuario que aprueba manualmente cada error.

   ![Configuración de canalización de producción](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. En el **Código fuente** debe definir dónde debe recuperar la canalización su código y qué tipo de código es.

   * **[Código front-end](#front-end-code)**
   * **[Código de pila completa](#full-stack-code)**
   * **[Configuración de nivel web](#web-tier-config)**

Los pasos para completar la creación de la canalización de producción varían según la opción de **Código fuente** ha seleccionado. Siga los enlaces anteriores para ir a la siguiente sección de este documento para completar la configuración de la canalización.

### Código front-end {#front-end-code}

Una canalización de código front-end implementa las compilaciones de código front-end que contienen una o más aplicaciones de interfaz de usuario del lado del cliente. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obtener más información sobre este tipo de canalización.

Para finalizar la configuración de la canalización de producción de código front-end, siga estos pasos.

1. En el **Código fuente** , debe definir las siguientes opciones.

   * **Repositorio** - Esta opción define desde qué repositorio de Git la canalización debe recuperar el código.
   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git** - Esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.
   * **Ubicación del código** - Esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
   * **Pausar antes de implementar en producción** : Esta opción pone en pausa la canalización antes de implementarla en producción.

   ![Código front-end](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. Haga clic en **Guardar** para guardar la canalización.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en el **Canalizaciones** en el **Información general del programa** página.

### Código de pila completa {#full-stack-code}

Una canalización de código de pila completa implementa simultáneamente compilaciones de código de back-end y front-end que contienen una o más aplicaciones de servidor AEM junto con la configuración HTTPD/Dispatcher. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) para obtener más información sobre este tipo de canalización.

>[!NOTE]
>
>Si ya existe una canalización de código de pila completa para el entorno seleccionado, esta selección se desactivará.

Para finalizar la configuración de la canalización de producción de código de pila completa, siga estos pasos.

1. En el **Código fuente** , debe definir las siguientes opciones.

   * **Repositorio** - Esta opción define desde qué repositorio de Git la canalización debe recuperar el código.
   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git** - Esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.
   * **Ubicación del código** - Esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
   * **Pausar antes de implementar en producción** : Esta opción pone en pausa la canalización antes de implementarla en producción.
   * **Programado** : esta opción permite al usuario activar la implementación de producción programada.

   ![Código de pila completo](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Haga clic en **Continuar** para avanzar al **Auditoría de experiencias** , donde puede definir las rutas que siempre deben incluirse en la auditoría de experiencias.

   ![Añadir auditoría de experiencia](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Proporcione una ruta que se incluya en la auditoría de experiencias.

   * Las rutas de página deben comenzar con `/`.
   * Por ejemplo, si desea incluir `https://wknd.site/us/en/about-us.html` en la auditoría de experiencias, introduzca la ruta `/us/en/about-us.html`.

   ![Definición de una ruta para la auditoría de experiencias](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. Haga clic en **Agregar página** y la ruta se completará automáticamente con la dirección de su entorno y se agregará a la tabla de rutas.

   ![Guardar ruta de acceso a la tabla](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. Siga agregando rutas según sea necesario repitiendo los dos pasos anteriores.

   * Puede agregar un máximo de 25 rutas.
   * Si no define ninguna ruta, la página principal del sitio se incluirá en la auditoría de experiencias de forma predeterminada.

1. Haga clic en **Guardar** para guardar la canalización.

Las rutas configuradas para la auditoría de experiencias se enviarán al servicio y se evaluarán según las pruebas de rendimiento, accesibilidad, SEO (Optimización del motor de búsqueda), prácticas recomendadas y PWA (Aplicación web progresiva) cuando se ejecute la canalización. Consulte [Comprender los resultados de la auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en el **Canalizaciones** en el **Información general del programa** página.

### Configuración de nivel web {#web-tier-config}

Una canalización de configuración de nivel web implementa las configuraciones de HTTPD/Dispatcher. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) para obtener más información sobre este tipo de canalización.

Para finalizar la configuración de la canalización de producción de código de pila completa, siga estos pasos.

1. En el **Código fuente** , debe definir las siguientes opciones.

   * **Repositorio** - Esta opción define desde qué repositorio de Git la canalización debe recuperar el código.
   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git** - Esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.
   * **Ubicación del código** - Esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
      * Para las canalizaciones de configuración de nivel web, esta es normalmente la ruta que contiene `conf.d`, `conf.dispatcher.d`y `opt-in` directorios.
      * Por ejemplo, si la estructura del proyecto se generó a partir de la variable [AEM tipo de archivo del proyecto,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) la ruta sería `/dispatcher/src`.
   * **Pausar antes de implementar en producción** : Esta opción pone en pausa la canalización antes de implementarla en producción.
   * **Programado** : esta opción permite al usuario activar la implementación de producción programada.

   ![Código de capa web](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. Haga clic en **Guardar** para guardar la canalización.

>[!NOTE]
>
>Si tiene una canalización de pila completa existente implementando en un entorno, al crear una canalización de configuración de capa web para el mismo entorno, se omitirá la configuración de capa web existente en la canalización de pila completa.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en el **Canalizaciones** en el **Información general del programa** página.

## Omitir paquetes de Dispatcher {#skip-dispatcher-packages}

Si desea que los paquetes de Dispatcher se creen como parte de la canalización, pero no desea que se publiquen para crear almacenamiento, puede desactivar la publicación, lo que puede reducir la duración de la ejecución de la canalización.

La siguiente configuración para deshabilitar la publicación de paquetes de Dispatcher debe agregarse a través del proyecto `pom.xml` archivo. Se basa en una variable de entorno, que sirve como indicador que puede establecer en el contenedor de compilación de Cloud Manager para definir cuándo se deben ignorar los paquetes de Dispatcher.

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
