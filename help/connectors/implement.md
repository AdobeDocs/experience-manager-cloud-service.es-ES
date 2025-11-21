---
title: Implementación de un conector de AEM
description: Obtenga información sobre los conectores, lo que pueden hacer y cómo implementar estas valiosas herramientas en Experience Manager.
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
feature: Operations
role: Admin
source-git-commit: a9cec66cf518a19a5a6152d431a052369b5b503a
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 71%

---


Implementación de un conector de AEM
=============================

A continuación se proporcionan referencias útiles para la creación de Conectores AEM y deben leerse con instrucciones sobre el [envío](submit.md) y el [mantenimiento de los conectores](maintain.md).

Se puede obtener una licencia de desarrollador para AEM a través del [Programa de Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).

Patrones de integración comunes
---------------------------

AEM es una solución de gestión de experiencia web de vanguardia y ofrece muchas potenciales áreas de integraciones. Los patrones de integración comunes incluyen:

* Extracción de datos de un sistema externo en AEM. Por ejemplo, la exportación de información de contacto desde un CRM para que esté disponible para un público más amplio que visite un sitio web con tecnología de AEM.  Las implementaciones deben utilizar los [Trabajos programados](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs) de Sling, que garantizan que el trabajo se ejecute incluso si los contenedores se desactivan. El código debe diseñarse para suponer que el trabajo se puede activar más de una vez.
* Exportación de datos de AEM a un sistema externo. Por ejemplo, la configuración de suscripción a la newsletter se envía en un sitio web con tecnología de AEM a un CRM.
* Recuperación de recursos de AEM. Por ejemplo, un sistema de administración de contenido (CMS) externo que haga referencia a un recurso almacenado en AEM Assets. O, como otro ejemplo, un sistema PIM que se vincula a una imagen en AEM Assets.
* Almacenamiento de recursos en la infraestructura de AEM. Por ejemplo, un sistema de administración de recursos de marketing (MRM) que almacene un recurso aprobado en AEM Assets.
* Configuración y procesamiento de un componente de IU personalizado. Por ejemplo, permita que un autor arrastre y suelte un componente de vídeo y configure un vídeo específico para que se reproduzca en el sitio en directo.
* Actuación en un recurso con un servicio de socio. Por ejemplo, enviar un recurso a una plataforma de vídeo cuando se publica una página.
* Análisis de un sitio, página o recurso en AEM Admin Console. Por ejemplo, hacer recomendaciones de SEO para una página existente o no publicada.
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
* Hay recursos técnicos de Adobe adicionales disponibles para ciertos niveles de socios. Obtenga más información acerca del [Programa de Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).
* Si su organización desea ayuda para la implementación, considere al equipo de [Servicios profesionales de Adobe](https://solutionpartners.adobe.com/s/directory) o consulte el [Buscador de socios de soluciones](https://solutionpartners.adobe.com/s/directory/) para obtener una lista de los socios de Adobe de todo el mundo

Reglas de estructura del paquete
-----------------------

Para facilitar las implementaciones móviles, los paquetes de AEM as a Cloud Service (como los conectores) mantienen una división estricta entre el contenido &quot;inmutable&quot; y el &quot;mutable&quot;. Los paquetes deben estar claramente organizados para incluir:

* `/apps`
* `/content` y `/conf`

Los conectores deben cumplir estas directrices de empaquetado, que se describen en [Estructura del proyecto AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Los conectores existentes también deben refactorizarse para ajustarse.

Además, solo Adobe debe escribir código en `/libs`, y los clientes y socios en `/apps`.

Es posible que también sea necesario refactorizar los conectores existentes para mover cualquier configuración que se haya colocado una vez `/etc` en otras carpetas de nivel superior, como `/conf`. Esta reestructuración se llevó a cabo como parte de AEM 6.5 y se describe en la [Documentación de AEM 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/restructuring/repository-restructuring).

Adobe recomienda colocar la mayor parte del código del conector en `/apps/connectors/<vendor>` para mantener una estructura de repositorio limpia, especialmente para los clientes que utilizan varios conectores.

Configuración de servicios de nube
-----------------------------

Un aspecto de la implementación del conector es el código que respalda la configuración del conector. Este código hace que aparezca una tarjeta con el nombre del conector en Herramientas > Operaciones > Cloud Services. Cuando se hace clic, un [explorador de configuración](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) aparece donde el cliente selecciona la carpeta principal para contener la configuración del conector. El código del conector debe generar un formulario con todas las propiedades que deben configurarse, almacenando finalmente los valores en una carpeta de configuración en `/conf`. Esta carpeta se puede seleccionar posteriormente en la pestaña Propiedades del sitio o en la pestaña Propiedades del activo.


Configuraciones según el contexto
-----------------------------

[Las configuraciones según el contexto](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) le permiten crear capas de configuración en diferentes carpetas, incluidas `/libs`, `/apps`, `/conf` y subcarpetas en `/conf`. Admite la herencia para que un cliente pueda configurar la configuración global mientras realiza cambios específicos para cada micrositio. Dado que es posible utilizar esta función para las configuraciones de Cloud Services, el código del conector debe hacer referencia a la configuración mediante la API de configuración según el contexto en lugar de hacer referencia a un nodo de configuración específico.

Si se utilizan configuraciones modificadas en el conector, cree el conector para gestionar la inclusión/combinación de cualquier actualización futura de las configuraciones predeterminadas proporcionadas por el conector con cualquier configuración del cliente. Tenga en cuenta que la modificación del contenido o las configuraciones personalizados por el cliente sin previo aviso y consentimiento puede interrumpir o provocar un comportamiento inesperado en su conector.

Prácticas recomendadas de codificación
----------------------

Como AEM as a Cloud Service es una solución nativa de la nube, hay algunas directrices que pueden afectar a las estrategias de código de un conector. Consulte [Directrices de desarrollo as a Cloud Service AEM](/help/implementing/developing/introduction/development-guidelines.md) para obtener más información.

Prueba del conector AEM
-------------------------

Se deben crear nuevos conectores (o se deben modificar los conectores existentes) mediante técnicas de desarrollo de entorno local. El equipo de socios proporciona a los socios de ISV un entorno de zona protegida en el que pueden implementar su conector de AEM en una aplicación convencional para garantizar que funcione.
