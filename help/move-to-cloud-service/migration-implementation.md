---
title: Fase de implementación
description: Fase de implementación
exl-id: 176dd79d-0d72-443c-87db-dab24fb48b96
source-git-commit: 82e22f0a0684491b5071fa232a0f90fb87da6992
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 90%

---

# Implementación {#implementation-phase}

Antes de realizar el inicio de la fase de ejecución, debe estar integrado en Cloud Service. También debe familiarizarse con Cloud Manager, ya que es el único mecanismo para implementar un código en AEM Cloud Service.

Cloud Manager permite que las organizaciones administren AEM de forma automática en la nube. Incluye un marco de trabajo de integración y entrega continuas (CI/CD) que permite a los equipo de TI y a los asociados de la implementación acelerar la entrega de las personalizaciones o actualizaciones sin poner en riesgo el rendimiento o la seguridad.

Consulte los siguientes recursos para obtener más detalles:

* [Incorporación de Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) para comprender los recursos de autoayuda sobre la integración de Experience Manager as a Cloud Service.

* [Integración de Git con Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) para aprender a utilizar un repositorio de Git único para implementar un código.

* [Configuración de Adobe Experience as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#aem-configuration) para obtener información sobre la administración de productos y el acceso de los usuarios en Admin Console.


## Introducción {#introduction}

Los pasos exactos de la transición a Cloud Service dependen de los sistemas que haya adquirido y de las prácticas de desarrollo de software que siga.

La siguiente imagen muestra los pasos principales involucrados en la fase de ejecución:

![image](/help/move-to-cloud-service/assets/exec-image1.png)

## Transferencia de contenido {#content-transfer}

Para transferir contenido de la instancia de AEM actual a la instancia de Cloud Service, puede utilizar la herramienta de transferencia de contenido de Adobe.

Con esta herramienta, puede especificar el subconjunto de contenido que desea transferir de la instancia de AEM de origen a la instancia de AEM de Cloud Service.

>[!NOTE]
>Se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

Consulte [la herramienta de transferencia de contenido](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md) para obtener más detalles.

>[!IMPORTANT]
>El requisito mínimo del sistema para la herramienta de transferencia de contenido es AEM 6.3+ y JAVA 8. Si dispone de una versión anterior de AEM, deberá actualizar el repositorio de contenido a AEM 6.5 para usar la herramienta de transferencia de contenido.

## Refactorización de código {#code-refactor}

El desarrollo y la ejecución del código en AEM as a Cloud Service requieren un cambio en la organización. Cabe señalar que el código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento. Debe tenerse en cuenta que el código que se ejecuta en Cloud Service siempre se realiza en un clúster. Esto significa que siempre hay más de una instancia en ejecución.

Es necesario realizar algunos cambios en los proyectos de AEM Maven para que sean compatibles con AEM as a Cloud Service. AEM as a Cloud Service requiere una separación de *contenido* y *código* en paquetes discretos para su implementación en AEM.

* `/apps` y `/libs`se consideran áreas inmutables de AEM, ya que no se pueden cambiar (crear, actualizar, eliminar) después de iniciarse AEM (es decir, durante la ejecución). Cualquier intento de cambiar un área inmutable durante la ejecución fallará.

* Todo lo demás en el repositorio, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp` , etc. son todas áreas mutables, lo que significa que se pueden cambiar durante el tiempo de ejecución.

Consulte la [Estructura del paquete recomendado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) para obtener más detalles.

Existen algunas directrices de desarrollo adicionales que debe tener en cuenta al desarrollar AEM as a Cloud Service. Consulte las [Directrices de desarrollo de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html) para obtener más información.

Desde la fase de planificación, debe tener una lista de áreas que deben refactorizarse para ser compatibles con Cloud Service. También debería revisar las [Directrices de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html) para obtener más detalles sobre cómo refactorizar y optimizar el código para pasar a Cloud Service.

Para acelerar algunas de las tareas de refactorización de código, puede utilizar las siguientes herramientas:

* [Migración del flujo de trabajo de recursos](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [Herramientas de modernización](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

Se recomienda refactorizar y probar el código localmente antes de colocarlo en un entorno de Cloud Service mediante Cloud Manager Git.

Consulte la documentación del SDK [de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) para obtener más información.

A continuación se enumeran algunos de los recursos adicionales:

* Vea la Instalación el SDK de Dispatcher para comprender cómo instalar el SDK de Dispatcher:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Vea la Configuración el SDK de Dispatcher para comprender cómo configurar el SDK de Dispatcher:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

* Revise la documentación de la [Configuración de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) para configurar un entorno de desarrollo local.


Para administrar el desarrollo continuo de código en su AEM activo junto con la tarea de refactorización de código como parte de su viaje de transición, se recomienda programar un período de congelación de código hasta que haya completado la reestructuración del proyecto Maven para que sea compatible con AEM as a Cloud Service.

Una vez que se haya realizado la reestructuración del proyecto, se podrá reanudar el nuevo desarrollo de código basado en esta nueva estructura. Esto reducirá los errores de canalización de Cloud Manager durante la implementación y la prueba del código.

>[!NOTE]
>Las tareas de Transferencia de contenido y Refactorización de código no se han realizado secuencialmente. Estas tareas se pueden hacer independientemente unas de otras. Sin embargo, se necesita una estructura de proyecto correcta para garantizar que el contenido se procese correctamente en el entorno de Cloud Service.

## Prácticas recomendadas para la implementación y prueba de códigos {#best-practices}

Las ejecuciones de canalizaciones de Cloud Manager para Cloud Services admitirán la ejecución de pruebas que se ejecuten con el entorno de ensayo.

Consulte [Prueba de la calidad del código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) para obtener información sobre cómo escribir secuencias de comandos de prueba y la cobertura recomendada de al menos un 50 %.

Además, consulte [Comprender las reglas de calidad de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md) para obtener más información sobre las reglas de calidad de código personalizadas y ejecutadas por Cloud Manager, creadas sobre la base de las prácticas recomendadas de ingeniería de AEM.

El uso de Cloud Manager es el único mecanismo para implementar los códigos en los entornos de Cloud Service.

Siga los recursos a continuación para aprender a utilizar Cloud Manager para administrar e implementar su código.

* [Administración de entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [Configuración de la canalización de CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [Implementar el código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)


