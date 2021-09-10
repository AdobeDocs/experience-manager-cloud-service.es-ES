---
title: 'Configuración de desarrollo de equipo empresarial: Cloud Services'
description: Siga esta página para obtener más información sobre la configuración de desarrollo de Enterprise Team
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: 3cdee254eebcf45762feff8fe081b006a803ef1b
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 0%

---

# Configuración de desarrollo de equipo empresarial para AEM as a Cloud Service {#enterprise-setup}

## Introducción {#introduction}

AEM como Cloud Service, una oferta nativa de la nube que ofrece AEM como servicio está diseñada para beneficiarse de más de 10 años de ofrecer software empresarial a equipos empresariales con sus requisitos específicos. Aunque catapulta AEM al mundo nativo de la nube, con nuevos valores como siempre en activo, siempre actual, siempre seguro y siempre a escala, conserva la principal propuesta de valor que AEM proporciona como plataforma personalizable a nuestros clientes y permite que los equipos de clasificación empresarial se integren en sus procedimientos de desarrollo y envío.

Para ayudar a nuestros clientes con configuraciones de desarrollo empresarial, AEM como Cloud Service se integra completamente con Cloud Manager y sus canalizaciones de CD/CI, creadas para su propósito, que están equipadas con las mejores prácticas y las lecciones de varios años de experiencia con implementaciones y desarrollo de nivel empresarial, lo que garantiza pruebas exhaustivas y la máxima calidad del código para ofrecer experiencias excepcionales.

## Asistencia de Cloud Manager en la configuración de desarrollo de equipo empresarial {#cloud-manager}

Para garantizar una integración rápida para los clientes, Cloud Manager proporciona todo lo necesario para empezar a desarrollar experiencias de inmediato, incluido un repositorio de Git para almacenar personalizaciones que luego Cloud Manager crea, verifica e implementa.
Con Cloud Manager, los equipos de desarrollo pueden trabajar para confirmar los cambios con frecuencia sin depender del personal de Adobe.

En Cloud Manager hay disponibles tres tipos de entorno:

* Desarrollo
* Escenario
* Producción

El código se puede implementar en entornos de desarrollo mediante una canalización que no sea de producción. Para Stage y Production, que siempre van juntas y, por lo tanto, garantizan la validación antes de la implementación de producción como práctica recomendada, una canalización de producción utiliza puertas de calidad para validar el código de la aplicación y los cambios de configuración.

La canalización de producción implementa primero el código y la configuración en el entorno de ensayo, prueba la aplicación y, finalmente, se implementa en la producción.
Un SDK de Cloud Service que siempre se actualiza con las últimas mejoras de Cloud Service permite el desarrollo local directamente utilizando el hardware local del desarrollador. Esto permite un rápido desarrollo con tiempos de respuesta muy bajos. Por lo tanto, los desarrolladores pueden permanecer en su entorno local familiar y elegir entre una amplia variedad de herramientas de desarrollo, y empujar a los entornos de desarrollo o a la producción cuando lo consideren adecuado.

Cloud Manager admite configuraciones flexibles de varios equipos que se pueden ajustar para adaptarse a las necesidades de una empresa. Esto se aplica tanto al Cloud Service como a AMS. Para garantizar implementaciones estables con varios equipos y evitar que un solo equipo afecte a la producción para todos los equipos, la canalización obstinada de Cloud Manager siempre valida y prueba el código de todos los equipos juntos.


## Ejemplo de Real World {#real-world-example}

Cada empresa tiene diferentes requisitos, incluida la configuración de equipos, los procesos y los flujos de trabajo de desarrollo. Adobe utiliza la configuración que se describe a continuación para varios proyectos que ofrecen experiencias además de AEM como Cloud Service.

Por ejemplo, las aplicaciones de Adobe Creative Cloud, como Adobe Photoshop o Adobe Illustrator, incluyen recursos de contenido como tutoriales, muestras y guías disponibles para los usuarios finales. Este contenido lo consumen las aplicaciones cliente mediante AEM como Cloud Service de forma *headless*, realizando llamadas API al nivel de publicación de AEM Cloud para recuperar el contenido estructurado como flujos JSON y aprovechando la [Content Delivery Network (CDN) en AEM como Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) para proporcionar contenido estructurado y no estructurado con un rendimiento óptimo.

Los equipos que contribuyen a este proyecto siguen el proceso que se describe a continuación.

>[!NOTE]
>Consulte [Uso de repositorios Git de varias fuentes](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code) para obtener más información sobre la configuración.

Cada equipo utiliza su propio flujo de trabajo de desarrollo y tiene un repositorio de Git independiente. Se utiliza un repositorio de Git compartido adicional para incorporar proyectos. Este repositorio de Git contiene la estructura raíz del repositorio de Git de Cloud Manager, incluida la configuración compartida de Dispatcher. La incorporación de un nuevo proyecto requiere la inclusión en el archivo de proyecto Maven del reactor en la raíz del repositorio de Git compartido. Para la configuración de Dispatcher, se crea un nuevo archivo de configuración dentro del proyecto de Dispatcher. Este archivo se incluye en la configuración principal de Dispatcher. Cada equipo es responsable de su propio archivo de configuración de Dispatcher. Los cambios en el repositorio de Git compartido son raros y normalmente solo son necesarios cuando se incorpora un nuevo proyecto. El trabajo principal lo realiza cada equipo de proyecto dentro de su propio repositorio de Git.

![](/help/implementing/cloud-manager/assets/team-setup1.png)

El repositorio de Git para cada equipo se ha configurado utilizando el tipo de archivo Maven de AEM y, por lo tanto, sigue las prácticas recomendadas para configurar AEM proyectos. La única excepción es el manejo de la configuración de Dispatcher que se realiza en el repositorio de Git compartido como se describe más arriba.
Cada equipo utiliza un flujo de trabajo de Git simplificado con dos ramas + N, siguiendo el modelo de flujo de Git:

* Una rama de versión estable contiene el código de producción

* Una rama de desarrollo contiene el último desarrollo

* Para cada función se crea una rama nueva


El desarrollo se realiza en una rama de funciones, cuando la función madura se fusiona en la rama de desarrollo. Las funciones completadas y validadas se seleccionan de la rama de desarrollo y se combinan en la rama estable. Todos los cambios se realizan mediante solicitudes de extracción (PR). Cada PR se valida automáticamente mediante puertas de calidad. Sonar se utiliza para comprobar la calidad del código y se ejecuta un conjunto de grupos de pruebas para garantizar que el nuevo código no introduce ninguna regresión.

La configuración del repositorio de Git de Cloud Manager tiene dos ramas:

* Una *rama de versión estable*, que contiene el código de producción de todos los equipos
* Una *rama de desarrollo* que contiene el código de desarrollo de todos los equipos

Cada inserción en el repositorio de Git de un equipo en el desarrollo o en la rama estable activa una [acción github](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html?lang=en#managing-code). Todos los proyectos siguen la misma configuración para la rama estable. Un push a la rama estable de un proyecto se inserta automáticamente en la rama estable del repositorio Git de Cloud Manager. La canalización de producción en Cloud Manager está configurada para activarse mediante una inserción en la rama estable. Por lo tanto, la canalización de producción se ejecuta mediante cada inserción de cualquier equipo en una rama estable y la implementación de producción se actualiza si pasan todas las puertas de calidad.

![](/help/implementing/cloud-manager/assets/team-setup2.png)

Los empujones a la rama de desarrollo se gestionan de forma diferente. Mientras que una inserción en una rama de desarrollador en el repositorio de Git de un equipo está activando una acción de GitHub y el código se inserta automáticamente en la rama de desarrollo en el repositorio de Git de Cloud Manager, la canalización que no es de producción no se activa automáticamente mediante la inserción de código. Se activa mediante una llamada a la api de Cloud Manager.
La ejecución de la canalización de producción incluye la comprobación del código de todos los equipos a través de las puertas de calidad proporcionadas. Una vez implementado el código en la fase, las pruebas y auditorías se ejecutan para garantizar que todo funciona según lo esperado. Una vez pasadas todas las puertas, los cambios se implementan en producción sin interrupciones ni downtime.
Para el desarrollo local, se utiliza el [SDK para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing). El SDK permite configurar un autor, publicación y Dispatcher local. Esto permite el desarrollo sin conexión y tiempos de respuesta rápidos. A veces solo se utiliza autor para el desarrollo, pero la configuración rápida de Dispatcher y Publish permite probar todo localmente antes de entrar en el repositorio de Git. Los miembros de cada equipo generalmente retiran el código del Git compartido para , así como su propio código de proyecto. No hay necesidad de retirar otros proyectos ya que los proyectos son independientes.

![](/help/implementing/cloud-manager/assets/team-setup3.png)

Esta configuración del mundo real puede utilizarse como modelo y luego personalizarse según las necesidades de una empresa. El concepto flexible de ramificación y combinación de git permite realizar variaciones de los flujos de trabajo anteriores, adaptadas a las necesidades de cada equipo. AEM como Cloud Service es compatible con todas estas variaciones sin sacrificar el valor principal de la canalización de Cloud Manager.

### Consideraciones para una configuración de varios equipos {#considerations}

>[!NOTE]
>Para cualquier configuración de varios equipos es crucial definir un modelo de gobernanza y un conjunto de estándares que todos los equipos deben seguir. El modelo descrito anteriormente para una configuración de varios equipos permite escalar un número mayor de equipos y puede utilizar este modelo como punto de partida.

Con el repositorio de Git de Cloud Manager y la canalización de producción, siempre se ejecuta el código de producción completo a través de todas las puertas de calidad, tratándolo como una unidad de implementación. De esta manera, el sistema de producción se mantiene *siempre activo* sin interrupciones ni downtime.
Por el contrario, sin un sistema de este tipo, ya que cada equipo puede realizar implementaciones por separado, existe el riesgo de que una actualización de un equipo único pueda provocar problemas de estabilidad de la producción. Además, requiere coordinación y tiempo de inactividad planificado para implementar actualizaciones. Con un número cada vez mayor de equipos, el esfuerzo de coordinación será mucho más complejo y rápidamente inmanejable.

Si se detecta un problema en las puertas de calidad, la producción no se ve afectada y el problema puede detectarse y solucionarse sin que el Adobe tenga que intervenir. Sin Cloud Service y sin probar siempre toda la implementación, las implementaciones parciales pueden provocar interrupciones que requieran una solicitud de reversión o incluso una restauración completa desde una copia de seguridad. Las pruebas parciales también podrían dar lugar a otros problemas que luego deberían solucionarse después de que el Adobe volviera a requerir coordinación y apoyo.
