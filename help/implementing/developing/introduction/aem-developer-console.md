---
title: AEM as a Cloud Service Developer Console (Beta)
description: Obtenga información sobre CRX/DE Lite y AEM as a Cloud Service Developer Console
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 16379d9cb7cdf876502205c12a233a95b410a67a
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---


# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>En este artículo se describe una experiencia renovada para AEM Cloud Service Developer Console, que ahora está en versión beta y disponible para algunos clientes haciendo clic en un botón en la parte superior de la IU clásica. Agradecemos cualquier comentario que pueda enviar a `aemcs-new-devconsole-ui-beta@adobe.com`. AEM Para obtener información acerca de la versión clásica de Developer Console, vea [este artículo](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console).

## Herramientas de desarrollo de AEM as a Cloud Service {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>El Developer Console de AEM as a Cloud Service no debe confundirse con el [*Adobe Developer Console*](https://developer.adobe.com/developer-console/) con nombre similar.
>

Los clientes pueden acceder a la lista CRXDE en el entorno de desarrollo del nivel de creación, pero no en la fase o en la producción. El repositorio inmutable (`/libs`, `/apps`) no se puede escribir en el tiempo de ejecución, por lo que al intentar hacerlo se producirán errores.

En su lugar, el Explorador de repositorios se puede iniciar desde AEM as a Cloud Service Developer Console, lo que proporciona una vista de solo lectura del repositorio para todos los entornos en los niveles de creación, publicación y vista previa. Para obtener más información, consulte [Explorador de repositorios](/help/implementing/developing/tools/repository-browser.md).

Un conjunto de herramientas para depurar entornos de desarrollador de AEM as a Cloud Service está disponible en AEM as a Cloud Service Developer Console para entornos de RDE, desarrollo, fase y producción. La dirección URL se puede determinar ajustando las direcciones URL del autor o del servicio Publish de la siguiente manera:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como método abreviado, se puede utilizar el siguiente comando CLI de Cloud Manager para iniciar AEM as a Cloud Service Developer Console en función de un parámetro de entorno que se describe a continuación:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [Información de la versión](/help/release-notes/home.md) para obtener más información.

Los desarrolladores pueden generar información de estado y resolver varios recursos.

Como se muestra a continuación, la información de estados disponibles incluye el estado de los paquetes, los componentes, las configuraciones de OSGI, los índices de Oak, los servicios OSGI y los trabajos de Sling.

### Paquetes OSGi {#osgi-bundles}

![Nueva pantalla de paquetes OSGi en la consola de desarrolladores](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* Esto produce una descripción general de los paquetes OSGI implementados en el tipo de entorno seleccionado. Permite una búsqueda de texto completo.
* Es útil obtener información sobre el estado real de los paquetes en el entorno. Puede obtener información como paquetes exportados, paquetes importados, servicios utilizados y más.
* Los desarrolladores quieren verificar el entorno real y comprobar si el paquete hace lo que esperan que haga.
* **Ejemplo de caso de uso:** Se ha especificado un intervalo de versiones de una dependencia en el paquete. Algo va mal en la dependencia. Desea comprobar qué versión de la dependencia se está cableando en el paquete. Para comprobar esto, vaya a los detalles del paquete y utilice la importación de paquetes/paquetes para comprobar qué versión del paquete o versión del paquete se está utilizando en el tiempo de ejecución para averiguarlo. Con esta información puede ajustar el intervalo de versiones de dependencia de Maven o adaptar el código.

### Paquetes Java {#java-packages}

![Paquetes Java en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Esto proporciona un mensaje de búsqueda que puede utilizar para buscar paquetes que estén activos en el sistema OSGI del entorno. En esta ubicación puede ver qué paquete exporta (o proporciona) el paquete y qué paquete importa (o utiliza) el paquete. También puede buscar paquetes duplicados (el mismo paquete, versiones diferentes), lo que puede causar problemas en algunos casos.
* **Caso de uso de ejemplo:** Un servicio personalizado que usa el [cargador dinámico de clases](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) está cargando una clase sin especificar una versión, que se exporta mediante varios paquetes con distintas versiones, lo que provoca que la implementación sea diferente y que cambie el comportamiento. El desarrollador desea ver qué paquetes están en el entorno sin analizar el modelo de funciones, por lo que busca este paquete y ve todas las versiones que se exportan. Esto les proporciona la información para introducir un mejor intervalo de versiones.

### Servlets {#servlets}

![Ficha Servlets en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* Esto proporciona un mensaje de búsqueda en el que se puede especificar una ruta con selectores y una extensión con GET o POST. A continuación, proporciona los resultados de los servlets en orden de preferencia que administrarán la solicitud en Sling.
* **Ejemplo de caso de uso:** Tiene un servlet OSGI que debe activarse en una solicitud e imprimir algo en la respuesta, pero en su lugar obtiene una respuesta vacía. Debe comprobar si algún otro servlet tiene prioridad sobre el servlet debido a selectores, `resourceType`, extensiones o clasificación más específicos. Busca la ruta esperada y descubre que hay otro servlet activo con una clasificación más alta. A continuación, decida si puede colocar el servlet por encima en la clasificación añadiendo selectores, por ejemplo.

### Servicios {#services}

![Pestaña Servicios en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/services-dev-console.png)

* Similar a la vista Componentes de OSGI, pero se basa en servicios. Puede buscar rápidamente qué servicios se proporcionan con determinadas propiedades.

### Componentes OSGi {#osgi-components}

![Pestaña Componentes OSGi en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* Esto produce una descripción general de los componentes OSGI presentes en el tipo de entorno seleccionado. Permite una búsqueda de texto completo.
* Puede obtener el estado activo de los componentes OSGI en el entorno. Puede ver qué servicios satisface, el paquete que lo proporciona y el tipo de activación (inmediata o retrasada).
* **Ejemplo de caso de uso 1:** Como desarrollador, desea comprobar si un componente activado con una configuración está activo o no en un entorno concreto, ya que no obtiene el comportamiento esperado. Simplemente debe buscar el componente en la búsqueda y comprobar si el componente está activo o no.
* **Ejemplo de caso de uso 2:** Para obtener más información sobre Adobe Experience Manager as a Cloud Service, le interesa ver qué componentes listos para usar están presentes en el entorno y qué servicios satisfacen. Puede desprotegerlos en la lista de componentes.

### Integraciones {#integrations}

![Pestaña Integraciones en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* Permite a los administradores generar, cambiar el nombre y eliminar credenciales de servicio y tokens de desarrollador.

### Repositorio {#repository}

* Abre el [Explorador del repositorio](/help/implementing/developing/tools/repository-browser.md).

### Volcados de estado/Consultas {#status-dumps-queries}

![Volcados de estado/pestaña Consultas en la IU de la consola de desarrollo](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* Proporciona un volcado de texto completo o JSON del estado actual de paquetes, paquetes, configuraciones, servicios, componentes, trabajos de sling o definiciones de oak.
* Esto puede resultar útil, especialmente si el desarrollador ha descubierto un estado inesperado y desea comunicarlo o documentarlo a otros desarrolladores. Al descargar el volcado, se obtiene una instantánea del estado para consultarlo más adelante.

### Configuraciones {#configurations}

![Pestaña Configuraciones en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* Esto le proporciona una lista de configuraciones activas en el entorno en la que se pueden buscar. Puede ver qué propiedades proporcionan las configuraciones desprotegiendo la página de detalles.
* **Ejemplo de caso de uso:** Un desarrollador desea asegurarse de que las configuraciones que especificó estén realmente presentes en el entorno. Si falta la configuración, pueden comprobar el modelo de funciones, el modo de ejecución de la configuración o la carpeta.

Para los programas de producción, el acceso a AEM as a Cloud Service Developer Console se define mediante la &quot;Cloud Manager - Developer Role&quot; en Adobe Admin Console, mientras que para los programas de zona protegida, AEM as a Cloud Service Developer Console está disponible para cualquier usuario con un perfil de producto que le permita acceder a AEM as a Cloud Service. Para todos los programas, se necesita &quot;Cloud Manager AEM AEM: función de desarrollador&quot; para los volcados de estado y el explorador de repositorios y los usuarios también deben definirse en el perfil de producto de los usuarios o administradores de la en los servicios de autor y publicación para ver los datos de ambos servicios. Para obtener más información sobre cómo configurar permisos de usuario, consulte [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).