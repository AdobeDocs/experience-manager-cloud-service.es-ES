---
title: Configurar canalizaciones que no sean de producción
description: Obtenga información sobre cómo configurar canalizaciones que no sean de producción para probar la calidad del código antes de implementarlas en entornos de producción.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '1356'
ht-degree: 100%

---


# Configurar canalizaciones que no sean de producción {#configuring-non-production-pipelines}

Obtenga información sobre cómo configurar canalizaciones que no sean de producción para probar la calidad del código antes de implementarlas en entornos de producción.

## Canalizaciones que no son de producción {#non-production-pipelines}

Además de [canalizaciones de producción](#configuring-production-pipelines.md) que se implementan en entornos de ensayo y producción, también puede configurar canalizaciones que no sean de producción para validar el código.

Existen dos tipos de canalizaciones que no son de producción:

* **Canalizaciones de calidad de código**: ejecutan análisis de calidad del código en el código de una rama de Git y ejecutan los pasos de compilación y calidad del código.
* **Canalizaciones de implementación**: además de ejecutar los pasos de compilación y calidad del código como las canalizaciones de calidad del código, estas canalizaciones implementan el código en un entorno que no es de producción.

>[!NOTE]
>
>Puede [editar la configuración de canalización](managing-pipelines.md) después de la configuración inicial.

## Adición de una nueva canalización que no sea de producción {#adding-non-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno utilizando la interfaz de usuario de Cloud Manager, estará listo para agregar una canalización que no sea de producción siguiendo estos pasos.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Acceda a la tarjeta **Canalizaciones** de la pantalla de inicio de Cloud Manager. Haga clic en **+Agregar** y seleccione **Añadir canalización que no es de producción**.

   ![Agregar canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. En la pestaña **Configuración** del cuadro de diálogo **Agregar canalización que no sea de producción**, seleccione el tipo de canalización que no sea de producción que desee agregar.

   * **Canalización de calidad de código**: cree una canalización que desarrolle su código, ejecute pruebas unitarias y evalúe la calidad del código, pero no la implemente.
   * **Canalización de implementación**: cree una canalización que desarrolle su código, ejecute pruebas unitarias, evalúe la calidad del código y se implemente en un entorno.

   ![Cuadro de diálogo Agregar canalización que no sea de producción](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Proporcione un **Nombre de canalización que no sea de producción** para identificar la canalización junto con la siguiente información adicional.

   * **Activador de implementación**: dispone de las siguientes opciones al definir los activadores de implementación para iniciar la canalización.

      * **Manual**: utilice esta opción para iniciar manualmente la canalización.
      * **Cambios en Git**: esta opción inicia la canalización CI/CD cada vez que se añaden confirmaciones a la rama de Git configurada. Con esta opción, aún puede iniciar la canalización manualmente según sea necesario.

1. Si elige crear una **canalización de implementación** también tendrá que definir el **comportamiento de errores de métricas importantes**.

   * **Preguntar cada vez**: esta es la configuración predeterminada y requiere intervención manual en caso de que se produzca algún error importante.
   * **Fallo inmediatamente**: si se selecciona, la canalización se cancela siempre que se produzca un fallo importante. Se trata, básicamente, de emular a un usuario que rechaza errores manualmente.
   * **Continuar inmediatamente**: si se selecciona, la canalización se ejecuta automáticamente cada vez que se produzca un error importante. Se trata, básicamente, de emular a un usuario que aprueba manualmente cada fallo.

1. Haga clic en **Continuar**.

1. En la pestaña **Código fuente** del cuadro de diálogo **Agregar canalización que no sea de producción**, debe seleccionar qué tipo de código debe procesar la canalización.

   * **[Código front-end](#front-end-code)**
   * **[Código de pila completa](#full-stack-code)**
   * **[Configuración de nivel web](#web-tier-config)**

Los pasos para completar la creación de la canalización que no sea de producción varían según la opción de **Código fuente** que haya seleccionado. Siga los vínculos anteriores para ir a la siguiente sección de este documento para poder completar la configuración de la canalización.

### Código front-end {#front-end-code}

Una canalización de código front-end implementa las compilaciones de código front-end que contienen una o más aplicaciones de interfaz de usuario del lado del cliente. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obtener más información sobre este tipo de canalización.

Para finalizar la configuración de la canalización de no producción de código front-end, siga estos pasos.

1. En el **Código fuente**, debe definir las siguientes opciones.

   * **Entornos de implementación aptos**: si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.
   * **Repositorio**: esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para poder aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo. Encuentra las ramas coincidentes que puede seleccionar.
   * **Ubicación del código**: esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.

   ![Canalización front-end](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. Haga clic en **Guardar**.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

### Código de pila completa {#full-stack-code}

Una canalización de código de pila completa implementa simultáneamente compilaciones de código de back-end y front-end que contienen una o más aplicaciones de servidor AEM junto con la configuración HTTPD/Dispatcher. Consulte el documento [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) para obtener más información sobre este tipo de canalización.

>[!NOTE]
>
>Si existe una canalización de código de pila completa para el entorno seleccionado, esta selección está deshabilitada.

Para finalizar la configuración de la canalización de no producción de código de pila completa, siga estos pasos.

1. En el **Código fuente**, debe definir las siguientes opciones.

   * **Entornos de implementación aptos**: si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.
   * **Repositorio**: esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para poder aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo. Le ayuda a encontrar las ramas coincidentes que puede seleccionar.
   * **Ignorar configuración de nivel web**: cuando se selecciona, la canalización no implementa la configuración del nivel web.

   * **Canalización**: si la canalización es de implementación, puede ejecutar una fase de prueba. Marque las opciones que desee habilitar en esta fase. Si no se selecciona ninguna de las opciones, la fase de prueba no se muestra durante la ejecución de la canalización.

      * **Prueba funcional del producto**: ejecutar [pruebas funcionales del producto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) contra el entorno de desarrollo.
      * **Pruebas funcionales personalizadas**: ejecutar [pruebas funcionales personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) contra el entorno de desarrollo.
      * **Pruebas de IU personalizadas**: ejecutar [pruebas de IU personalizadas](/help/implementing/cloud-manager/ui-testing.md) para aplicaciones personalizadas.

   ![Canalización de pila completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Haga clic en **Guardar**.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

### Configuración de nivel web {#web-tier-config}

Una canalización de configuración de nivel web implementa las configuraciones de HTTPD/Dispatcher. Consulte las [canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) para obtener más información sobre este tipo de canalización.

>[!NOTE]
>
>Si existe una canalización de código de nivel web para el entorno seleccionado, esta selección está deshabilitada.

Para finalizar la configuración de la canalización de no producción de código de capa web, siga estos pasos.

1. En el **Código fuente**, debe definir las siguientes opciones.

   * **Entornos de implementación aptos**: si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.
   * **Repositorio**: esta opción define desde qué repositorio Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para poder aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
   * **Ubicación del código**: esta opción define la ruta en la rama de la repo seleccionada desde la que la canalización debe recuperar el código.
      * Para las canalizaciones de configuración de nivel web, esta ruta generalmente contiene directorios `conf.d`, `conf.dispatcher.d` y `opt-in`.
      * Por ejemplo, si la estructura del proyecto se generó a partir del [tipo de archivo del proyecto de AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) la ruta sería `/dispatcher/src`.

   ![Canalización de niveles web](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. Haga clic en **Guardar**.

>[!NOTE]
>
>Si tiene una canalización de pila completa existente implementando en un entorno, al crear una canalización de configuración de capa web para el mismo entorno, se omitirá la configuración de capa web existente en la canalización de pila completa.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

## Desarrollo de Sites con la canalización front-end {#developing-with-front-end-pipeline}

Con las canalizaciones front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo se puede acelerar.

Consulte el documento [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber cómo funciona este proceso, así como algunas consideraciones que deben tenerse en cuenta para aprovechar al máximo este proceso.

## Omitir paquetes de Dispatcher {#skip-dispatcher-packages}

Si desea que los paquetes de Dispatcher se creen como parte de la canalización, pero no desea que se publiquen para crear almacenamiento, puede desactivar la publicación, lo que puede reducir la duración de la ejecución de la canalización.

La siguiente configuración para deshabilitar la publicación de paquetes de Dispatcher debe agregarse a través del archivo `pom.xml` del proyecto. Se basa en una variable de entorno, que sirve como indicador que puede establecer en el contenedor de compilación de Cloud Manager para definir cuándo se deben ignorar los paquetes de Dispatcher.

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
