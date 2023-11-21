---
title: Implementación de un conector de AEM
description: AEM Obtenga información sobre cómo generar, probar e implementar un conector de. Además, aprenderá sobre los patrones de integración comunes.
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 95%

---

Implementación de un conector de AEM
=============================

A continuación se proporcionan referencias útiles para la creación de [Conectores AEM](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) y deben leerse junto con directrices sobre el [envío](submit.md) y el [mantenimiento](maintain.md) de los conectores.

Tenga en cuenta que se puede obtener una licencia de desarrollador para AEM a través del [Programa Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

Patrones de integración comunes
---------------------------

AEM es una solución de gestión de experiencia web de vanguardia y ofrece muchas potenciales áreas de integraciones. Los patrones de integración comunes incluyen:

* Extracción de datos de un sistema externo en AEM. Por ejemplo, la exportación de información de contacto desde un CRM para que esté disponible para una audiencia más amplia que visite un sitio web con tecnología de AEM.  Las implementaciones deben utilizar los [Trabajos programados](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs) de Sling, que garantizan que el trabajo se ejecute incluso si los contenedores se desactivan. El código debe diseñarse para suponer que el trabajo se puede activar más de una vez.
* Exportación de datos de AEM a un sistema externo. Por ejemplo, la configuración de suscripción a la newsletter se envía en un sitio web con tecnología de AEM a un CRM.
* Recuperación de recursos de AEM. Por ejemplo, un sistema de administración de contenido (CMS) externo que haga referencia a un recurso almacenado en AEM Assets. O, como otro ejemplo, un sistema GIP que se vincula a una imagen en AEM Assets.
* Almacenamiento de recursos en la infraestructura de AEM. Por ejemplo, un sistema de administración de recursos de marketing (MRM) que almacene un recurso aprobado en AEM Assets.
* Configuración y procesamiento de un componente de IU personalizado. Por ejemplo, permita que un autor arrastre y suelte un componente de vídeo y configure un vídeo específico para que se reproduzca en el sitio en directo.
* Actuación en un recurso con un servicio de socio. Por ejemplo, enviar un recurso a una plataforma de vídeo cuando se publica una página.
* Análisis de un sitio, página o recurso en la Admin Console de AEM. Por ejemplo, hacer recomendaciones de SEO para una página existente o no publicada.
* Acceso de nivel de página a los datos de usuario mantenidos por un servicio externo. Por ejemplo, utilice la información demográfica para personalizar la experiencia del sitio. Obtenga información acerca de ContextHub, un marco de trabajo para almacenar, manipular y presentar datos de contexto.
* Traducción de metadatos de recursos o copias de sitios. Consulte el [Conector del Bootstrap del marco de trabajo de traducciones de AEM](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) para ver el código de muestra mediante el marco de trabajo de traducciones de AEM, que es la implementación preferida de los conectores de traducción.


Documentación útil
--------------------

La [documentación](../overview/introduction.md) de Experience Manager as a Cloud Service proporciona información valiosa sobre el desarrollo en AEM. A continuación, se presentan algunos temas técnicos específicos y referencias que pueden resultar útiles al implementar un conector de AEM:

* Las [Muestras de AEM](https://adobe-consulting-services.github.io/acs-aem-samples/) de los Servicios de consultoría de Adobe (ACS) para obtener código bien comentado que ayude a formar a los desarrolladores de AEM
* Los diversos vínculos de documentación de la sección Patrones de integración comunes de este artículo

Recursos de la comunidad
--------------------

Además de la documentación estática anterior, Adobe y la comunidad de AEM ofrecen recursos para ayudar a llevar un conector al mercado:

* El [Foro de AEM](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) de la Comunidad de Adobe es un sitio activo donde sus iguales formulan y responden preguntas
* Hay recursos técnicos de Adobe adicionales disponibles para ciertos niveles de socios. Obtenga más información acerca del [Programa de Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).
* Si su organización desea ayuda para la implementación, considere al equipo de [Servicios profesionales de Adobe](https://www.adobe.com/es/marketing-cloud/service-support/professional-consulting-training.html) o consulte el [Buscador de socios de soluciones](https://solutionpartners.adobe.com/home/partnerFinder.html) para obtener una lista de los socios de Adobe de todo el mundo

Reglas de estructura del paquete
-----------------------

Para admitir implementaciones móviles, los paquetes de AEM as a Cloud Service, de los cuales los conectores son ejemplos, tienen una estricta separación entre el contenido “inmutable” y el “mutable”. Los paquetes deben separarse claramente entre los que incluyen:

* `/apps`
* `/content` y `/conf`

Los conectores deben cumplir estas directrices de empaquetado, que se describen en [este artículo](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Los conectores existentes también deben refactorizarse para ajustarse.

Además, solo Adobe debe escribir código en `/libs`, y los clientes y socios en `/apps`.

Es posible que también sea necesario refactorizar los conectores existentes para mover cualquier configuración que se haya colocado una vez `/etc` en otras carpetas de nivel superior, como `/conf`. Esta reestructuración se llevó a cabo como parte de AEM 6.5 y se describe en la [Documentación de AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=es).

Se recomienda colocar la mayoría del código del conector en `/apps/connectors/<vendor>` para promocionar una estructura de repositorio limpia para los clientes que tienen varios conectores.

Configuración de servicios de nube
-----------------------------

Un aspecto de la implementación del conector es el código que respalda la configuración del conector. Este código hace que aparezca una tarjeta con el nombre del conector en Herramientas > Operaciones > Cloud Services. Cuando se hace clic, un [explorador de configuración](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) aparece donde el cliente selecciona la carpeta principal para contener la configuración del conector. El código del conector debe generar un formulario con todas las propiedades que deben configurarse, almacenando finalmente los valores en una carpeta de configuración en `/conf`. Esta carpeta se puede seleccionar posteriormente en la pestaña Propiedades del sitio o en la pestaña Propiedades del activo.


Configuraciones según el contexto
-----------------------------

[Configuraciones según el contexto](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) permite crear capas de configuración en distintas carpetas, incluso `/libs`, `/apps`, `/conf` y subcarpetas en `/conf`. Admite la herencia para que un cliente pueda configurar la configuración global mientras realiza cambios específicos para cada micrositio. Dado que es posible utilizar esta función para las configuraciones de Cloud Service, el código del conector debe hacer referencia a la configuración mediante la API de configuración según el contexto en lugar de hacer referencia a un nodo de configuración específico.

Si se utilizan configuraciones modificadas en el conector, cree el conector para gestionar la inclusión/combinación de cualquier actualización futura de las configuraciones predeterminadas proporcionadas por el conector con cualquier configuración del cliente. Recuerde que el cambio de contenido o configuración personalizado (como el que ha cambiado el cliente) sin advertencia ni consentimiento del cliente puede romperse (o crear un comportamiento inesperado) con su conector.

Prácticas recomendadas de codificación
----------------------

Dado que AEM as a Cloud Service es una solución nativa de la nube, existen algunas directrices que pueden afectar a las estrategias de código de un conector. Consulte [Directrices de desarrollo as a Cloud Service AEM](/help/implementing/developing/introduction/development-guidelines.md) para obtener más información.

Prueba del conector AEM
-------------------------

Se deben crear nuevos conectores (o se deben modificar los conectores existentes) mediante técnicas de desarrollo de entorno local. El equipo de socios proporcionará a los socios de ISV un entorno de zona protegida en el que pueden implementar su conector de AEM en una aplicación convencional para garantizar que funcione.
