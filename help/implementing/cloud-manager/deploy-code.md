---
title: 'Implementar el código: Cloud Services'
description: 'Implementar el código: Cloud Services'
translation-type: tm+mt
source-git-commit: 533707b9073231ed16757884afeb968ace0785b3
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 1%

---


# Implementar el código {#deploy-your-code}

## Implementación de código con Cloud Manager {#deploying-code-with-cloud-manager}

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
   * Prueba de compilación y unidad: Este paso ejecuta un proceso de compilación en contenedores. Consulte [Detalles del entorno de compilación](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md) para obtener más información sobre el entorno de compilación.
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
Consulte Pruebas de IU personalizadas para obtener más información.


   * **Auditoría de experiencias**: Este paso en la canalización siempre está presente y no se puede omitir. A medida que se ejecuta una canalización de producción, se incluye un paso de auditoría de experiencias después de realizar pruebas funcionales personalizadas que ejecutarán las comprobaciones. Las páginas configuradas se enviarán al servicio y se evaluarán. Los resultados son informativos y permiten al usuario ver las puntuaciones y el cambio entre las puntuaciones actual y anterior. Esta perspectiva es valiosa para determinar si hay una regresión que se introducirá con la implementación actual.
Consulte [Explicación de los resultados de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

      ![](assets/stage-testing.png)





## Proceso de implementación {#deployment-process}

En la siguiente sección se describe cómo se implementan los paquetes AEM y Dispatcher en la fase de fase y en la fase de producción.

Cloud Manager carga todos los archivos target/*.zip producidos por el proceso de compilación en una ubicación de almacenamiento.  Estos artefactos se recuperan de esta ubicación durante las fases de implementación de la canalización.

Cuando Cloud Manager se implementa en topologías que no son de producción, el objetivo es completar la implementación lo antes posible y, por lo tanto, los artefactos se implementan en todos los nodos de forma simultánea de la siguiente manera:

1. Cloud Manager determina si cada artefacto es un paquete AEM o dispatcher.
1. Cloud Manager elimina todos los distribuidores del equilibrador de carga para aislar el entorno durante la implementación.

   A menos que se configure lo contrario, puede omitir los cambios del equilibrador de carga en las implementaciones de desarrollo y ensayo, es decir, separar y adjuntar pasos en ambas canalizaciones que no sean de producción, para entornos de desarrollo y para la canalización de producción, para entornos de ensayo.

   >[!NOTE]
   >
   >Se espera que esta función la usen principalmente los clientes 1-1-1.

1. Cada artefacto de AEM se implementa en cada instancia de AEM a través de las API del administrador de paquetes, con dependencias de paquete que determinan el orden de implementación.

   Para obtener más información sobre cómo puede utilizar paquetes para instalar nuevas funciones, transferir contenido entre instancias y realizar copias de seguridad del contenido del repositorio, consulte Cómo trabajar con paquetes.

   >[!NOTE]
   >
   >Todos los artefactos AEM se implementan tanto en el autor como en los editores. Los modos de ejecución deben aprovecharse cuando se requieran configuraciones específicas de nodos. Para obtener más información sobre cómo los modos de ejecución permiten ajustar la instancia de AEM para un fin específico, consulte los modos de ejecución.

1. El artefacto de Dispatcher se implementa en cada Dispatcher de la siguiente manera:

   1. Las configuraciones actuales se respaldan y copian en una ubicación temporal
   1. Todas las configuraciones se eliminan excepto los archivos inmutables. Consulte Administrar las configuraciones de Dispatcher para obtener más información. Esto borra los directorios para garantizar que no queden archivos huérfanos.
   1. El artefacto se extrae en el directorio `httpd`.  Los archivos inmutables no se sobrescriben. Los cambios que realice en los archivos inmutables del repositorio de Git se ignorarán en el momento de la implementación.  Estos archivos son fundamentales para el marco de Dispatcher de AMS y no se pueden cambiar.
   1. Apache realiza una prueba de configuración. Si no se encuentran errores, el servicio se vuelve a cargar. Si se produce un error, las configuraciones se restauran desde la copia de seguridad, el servicio se vuelve a cargar y el error se devuelve a Cloud Manager.
   1. Cada ruta especificada en la configuración de la canalización se invalida o se vacía de la caché de Dispatcher.

   >[!NOTE]
   >
   >Cloud Manager espera que el artefacto de Dispatcher contenga el conjunto completo de archivos.  Todos los archivos de configuración de Dispatcher deben estar presentes en el repositorio de Git. Si faltan archivos o carpetas, se producirá un error de implementación.

1. Después de la implementación correcta de todos los paquetes de AEM y Dispatcher en todos los nodos, los distribuidores se vuelven a añadir al equilibrador de carga y la implementación se completa.

   >[!NOTE]
   >
   >Puede omitir los cambios del equilibrador de carga en las implementaciones de desarrollo y fase, es decir, separar y adjuntar pasos en ambas canalizaciones que no sean de producción, para entornos de desarrollador y para la canalización de producción, para entornos de ensayo.

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


