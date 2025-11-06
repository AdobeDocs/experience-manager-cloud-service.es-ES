---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: Obtenga información sobre CRXDE Lite y AEM as a Cloud Service Developer Console.
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 1%

---

# AEM as a Cloud Service Developer Console (beta) {#developer-console}

>[!NOTE]
>
>En este artículo se describe una experiencia renovada para AEM Cloud Service Developer Console, que ahora está en versión beta. Algunos clientes pueden acceder a él haciendo clic en un botón de la parte superior de la IU clásica. Adobe recibe con agrado sus comentarios enviándolos a `aemcs-new-devconsole-ui-beta@adobe.com`. Para obtener información acerca del Developer Console clásico de AEM, vea [este artículo](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console).

AEM as a Cloud Service Developer Console incluye un conjunto de herramientas para la depuración en entornos en la nube. Se puede acceder a través de un vínculo por entorno en Cloud Manager.

>[!NOTE]
>El Developer Console de AEM as a Cloud Service no debe confundirse con el [*Adobe Developer Console*](https://developer.adobe.com/developer-console/) con nombre similar.
>


<!--
There are multiple ways of accessing it:

1. Launch from Cloud Manager  

1. Type a url that can be determined by adjusting the Author or Publish service urls as follows:
   ```  
   https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com
   ```  

1. As a shortcut, the following Cloud Manager CLI command can be used to launch the AEM as a Cloud Service Developer Console based on an environment parameter described below:    
   ```
   aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>
   ```
-->

Los desarrolladores pueden acceder a las funciones que se describen a continuación:

## Paquetes OSGi {#osgi-bundles}

![Nueva pantalla de paquetes OSGi en la consola de desarrolladores](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* Una descripción general de los paquetes OSGI implementados en el tipo de entorno seleccionado. Permite una búsqueda de texto completo.
* Es útil obtener información sobre el estado real de los paquetes en el entorno. Puede obtener información como paquetes exportados, paquetes importados, servicios utilizados y más.
* Los desarrolladores quieren verificar el entorno real y comprobar si el paquete hace lo que esperan que haga.
* **Ejemplo de caso de uso:** Se ha especificado un intervalo de versiones de una dependencia en el paquete. Algo va mal en la dependencia. Desea comprobar qué versión de la dependencia se está cableando en el paquete. Para comprobarlo, vaya a los detalles del paquete y utilice la importación de paquetes/paquetes para comprobar qué versión del paquete o versión del paquete se está utilizando en el tiempo de ejecución. Con esta información, puede ajustar el intervalo de versiones de dependencia de Maven o adaptar el código.

## Paquetes Java {#java-packages}

![Paquetes Java en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Un mensaje de búsqueda que puede utilizar para buscar paquetes que estén activos en el sistema OSGI del entorno. En esta ubicación puede ver qué paquete exporta (o proporciona) el paquete y qué paquete importa (o utiliza) el paquete. También puede buscar paquetes duplicados (el mismo paquete, versiones diferentes), lo que puede causar problemas en algunos casos.
* **Ejemplo de caso de uso:** Un servicio personalizado que usa el [cargador de clases dinámicas](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) carga una clase sin especificar una versión. Dado que varios paquetes exportan versiones diferentes, la implementación varía, lo que provoca cambios en el comportamiento. El desarrollador desea comprobar qué paquetes se encuentran en el entorno sin analizar el modelo de funciones. Buscan el paquete y ven todas las versiones exportadas. Esta capacidad les proporciona la información para introducir un mejor intervalo de versiones.

## Servlets {#servlets}

![Ficha Servlets en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* Un mensaje de búsqueda en el que se puede especificar una ruta con selectores y una extensión con GET o POST. A continuación, proporciona los resultados de los servlets en orden de preferencia que administra la solicitud en Sling.
* **Ejemplo de caso de uso:** Tiene un servlet OSGI que debe activarse tras una solicitud e imprimirse en la respuesta. Sin embargo, en lugar del resultado esperado, la respuesta devuelve empty. Debe comprobar si algún otro servlet tiene prioridad sobre el servlet debido a selectores, `resourceType`, extensiones o clasificación más específicos. Busca la ruta esperada y descubre que hay otro servlet activo con una clasificación más alta. A continuación, decida si puede colocar el servlet por encima en la clasificación añadiendo selectores, por ejemplo.

## Servicios {#services}

![Pestaña Servicios en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/services-dev-console.png)

* Similar a la vista Componentes de OSGI, pero se basa en servicios. Puede buscar rápidamente qué servicios se proporcionan con determinadas propiedades.

## Componentes OSGi {#osgi-components}

![Pestaña Componentes OSGi en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* Una descripción general de los componentes de OSGI presentes en el tipo de entorno seleccionado. Permite una búsqueda de texto completo.
* Puede obtener el estado activo de los componentes OSGI en el entorno. Puede ver qué servicios satisface, el paquete que lo proporciona y el tipo de activación (inmediata o retrasada).
* **Ejemplo de caso de uso 1:** Como desarrollador, debe comprobar si un componente activado con una configuración está activo en un entorno específico. El motivo es que el comportamiento esperado no se está produciendo. Basta con buscar el componente en la búsqueda y comprobar si está activo o no.
* **Ejemplo de caso de uso 2:** Desea ver qué componentes listos para usar están disponibles en el entorno e identificar los servicios que admiten. Esta capacidad le ayuda a obtener más información sobre Adobe Experience Manager as a Cloud Service. Puede desprotegerlos en la lista de componentes.

## Integraciones {#integrations}

![Pestaña Integraciones en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* Los administradores tienen la capacidad de generar, cambiar el nombre y eliminar credenciales de servicio y tokens de desarrollador.

## Repositorio {#repository}

* Abre el [Explorador del repositorio](/help/implementing/developing/tools/repository-browser.md).

## Volcados de estado/Consultas {#status-dumps-queries}

![Volcados de estado/pestaña Consultas en la IU de la consola de desarrollo](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* Un volcado de texto completo o JSON del estado actual de paquetes, paquetes, configuraciones, servicios, componentes, trabajos de Sling o definiciones de Oak.
* Resulta útil, especialmente si el desarrollador ha descubierto algún estado inesperado y desea comunicar o documentar este estado para otros desarrolladores. Al descargar el volcado, se obtiene una instantánea del estado para consultarlo más adelante.

## Configuraciones {#configurations}

![Pestaña Configuraciones en la interfaz de usuario de la consola de desarrollo](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* Una lista de configuraciones activa en el entorno en la que se pueden buscar. Puede ver qué propiedades proporcionan las configuraciones desprotegiendo la página de detalles.
* **Ejemplo de caso de uso:** Un desarrollador desea asegurarse de que las configuraciones que especificó estén realmente presentes en el entorno. Si falta la configuración, pueden comprobar el modelo de funciones o el modo de ejecución o la carpeta de configuración.

Para los programas de producción, la &quot;Cloud Manager - Función de desarrollador&quot; en Adobe Admin Console controla el acceso a AEM as a Cloud Service Developer Console. Para los programas de zonas protegidas, cualquier usuario con un perfil de producto que conceda acceso a AEM puede utilizar Developer Console. Para todos los programas, se requiere el &quot;Cloud Manager - Función de desarrollador&quot; para los volcados de estado y el acceso al explorador del repositorio. Para ver datos de los servicios de autor y publicación, los usuarios también deben estar asignados al Perfil de producto de los usuarios de AEM o de los administradores de AEM en ambos servicios.

Para obtener más información sobre cómo configurar permisos de usuario, consulte [Documentación de Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

