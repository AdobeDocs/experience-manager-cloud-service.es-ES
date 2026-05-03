---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: Obtenga información acerca de AEM as a Cloud Service Developer Console y su conjunto de herramientas de solo lectura para depurar entornos de nube.
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: 51c14ba3c15e0136911003752253d21ed673a0eb
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---


# AEM as a Cloud Service Developer Console (beta) {#developer-console}

AEM as a Cloud Service Developer Console incluye un conjunto de herramientas de solo lectura para depurar entornos de nube. Se puede acceder a él a través de un vínculo por entorno en Cloud Manager y ofrece funciones para ver paquetes, configuración de OSGi, servicios y servlets, etc.

>[!NOTE]
>
>En este artículo se describe una experiencia renovada para AEM Cloud Service Developer Console, que ahora está en versión beta.
>
>* Un conjunto limitado de usuarios puede acceder a la nueva consola mediante un botón en la parte superior de la Developer Console actual.
>* Adobe agradece cualquier comentario que pueda enviar a `aemcs-new-devconsole-ui-beta@adobe.com`.
>* Para obtener la documentación sobre AEM Developer Console actual, consulte [este artículo.](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)
>* El Developer Console de AEM as a Cloud Service no debe confundirse con el [*Adobe Developer Console* con nombre similar.](https://developer.adobe.com/developer-console/)

>[!TIP]
>
>Developer Console es de solo lectura. Si está trabajando en el desarrollo local mediante SDK y necesita modificar la configuración de OSGi o el contenido del repositorio, puede utilizar:
>
>* [CRXDE Lite](/help/implementing/developing/tools/crxde.md)

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

## Requisitos previos {#prerequisites}

Developer Console solo es accesible para usuarios con ciertas funciones en ciertos programas.

* Para los programas de producción, la &quot;Cloud Manager - Función de desarrollador&quot; en Adobe Admin Console controla el acceso a Developer Console.
* Para los programas de zonas protegidas, cualquier usuario con un perfil de producto que conceda acceso a AEM puede utilizar Developer Console.
* Para todos los programas, se requiere el &quot;Cloud Manager - Función de desarrollador&quot; para los volcados de estado y el acceso al explorador del repositorio.

Para ver datos de los servicios de autor y publicación, los usuarios también deben estar asignados a &quot;Usuarios de AEM&quot; o &quot;Perfil de producto de los administradores de AEM&quot; en ambos servicios.

Para obtener más información acerca de la configuración de permisos de usuario, consulte la [Documentación de Cloud Manager.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)

## Pestaña Paquetes OSGi {#osgi-bundles}

La pestaña **Paquetes OSGi** proporciona una descripción general de los paquetes OSGi implementados en el entorno seleccionado y ofrece una búsqueda de texto completo.

![Nueva pantalla de paquetes OSGi en Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* La pestaña proporciona información sobre el estado real de los paquetes en el entorno, como paquetes exportados, paquetes importados, servicios utilizados y más.
* Es ideal comprobar el estado de los paquetes para ver si el paquete hace lo que se espera que haga.

**Ejemplo de caso de uso:** Supongamos que especifica un intervalo de versiones para una dependencia en el paquete. Pero algo va mal con la dependencia y necesita comprobar qué versión de la dependencia utiliza realmente el paquete. Para comprobarlo, abra Developer Console y haga clic en el nombre de un paquete en la ficha **Paquetes OSGi** para acceder a los detalles del paquete y utilice el acordeón **Importación de paquetes** para comprobar qué versión del paquete o versión del paquete se está utilizando durante la ejecución. Con esta información, puede ajustar el intervalo de versiones de dependencia de Maven o adaptar el código.

## Pestaña Paquetes Java {#java-packages}

La pestaña **Paquetes Java** ofrece un campo de búsqueda para buscar paquetes que estén activos en el sistema OSGi del entorno.

![Paquetes Java en la IU de Developer Console](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Puede ver qué paquete exporta (o proporciona) el paquete y puede ver qué paquetes importan (o utilizan) el paquete.
* También puede buscar paquetes duplicados (el mismo paquete, versiones diferentes), lo que puede causar problemas en algunos casos.

**Ejemplo de caso de uso:** Supongamos que un servicio personalizado que utiliza el [cargador dinámico de clases](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) carga una clase sin especificar una versión. Dado que varios paquetes exportan versiones diferentes, la implementación varía, lo que provoca cambios en el comportamiento. Desea comprobar qué paquetes se encuentran en el entorno sin analizar el modelo de funciones. Con esta pestaña puede buscar el paquete y ver todas las versiones exportadas, y luego puede utilizar un mejor intervalo de versiones.

## Pestaña Configuraciones {#configurations}

La ficha **Configuraciones** ofrece una lista de configuraciones activa en el entorno en la que se pueden realizar búsquedas. Puede ver qué propiedades proporciona cada configuración haciendo clic en ella y viendo la página de detalles.

![Pestaña Configuraciones en la interfaz de usuario de Developer Console](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* **Ejemplo de caso de uso:** Supongamos que desea asegurarse de que las configuraciones especificadas estén realmente presentes en el entorno. Si busca en la ficha **Configuraciones** de la consola y falta la configuración, puede comprobar el modelo de características, el modo de ejecución de la configuración o la carpeta.

## Pestaña Servlets {#servlets}

La ficha **Servlets** incluye un campo de búsqueda donde puede especificar una ruta con selectores y una extensión con GET o POST. A continuación, proporciona una lista de servlets en orden de preferencia que administra la solicitud en Sling.

![Ficha Servlets en la IU de Developer Console](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

**Ejemplo de caso de uso:** Supongamos que tiene un servlet OSGi que debe activarse tras una solicitud y mostrar la salida de impresión en la respuesta. Sin embargo, en lugar del resultado esperado, se obtiene una respuesta vacía. Debe comprobar si algún otro servlet tiene prioridad sobre el servlet debido a selectores, `resourceType`, extensiones o clasificación más específicos. Busca la ruta esperada y encuentra otro servlet activo con una clasificación más alta. A continuación, puede decidir si puede aumentar la clasificación del servlet añadiendo selectores, por ejemplo.

## Pestaña Servicios {#services}

La ficha **Servicios** proporciona una descripción general de los servicios presentes en el entorno seleccionado y ofrece una búsqueda de texto completo.

![Pestaña Servicios en la interfaz de usuario de Developer Console](/help/implementing/developing/introduction/assets/services-dev-console.png)

Haga clic en un servicio para ver sus detalles.

## Pestaña Componentes OSGi {#osgi-components}

La pestaña **Componentes OSGi** proporciona una descripción general de los componentes OSGi que están presentes en el tipo de entorno seleccionado y ofrece una búsqueda de texto completo. Puede ver el estado activo de los componentes OSGi en el entorno y a qué servicios satisface, el paquete que lo proporciona y el tipo de activación (inmediata o retrasada).

![Pestaña Componentes OSGi en la IU de Developer Console](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* **Ejemplo de caso de uso 1:** Supongamos que necesita comprobar si un componente activado con una configuración está activo en un entorno específico porque se está produciendo un comportamiento inesperado. Basta con buscar el componente en la búsqueda y comprobar si está activo o no.
* **Ejemplo de caso de uso 2:** Supongamos que desea ver qué componentes listos para usar están disponibles en el entorno e identificar los servicios que admiten para obtener más información acerca de Adobe Experience Manager as a Cloud Service. Puede comprobar los componentes en la lista de componentes.

## Pestaña Integraciones {#integrations}

La pestaña **Integraciones** permite a los administradores generar, cambiar el nombre y eliminar credenciales de servicio y tokens de desarrollador.

![Pestaña Integraciones en la interfaz de usuario de Developer Console](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

## Pestaña Repositorio {#repository}

La ficha **Repositorio** abre el explorador [Repositorio.](/help/implementing/developing/tools/repository-browser.md)

## Volcados de estado/Pestaña Consultas {#status-dumps-queries}

La pestaña **volcados de estado / consultas** le permite descargar un volcado de texto completo o JSON del estado actual de paquetes, paquetes, configuraciones, servicios, componentes, trabajos de Sling o definiciones de Oak.

![Volcados de estado/pestaña Consultas en la IU de Developer Console](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

También puede abrir la herramienta [Rendimiento de la consulta.](/help/operations/query-and-indexing-best-practices.md#query-performance-tool)

* **Ejemplo de caso de uso:** Esta ficha es especialmente útil si encuentra un estado inesperado y desea comunicarlo o documentarlo para otros desarrolladores. Al descargar el volcado, se obtiene una instantánea del estado para consultarlo más adelante.
