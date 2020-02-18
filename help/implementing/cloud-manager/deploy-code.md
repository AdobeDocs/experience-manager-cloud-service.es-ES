---
title: Implementar el código - Servicios de nube
description: Implementar el código - Servicios de nube
translation-type: tm+mt
source-git-commit: 7758c6df49583dafdf2bf262eae8db466bb3c504

---


# Implementación del código {#deploy-your-code}

## Implementación de código con Cloud Manager {#deploying-code-with-cloud-manager}

Una vez configurada la **canalización** (repositorio, entorno y entorno de prueba), estará listo para implementar el código.

1. Haga clic en **Implementar** desde el Administrador de nube para iniciar el proceso de implementación.

   ![](assets/deploy-code1.png)


1. Aparece la pantalla Ejecución **de la canalización** .

   Haga clic en **Generar** para iniciar el proceso.

   ![](assets/deploy-code2.png)

1. El proceso de compilación completa implementa el código.

   En el proceso de compilación se encuentran las siguientes etapas:

   1. Implementación de etapa
   1. Prueba de etapa
   1. Implementación de producción
   >[!NOTE]
   >
   >Además, puede revisar los pasos de varios procesos de implementación mediante la visualización de registros o la revisión de los resultados de los criterios de prueba.

   La implementación **de la** etapa incluye los siguientes pasos:

   * Validación: Este paso garantiza que la canalización esté configurada para utilizar los recursos disponibles actualmente, por ejemplo, que la ramificación configurada exista, que los entornos estén disponibles.
   * Prueba de generación y unidad: Este paso ejecuta un proceso de compilación en contenedores. Consulte [Creación de un proyecto](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md) de aplicación de AEM para obtener más información sobre el entorno de compilación.
   * Análisis de código: Este paso evalúa la calidad del código de la aplicación. Consulte [Explicación de los resultados](/help/implementing/developing/introduction/understand-test-results.md) de la prueba para obtener más información sobre el proceso de prueba.
   * Generar imágenes: Este paso tiene un archivo de registro del proceso utilizado para generar imágenes. Este proceso es responsable de transformar el contenido y los paquetes de despachante producidos por el paso de compilación en imágenes de Docker y configuración de Kubernetes.
   * Implementar en etapa

      ![](assets/stage-deployment.png)
   La prueba **de** fase incluye los siguientes pasos:

   * Prueba funcional del producto: Las ejecuciones de canalizaciones de Cloud Manager admitirán la ejecución de pruebas que se ejecuten en el entorno de ensayo. Consulte [Explicación de los resultados](/help/implementing/developing/introduction/understand-test-results.md) de la prueba para obtener más información sobre el proceso de prueba.
   * Prueba funcional personalizada: Este paso en la canalización siempre está presente y no se puede omitir. Sin embargo, si la compilación no produce JAR de prueba, la prueba pasa de forma predeterminada. Consulte [Explicación de los resultados](/help/implementing/developing/introduction/understand-test-results.md) de la prueba para obtener más información sobre el proceso de prueba.

      ![](assets/stage-testing.png)





>Precaución:
>Las siguientes secciones deben actualizarse para Cloud Manager para los servicios de nube de AEM y están en curso.

## Proceso de implementación {#deployment-process}

En la siguiente sección se describe cómo se implementan los paquetes AEM y Dispatcher en la fase de fase y en la fase de producción.

Cloud Manager carga todos los archivos target/*.zip producidos por el proceso de compilación en una ubicación de almacenamiento.  Estos artefactos se recuperan de esta ubicación durante las fases de implementación de la canalización.

Cuando Cloud Manager se implementa en topologías que no son de producción, el objetivo es completar la implementación lo más rápido posible y, por lo tanto, los artefactos se implementan en todos los nodos simultáneamente de la siguiente manera:

1. Cloud Manager determina si cada artefacto es un paquete de AEM o de distribuidor.
1. Cloud Manager elimina todos los distribuidores del equilibrador de carga para aislar el entorno durante la implementación.

   A menos que se configure lo contrario, puede omitir los cambios del equilibrador de carga en las implementaciones de desarrollo y de fase, es decir, separar y adjuntar los pasos en las tuberías que no sean de producción, en los entornos de desarrollo y en la canalización de producción, para los entornos de escenario.

   >[!NOTE]
   >
   >Se espera que esta función la utilicen principalmente los clientes 1-1-1.

1. Cada artefacto de AEM se implementa en cada instancia de AEM a través de las API del administrador de paquetes, y las dependencias del paquete determinan el orden de implementación.

   Para obtener más información sobre cómo puede utilizar los paquetes para instalar nueva funcionalidad, transferir contenido entre instancias y realizar una copia de seguridad del contenido del repositorio, consulte Cómo trabajar con paquetes.

   >[!NOTE]
   >
   >Todos los artefactos de AEM se implementan tanto en el autor como en los editores. Los modos de ejecución deben aprovecharse cuando se requieran configuraciones específicas de nodos. Para obtener más información sobre cómo los modos de ejecución le permiten ajustar la instancia de AEM para un fin específico, consulte Run Modes (Modos de ejecución).

1. El artefacto del despachante se implementa en cada distribuidor de la siguiente manera:

   1. Se realiza una copia de seguridad de las configuraciones actuales y se copian en una ubicación temporal
   1. Todas las configuraciones se eliminan excepto los archivos inmutables. Consulte Administrar las configuraciones de despachante para obtener más detalles. Esto borra los directorios para asegurarse de que no quedan archivos huérfanos.
   1. El artefacto se extrae en el directorio httpd.  Los archivos inmutables no se sobrescriben. Los cambios que realice en los archivos inmutables del repositorio de Git se ignorarán en el momento de la implementación.  Estos archivos son fundamentales para el marco de distribución de AMS y no se pueden cambiar.
   1. Apache realiza una prueba de configuración. Si no se encuentran errores, se vuelve a cargar el servicio. Si se produce un error, las configuraciones se restauran desde la copia de seguridad, el servicio se vuelve a cargar y el error se devuelve al Administrador de nube.
   1. Cada ruta especificada en la configuración de la canalización se invalida o se borra de la caché del despachante.
   >[!NOTE]
   >
   >Cloud Manager espera que el artefacto del distribuidor contenga el conjunto de archivos completo.  Todos los archivos de configuración del despachante deben estar presentes en el repositorio git. Si faltan archivos o carpetas, se producirá un error en la implementación.

1. Tras la implementación correcta de todos los paquetes de AEM y de despachante en todos los nodos, los despachantes se agregan de nuevo al equilibrador de carga y la implementación se completa.

   >[!NOTE]
   >
   >Puede omitir los cambios del equilibrador de carga en implementaciones de desarrollo y de etapa, es decir, separar y adjuntar pasos en las tuberías que no son de producción, en los entornos de desarrollador y en la canalización de producción, en los entornos de escenario.

### Implementación en fase de producción {#deployment-production-phase}

El proceso de implementación en topologías de producción difiere ligeramente para minimizar el impacto en los visitantes del sitio de AEM.

Las implementaciones de producción generalmente siguen los mismos pasos que antes, pero de manera continua:

1. Implemente los paquetes de AEM para crear.
1. Separe dispatcher1 del equilibrador de carga.
1. Implemente los paquetes de AEM en publish1 y el paquete de distribuidor en dispatcher1, vacíe la caché del despachante.
1. Vuelva a colocar dispatcher1 en el equilibrador de carga.
1. Una vez que el distribuidor1 vuelva a estar en servicio, separe el distribuidor2 del equilibrador de carga.
1. Implemente los paquetes de AEM en publish2 y el paquete dispatcher en dispatcher2, vacíe la caché del despachante.
1. Vuelva a colocar dispatcher2 en el equilibrador de carga.
Este proceso continúa hasta que la implementación ha llegado a todos los editores y despachantes de la topología.


