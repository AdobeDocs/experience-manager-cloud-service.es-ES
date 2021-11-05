---
title: Configurar la canalización
description: Cree una canalización front-end para administrar la personalización del tema del sitio.
source-git-commit: f8695dd8fdc9ffb203bab943c335ab2957df6251
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---


# Configurar la canalización {#set-up-your-pipeline}

Cree una canalización front-end para administrar la personalización del tema del sitio.

>[!CAUTION]
>
>La herramienta Creación rápida de sitios es actualmente una vista previa técnica. Está disponible con fines de ensayo y evaluación y no está pensado para su uso en producción a menos que se acuerde con la asistencia al Adobe.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de Creación Rápida del Sitio de AEM, [Crear sitio a partir de una plantilla,](create-site.md) ha aprendido a utilizar una plantilla de sitio para crear rápidamente un sitio AEM que se pueda personalizar aún más con herramientas front-end y ahora debería:

* Obtenga información sobre cómo obtener AEM plantillas del sitio.
* Aprenda a crear un nuevo sitio con una plantilla.
* Consulte cómo descargar la plantilla del nuevo sitio para proporcionarla al desarrollador del front-end.

Este artículo se basa en estos aspectos básicos para que pueda configurar una canalización front-end que el desarrollador de front-end utilizará más adelante en el recorrido para implementar personalizaciones front-end.

## Objetivo {#objective}

Este documento le ayuda a comprender las canalizaciones de front-end y cómo crearlas para administrar la implementación del tema personalizado del sitio. Después de leer, debe:

* Comprender qué es una canalización front-end.
* Obtenga información sobre cómo configurar una canalización front-end en Cloud Manager.

## Función responsable {#responsible-role}

Esta parte del recorrido se aplica al administrador de Cloud Manager.

## Requisitos {#requirements}

* Debe tener acceso a Cloud Manager.
* Debe ser miembro del **Administrador de implementación** en Cloud Manager.
* Se debe configurar un repositorio de Git para el entorno de AEM en Cloud Manager.
   * Esto suele ocurrir ya en cualquier proyecto activo. Sin embargo, si no es así, consulte la documentación de los repositorios de Cloud Manager disponible en la sección [Recursos adicionales](#additional-resources) para obtener más información.

## ¿Qué es una canalización front-end? {#front-end-pipeline}

El desarrollo del front-end implica la personalización de JavaScript, CSS y recursos estáticos que definen el estilo del sitio AEM. El desarrollador de front-end trabajará en sus propios entornos locales para realizar estas personalizaciones. Una vez que estén listos, los cambios se comprometen con el repositorio de Git AEM. Pero solo están comprometidos con el código fuente. Todavía no están vivos.

La canalización front-end lleva estas personalizaciones comprometidas y las implementa en un entorno AEM, generalmente en entornos de producción o no de producción.

De este modo, el desarrollo del front-end puede funcionar de forma independiente y paralela a cualquier desarrollo del back-end completo en AEM, que tiene sus propias canalizaciones de implementación.

>[!NOTE]
>
>Las canalizaciones front-end solo pueden implementar recursos estáticos, CSS y JavaScript para aplicar estilo a su sitio AEM. El contenido del sitio, como páginas o recursos, no se puede implementar en una canalización.

## Acceso a Cloud Manager {#login}

1. Inicie sesión en Adobe Experience Cloud en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Una vez que haya iniciado sesión, compruebe que se encuentra en la organización correcta en la esquina superior derecha de la pantalla. Si solo es miembro de una organización, este paso no es necesario. A continuación, toque o haga clic en **Experience Manager**.

   ![Información general del Experience Cloud](assets/experience-cloud-overview.png)

1. En la página siguiente, toque o haga clic en el botón **Launch** para iniciar el **Cloud Manager** aplicación.

   ![aplicaciones Experience Manager](assets/experience-manager-apps.png)

1. En la página siguiente se enumeran los distintos programas disponibles. Toque o haga clic en el que desee administrar. Si acaba de empezar con AEM as a Cloud Service, es probable que solo tenga disponible un programa.

   ![Selección de un programa en Cloud Manager](assets/cloud-manager-select-program.png)

Ahora verá una descripción general de su Cloud Manager. Su página tendrá un aspecto diferente pero similar al de este ejemplo.

![Información general de Cloud Manager](assets/cloud-manager-overview.png)

Observe el nombre del programa al que ha accedido o copie la URL. Deberá proporcionárselo más adelante al desarrollador del front-end.

## Creación de una canalización front-end {#create-front-end-pipeline}

Ahora que ha accedido a Cloud Manager, puede crear una canalización para la implementación del front-end.

1. En el **Canalizaciones** de la página Cloud Manager, toque o haga clic en el botón **Agregar** botón.

   ![Canalizaciones](assets/pipelines-add.png)

1. En el menú emergente que aparece debajo de la sección **Agregar** botón seleccionar **Agregar canalización que no sea de producción** a efectos del presente recorrido.

1. En el **Configuración** de la pestaña **Agregar canalización que no sea de producción** que se abre:
   * Select **Canalización de implementación**.
   * Proporcione un nombre a la canalización en la variable **Nombre de canalización que no es de producción** campo .

   ![Agregar configuración de canalización](assets/add-pipeline-configuration.png)

1. Toque o haga clic **Continuar**.

1. En el **Código fuente** pestaña:
   * Select **Código front-end** como el tipo de código que se va a implementar.
   * Asegúrese de que el entorno correcto está seleccionado en **Entornos de implementación aptos**.
   * Seleccione el **Repositorio**.
   * Defina qué **Rama de Git** la canalización debe estar asociada a .
   * Defina el **Ubicación del código** si el desarrollo front-end se encuentra bajo una ruta particular en el repositorio seleccionado. El valor predeterminado es la raíz del repositorio, pero a menudo el desarrollo del front-end y el back-end estarán bajo diferentes rutas.

   ![Información del código fuente para agregar una canalización](assets/add-pipeline-source-code.png)

1. Toque o haga clic **Guardar**.

La nueva canalización se crea y se puede ver en el **Canalizaciones** de la ventana Cloud Manager. Si toca hacer clic en los puntos suspensivos después del nombre de la canalización, aparecerán opciones para editar o ver los detalles según sea necesario.

![Opciones de canalización](assets/new-pipeline.png)

>[!TIP]
>
>Si ya está familiarizado con las canalizaciones en AEMaaCS y desea obtener más información sobre las diferencias entre los distintos tipos de canalizaciones, incluidos más detalles sobre la canalización front-end, consulte Configurar canalización de CI/CD: Cloud Services vinculados en la [Recursos adicionales](#additional-resources) a continuación.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de creación rápida AEM sitio, debe:

* Comprender qué es una canalización front-end.
* Obtenga información sobre cómo configurar una canalización front-end en Cloud Manager.

Aproveche este conocimiento y continúe con su recorrido de Creación Rápida AEM Sitio revisando el documento [Conceder acceso al desarrollador de front-end,](grant-access.md) donde incorporará a los desarrolladores de front-end en Cloud Manager para que tengan acceso al repositorio de Git de su sitio AEM y a la canalización.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de creación rápida del sitio revisando el documento [Personalizar el tema del sitio,](customize-theme.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido.

* [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) : Si desea obtener más información sobre las funciones de Cloud Manager, puede consultar directamente los documentos técnicos detallados.
* [Repositorios de Cloud Manager](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) - Si necesita más información sobre cómo configurar y administrar repositorios Git para su proyecto AEMaaCS, consulte este documento.
* [Configuración de la canalización de CI/CD: Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) - Obtenga más información sobre la configuración de canalizaciones, tanto de pila completa como del front-end, en este documento.