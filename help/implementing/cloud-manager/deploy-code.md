---
title: 'Implementar el código: Cloud Services'
description: 'Implementar el código: Cloud Services'
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: bcd106a39bec286e2a09ac7709758728f76f9544
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---

# Implementar el código {#deploy-your-code}

## Implementación de código con Cloud Manager en AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Una vez configurada la canalización de producción (repositorio, entorno y entorno de prueba), estará listo para implementar el código.

1. Haga clic en **Implementar** desde Cloud Manager para iniciar el proceso de implementación.

   ![](assets/deploy-code1.png)


1. Aparece la pantalla **Pipeline Execution**.

   Haga clic en **Build** para iniciar el proceso.

   ![](assets/deploy-code2.png)

1. El proceso de compilación completa implementa el código.

   En el proceso de compilación participan las siguientes etapas:

   1. Implementación de fase
   1. Prueba de prueba
   1. Implementación de producción

   >[!NOTE]
   >
   >Además, puede revisar los pasos de varios procesos de implementación consultando los registros o revisando los resultados de los criterios de prueba.

   La **implementación por fases** incluye los siguientes pasos:

   * Validación: Este paso garantiza que la canalización esté configurada para utilizar los recursos disponibles actualmente, por ejemplo, que la rama configurada exista, los entornos estén disponibles.
   * Prueba de compilación y unidad: Este paso ejecuta un proceso de compilación en contenedores. Consulte [Detalles del entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) para obtener más información sobre el entorno de compilación.
   * Escaneo de código: Este paso evalúa la calidad del código de la aplicación. Consulte [Prueba de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md) para obtener más información sobre el proceso de prueba.
   * Generar imágenes: Este paso tiene un archivo de registro del proceso utilizado para crear imágenes. Este proceso es responsable de transformar el contenido y los paquetes de Dispatcher producidos por el paso de compilación en imágenes de Docker y configuración de Kubernetes.
   * Implementar en fase

      ![](assets/stage-deployment.png)
   La **prueba de fase** incluye los siguientes pasos:

   * **Prueba funcional del producto**: Las ejecuciones de canalización de Cloud Manager admitirán la ejecución de pruebas que se ejecuten con el entorno de ensayo.
Consulte [Prueba funcional del producto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) para obtener más información.

   * **Prueba funcional personalizada**: Este paso en la canalización siempre está presente y no se puede omitir. Sin embargo, si la compilación no produce ningún JAR de prueba, la prueba pasa de forma predeterminada.\
      Consulte [Pruebas funcionales personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) para obtener más información.

   * **Pruebas** de IU personalizadas: Este paso es una función opcional que permite a nuestros clientes crear y ejecutar automáticamente pruebas de IU para sus aplicaciones. Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium).
Consulte [Pruebas de IU personalizadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/functional-testing.html?lang=en#custom-ui-testing) para obtener más información.


   * **Auditoría de experiencias**: Este paso en la canalización siempre está presente y no se puede omitir. A medida que se ejecuta una canalización de producción, se incluye un paso de auditoría de experiencias después de realizar pruebas funcionales personalizadas que ejecutarán las comprobaciones. Las páginas configuradas se enviarán al servicio y se evaluarán. Los resultados son informativos y permiten al usuario ver las puntuaciones y el cambio entre las puntuaciones actual y anterior. Esta perspectiva es valiosa para determinar si hay una regresión que se introducirá con la implementación actual.
Consulte [Explicación de los resultados de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

      ![](assets/stage-testing.png)





## Proceso de implementación {#deployment-process}

Todas las implementaciones de Cloud Service siguen un proceso gradual para garantizar que no haya downtime. Consulte [Cómo funcionan las implementaciones móviles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#how-rolling-deployments-work) para obtener más información.

### Implementación en fase de producción {#deployment-production-phase}

El proceso de implementación en topologías de producción difiere ligeramente para minimizar el impacto en los visitantes AEM sitio.

Las implementaciones de producción generalmente siguen los mismos pasos que se describen arriba, pero de forma gradual:

1. Implemente AEM paquetes para crear.
1. Desasocie Dispatcher1 del equilibrador de carga.
1. Implemente AEM paquetes para publicar1 y el paquete de Dispatcher para dispatcher1, vacíe la caché de Dispatcher.
1. Vuelva a colocar Dispatcher1 en el equilibrador de carga.
1. Una vez que Dispatcher1 vuelva a estar en servicio, separe Dispatcher2 del equilibrador de carga.
1. Implemente AEM paquetes para publicar2 y el paquete de Dispatcher para dispatcher2, vacíe la caché de Dispatcher.
1. Vuelva a colocar Dispatcher2 en el equilibrador de carga.
Este proceso continúa hasta que la implementación haya llegado a todos los editores y distribuidores de la topología.
