---
title: Configuración de canalizaciones que no sean de producción
description: Obtenga información sobre cómo configurar canalizaciones que no sean de producción para probar la calidad del código antes de implementarlas en entornos de producción.
index: true
source-git-commit: e2031cabfa06a4d55dfa3ec0a77d3d3b0f835f5b
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 1%

---


# Configuración de canalizaciones que no sean de producción {#configuring-non-production-pipelines}

Obtenga información sobre cómo configurar canalizaciones que no sean de producción para probar la calidad del código antes de implementarlas en entornos de producción.

## Canalizaciones que no son de producción {#non-production-pipelines}

Además de [canalizaciones de producción](#configuring-production-pipelines.md) que se implementa en entornos de ensayo y producción, también puede configurar canalizaciones que no sean de producción para validar el código.

Existen dos tipos de canalizaciones que no son de producción:

* **Canalizaciones de calidad de código** : ejecutan análisis de calidad del código en el código de una rama de Git y ejecutan los pasos de compilación y calidad del código.
* **Canalizaciones de implementación** - Además de ejecutar los pasos de compilación y calidad del código como las canalizaciones de calidad del código, estas canalizaciones implementan el código en un entorno que no es de producción.

>[!NOTE]
>
>Puede [editar configuración de canalización](managing-pipelines.md) después de la configuración inicial.

## Adición de una nueva canalización que no sea de producción {#adding-non-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno utilizando la interfaz de usuario de Cloud Manager, estará listo para agregar una canalización que no sea de producción siguiendo estos pasos.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Acceda a la **Canalizaciones** de la pantalla de inicio de Cloud Manager. Haga clic en **+Añadir** y seleccione **Agregar canalización que no sea de producción**.

   ![Añadir canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. En el **Configuración** de la pestaña **Agregar canalización que no sea de producción** , seleccione el tipo de canalización que no sea de producción que desee añadir, ya sea **Canalización de calidad de código** o **Canalización de implementación**.

   ![Cuadro de diálogo Agregar canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Proporcione un **Nombre de canalización que no es de producción** para identificar la canalización junto con la siguiente información adicional.

   * **Déclencheur de implementación** : dispone de las siguientes opciones al definir los déclencheur de implementación para iniciar la canalización.

      * **Manual** - Utilice esta opción para iniciar manualmente la canalización.
      * **Cambios en Git** - Esta opción inicia la canalización CI/CD cada vez que se añaden confirmaciones a la rama git configurada. Con esta opción, aún puede iniciar la canalización manualmente según sea necesario.
   * **Comportamiento de errores de métricas importantes** - Durante la configuración o edición de la canalización, la variable **Administrador de implementación** tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad. Tiene las opciones siguientes.

      * **Pregunte cada vez** - Esta es la configuración predeterminada y requiere intervención manual en caso de que se produzca algún error importante.
      * **Fallo Inmediatamente** - Si se selecciona, la canalización se cancelará siempre que se produzca un fallo importante. Básicamente, esto emula a un usuario rechazando manualmente cada error.
      * **Continuar inmediatamente** - Si se selecciona, la canalización se realizará automáticamente cada vez que se produzca un error importante. Básicamente, esto está emulando a un usuario que aprueba manualmente cada error.


1. Haga clic en **Continuar**.

1. En el **Código fuente** de la pestaña **Agregar canalización que no sea de producción** , debe seleccionar qué tipo de código debe procesar la canalización.

   * **[Código front-end](#front-end-code)**
   * **[Código de pila completa](#full-stack-code)**
   * **[Configuración de nivel web](#web-tier-config)**

Los pasos para completar la creación de la canalización que no es de producción varían según la opción de **Código fuente** ha seleccionado. Siga los enlaces anteriores para ir a la siguiente sección de este documento para completar la configuración de la canalización.

### Código front-end {#front-end-code}

Una canalización de código front-end implementa las compilaciones de código front-end que contienen una o más aplicaciones de interfaz de usuario del lado del cliente. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obtener más información sobre este tipo de canalización.

Para finalizar la configuración de la canalización de no producción de código front-end, siga estos pasos.

1. En el **Código fuente** , debe definir las siguientes opciones.

   * **Entornos de implementación aptos** : Si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.
   * **Repositorio** - Esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git** - Esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
   * **Ubicación del código** - Esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.

   ![Canalización front-end](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. Haga clic en **Guardar**.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en el **Canalizaciones** en el **Información general del programa** página.

### Código de pila completa {#full-stack-code}

Una canalización de código de pila completa implementa simultáneamente compilaciones de código de back-end y front-end que contienen una o más aplicaciones de servidor AEM junto con la configuración HTTPD/Dispatcher. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) para obtener más información sobre este tipo de canalización.

>[!NOTE]
>
>Si ya existe una canalización de código de pila completa para el entorno seleccionado, esta selección se desactivará.

Para finalizar la configuración de la canalización de no producción de código de pila completa, siga estos pasos.

1. En el **Código fuente** , debe definir las siguientes opciones.

   * **Entornos de implementación aptos** : Si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.
   * **Repositorio** - Esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git** - Esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
   * **Ignorar configuración de nivel web** -

   ![Canalización de pila completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Haga clic en **Guardar**.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en el **Canalizaciones** en el **Información general del programa** página.

### Configuración de nivel web {#web-tier-config}

Una canalización de configuración de nivel web implementa las configuraciones de HTTPD/Dispatcher. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) para obtener más información sobre este tipo de canalización.

>[!NOTE]
>
>Si ya existe una canalización de código de capa web para el entorno seleccionado, se desactivará esta selección.

Para finalizar la configuración de la canalización de no producción de código de capa web, siga estos pasos.

1. En el **Código fuente** , debe definir las siguientes opciones.

   * **Entornos de implementación aptos** : Si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.
   * **Repositorio** - Esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte el documento [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git** - Esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
   * **Ubicación del código** - Esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
      * Para las canalizaciones de configuración de nivel web, esta es normalmente la ruta que contiene `conf.d`, `conf.dispatcher.d`y `opt-in` directorios.
      * Por ejemplo, si la estructura del proyecto se generó a partir de la variable [AEM tipo de archivo del proyecto,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) la ruta sería `/dispatcher/src`.

   ![Canalización de niveles web](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. Haga clic en **Guardar**.

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
