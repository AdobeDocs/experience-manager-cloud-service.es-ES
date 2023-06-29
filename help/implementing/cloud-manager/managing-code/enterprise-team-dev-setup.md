---
title: Configuración del equipo de desarrollo empresarial
description: Aprenda a configurar y escalar su equipo de desarrollo empresarial y vea cómo AEM as a Cloud Service puede ayudarle con su proceso de desarrollo.
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 83%

---

# Configuración del equipo de desarrollo empresarial para AEM as a Cloud Service {#enterprise-setup}

Aprenda a configurar y escalar su equipo de desarrollo empresarial y vea cómo AEM as a Cloud Service puede ayudarle con su proceso de desarrollo.

## Introducción {#introduction}

Para dar compatibilidad a los clientes con configuraciones de desarrollo empresarial, AEM as a Cloud Service se integra completamente con Cloud Manager y sus [canalizaciones de CI/CD creadas específicamente](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Estas canalizaciones y servicios se basan en las prácticas recomendadas, lo que garantiza unas [pruebas y una calidad del código mejores](/help/implementing/cloud-manager/code-quality-testing.md).

## Soporte de Cloud Manager en la configuración del equipo de desarrollo empresarial {#cloud-manager}

Para garantizar una incorporación rápida, Cloud Manager proporciona todo lo necesario para comenzar a desarrollar experiencias digitales de inmediato, incluido un repositorio de Git para almacenar personalizaciones que luego Cloud Manager creará, verificará e implementará.

Con Cloud Manager, los equipos de desarrollo pueden trabajar para confirmar los cambios con frecuencia sin depender del personal de Adobe.

En Cloud Manager hay disponibles tres tipos de entornos.

* Desarrollo
* Escenario
* Producción

El código se puede implementar en entornos de desarrollo mediante una canalización que no sea de producción. Para los entornos de ensayo y producción, que siempre van juntos y garantizan la validación antes de la implementación de producción como práctica recomendada, una canalización de producción utiliza [puertas de calidad](/help/implementing/cloud-manager/custom-code-quality-rules.md) para validar el código de la aplicación y los cambios de configuración.

La canalización de producción implementa primero el código y la configuración en el entorno de ensayo, prueba la aplicación y, finalmente, se implementa en la producción.

Un SDK de Cloud Service AEM que siempre se actualiza con las últimas mejoras as a Cloud Service de la aplicación permite el desarrollo local directamente mediante el hardware local del desarrollador. Esto permite un desarrollo rápido con tiempos de respuesta muy bajos. Por lo tanto, los desarrolladores pueden permanecer en su entorno local familiar y elegir entre una amplia variedad de herramientas de desarrollo y favorecer los entornos de desarrollo o producción cuando lo consideren adecuado.

Cloud Manager admite configuraciones flexibles de varios equipos que se pueden ajustar para adaptarse a las necesidades de una empresa. Para garantizar implementaciones estables con varios equipos y evitar al mismo tiempo situaciones en las que un equipo afecte a la producción de los demás, la canalización de Cloud Manager siempre valida y prueba el código de todos los equipos juntos.

## Ejemplo del mundo real {#real-world-example}

Cada empresa tiene diferentes requisitos, incluida la configuración de equipos, los procesos y los flujos de trabajo de desarrollo. Adobe utiliza la configuración que se describe a continuación para varios proyectos que ofrecen experiencias además de AEM as a Cloud Service.

Por ejemplo, las aplicaciones de Adobe Creative Cloud, como Adobe Photoshop o Adobe Illustrator, incluyen recursos de contenido como tutoriales, ejemplos y guías para los usuarios finales. Este contenido lo consumen las aplicaciones cliente mediante AEM as a Cloud Service de forma directa, realizan llamadas de la API al nivel de publicación de AEM Cloud para recuperar el contenido estructurado como flujos JSON y aprovechan la [Red de entrega de contenido (CDN) en AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery) para ofrecer contenido estructurado y no estructurado con un rendimiento óptimo.

Los equipos que contribuyen a este proyecto se adhieren al siguiente proceso.

Cada equipo utiliza su propio flujo de trabajo de desarrollo y tiene un repositorio de Git independiente. Se utiliza un repositorio de Git compartido adicional para incorporar proyectos. Este repositorio de Git contiene la estructura raíz del repositorio de Git de Cloud Manager, incluida la configuración compartida de Dispatcher.

La incorporación de un nuevo proyecto requiere la inclusión en el archivo de proyecto de Maven del reactor en la raíz del repositorio de Git compartido. Para la configuración de Dispatcher, se crea un nuevo archivo de configuración dentro del proyecto de Dispatcher. Este archivo se incluye en la configuración principal de Dispatcher. Cada equipo es responsable de su propio archivo de configuración de Dispatcher. Los cambios en el repositorio de Git compartido son raros y normalmente solo son necesarios cuando se incorpora un proyecto nuevo. El trabajo principal lo realiza cada equipo de proyecto dentro de su propio repositorio de Git.

![Diagrama del flujo de trabajo](/help/implementing/cloud-manager/assets/team-setup1.png)

El repositorio de Git para cada uno se configura con el [Arquetipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) y, por lo tanto, sigue las prácticas recomendadas para configurar proyectos AEM. La única excepción es la configuración de Dispatcher que se realiza en el repositorio de Git compartido como se describe más arriba.

Cada equipo utiliza un flujo de trabajo de Git simplificado con dos ramas + N, en base al modelo de flujo de Git:

* Una rama de versión estable contiene el código de producción.

* Una rama de desarrollo contiene el último desarrollo.

* Para cada característica se crea una rama nueva.

El desarrollo se realiza en una rama de características. Cuando la característica madura, se combina con la rama de desarrollo. Las características completadas y validadas se seleccionan de la rama de desarrollo y se combinan en la rama estable.

Todos los cambios se realizan mediante solicitudes de extracción (PR). Cada PR se valida automáticamente mediante puertas de calidad. Sonar se utiliza para comprobar la calidad del código, y se ejecuta un conjunto de grupos de pruebas para garantizar que el código nuevo no introduce ninguna regresión.

La configuración del repositorio de Git de Cloud Manager tiene dos ramas.

* Una rama de versión estable que contiene el código de producción de todos los equipos.
* Una rama de desarrollo que contiene el código de desarrollo de todos los equipos.

Cada inserción en el repositorio de Git de un equipo en los déclencheur de rama estable o de desarrollo a [Acción de GitHub](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code).

Todos los proyectos siguen la misma configuración para la rama estable. Una inserción en la rama estable de un proyecto se inserta automáticamente a la rama estable en el repositorio de Git de Cloud Manager. La canalización de producción en Cloud Manager está configurada para activarse mediante una inserción en la rama estable. Por lo tanto, la canalización de producción se ejecuta mediante cada inserción de cualquier equipo en una rama estable y la implementación de producción se actualiza si aprueban todas las puertas de calidad.

![Diagrama de inserciones](/help/implementing/cloud-manager/assets/team-setup2.png)

Las inserciones en la rama de desarrollo se administran de forma diferente. Mientras que una inserción en una rama de desarrollo en el repositorio de Git de un equipo activa una acción de GitHub y el código se inserta automáticamente a la rama de desarrollo en el repositorio de Git de Cloud Manager, la canalización de no producción no se activa automáticamente por la inserción de código. Se activa mediante una llamada a la API de Cloud Manager.

La ejecución de la canalización de producción incluye la comprobación del código de todos los equipos a través de las puertas de calidad proporcionadas. Una vez implementado el código en la fase, las pruebas y auditorías se ejecutan para garantizar que todo funciona según lo esperado. Una vez aprobadas todas las puertas, los cambios se implementan en producción sin interrupciones ni tiempo de inactividad.

Para el desarrollo local, se utiliza [SDK para AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing). SDK permite configurar el autor, la publicación y el Dispatcher local. Esto permite el desarrollo sin conexión y tiempos de respuesta rápidos. A veces solo se utiliza el entorno de creación para el desarrollo, pero la configuración rápida de los entornos de Dispatcher y de publicación permite probar todo localmente antes de insertarlo en el repositorio de Git.

Los miembros de cada equipo suelen comprobar el código de Git compartido para su propio código de proyecto. No hay necesidad de comprobar otros proyectos ya que son independientes.

![Comprobación local y SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

Esta configuración del mundo real puede utilizarse como modelo y luego personalizarse según las necesidades de cada empresa. El concepto flexible de ramificación y combinación de Git permite realizar variaciones de los flujos de trabajo anteriores, adaptadas a las necesidades de cada equipo. AEM as a Cloud Service es compatible con todas estas variaciones sin sacrificar el valor principal de la canalización de Cloud Manager.

>[!TIP]
>
>Consulte [Uso de repositorios de Git de varias fuentes](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html?lang=es#managing-code) para obtener más información sobre esta configuración.

### Consideraciones para la configuración de varios equipos {#considerations}

Con el repositorio de Git de Cloud Manager y la canalización de producción, el código de producción completo siempre se ejecuta a través de todas las puertas de calidad y se trata como una unidad de implementación. De esta manera, el sistema de producción siempre está activo sin interrupciones ni tiempo de espera.

Por el contrario, sin un sistema de este tipo, ya que cada equipo puede realizar implementaciones por separado, existe el riesgo de que una actualización de un equipo único pueda provocar problemas de estabilidad de la producción. Además, se requiere coordinación y tiempo de inactividad planificado para implementar actualizaciones. Con un número cada vez mayor de equipos, el esfuerzo de coordinación se vuelve mucho más complejo y rápidamente inmanejable.

Si se detecta un problema en las puertas de calidad, la producción no se verá afectada y el problema podrá detectarse y solucionarse sin que el personal de Adobe tenga que intervenir. Sin Cloud Service y sin probar siempre toda la implementación, las implementaciones parciales pueden provocar interrupciones que requieran una solicitud de reversión o incluso una restauración completa desde una copia de seguridad. Las pruebas parciales también podrían dar lugar a otros problemas que deben solucionarse, lo que también requeriría la coordinación y el apoyo del personal de Adobe.

>[!TIP]
>
>Para cualquier configuración de varios equipos es crucial definir un modelo de gobernanza y un conjunto de estándares que todos los equipos deben seguir. El modelo anterior para una configuración de varios equipos permite escalar un número mayor de equipos, que puede utilizar como punto de partida.
