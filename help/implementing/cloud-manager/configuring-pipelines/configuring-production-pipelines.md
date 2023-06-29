---
title: Configurar canalizaciones de producción
description: Aprenda a configurar canalizaciones de producción para crear e implementar su código en entornos de producción.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 90%

---


# Configuración de una canalización de producción {#configure-production-pipeline}

Aprenda a configurar canalizaciones de producción para crear e implementar su código en entornos de producción. Una canalización de producción implementa el código primero en el entorno de ensayo y, tras la aprobación, implementa el mismo código en el entorno de producción.

Un usuario debe tener la función **[Administrador de implementación](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar las canalizaciones de producción.

>[!NOTE]
>
>No se puede configurar una canalización de producción hasta que se complete la creación del programa, un repositorio de Git tenga al menos una rama y se cree un conjunto de entornos de producción y ensayo.

Antes de comenzar a implementar el código, debe configurar la configuración de la canalización desde [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Puede [editar la configuración de canalización](managing-pipelines.md) después de la configuración inicial.

## Adición de una nueva canalización de producción {#adding-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno usando la interfaz de usuario de [!UICONTROL Cloud Manager], puede añadir una canalización de producción siguiendo estos pasos.

>[!TIP]
>
>Antes de configurar una canalización front-end, consulte [Recorrido de creación rápida de sitios de AEM](/help/journey-sites/quick-site/overview.md) para obtener una guía completa a través de la herramienta de creación rápida de sitios de AEM fácil de usar. Este recorrido le ayudará a optimizar el desarrollo front-end de su sitio de AEM, lo que le permitirá personalizar rápidamente su sitio sin conocimiento del back-end de AEM.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Información general del programa** y haga clic en **Agregar** para seleccionar **Agregar canalización de producción**.

   ![Información general de la tarjeta Canalizaciones de Administrador de programa](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Aparece el cuadro de diálogo **Agregar canalización de producción**. Proporcione un **Nombre de canalización** para identificar la canalización junto con las siguientes opciones. Haga clic en **Continuar**.

   **Activador de implementación**: dispone de las siguientes opciones al definir los activadores de implementación para iniciar la canalización.

   * **Manual**: utilice esta opción para iniciar manualmente la canalización.
   * **Cambios en Git**: esta opción inicia la canalización CI/CD cada vez que se añaden confirmaciones a la rama git configurada. Con esta opción, aún puede iniciar la canalización manualmente según sea necesario.

   **Comportamiento de errores de métricas importantes**: durante la configuración o edición de la canalización, el **Administrador de implementación** tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad. Las opciones disponibles son:

   * **Preguntar cada vez**: esta es la configuración predeterminada y requiere intervención manual en caso de que se produzca algún error importante.
   * **Fallo inmediatamente** : si se selecciona, la canalización se cancela siempre que se produce un error importante. Básicamente, esto emula a un usuario rechazando manualmente cada error.
   * **Continuar inmediatamente**: si se selecciona, la canalización se realizará automáticamente cada vez que se produzca un error importante. Básicamente, esto está emulando a un usuario que aprueba manualmente cada error.

   ![Configuración de canalización de producción](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. En el **Código fuente** debe definir dónde debe recuperar la canalización su código y qué tipo de código es.

   * **[Código front-end](#front-end-code)**
   * **[Código de pila completa](#full-stack-code)**
   * **[Configuración de nivel web](#web-tier-config)**

Los pasos para completar la creación de la canalización de producción varían según la opción de **Código fuente** que haya seleccionado. Siga los enlaces anteriores para ir a la siguiente sección de este documento para completar la configuración de la canalización.

### Código front-end {#front-end-code}

Una canalización de código front-end implementa las compilaciones de código front-end que contienen una o más aplicaciones de interfaz de usuario del lado del cliente. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obtener más información sobre este tipo de canalización.

Para finalizar la configuración de la canalización de producción de código front-end, siga estos pasos.

1. En el **Código fuente**, debe definir las siguientes opciones.

   * **Repositorio**: esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.
   * **Ubicación del código**: esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
   * **Pausar antes de implementar en producción**: esta opción pone en pausa la canalización antes de implementarla en producción.

   ![Código front-end](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. Haga clic en **Guardar** para guardar la canalización.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

### Código de pila completa {#full-stack-code}

Una canalización de código de pila completa implementa simultáneamente compilaciones de código de back-end y front-end que contienen una o más aplicaciones de servidor AEM junto con la configuración HTTPD/Dispatcher. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) para obtener más información sobre este tipo de canalización.

>[!NOTE]
>
>Si ya existe una canalización de código de pila completa para el entorno seleccionado, esta selección está desactivada.

Para finalizar la configuración de la canalización de producción de código de pila completa, siga estos pasos.

1. En el **Código fuente**, debe definir las siguientes opciones.

   * **Repositorio**: esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.
   * **Ubicación del código**: esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
   * **Pausar antes de implementar en producción**: esta opción pone en pausa la canalización antes de implementarla en producción.
   * **Programada**: esta opción permite al usuario activar la implementación de producción programada.

   ![Código de pila completa](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Haga clic en **Continuar** para avanzar a la pestaña **Auditoría de experiencias**, donde puede definir las rutas que siempre deben incluirse en la auditoría de experiencias.

   ![Añadir auditoría de experiencias](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Proporcione una ruta que se incluya en la auditoría de experiencias.

   * Las rutas de página deben comenzar con `/`.
   * Por ejemplo, si desea incluir `https://wknd.site/us/en/about-us.html` en la auditoría de experiencias, introduzca la ruta `/us/en/about-us.html`.

   ![Definición de una ruta para la auditoría de experiencias](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. Clic **Agregar página** y la ruta se completa automáticamente con la dirección de su entorno y se agrega a la tabla de rutas.

   ![Guardar ruta de acceso a la tabla](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. Siga agregando rutas según sea necesario repitiendo los dos pasos anteriores.

   * Puede agregar un máximo de 25 rutas.
   * Si no define ninguna ruta, la página principal del sitio se incluye en la auditoría de experiencias de forma predeterminada.

1. Haga clic en **Guardar** para guardar la canalización.

Las rutas configuradas para la auditoría de experiencias se envían al servicio y se evalúan según las pruebas de rendimiento, accesibilidad, SEO (Optimización del motor de búsqueda), prácticas recomendadas y PWA (Aplicación web progresiva) cuando se ejecuta la canalización. Consulte [Comprender los resultados de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

### Configuración de nivel web {#web-tier-config}

Una canalización de configuración de nivel web implementa las configuraciones de HTTPD/Dispatcher. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) para obtener más información sobre este tipo de canalización.

Para finalizar la configuración de la canalización de producción de código de pila completa, siga estos pasos.

1. En el **Código fuente**, debe definir las siguientes opciones.

   * **Repositorio**: esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.
   * **Ubicación del código**: esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
      * Para las canalizaciones de configuración de nivel web, esta es normalmente la ruta que contiene los directorios `conf.d`, `conf.dispatcher.d` y `opt-in`.
      * Por ejemplo, si la estructura del proyecto se generó a partir del [tipo de archivo del proyecto de AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) la ruta sería `/dispatcher/src`.
   * **Pausar antes de implementar en producción**: esta opción pone en pausa la canalización antes de implementarla en producción.
   * **Programada**: esta opción permite al usuario activar la implementación de producción programada.

   ![Código de capa web](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. Haga clic en **Guardar** para guardar la canalización.

>[!NOTE]
>
>Si tiene una canalización de pila completa existente implementando en un entorno, al crear una canalización de configuración de capa web para el mismo entorno, se omitirá la configuración de capa web existente en la canalización de pila completa.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

## Desarrollo de Sites con la canalización front-end {#developing-with-front-end-pipeline}

Con las canalizaciones front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo se puede acelerar.

Consulte [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber cómo funciona este proceso, así como algunas consideraciones que deben tenerse en cuenta para aprovechar al máximo este proceso.

## Omitir paquetes de Dispatcher {#skip-dispatcher-packages}

Si desea que los paquetes de Dispatcher se creen como parte de la canalización, pero no desea que se publiquen para crear almacenamiento, puede desactivar la publicación, lo que puede reducir la duración de la ejecución de la canalización.

La siguiente configuración para deshabilitar la publicación de paquetes de Dispatcher debe agregarse a través del archivo `pom.xml` del proyecto. Se basa en una variable de entorno, que sirve como un indicador que puede establecer en el contenedor de compilación de Cloud Manager para definir cuándo se deben ignorar los paquetes de Dispatcher.

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
