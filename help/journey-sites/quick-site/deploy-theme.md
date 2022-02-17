---
title: Implementar el tema personalizado
description: Obtenga información sobre cómo implementar el tema del sitio mediante la canalización.
source-git-commit: 97c7590fd7b77e78cf2d465454fac80906d37803
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 1%

---


# Implementar el tema personalizado {#deploy-your-customized-theme}

Obtenga información sobre cómo implementar el tema del sitio mediante la canalización.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de Creación Rápida del Sitio de AEM, [Personalizar el tema del sitio,](customize-theme.md) ha aprendido cómo se crea el tema, cómo personalizarlo y cómo probarlo con contenido AEM en directo, y ahora debería:

* Comprender la estructura básica del tema del sitio y cómo editarlo.
* Consulte cómo probar las personalizaciones de temas mediante contenido AEM real a través de un proxy local.
* Obtenga información sobre cómo confirmar los cambios en el repositorio de Git de AEM.

Ahora puede realizar el último paso y utilizar la canalización para implementarlos.

## Objetivo {#objective}

En este documento se explica cómo implementar el tema mediante la canalización. Después de leer, debe:

* Conozca cómo puede almacenar en déclencheur una implementación de canalización.
* Consulte cómo comprobar el estado de implementación.

## Función responsable {#responsible-role}

Esta parte del recorrido se aplica al desarrollador del front-end.

## Iniciar la canalización {#start-pipeline}

Una vez que haya confirmado los cambios de personalización del tema en el repositorio de Git de AEM, puede ejecutar [la canalización que el administrador creó](pipeline-setup.md) para implementar los cambios.

1. Iniciar sesión en Cloud Manager [como lo hizo para recuperar la información de acceso de Git](retrieve-access.md) Y acceda a su programa. En el **Información general** , verá una tarjeta para **Canalizaciones**.

   ![Información general de Cloud Manager](assets/cloud-manager-overview.png)

1. Toque o haga clic en los puntos suspensivos junto a la canalización que necesita iniciar. En el menú desplegable, seleccione **Ejecutar**.

   ![Ejecutar canalización](assets/run-pipeline.png)

1. En el **Ejecutar canalización** cuadro de diálogo de confirmación, toque o haga clic en **Sí**.

   ![Confirmar ejecución de canalización](assets/pipeline-confirm.png)

1. En la lista de canalizaciones, la columna de estado indica que la canalización se está ejecutando.

   ![Estado de ejecución de la canalización](assets/pipeline-running.png)

## Comprobar estado de la canalización {#pipeline-status}

Puede comprobar el estado de la canalización para ver los detalles de su progreso en cualquier momento.

1. Toque o haga clic en los puntos suspensivos junto a la canalización.

   ![Ver detalles de canalización](assets/view-pipeline-details.png)

1. La ventana de detalles de la canalización muestra el desglose del progreso de la canalización.

   ![Detalles de canalización](assets/pipeline-details.png)

>[!TIP]
>
>En la ventana de detalles de la canalización, puede tocar o hacer clic en **Descargar registro** para cualquier paso de la canalización con fines de depuración si algún paso debe fallar. La depuración de la canalización está fuera del ámbito de este recorrido. Consulte los documentos técnicos de Cloud Manager en la [Recursos adicionales](#additional-resources) de esta página.

## Validación de las personalizaciones implementadas {#view-customizations}

Una vez finalizada la canalización, puede informar al administrador para validar los cambios. El administrador:

1. Abra el entorno de creación de AEM.
1. Vaya a [el sitio que el administrador creó anteriormente.](create-site.md)
1. Edite una de las páginas de contenido.
1. Consulte los cambios aplicados.

![Cambios aplicados](assets/changes-applied.png)

## ¿Fin del Recorrido? {#end-of-journey}

Felicitaciones! ¡Ha completado el recorrido de creación rápida de sitios AEM! Ahora debería:

* Obtenga información sobre cómo Cloud Manager y la canalización front-end funcionan para administrar e implementar personalizaciones front-end.
* Obtenga información sobre cómo crear un sitio AEM basado en una plantilla y cómo descargar el tema del sitio.
* Cómo incorporar un desarrollador de front-end para que pueda acceder al repositorio de Git de AEM.
* Personalización y prueba de un tema mediante contenido AEM proxy y confirmación de esos cambios en AEM Git.
* Cómo implementar la personalización del front-end mediante la canalización.

Ya está listo para personalizar los temas de su propio sitio AEM. Sin embargo, antes de empezar a crear diferentes flujos de trabajo usando varias canalizaciones front-end, revise el documento [Desarrollo de sitios con la canalización front-end.](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) Le ayudará a sacar el máximo partido a su desarrollo front-end mediante:

* Mantener una única fuente de verdad.
* Mantener una separación de preocupaciones.

AEM es una potente herramienta y hay muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la [Sección Recursos adicionales](#additional-resources) para obtener más información sobre las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

A continuación se muestran algunos recursos adicionales que profundizan en algunos conceptos mencionados en este documento.

* [Uso del carril del sitio para administrar el tema del sitio](/help/sites-cloud/administering/site-creation/site-rail.md) - Conozca las potentes funciones del carril del sitio para ayudarle a personalizar y administrar fácilmente el tema del sitio, lo que incluye la descarga de fuentes temáticas y la administración de versiones de temas.
* [AEM documentación técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) - Si ya tiene una comprensión firme de AEM, puede que desee consultar directamente los documentos técnicos detallados.
* [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) : Si desea obtener más información sobre las funciones de Cloud Manager, puede consultar directamente los documentos técnicos detallados.
* [Permisos basados en roles](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) : Cloud Manager tiene funciones preconfiguradas con los permisos adecuados. Consulte este documento para obtener detalles sobre estas funciones y cómo administrarlas.
* [Repositorios de Cloud Manager](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) - Si necesita más información sobre cómo configurar y administrar repositorios Git para su proyecto AEMaaCS, consulte este documento.
* [Configuración de la canalización de CI/CD: Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) - Obtenga más información sobre la configuración de canalizaciones, tanto de pila completa como del front-end, en este documento.
* [Plantilla de sitio estándar AEM](https://github.com/adobe/aem-site-template-standard) - Este es el repositorio de GitHub de la plantilla de Sitio estándar AEM.
* [AEM tema del sitio](https://github.com/adobe/aem-site-template-standard-theme-e2e) - Este es el repositorio de GitHub del tema del sitio AEM.
* [npm](https://www.npmjs.com) - AEM temas utilizados para construir sitios rápidamente se basan en npm.
* [webpack](https://webpack.js.org) - AEM temas utilizados para construir sitios rápidamente dependen del webpack.
* [Creación y organización de páginas](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) - Esta guía detalla cómo administrar las páginas de su sitio AEM si desea personalizarlo aún más después de crearlo a partir de la plantilla.
* [Cómo trabajar con el paquete](/help/implementing/developing/tools/package-manager.md) : Los paquetes permiten importar y exportar el contenido del repositorio. Este documento explica cómo trabajar con paquetes en AEM 6.5, que también se aplica a AEMaaCS.
* [Recorrido de incorporación](/help/journey-onboarding/home.md) - Esta guía sirve como punto de partida para garantizar que sus equipos estén configurados y tengan acceso a AEM as a Cloud Service.
* [Documentación de Adobe Experience Manager Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es) : Explore la documentación de Cloud Manager para obtener información detallada sobre sus funciones.
* [Documentación de administración del sitio](/help/sites-cloud/administering/site-creation/create-site.md) - Consulte los documentos técnicos sobre la creación de sitios para obtener más información sobre las funciones de la herramienta de creación rápida de sitios.
* [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) - Este documento describe algunas consideraciones que hay que tener en cuenta para aprovechar todo el potencial del proceso de desarrollo del front-end mediante la canalización del front-end.
