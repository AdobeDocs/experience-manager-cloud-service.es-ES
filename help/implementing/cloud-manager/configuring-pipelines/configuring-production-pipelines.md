---
title: Añadir una canalización de producción
description: Aprenda a añadir una canalización de producción para crear e implementar su código en entornos de producción.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 35%

---


# Añadir una canalización de producción {#configure-production-pipeline}

Obtenga información sobre cómo configurar canalizaciones de producción para crear e implementar su código en entornos de producción. Una canalización de producción implementa el código primero en el entorno de ensayo. En el momento de la aprobación, implementa el mismo código en el entorno de producción.

Un usuario debe tener la función **[Administrador de implementación](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar las canalizaciones de producción.

>[!NOTE]
>
>No se puede configurar una canalización de producción hasta que se produzca lo siguiente:
>
>* Se crea el programa.
>* El repositorio de Git tiene al menos una rama.
>* Se crean los entornos de producción y ensayo.

Antes de comenzar a implementar el código, establece la configuración de la canalización desde [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Puede [editar la configuración de canalización](managing-pipelines.md) después de la configuración inicial.

## Adición de una nueva canalización de producción {#adding-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno usando la interfaz de usuario de [!UICONTROL Cloud Manager], podrá agregar una canalización de producción siguiendo estos pasos.

>[!TIP]
>
>Antes de configurar una canalización front-end, consulte el [Recorrido de creación rápida de sitios de AEM](/help/journey-sites/quick-site/overview.md) para obtener una guía completa a través de la herramienta de creación rápida de sitios de AEM fácil de usar. Este recorrido puede ayudarle a optimizar el desarrollo front-end de su sitio de AEM, lo que le permite personalizar su sitio rápidamente sin conocimiento del back-end de AEM.

1. Inicie sesión en Cloud Manager en [experiece.adobe.com](https://experience.adobe.com).
1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización que desee.
1. En la consola **Mis programas**, haga clic en un programa.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Vaya a la tarjeta **Canalizaciones** de la página **Resumen del programa** y haga clic en **Agregar** para seleccionar **Agregar canalización de producción**.

   ![Información general de la tarjeta Canalizaciones de Administrador de programa](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Aparece el cuadro de diálogo **Agregar canalización de producción**. Proporcione un **Nombre de canalización** para identificar la canalización junto con las siguientes opciones. Haga clic en **Continuar**.

   **Activador de implementación**: dispone de las siguientes opciones al definir los activadores de implementación para iniciar la canalización.

   * **Manual**: inicie la canalización manualmente.
   * **Cambios en Git**: inicia la canalización de CI/CD cada vez que se agregan confirmaciones a la rama Git configurada. Con esta opción, aún puede iniciar la canalización manualmente según sea necesario.

   **Comportamiento de errores de métricas importantes**: durante la configuración o edición de la canalización, el **Administrador de implementación** tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad. Las opciones disponibles son:

   * **Preguntar cada vez**: configuración predeterminada. Requiere intervención manual en cualquier fallo importante.
   * **Fallo inmediatamente**: si se selecciona, la canalización se cancela siempre que se produzca un fallo importante. Básicamente, este proceso emula a un usuario rechazando manualmente cada error.
   * **Continuar inmediatamente**: si se selecciona, la canalización se ejecuta automáticamente cada vez que se produce un error importante. Básicamente, este proceso emula al usuario que aprueba manualmente cada error.

   ![Configuración de canalización de producción](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. En la ficha **Código Source**, seleccione qué tipo de código debe procesar la canalización.

   * **[Configurar una canalización de código de pila completa](#full-stack-code)**
   * **[Configurar una canalización de implementación de destino](#targeted-deployment)**

Consulte [Canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información sobre los tipos de canalizaciones.

Los pasos para completar la creación de la canalización de producción varían según el tipo de código fuente seleccionado. Siga los vínculos anteriores para ir a la siguiente sección de este documento para poder completar la configuración de la canalización.

### Configuración de una canalización de código de pila completa {#full-stack-code}

Una canalización de código de pila completa implementa simultáneamente generaciones de código back-end y front-end que contienen una o más aplicaciones de servidor de AEM junto con la configuración HTTPD/Dispatcher.

>[!NOTE]
>
>Si ya existe una canalización de código de pila completa para el entorno seleccionado, esta selección se desactiva.

**Para configurar una canalización de código de pila completa:**

1. En la ficha **Código Source**, defina las siguientes opciones.

   * **Repositorio**: define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte [Agregar y administrar repositorios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para obtener información sobre cómo agregar y administrar repositorios en Cloud Manager.

   * **Rama de Git**: define desde qué rama la canalización seleccionada debe recuperar el código.
Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo encontrará las ramas coincidentes que le ayudarán a seleccionar.
   * **Ignorar configuración de nivel web**: cuando se selecciona, la canalización no implementa la configuración del nivel web.
   * **Pausar antes de implementar en producción**: pausa la canalización antes de implementarla en producción.
   * **Programado**: permite al usuario habilitar la implementación de producción programada.

   ![Código de pila completa](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Haga clic en **Continuar** para avanzar a la pestaña **Auditoría de experiencias**, donde puede definir las rutas que siempre deben incluirse en la auditoría de experiencias.

   ![Añadir auditoría de experiencias](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Proporcione las rutas que se incluirán en la auditoría de experiencias.

   * Consulte [Pruebas de auditoría de experiencias](/help/implementing/cloud-manager/reports/report-experience-audit.md#configuration) para obtener más información.

1. Haga clic en **Guardar** para guardar la canalización.

Cuando se ejecuta la canalización, las rutas configuradas para la auditoría de experiencias se envían y evalúan en función del rendimiento, la accesibilidad, la SEO, las prácticas recomendadas y las pruebas de PWA. Para obtener más información, consulte [Comprender los resultados de la auditoría de experiencias](/help/implementing/cloud-manager/reports/report-experience-audit.md).

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

### Configuración de una canalización de implementación de destino {#targeted-deployment}

Una implementación de destino implementa código solo para partes seleccionadas de la aplicación de AEM. En una implementación de este tipo, puede elegir **Incluir** uno de los siguientes tipos de código:

* **Configuración**: configure las opciones para varias características de su entorno de AEM.
   * Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md) para obtener una lista de las configuraciones admitidas, que incluyen el reenvío de registros, las tareas de mantenimiento relacionadas con la depuración y varias configuraciones de CDN, y para administrarlas en el repositorio de modo que se implementen correctamente.
   * Al ejecutar una canalización de implementación de destino, se implementan las configuraciones, siempre que se guarden en el entorno, el repositorio y la rama definidos en la canalización.
   * En cualquier momento, solo puede haber una canalización de configuración por entorno.
* **Configurar canalización de configuración de Edge Delivery Services**: las canalizaciones de configuración de Edge Delivery no tienen entornos de desarrollo, ensayo y producción independientes. En AEM as a Cloud Service, los cambios se mueven a través de los niveles de desarrollo, fase y producción. Por el contrario, una canalización de configuración de Edge Delivery aplica su configuración directamente a todos los dominios de Edge Delivery Sites registrados en Cloud Manager. Para obtener más información, consulte [Agregar una canalización de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
* **Código front-end**: configure JavaScript y CSS para el front-end de su aplicación AEM.
   * Con las canalizaciones front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo se puede acelerar.
   * Consulte el documento [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber cómo funciona este proceso, así como algunas consideraciones que deben tenerse en cuenta para aprovechar al máximo este proceso.
* **Configuración de nivel web**: configure las propiedades de Dispatcher para almacenar, procesar y enviar páginas web al cliente.
   * Consulte el documento [Canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) para obtener más información.
   * Si existe una canalización de código de nivel web para el entorno seleccionado, esta selección está deshabilitada.
   * Si crea una canalización de configuración de nivel web para un entorno con una canalización de pila completa existente, se ignorará la configuración de nivel web en la canalización de pila completa. Este cambio solo afecta a la configuración del nivel web en ese entorno.

>[!NOTE]
>
>Las canalizaciones de configuración de nivel web no son compatibles con los repositorios privados. Consulte [Agregar repositorios privados en Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obtener detalles y la lista completa de limitaciones.

**Para configurar una canalización de implementación de destino:**

1. Elija el tipo de implementación que necesita.

![Opciones de implementación de destino](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. Defina los **Entornos de implementación aptos**.

   * Si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.

1. En **Código Source**, defina las siguientes opciones:

   * **Repositorio**: esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para poder aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo. Encuentra las ramas coincidentes que puede seleccionar.
   * **Ubicación del código**: esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
   * **Pausar antes de implementar en producción**: esta opción pone en pausa la canalización antes de implementarla en producción.
   * **Programado**: permite al usuario habilitar la implementación de producción programada. Solo disponible para implementaciones de destino de nivel web.

   ![Canalización de configuración](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. Haga clic en **Guardar**.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

## Omitir paquetes de Dispatcher {#skip-dispatcher-packages}

Para crear paquetes de Dispatcher en la canalización sin publicarlos en el almacenamiento de compilación, puede desactivar la opción de publicación. Hacerlo puede ayudar a reducir el tiempo de ejecución de la canalización.

La siguiente configuración para deshabilitar la publicación de paquetes de Dispatcher debe agregarse a través del archivo `pom.xml` del proyecto. Una variable de entorno sirve como un indicador que se establece en el contenedor de compilación de Cloud Manager para determinar cuándo se deben ignorar los paquetes de Dispatcher.

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
