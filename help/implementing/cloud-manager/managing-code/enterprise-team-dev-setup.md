---
title: Configuración del equipo de desarrollo empresarial
description: Aprenda a configurar y escalar su equipo de desarrollo empresarial y vea cómo AEM as a Cloud Service puede apoyar su proceso de desarrollo.
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: a31c3693c9b2af9bd7f9d7f1f6fb0a61a4411df0
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 0%

---

# Configuración del equipo de desarrollo empresarial para AEM as a Cloud Service {#enterprise-setup}

Aprenda a configurar y escalar su equipo de desarrollo empresarial y vea cómo AEM as a Cloud Service puede apoyar su proceso de desarrollo.

## Introducción {#introduction}

Para dar compatibilidad a los clientes con configuraciones de desarrollo empresarial, AEM as a Cloud Service se integra completamente con Cloud Manager y su versión diseñada para cada fin. [canalizaciones de CI/CD obstinadas.](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) Estas canalizaciones y servicios se basan en las prácticas recomendadas, lo que garantiza una [las pruebas y la calidad de código más alta.](/help/implementing/cloud-manager/code-quality-testing.md)

## Asistencia de Cloud Manager en la configuración de desarrollo de equipo empresarial {#cloud-manager}

Para garantizar una incorporación rápida, Cloud Manager proporciona todo lo necesario para comenzar a desarrollar experiencias digitales de inmediato, incluido un repositorio de Git para almacenar personalizaciones que luego Cloud Manager crea, verifica e implementa.

Con Cloud Manager, los equipos de desarrollo pueden trabajar para confirmar los cambios con frecuencia sin depender del personal de Adobe.

En Cloud Manager hay disponibles tres tipos de entornos.

* Desarrollo
* Escenario
* Producción

El código se puede implementar en entornos de desarrollo mediante una canalización que no sea de producción. Para los entornos de ensayo y producción, que siempre van juntos y garantizan la validación antes de la implementación de producción como práctica recomendada, una canalización de producción utiliza [puertas de calidad](/help/implementing/cloud-manager/custom-code-quality-rules.md) para validar el código de la aplicación y los cambios de configuración.

La canalización de producción implementa primero el código y la configuración en el entorno de ensayo, prueba la aplicación y, finalmente, se implementa en la producción.

Un SDK de Cloud Service que siempre se actualiza con las últimas AEM mejoras as a Cloud Service permite el desarrollo local directamente utilizando el hardware local del desarrollador. Esto permite un rápido desarrollo con tiempos de respuesta muy bajos. Por lo tanto, los desarrolladores pueden permanecer en su entorno local familiar y elegir entre una amplia variedad de herramientas de desarrollo, y empujar a los entornos de desarrollo o a la producción cuando lo consideren adecuado.

Cloud Manager admite configuraciones flexibles de varios equipos que se pueden ajustar para adaptarse a las necesidades de una empresa. Para garantizar implementaciones estables con varios equipos, evitando al mismo tiempo situaciones en las que un equipo afecte a la producción para todos los equipos, la canalización obstinada de Cloud Manager siempre valida y prueba el código de todos los equipos juntos.

## Ejemplo de Real World {#real-world-example}

Cada empresa tiene diferentes requisitos, incluida la configuración de equipos, los procesos y los flujos de trabajo de desarrollo. Adobe utiliza la configuración que se describe a continuación para varios proyectos que ofrecen experiencias además de AEM as a Cloud Service.

Por ejemplo, las aplicaciones de Adobe Creative Cloud, como Adobe Photoshop o Adobe Illustrator, incluyen recursos de contenido como tutoriales, muestras y guías disponibles para los usuarios finales. Este contenido lo consumen las aplicaciones cliente mediante AEM as a Cloud Service de forma directa, realizando llamadas de API al nivel de publicación de AEM Cloud para recuperar el contenido estructurado como flujos JSON y aprovechando el [Red de entrega de contenido (CDN) en AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery) para ofrecer contenido estructurado y no estructurado con un rendimiento óptimo.

Los equipos que contribuyen a este proyecto se adhieren al siguiente proceso.

Cada equipo utiliza su propio flujo de trabajo de desarrollo y tiene un repositorio de Git independiente. Se utiliza un repositorio de Git compartido adicional para incorporar proyectos. Este repositorio de Git contiene la estructura raíz del repositorio de Git de Cloud Manager, incluida la configuración compartida de Dispatcher.

La incorporación de un nuevo proyecto requiere la inclusión en el archivo de proyecto Maven del reactor en la raíz del repositorio de Git compartido. Para la configuración de Dispatcher, se crea un nuevo archivo de configuración dentro del proyecto de Dispatcher. Este archivo se incluye en la configuración principal de Dispatcher. Cada equipo es responsable de su propio archivo de configuración de Dispatcher. Los cambios en el repositorio de Git compartido son raros y normalmente solo son necesarios cuando se incorpora un nuevo proyecto. El trabajo principal lo realiza cada equipo de proyecto dentro de su propio repositorio de Git.

![Diagrama del flujo de trabajo](/help/implementing/cloud-manager/assets/team-setup1.png)

El repositorio de Git para cada se configura con la variable [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) y, por lo tanto, sigue las prácticas recomendadas para configurar AEM proyectos. La única excepción es la configuración de Dispatcher que se realiza en el repositorio de Git compartido como se describe más arriba.

Cada equipo utiliza un flujo de trabajo de Git simplificado con dos ramas + N, siguiendo el modelo de flujo de Git:

* Una rama de versión estable contiene el código de producción.

* Una rama de desarrollo contiene el último desarrollo.

* Para cada función se crea una rama nueva.

El desarrollo se realiza en una rama de características. Cuando la función madura, se combina con la rama de desarrollo. Las funciones completadas y validadas se seleccionan de la rama de desarrollo y se combinan en la rama estable.

Todos los cambios se realizan mediante solicitudes de extracción (PR). Cada PR se valida automáticamente mediante puertas de calidad. Sonar se utiliza para comprobar la calidad del código y se ejecuta un conjunto de grupos de pruebas para garantizar que el nuevo código no introduce ninguna regresión.

La configuración del repositorio de Git de Cloud Manager tiene dos ramas.

* Una rama de versión estable contiene el código de producción de todos los equipos.
* Una rama de desarrollo contiene el código de desarrollo de todos los equipos.

Cada inserción en el repositorio de Git de un equipo en los déclencheur de desarrollo o rama estable a [Acción de GitHub.](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)

Todos los proyectos siguen la misma configuración para la rama estable. Un push a la rama estable de un proyecto se inserta automáticamente en la rama estable del repositorio Git de Cloud Manager. La canalización de producción en Cloud Manager está configurada para activarse mediante una inserción en la rama estable. Por lo tanto, la canalización de producción se ejecuta mediante cada inserción de cualquier equipo en una rama estable y la implementación de producción se actualiza si pasan todas las puertas de calidad.

![Diagrama push](/help/implementing/cloud-manager/assets/team-setup2.png)

Los empujones a la rama de desarrollo se gestionan de forma diferente. Mientras que una inserción en una rama de desarrollador en el repositorio de Git de un equipo está activando también una acción de GitHub y el código se inserta automáticamente en la rama de desarrollo del repositorio de Git de Cloud Manager, la canalización que no es de producción no se activa automáticamente mediante la inserción de código. Se activa mediante una llamada a la API de Cloud Manager.

La ejecución de la canalización de producción incluye la comprobación del código de todos los equipos a través de las puertas de calidad proporcionadas. Una vez implementado el código en la fase, las pruebas y auditorías se ejecutan para garantizar que todo funciona según lo esperado. Una vez pasadas todas las puertas, los cambios se implementan en producción sin interrupciones ni downtime.

Para el desarrollo local, la variable [SDK para AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing) se utiliza. El SDK permite configurar un autor, publicación y Dispatcher local. Esto permite el desarrollo sin conexión y tiempos de respuesta rápidos. A veces solo se utiliza el entorno de creación para el desarrollo, pero la configuración rápida de los entornos de Dispatcher y publicación permite probar todo localmente antes de insertarlo en el repositorio de Git.

Los miembros de cada equipo generalmente retiran el código del Git compartido para , así como su propio código de proyecto. No hay necesidad de retirar otros proyectos ya que los proyectos son independientes.

![Cierre de compra local y SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

Esta configuración del mundo real puede utilizarse como modelo y luego personalizarse según las necesidades de una empresa. El concepto flexible de ramificación y combinación de git permite realizar variaciones de los flujos de trabajo anteriores, adaptadas a las necesidades de cada equipo. AEM as a Cloud Service es compatible con todas estas variaciones sin sacrificar el valor principal de la canalización de Cloud Manager.

>[!TIP]
>
>Consulte el documento [Uso de repositorios Git de varias fuentes](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code) para obtener más información sobre esta configuración.

### Consideraciones para una configuración de varios equipos {#considerations}

Con el repositorio de Git de Cloud Manager y la canalización de producción, el código de producción completo siempre se ejecuta a través de todas las puertas de calidad, tratándolo como una unidad de implementación. De esta manera, el sistema de producción siempre está activo sin interrupciones ni downtime.

Por el contrario, sin un sistema de este tipo, ya que cada equipo puede realizar implementaciones por separado, existe el riesgo de que una actualización de un equipo único pueda provocar problemas de estabilidad de la producción. Además, requiere coordinación y tiempo de inactividad planificado para implementar actualizaciones. Con un número cada vez mayor de equipos, el esfuerzo de coordinación será mucho más complejo y rápidamente inmanejable.

Si se detecta un problema en las puertas de calidad, la producción no se ve afectada y el problema puede detectarse y solucionarse sin que el Adobe tenga que intervenir. Sin Cloud Service y sin probar siempre toda la implementación, las implementaciones parciales pueden provocar interrupciones que requieran una solicitud de reversión o incluso una restauración completa desde una copia de seguridad. Las pruebas parciales también podrían dar lugar a otros problemas que luego deberían solucionarse después de que el Adobe volviera a requerir coordinación y apoyo.

>[!TIP]
>
>Para cualquier configuración multiequipo es crucial definir un modelo de gobernanza y un conjunto de estándares que todos los equipos deben seguir. El modelo anterior para una configuración de varios equipos permite escalar un número mayor de equipos, que puede utilizar como punto de partida.
