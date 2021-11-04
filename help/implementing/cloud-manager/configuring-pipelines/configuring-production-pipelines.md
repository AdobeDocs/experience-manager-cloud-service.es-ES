---
title: Configuración de canalizaciones de producción
description: Configuración de canalizaciones de producción
index: true
source-git-commit: 8bdc246d1f47e1bdc9a217588f0be69a09982be5
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---


# Configuración de una canalización de producción {#configure-production-pipeline}

El administrador de implementación es responsable de configurar la canalización de producción.

>[!NOTE]
>No se puede configurar una canalización de producción hasta que no se haya completado la creación de un programa, el repositorio de Git tenga al menos una rama y se haya creado un conjunto de entornos de producción y ensayo.

Antes de comenzar a implementar el código, debe configurar la configuración de la canalización desde la [!UICONTROL Cloud Manager].

>[!NOTE]
>Puede cambiar la configuración de la canalización después de la configuración inicial.

## Adición de una nueva canalización de producción {#adding-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno usando [!UICONTROL Cloud Manager] La interfaz de usuario de está lista para añadir una canalización de producción.

Siga estos pasos para configurar el comportamiento y las preferencias de la canalización de producción:

1. Vaya a la **Canalizaciones** de la **Información general del programa** página.
Haga clic en **+Añadir** y seleccione **Agregar canalización de producción**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Agregar canalización de producción** se abre. Introduzca el nombre de la canalización.

   Además, también puede configurar **Déclencheur de implementación** y **Comportamiento de errores de métricas importantes** from **Opciones de implementación**. Haga clic en **Continuar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Puede definir los déclencheur de implementación para iniciar la canalización.

   * **Manual** : al usar la interfaz de usuario, se inicia manualmente la canalización.
   * **Cambios en Git** - inicia la canalización CI/CD cada vez que se añaden confirmaciones a la rama git configurada. Incluso si selecciona esta opción, siempre puede iniciar la canalización manualmente.

      Durante la configuración o edición de la canalización, el administrador de implementación tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad.

      Esto resulta útil para los clientes que desean procesos más automatizados. Las opciones disponibles son:
   Puede definir el comportamiento importante de las métricas de error para iniciar la canalización.

   * **Pregunte cada vez** - Esta es la configuración predeterminada y requiere una intervención manual en cualquier error importante.
   * **Fallo Inmediatamente** - Si se selecciona, la canalización se cancelará siempre que se produzca un error importante. Básicamente, esto emula a un usuario rechazando manualmente cada error.
   * **Continuar inmediatamente** - Si está seleccionada, la canalización se realizará automáticamente cada vez que se produzca un error importante. Básicamente, esto está emulando a un usuario que aprueba manualmente cada error.


1. La variable **Agregar canalización de producción** El cuadro de diálogo incluye una segunda ficha etiquetada como **Código fuente**. Puede seleccionar **[Código front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)** o **[Código de pila completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack1.png)

   Si ha seleccionado **Código front-end**, debe seleccionar **Repositorio**, **Rama de Git** y **Ubicación del código**, como se muestra en la figura siguiente:
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack1.png)

   Si ha seleccionado **Código de pila completa**, debe seleccionar **Repositorio**, **Rama de Git** y **Opciones de implementación de producción** (detalles a continuación), como se muestra en la figura:
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack2.png)

   **Opciones de implementación de producción:**

   * **Pausar antes de implementar en producción**: Esta opción permite que la implementación se detenga antes de la producción.
   * **Programado**: Esta opción permite al usuario activar la implementación de producción programada.

   >[!IMPORTANT]
   >Si ya existe una canalización de código de pila completa para el entorno seleccionado, esta selección se desactivará.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/full-stack-disabled.png)

   >[!NOTE]
   >Antes de empezar a configurar las canalizaciones del front-end, consulte [AEM Recorrido de creación rápida de sitios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) para obtener un flujo de trabajo completo mediante la herramienta de creación rápida AEM sitios, que es muy fácil de usar. Este sitio de documentación le ayudará a optimizar el desarrollo front-end de su sitio AEM y a personalizar rápidamente su sitio sin AEM conocimiento back-end.

1. Haga clic en **Continuar** una vez seleccionadas las opciones en el **Código fuente** pestaña .

1. La variable **Agregar canalización de producción** El cuadro de diálogo incluye una tercera ficha etiquetada como **Auditoría de experiencias**. Esta opción proporciona una tabla para las rutas URL que siempre deben incluirse en la auditoría de experiencias.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >Debe hacer clic en **Agregar página** para definir su propio vínculo personalizado. La ruta de página debe comenzar con `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   Haga clic en **Agregar nueva página** para proporcionar una ruta de URL que se incluya en la auditoría de experiencias.

   Por ejemplo, si desea incluir `https://wknd.site/us/en/about-us.html` en la auditoría de experiencias, introduzca la ruta `/us/en/about-us.html` en este campo y haga clic en **Guardar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   La dirección URL que aparece en la tabla es:

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   Se puede incluir un máximo de 25 filas. Si el usuario no envía páginas en esta sección, la página principal del sitio se incluirá en la auditoría de experiencias de forma predeterminada.

   Consulte [Comprender los resultados de la auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

   >[!NOTE]
   > Las páginas configuradas se enviarán al servicio y se evaluarán según las pruebas de rendimiento, accesibilidad, SEO (Optimización del motor de búsqueda), prácticas recomendadas y PWA (Aplicación web progresiva).

1. Haga clic en **Guardar**. La canalización de producción recién creada ahora se muestra en la sección **Canalizaciones** tarjeta.

   La canalización se muestra en la tarjeta de la pantalla principal con cuatro acciones, como se muestra a continuación:

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-created.png)

   * **Agregar** : permite añadir una nueva canalización.
   * **Mostrar todo** : permite al usuario ver todas las canalizaciones.
   * **Acceder a información de repositorios** : permite al usuario obtener la información necesaria para acceder al repositorio Git de Cloud Manager.
   * **Más información** : navega para comprender el recurso de documentación de canalización CI/CD.


