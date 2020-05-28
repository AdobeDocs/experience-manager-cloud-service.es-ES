---
title: Fase de ejecución
description: Fase de ejecución
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 7%

---


# Ejecución {#execution-phase}

Antes de realizar el inicio de la fase de ejecución, debe estar integrado en el servicio de nube. También debe familiarizarse con Cloud Manager, ya que es el único mecanismo para implementar código en AEM Cloud Service.

Cloud Manager permite que las organizaciones gestionen AEM de forma automática en la nube. Incluye un marco de integración y entrega continuas (CI/CD) que permite a los equipo de TI y a los asociados de la implementación acelerar la entrega de las personalizaciones o actualizaciones sin poner en riesgo el rendimiento o la seguridad.

Consulte los siguientes recursos para obtener más detalles:

* [Incorporarse a Experience Manager como un servicio](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/home.html) en la nube para comprender los recursos de autoayuda sobre la integración de Experience Manager como un servicio en la nube.

* [Integración de Git con Adobe Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) para aprender a utilizar un repositorio de Git único para implementar código.

* [Configuración](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#aem-configuration) de Adobe Experience como servicio de nube para obtener información sobre la administración de productos y el acceso de usuarios en Admin Console.


## Introducción {#introduction}

Los pasos exactos de su transición al servicio de nube dependen de los sistemas que haya adquirido y de las prácticas de desarrollo de software que siga.

La siguiente figura muestra los pasos principales involucrados en la fase de ejecución:

![image](/help/move-to-cloud-service/assets/exec-image1.png)

## Transferencia de contenido {#content-transfer}

Para transferir contenido de la instancia de AEM actual a su instancia de servicio de nube, puede utilizar la herramienta de transferencia de contenido de Adobe.

Con esta herramienta, puede especificar el subconjunto de contenido que desea transferir de la instancia de AEM de origen a la instancia de AEM Cloud Service.

>[!NOTE]
>Se recomienda realizar recargas frecuentes de contenido diferencial para reducir el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse al servicio de nube.

Consulte Herramienta [de transferencia de](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md) contenido para obtener más detalles.

>[!IMPORTANT]
>El requisito mínimo del sistema para la herramienta de transferencia de contenido es AEM 6.3 + y JAVA 8. Si dispone de una versión inferior de AEM, deberá actualizar el repositorio de contenido a AEM 6.5 para utilizar la herramienta de transferencia de contenido.

## Refactorización de código {#code-refactor}

El desarrollo y la ejecución de código en AEM como un servicio en la nube requiere un cambio en la mentalidad. Cabe señalar que el código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento. El código que se ejecuta en el servicio de nube debe tener en cuenta que siempre se ejecuta en un clúster. Esto significa que siempre hay más de una instancia en ejecución.

Es necesario realizar algunos cambios en los proyectos de AEM Maven para que sean compatibles con AEM como servicio de nube. AEM como servicio de nube requiere una separación de *contenido* y *código* en paquetes discretos para su implementación en AEM.

* `/apps` y `/libs` se consideran áreas inmutables de AEM, ya que no se pueden cambiar (crear, actualizar, eliminar) después de iniciarse AEM (es decir, durante la ejecución). Cualquier intento de cambiar un área inmutable durante la ejecución fallará.

* Todo lo demás en el repositorio, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp` , etc. son todas áreas mutables, lo que significa que se pueden cambiar en tiempo de ejecución.

Consulte Estructura [de paquetes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) recomendada para obtener más información.

Existen algunas directrices de desarrollo adicionales que debe tener en cuenta al desarrollar AEM como un servicio en la nube. Consulte [AEM como directrices](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) de desarrollo de servicios en la nube para obtener más información.

Desde la fase de planificación, debe tener una lista de áreas que deben refactorizarse para ser compatibles con Cloud Service. También debería revisar las Directrices [](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) de desarrollo para obtener más detalles sobre cómo refactorizar y optimizar el código para pasar a Cloud Service.

Para ayudarle a acelerar algunas de sus tareas de refactorización de código, puede utilizar las siguientes herramientas:

* [Migración del flujo de trabajo de recursos](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [Herramientas de modernización](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

Se recomienda cambiar el factor y probar el código localmente antes de colocarlo en un entorno de servicios de nube mediante Cloud Manager Git.

Consulte la documentación del SDK [de](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) AEM para obtener más información.

A continuación se enumeran algunos recursos adicionales:

* Vea Instalar el SDK de Dispatcher para comprender cómo instalar el SDK de Dispatcher:

   > [!VIDEO](https://video.tv.adobe.com/v/30601)

* Vea Configurar el SDK de Dispatcher para saber cómo configurar el SDK de Dispatcher:

   > [!VIDEO](https://video.tv.adobe.com/v/30602)

* Revise la documentación de Configuración [de desarrollo](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) local para configurar un entorno de desarrollo local


Para gestionar el desarrollo continuo de código en su AEM activo junto con la tarea de refactorización de código como parte de su viaje de transición, se recomienda programar un período de congelación de código hasta que haya completado la reestructuración del proyecto Maven para que sea compatible con AEM como servicio de nube.

Una vez que se haya realizado la reestructuración del proyecto, podrá reanudar el nuevo desarrollo de código basado en esta nueva estructura. Esto reducirá los errores de canalización de Cloud Manager durante la implementación y la prueba del código.

>[!NOTE]
>Las tareas Transferencia de contenido y Refactor de código no se han realizado secuencialmente. Estas tareas se pueden hacer independientemente unas de otras. Sin embargo, se necesita la estructura de proyecto correcta para garantizar que el contenido se procese correctamente en el entorno del servicio de nube.

## Prácticas recomendadas para la implementación y prueba de código {#best-practices}

Las ejecuciones de canalizaciones de Cloud Manager para servicios de nube admitirán la ejecución de pruebas que se ejecuten con el entorno de la fase.

Consulte Prueba [de calidad del](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) código para obtener información sobre cómo escribir secuencias de comandos de prueba y la cobertura recomendada de al menos un 50 %.

Además, consulte [Explicación de las reglas](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) de calidad de código personalizado para obtener más información sobre las reglas de calidad de código personalizadas ejecutadas por Cloud Manager creadas en base a las prácticas recomendadas de ingeniería de AEM.

El uso de Cloud Manager es el único mecanismo para implementar código en los entornos de Cloud Service.

Siga los recursos a continuación para aprender a utilizar Cloud Manager para administrar e implementar su código.

* [Administrar entornos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [Configuración de la canalización CI-CD](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [Implementar el código](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## Prácticas recomendadas para la preparación en directo {#go-live}

Para garantizar un lanzamiento sin problemas y exitoso de AEM como servicio de nube, debe considerar la ejecución de los siguientes pasos:

* Programar código y período de congelación de contenido
* Realizar el resumen final del contenido
* Completar iteraciones de prueba
* Ejecutar pruebas de rendimiento y seguridad
* Cortar
