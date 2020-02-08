---
title: Implementación de un conector AEM
description: Implementación de un conector AEM
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f

---


Implementación de un conector AEM
=============================

A continuación se proporcionan referencias útiles para la creación de [Conectores](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) AEM y deben leerse junto con directrices sobre el [envío](submit.md) y el [mantenimiento](maintain.md) de los conectores.

Tenga en cuenta que se puede obtener una licencia de desarrollador para AEM a través del programa [Adobe Exchange](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html).

Patrones de integración comunes
---------------------------

AEM es una solución de administración de experiencias web de vanguardia y ofrece muchas áreas de integraciones potenciales. Los patrones de integración comunes incluyen:

* Extracción de datos de un sistema externo en AEM. Por ejemplo, exportar información de contacto desde un CRM para que esté disponible para un público más amplio que visite un sitio web con tecnología AEM.  Las implementaciones deben utilizar los trabajos [programados](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)de Sling, lo que garantiza que el trabajo se ejecute incluso si los contenedores se desactivan. El código debe estar diseñado para suponer que el trabajo puede activarse más de una vez.
* Exportación de datos de AEM a un sistema externo. Por ejemplo, la configuración de suscripción a la newsletter se envía en un sitio web con tecnología AEM a un CRM.
* Recuperación de recursos de AEM. Por ejemplo, un sistema de gestión de contenido (CMS) externo que hace referencia a un recurso almacenado en Recursos AEM. O como otro ejemplo, un sistema PIM que se vincula a una imagen en Recursos AEM.
* Almacenamiento de recursos en la infraestructura de AEM. Por ejemplo, un sistema de administración de recursos de marketing (MRM) que almacena un recurso aprobado en Recursos AEM.
* Configuración y representación de un componente de interfaz de usuario personalizado. Por ejemplo, permita que un autor arrastre y suelte un componente de vídeo y configure un vídeo específico para que se reproduzca en el sitio de lanzamiento.
* Actuar en un recurso con un servicio asociado. Por ejemplo, enviar un recurso a una plataforma de vídeo cuando se publica una página.
* Análisis de un sitio, página o recurso en la consola de administración de AEM. Por ejemplo, hacer recomendaciones SEO para una página existente o no publicada.
* Acceso de nivel de página a los datos de usuario que mantiene un servicio externo. Por ejemplo: aproveche la información demográfica para personalizar la experiencia del sitio. Obtenga información sobre ContextHub, un marco para almacenar, manipular y presentar datos de contexto.
* Traduciendo la copia del sitio o los metadatos del recurso. Consulte el Conector [de arranque de](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) AEM Translation Framework para obtener código de muestra con AEM Translation Framework, que es la implementación preferida de los conectores de traducción.


Documentación útil
--------------------

Experience Manager como [documentación](../overview/introduction.md) de servicios en la nube proporciona información valiosa sobre el desarrollo en AEM. A continuación se presentan algunos temas técnicos específicos y referencias que puede resultar útiles a la hora de implementar un conector AEM:

* Ejemplos [de Adobe Consulting Services (ACS)](http://adobe-consulting-services.github.io/acs-aem-samples/) AEM para obtener un código bien comentado que ayude a educar a los desarrolladores de AEM
* Los diversos vínculos de documentación de la sección Patrones de integración comunes de este artículo

Recursos de la comunidad
--------------------

Además de la documentación estática anterior, Adobe y la comunidad de AEM ofrecen recursos para ayudar a comercializar un conector:

* El foro [de](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) AEM de la comunidad de Adobe es un sitio activo en el que sus compañeros formulan preguntas y responden a ellas
* Hay recursos técnicos adicionales de Adobe disponibles para determinados niveles de socios. Obtenga más información sobre el programa [Adobe Exchange](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html).
* Si su organización desea ayuda para la implementación, considere al equipo de Adobe [Professional Services](http://www.adobe.com/marketing-cloud/service-support/professional-consulting-training.html) o consulte el Buscador [de socios de](https://solutionpartners.adobe.com/home/partnerFinder.html) soluciones para obtener una lista de los socios de Adobe de todo el mundo

Reglas de estructura de paquetes
-----------------------

Para admitir implementaciones móviles, AEM como paquete de servicios en la nube, de los cuales los conectores son ejemplos, tiene una separación estricta entre el contenido &quot;inmutable&quot; y el &quot;mutable&quot;. Los paquetes deben separarse de forma limpia entre los que incluyen:

* `/apps`
* `/content` y `/conf`

Los conectores deben atenerse a estas directrices de empaquetado, que se describen en [este artículo](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Los conectores existentes también deben refactorizarse para ajustarse a ellos.

Además, solo Adobe debe escribir código en `/libs`, con clientes y socios escribiendo en `/apps`.

Es posible que también sea necesario refactorizar los conectores existentes para mover cualquier configuración que alguna vez se haya colocado `/etc` en otras carpetas de nivel superior, como `/conf`. Esto se describe en la documentación [de](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)AEM.

Se recomienda colocar la mayoría del código de conector en `/apps/connectors/<vendor>` para promocionar una estructura de repositorio limpia para los clientes que tienen varios conectores.

Configuración de servicios de nube
-----------------------------

Un aspecto de la implementación del conector es el código que respalda la configuración del conector. Este código hace que una tarjeta con el nombre del conector aparezca en Herramientas > Operaciones > Servicios de nube. Cuando se hace clic en él, aparece un navegador de configuración donde el cliente selecciona la carpeta principal para que contenga la configuración del conector. El código del conector debe resultar en un formulario con todas las propiedades que deben configurarse, almacenando finalmente los valores en una carpeta de configuración debajo de `/conf`. Esta carpeta se puede seleccionar posteriormente en la ficha Propiedades del sitio o en la ficha Propiedades de los recursos.


Configuraciones según el contexto
-----------------------------

[Las configuraciones](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) según el contexto permiten crear capas de configuración en diferentes carpetas, incluidas `/libs`, `/apps``/conf` y subcarpetas en `/conf`. Admite herencia para que un cliente pueda configurar la configuración global mientras realiza cambios específicos para cada micrositio. Dado que es posible aprovechar esta función para las configuraciones de servicios de nube, el código del conector debe hacer referencia a la configuración mediante la API de configuración según el contexto en lugar de hacer referencia a un nodo de configuración específico.

Si se utilizan configuraciones modificadas en el conector, diseñe el conector para gestionar incluyendo/fusionando cualquier actualización futura de las configuraciones predeterminadas proporcionadas por el conector con cualquier configuración del cliente. Recuerde que cambiar el contenido o la configuración personalizados (como en el caso de los cambios realizados por el cliente) sin previo aviso y consentimiento del cliente puede dañar (o crear un comportamiento inesperado) con su conector.

Prácticas recomendadas de codificación
----------------------

Dado que AEM como servicio de nube es una solución nativa de la nube, existen algunas directrices que pueden afectar a las estrategias de código de un conector. Consulte [AEM as a Cloud Service Development Guidelines](/help/implementing/developing/introduction/development-guidelines.md) para obtener más información.

Prueba del conector AEM
-------------------------

Se deben crear nuevos conectores (o modificar los existentes) utilizando técnicas de desarrollo del entorno local. El equipo de socios proporcionará a los socios ISV un entorno de simulación de pruebas en el que pueden implementar su conector AEM en una aplicación de vainilla para garantizar su funcionamiento.
