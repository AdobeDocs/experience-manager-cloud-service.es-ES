---
title: Agregar una canalización que no sea de producción
description: Obtenga información sobre cómo añadir una canalización que no sea de producción para probar la calidad del código antes de implementarla en entornos de producción.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 71%

---


# Adición de una canalización que no es de producción {#configuring-non-production-pipelines}

Obtenga información sobre cómo configurar canalizaciones que no sean de producción para probar la calidad del código antes de implementarlas en entornos de producción.

Un usuario debe tener la función **[Administrador de implementación](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar canalizaciones que no sean de producción.

## Canalizaciones que no sean de producción {#non-production-pipelines}

Además de [canalizaciones de producción](#configuring-production-pipelines.md) que se implementan en entornos de ensayo y producción, también puede configurar canalizaciones que no sean de producción para validar el código.

Existen dos tipos de canalizaciones que no son de producción:

* **Canalizaciones de calidad de código**: ejecutan análisis de calidad del código en el código de una rama de Git y ejecutan los pasos de compilación y calidad del código.
* **Canalizaciones de implementación**: además de ejecutar los pasos de compilación y calidad del código como las canalizaciones de calidad del código, estas canalizaciones implementan el código en un entorno que no es de producción.

>[!NOTE]
>
>Puede [editar la configuración de canalización](managing-pipelines.md) después de la configuración inicial.

## Agregar una nueva canalización que no sea de producción {#adding-non-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno utilizando la interfaz de usuario de Cloud Manager, estará listo para agregar una canalización que no sea de producción siguiendo estos pasos.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

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

   * **[Código de pila completa](#full-stack-code)**
   * **[Implementación de destino](#targeted-deployment)**

Consulte [Canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información sobre los tipos de canalizaciones.

Los pasos para completar la creación de la canalización que no sea de producción varían según el tipo de código fuente seleccionado. Siga los vínculos anteriores para ir a la siguiente sección de este documento para poder completar la configuración de la canalización.

### Código de pila completa {#full-stack-code}

AEM Una canalización de código de pila completa implementa simultáneamente compilaciones de código de back-end y front-end que contienen una o más aplicaciones de servidor de junto con la configuración HTTPD/Dispatcher.

>[!NOTE]
>
>Si existe una canalización de código de pila completa para el entorno seleccionado, esta selección está deshabilitada.

Para finalizar la configuración de la canalización de no producción de código de pila completa, siga estos pasos.

1. En el **Código fuente**, debe definir las siguientes opciones.

   * **Entornos de implementación aptos**: si la canalización es una canalización de implementación, debe seleccionar a qué entornos debe implementar.
   * **Repositorio**: esta opción define desde qué repositorio de Git la canalización debe recuperar el código.

   >[!TIP]
   > 
   >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para poder aprender a añadir y administrar repositorios en Cloud Manager.

   * **Rama de Git**: esta opción define desde qué rama de la canalización seleccionada debe recuperar el código.
      * Introduzca los primeros caracteres del nombre de la rama y la función de autocompletar de este campo. Le ayuda a encontrar las ramas coincidentes que puede seleccionar.
   * **Ignorar configuración de nivel web**: cuando se selecciona, la canalización no implementa la configuración del nivel web.
   * **Canalización**: si la canalización es de implementación, puede ejecutar una fase de prueba. Marque las opciones que desee habilitar en esta fase. Si no se selecciona ninguna de las opciones, la fase de prueba no se muestra durante la ejecución de la canalización.

      * **Prueba funcional del producto**: ejecutar [pruebas funcionales del producto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) contra el entorno de desarrollo.
      * **Pruebas funcionales personalizadas**: ejecutar [pruebas funcionales personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) contra el entorno de desarrollo.
      * **Pruebas de IU personalizadas**: ejecutar [pruebas de IU personalizadas](/help/implementing/cloud-manager/ui-testing.md) para aplicaciones personalizadas.
      * **Auditoría de experiencias** - Ejecutar [Auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-dashboard.md)

   ![Canalización de pila completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Haga clic en **Guardar**.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

### Implementación dirigida {#targeted-deployment}

AEM Una implementación de destino implementa el código únicamente para partes seleccionadas de la aplicación de. En una implementación de este tipo, puede elegir **Incluir** uno de los siguientes tipos de código:

* AEM **Configuración**: configure las opciones para las distintas características de su entorno de.
   * Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md) para obtener una lista de las configuraciones admitidas, que incluye el reenvío de registros, las tareas de mantenimiento relacionadas con la depuración y varias configuraciones de CDN, y para administrarlas en el repositorio de modo que se implementen correctamente.
   * Al ejecutar una canalización de implementación de destino, se implementarán las configuraciones, siempre que se guarden en el entorno, el repositorio y la rama que haya definido en la canalización.
   * En cualquier momento, solo puede haber una canalización de configuración por entorno.
* **Código front-end**: configure JavaScript AEM y CSS para el front-end de la aplicación.
   * Con las canalizaciones front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo se puede acelerar.
   * Consulte el documento [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber cómo funciona este proceso, así como algunas consideraciones que deben tenerse en cuenta para aprovechar al máximo este proceso.
* **Configuración de nivel web**: configure las propiedades de Dispatcher para almacenar, procesar y enviar páginas web al cliente.
   * Consulte el documento [Canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) para obtener más información.
   * Si existe una canalización de código de nivel web para el entorno seleccionado, esta selección está deshabilitada.
   * Si tiene una canalización de pila completa existente implementando en un entorno, al crear una canalización de configuración de capa web para el mismo entorno, se omitirá la configuración de capa web existente en la canalización de pila completa.

>[!NOTE]
>
>Las canalizaciones de configuración de nivel web no son compatibles con los repositorios privados. Consulte [Agregar repositorios privados en Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obtener detalles y la lista completa de limitaciones.

Los pasos para completar la creación de la canalización de implementación de destino que no sea de producción son los mismos una vez que elija un tipo de implementación.

1. Elija el tipo de implementación que necesita.

![Opciones de implementación de destino](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

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
   * **Canalización**: para las canalizaciones front-end que no sean de producción, tiene la opción de habilitar **[Auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-dashboard.md)**.

   ![Canalización de configuración](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)

1. Si habilitó la auditoría de experiencias, haga clic en **Continuar** para avanzar a la pestaña **Auditoría de experiencias**, donde puede definir las rutas que siempre se deben incluir en la auditoría de experiencias.

   * Si habilitó **Auditoría de experiencias**, consulte el documento [Auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-dashboard.md) para obtener detalles sobre cómo configurar.
   * Si no lo ha hecho, omita este paso.

1. Haga clic en **Guardar** para guardar la canalización.

La canalización se guarda y ahora puede [administrar las canalizaciones](managing-pipelines.md) en la tarjeta **Canalizaciones** en la página **Información general del programa**.

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
