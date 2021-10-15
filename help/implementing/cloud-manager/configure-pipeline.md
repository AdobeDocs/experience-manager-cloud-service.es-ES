---
title: 'Configuración de la canalización de CI/CD: Cloud Services'
description: 'Configuración de la canalización de CI/CD: Cloud Services'
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: 03c058c17e8a9ff5a0be9203a65207bb367a02a6
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# Configuración de la canalización de CI/CD {#configure-ci-cd-pipeline}

En Cloud Manager, hay dos tipos de Canalización:

* **Canalización** de producción:

   Una canalización de producción solo se puede añadir una vez que se crea un conjunto de entornos de producción y de fase.

   Consulte [Configuración de la canalización de producción](configure-pipeline.md#setting-up-the-pipeline) para obtener más información.

* **Canalización que no es de producción**:

   Se puede añadir una canalización que no sea de producción desde la página **Overview** de la interfaz de usuario de Cloud Manager.

   Para obtener más información, consulte [Tutoriales de solo calidad de código y no producción](configure-pipeline.md#non-production-pipelines) .

   >[!NOTE]
   >Para configurar la canalización, debe:
   > * defina el déclencheur que iniciará la canalización.
   > * defina los parámetros que controlan la implementación de producción.
   > * configure los parámetros de prueba de rendimiento.


## Configuración de canalización de producción {#setting-up-production-pipeline}

El administrador de implementación es responsable de configurar la canalización de producción.

>[!NOTE]
>No se puede configurar una canalización de producción hasta que no se haya completado la creación de un programa, el repositorio de Git tenga al menos una rama y se haya creado un conjunto de entornos de producción y ensayo.

Antes de comenzar a implementar el código, debe configurar la configuración de la canalización desde [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Puede cambiar la configuración de la canalización después de la configuración inicial.

### Adición de una nueva canalización de producción {#adding-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno utilizando la interfaz de usuario de [!UICONTROL Cloud Manager], estará listo para agregar una canalización de producción.

Siga estos pasos para configurar el comportamiento y las preferencias de la canalización de producción:

1. Vaya a la tarjeta **Canalizaciones** desde la página **Información general del programa**.
Haga clic en **+Add** y seleccione **Add Production Pipeline**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Aparece el cuadro de diálogo Añadir** canalización de producción . Introduzca el nombre de la canalización.

   Además, también puede configurar **Déclencheur de implementación** y **Comportamiento de errores de métricas importantes** desde **Opciones de implementación**. Haga clic en **Continue**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Puede definir los déclencheur de implementación para iniciar la canalización.

   * **Manual** : al utilizar la IU, se inicia manualmente la canalización.
   * **Cambios en Git** : inicia la canalización CI/CD cada vez que se agregan confirmaciones a la rama git configurada. Incluso si selecciona esta opción, siempre puede iniciar la canalización manualmente.

      Durante la configuración o edición de la canalización, el administrador de implementación tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad.

      Esto resulta útil para los clientes que desean procesos más automatizados. Las opciones disponibles son:
   Puede definir el comportamiento importante de las métricas de error para iniciar la canalización.

   * **Pregunte cada vez** : esta es la configuración predeterminada y requiere una intervención manual en cualquier error importante.
   * **Fail Inmediatamente** : Si se selecciona, la canalización se cancelará siempre que se produzca un error importante. Básicamente, esto emula a un usuario rechazando manualmente cada error.
   * **Continuar inmediatamente** : si se selecciona, la canalización se realizará automáticamente cada vez que se produzca un error importante. Básicamente, esto está emulando a un usuario que aprueba manualmente cada error.


1. El cuadro de diálogo **Añadir Canalización de producción** incluye una segunda pestaña etiquetada como **Código fuente**. **Código de pila completa** seleccionado. Puede elegir el **Repositorio** y la **Rama Git**. Seleccione las Opciones de implementación de producción, tal como se explica a continuación. Haga clic en **Continue**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   Opciones de implementación de producción:

   * **Pausar antes de implementar en producción**: Esta opción permite que la implementación se detenga antes de la producción.
   * **Programado**: Esta opción permite al usuario activar la implementación de producción programada.

1. El cuadro de diálogo **Añadir Canalización de producción** incluye una tercera pestaña etiquetada como **Auditoría de experiencias**. Esta opción proporciona una tabla para las rutas URL que siempre deben incluirse en la auditoría de experiencias.

   >[!NOTE]
   >Debe hacer clic en **Agregar página** para definir su propio vínculo personalizado.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   Haga clic en **Agregar nueva página** para proporcionar una ruta URL que se incluirá en la auditoría de experiencias.

   Por ejemplo, si desea incluir `https://wknd.site/us/en/about-us.html` en la auditoría de experiencias, introduzca la ruta `us/en/about-us.html` en este campo y haga clic en **Guardar**.

   ![](assets/exp-audit4.png)

   La dirección URL que aparece en la tabla es:

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   Se puede incluir un máximo de 25 filas. Si el usuario no envía páginas en esta sección, la página principal del sitio se incluirá en la auditoría de experiencias de forma predeterminada.

   Consulte [Explicación de los resultados de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

   >[!NOTE]
   > Las páginas configuradas se enviarán al servicio y se evaluarán según las pruebas de rendimiento, accesibilidad, SEO (Optimización del motor de búsqueda), prácticas recomendadas y PWA (Aplicación web progresiva).

1. Haga clic en **Save**. La canalización de producción recién creada ahora se muestra en la tarjeta **Canalizaciones**.

   La canalización se muestra en la tarjeta de la pantalla principal con tres acciones, como se muestra a continuación:

   * **Añadir** : permite añadir una nueva canalización.
   * **Acceso a información de repositorios** : permite al usuario obtener la información necesaria para acceder al repositorio Git de Cloud Manager.
   * **Más información** : navega para comprender el recurso de documentación de canalización de CI/CD.

### Edición de una canalización de producción {#editing-prod-pipeline}

Puede editar las configuraciones de canalización desde la página **Información general del programa**.

Siga los pasos a continuación para editar la canalización configurada:

1. Vaya a la tarjeta **Canalizaciones** desde la página **Información general del programa**.

1. Haga clic en **...** desde la tarjeta **Canalizaciones** y haga clic en **Editar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. Aparece el cuadro de diálogo **Editar canalización de producción**.

   1. La pestaña **Configuration** permite actualizar el **Pipeline Name**, el **Deployment Déclencheur** y el **Importante Metrics Failure Behavior**.

      >[!NOTE]
      >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para obtener información sobre cómo agregar y administrar repositorios en Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. La pestaña **Source** le ofrece la opción de comprobar o desmarcar **Pause antes de implementar las opciones Production** y **Scheduled** de **Production Deployment Options**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. La opción **Auditoría de experiencias** permite actualizar o agregar nuevas páginas.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Haga clic en **Update** una vez que haya terminado de editar la canalización.

### Acciones adicionales de canalización de producción {#additional-prod-actions}

#### Ejecución de una canalización de producción {#run-prod}

Puede ejecutar la canalización de producción desde la tarjeta Canalizaciones:

1. Vaya a la tarjeta **Canalizaciones** desde la página **Información general del programa**.

1. Haga clic en **...** desde la tarjeta **Canalizaciones** y haga clic en **Ejecutar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### Eliminación de una canalización de producción {#delete-prod}

Puede eliminar la canalización de producción de la tarjeta Canalizaciones:

1. Vaya a la tarjeta **Canalizaciones** desde la página **Información general del programa**.

1. Haga clic en **...** de la tarjeta **Canalizaciones** y haga clic en **Eliminar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >Un usuario con la función Gestor de implementación ahora puede eliminar la canalización de producción de forma autoservicio mediante la opción **Delete** de la tarjeta Canalización.


## Canalizaciones de calidad de código y no producción {#non-production-pipelines}

Además de la canalización principal que se implementa en las fases y la producción, los clientes pueden configurar canalizaciones adicionales, denominadas **Canalizaciones que no son de producción**. Estas canalizaciones siempre ejecutan los pasos de compilación y calidad del código. Opcionalmente, también pueden implementarse en AEM entorno as a Cloud Service.

### Adición de una nueva canalización que no sea de producción {#adding-non-production-pipeline}

En la pantalla de inicio, estas canalizaciones se enumeran en una tarjeta nueva:

1. Acceda a la tarjeta **Canalizaciones** desde la pantalla de inicio de Cloud Manager. Haga clic en **+Add** y seleccione **Add Non-Production Pipeline**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Aparece el cuadro de diálogo Añadir**  canalización no de producción . Seleccione el tipo de canalización que desea crear, ya sea **Canalización de calidad de código** o **Canalización de implementación**.

   Además, también puede configurar **Déclencheur de implementación** y **Comportamiento de errores de métricas importantes** desde **Opciones de implementación**. Haga clic en **Continue**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **Código de pila completa** seleccionado. Puede elegir el **Repositorio** y la **Rama Git**. Haga clic en **Save**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. La canalización que no es de producción recién creada ahora se muestra en la tarjeta **Canalizaciones**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   La canalización se muestra en la tarjeta de la pantalla principal con tres acciones, como se muestra a continuación:

   * **Añadir** : permite añadir una nueva canalización.
   * **Acceso a información de repositorios** : permite al usuario obtener la información necesaria para acceder al repositorio Git de Cloud Manager.
   * **Más información** : navega para comprender el recurso de documentación de canalización de CI/CD.

### Edición de una canalización que no es de producción {#editing-nonprod-pipeline}

Puede editar las configuraciones de canalización desde la **Tarjeta de canalización** de la página **Información general del programa**.

Siga los pasos a continuación para editar la canalización configurada que no sea de producción:

1. Vaya a la tarjeta **Canalizaciones** desde la página **Información general del programa**.

1. Seleccione la canalización que no es de producción y haga clic en **...**. Haga clic en **Editar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. Aparece el cuadro de diálogo **Editar canalización de producción**.

   1. La pestaña **Configuration** permite actualizar el **Pipeline Name**, el **Deployment Déclencheur** y el **Importante Metric Errors Behavior**.

      >[!NOTE]
      >Consulte [Adición y administración de repositorios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para obtener información sobre cómo agregar y administrar repositorios en Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. La pestaña **Source Code** permite actualizar el **Repository** y la **Git Branch**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. Haga clic en **Update** una vez que haya terminado de editar la canalización que no es de producción.

### Acciones adicionales de canalización que no son de producción {#additional-nonprod-actions}

#### Ejecución de una canalización que no sea de producción {#run-nonprod}

Puede ejecutar la canalización de producción desde la tarjeta Canalizaciones:

1. Vaya a la tarjeta **Canalizaciones** desde la página **Información general del programa**.

1. Haga clic en **...** desde la tarjeta **Canalizaciones** y haga clic en **Ejecutar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### Eliminación de una canalización que no es de producción {#delete-nonprod}

Puede eliminar la canalización de producción de la tarjeta Canalizaciones:

1. Vaya a la tarjeta **Canalizaciones** desde la página **Información general del programa**.

1. Haga clic en **...** de la tarjeta **Canalizaciones** y haga clic en **Eliminar**, como se muestra en la figura siguiente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## Pasos siguientes {#the-next-steps}

Una vez configurada la canalización, debe implementar el código.

Consulte [Implementar el código](deploy-code.md) para obtener más información.
