---
title: Implementación del código
description: Obtenga información sobre cómo implementar su código mediante canalizaciones de Cloud Manager en AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: a7555507f4fb0fb231e27d7c7a6413b4ec6b94e6
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# Implementación del código {#deploy-your-code}

Obtenga información sobre cómo implementar su código mediante canalizaciones de Cloud Manager en AEM as a Cloud Service.

## Implementación del código con Cloud Manager en AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Una vez que haya [configuró la canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) incluido el repositorio, el entorno y el entorno de prueba, está listo para implementar su código.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea implementar el código.

1. Haga clic en **Implementación** de la llamada a la acción en la variable **Información general** para iniciar el proceso de implementación.

   ![CTA](assets/deploy-code1.png)

1. La variable **Ejecución de canalización** se abre. Haga clic en **Generar** para iniciar el proceso.

   ![Pantalla de ejecución de canalización](assets/deploy-code2.png)

El proceso de compilación implementa el código en tres fases.

1. [Implementación de fase](#stage-deployment)
1. [Prueba de prueba](#stage-testing)
1. [Implementación de producción](#production-deployment)

>[!TIP]
>
>Puede revisar los pasos de varios procesos de implementación consultando los registros o revisando los resultados de los criterios de prueba.

## Fase de implementación de fase {#stage-deployment}

La variable **Implementación de fase** fase. implica estos pasos.

* **Validación**  : este paso garantiza que la canalización esté configurada para utilizar los recursos disponibles actualmente. Por ejemplo, probar que la rama configurada existe y que los entornos están disponibles.
* **Prueba de compilación y unidad** - Este paso ejecuta un proceso de compilación en contenedores.
   * Consulte el documento [Generar detalles del entorno](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) para obtener más información sobre el entorno de compilación.
* **Escaneo de código** - Este paso evalúa la calidad del código de la aplicación.
   * Consulte el documento [Prueba de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md) para obtener más información sobre el proceso de prueba.
* **Crear imágenes** - Este proceso es responsable de transformar el contenido y los paquetes de Dispatcher producidos por el paso de compilación en imágenes Docker y configuraciones de Kubernetes.
* **Implementar en fase** - La imagen se implementa en el entorno de ensayo como preparación para la [Etapa de prueba de fase.](#stage-testing)

![Implementación de fase](assets/stage-deployment.png)

## Fase de prueba de fase {#stage-testing}

La variable **Prueba de fase** incluye estos pasos.

* **Prueba funcional del producto** : la canalización de Cloud Manager ejecuta pruebas que se ejecutan en el entorno de ensayo.
   * Consulte el documento [Prueba funcional del producto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) para obtener más información.

* **Pruebas funcionales personalizadas** - Este paso en la canalización siempre se ejecuta y no se puede omitir. Si la compilación no produce JAR de prueba, la prueba pasa de forma predeterminada.
   * Consulte el documento [Pruebas funcionales personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) para obtener más información.

* **Pruebas de IU personalizadas** : Este paso es una función opcional que ejecuta automáticamente las pruebas de IU creadas para aplicaciones personalizadas.
   * Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium).
   * Consulte el documento [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) para obtener más información.

* **Auditoría de experiencias** - Este paso en la canalización siempre se ejecuta y no se puede omitir. A medida que se ejecuta una canalización de producción, se incluye un paso de auditoría de experiencias después de realizar pruebas funcionales personalizadas que ejecutarán las comprobaciones.
   * Las páginas configuradas se envían al servicio y se evalúan.
   * Los resultados son informativos y muestran las puntuaciones y el cambio entre las puntuaciones actual y anterior.
   * Esta perspectiva es valiosa para determinar si hay una regresión que se introducirá con la implementación actual.
   * Consulte el documento [Comprender los resultados de la auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

![Prueba de prueba](assets/stage-testing.png)

## Fase de implementación de producción {#deployment-production}

El proceso de implementación en topologías de producción difiere ligeramente para minimizar el impacto de los visitantes en un sitio AEM.

Las implementaciones de producción suelen seguir los mismos pasos que se describieron anteriormente, pero de forma gradual.

1. Implemente AEM paquetes para crear.
1. Desasocie Dispatcher1 del equilibrador de carga.
1. Implemente AEM paquetes para publicar1 y el paquete de Dispatcher para dispatcher1, vacíe la caché de Dispatcher.
1. Vuelva a colocar Dispatcher1 en el equilibrador de carga.
1. Una vez que Dispatcher1 vuelva a estar en servicio, separe Dispatcher2 del equilibrador de carga.
1. Implemente AEM paquetes para publicar2 y el paquete de Dispatcher para dispatcher2, vacíe la caché de Dispatcher.
1. Vuelva a colocar Dispatcher2 en el equilibrador de carga.

Este proceso continúa hasta que la implementación haya llegado a todos los editores y distribuidores de la topología.

![Fase de implementación de producción](assets/production-deployment.png)

## Proceso de implementación {#deployment-process}

Todas las implementaciones de Cloud Service siguen un proceso gradual para garantizar que no haya downtime. Consulte el documento [Cómo funcionan las implementaciones móviles](/help/implementing/deploying/overview.md#how-rolling-deployments-work) para obtener más información.