---
title: 'Qué es diferente y qué es lo nuevo: Adobe Experience Manager como Cloud Service'
description: 'Qué es diferente y Qué es nuevo: Adobe Experience Manager (AEM) como Cloud Service. '
translation-type: tm+mt
source-git-commit: 52e8cf1e3fb503c1d222a9543cfc1ddfe87132b6
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 10%

---


# Novedades y diferencias {#what-is-new-and-what-is-different}

Durante muchos años AEM ha estado disponible ambos:

* Local

* como un servicio administrado

Existen diferencias intrínsecas entre estos enfoques anteriores y AEM como Cloud Service:

* [Arquitectura](#architecture)
* [Actualizaciones](#upgrades)
* [Cloud Manager](#cloud-manager)
* [Incorporación](#onboarding)
* [Desarrollo de](#developing)
* [Operaciones y rendimiento](#operations-and-performance)
* [Administración de identidades](#identity-management)
* [Creación de la interfaz de usuario](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>Estas descripciones generales no son exhaustivas, pero tienen por objeto proporcionar una introducción.

>[!NOTE]
>
>Para obtener más información sobre las versiones de On-Premise y Managed Service, consulte el conjunto de documentación de [AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html).

## Arquitectura {#architecture}

>[!NOTE]
>
>Para obtener más información, consulte [Arquitectura](/help/core-concepts/architecture.md).

AEM as a Cloud Service ahora tiene:

* Arquitectura dinámica con un número variable de imágenes de AEM.

![Arquitectura dinámica](assets/introduction-03.png "Arquitectura dinámica")

Esta arquitectura:

* Se adapta en función del tráfico *real* y la actividad *real*.

* Tiene instancias individuales que solo se ejecutan cuando es necesario.

* Utiliza aplicaciones modulares.

* Tiene un clúster de creación predeterminado, lo que elimina el tiempo de inactividad durante las tareas de mantenimiento.

Esto permite adaptarse automáticamente a distintos patrones de uso:

![Adaptación automática para patrones de uso variables](assets/introduction-04.png "Adaptación automática para patrones de uso variables")


## Actualizaciones de AEM {#aem-updates}

>[!NOTE]
>Para obtener más información, consulte las [Actualizaciones de versiones de AEM](/help/implementing/deploying/aem-version-updates.md).

AEM como Cloud Service ahora utiliza la integración continua y el Envío continuo (CI/CD) para garantizar que los proyectos se encuentren en la versión AEM más actual. Esto significa que las instancias de Producción y Fase se actualizan a la última versión de AEM sin interrupción del servicio para los usuarios.

>[!NOTE]
> Si falla la actualización al entorno de producción, Cloud Manager invertirá automáticamente el entorno del escenario. Esto se realiza automáticamente para asegurarse de que, una vez finalizada la actualización, tanto los entornos de fase como de producción se encuentren en la misma versión AEM.

AEM actualizaciones de versión son de dos tipos:

* **AEM actualizaciones push**

   * Se puede liberar diariamente.
   * Principalmente mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.

      A medida que los cambios se aplican con regularidad, el impacto es incremental, lo que reduce el impacto en el servicio.

* **Nuevas actualizaciones de funciones**

   * Publicado mediante un programa mensual predecible.

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager es una parte integral del enfoque de actualización continua de AEM como Cloud Service, ya que controla todas las actualizaciones de las instancias. Esto es obligatorio.

Adobe puede activar las actualizaciones cuando hay una nueva versión del servicio en la nube disponible. También puede activar las actualizaciones de la aplicación mediante las canalizaciones proporcionadas por Cloud Manager.

Cloud Manager es:

* se utiliza para gestionar AEM programas y entornos,

* un componente esencial de AEM como Cloud Service; cada nuevo inquilino se aprovisiona primero para el acceso a Cloud Manager,

* el único punto de entrada para su personal de operaciones y desarrollo.

Específicamente, el número y el tipo de programas de AEM que se pueden crear desde el Administrador de nube se derivan de:

* del acuerdo de licencia del cliente,

* de agentes impulsados por el interior cuando se utiliza AEM como Cloud Service para la habilitación o la formación,

* desde procesos impulsados por el exterior, como los ensayos, comenzaron desde Adobe.com.

Cloud Manager ha evolucionado como un portal de autoservicio en el que se pueden crear y configurar los componentes principales de AEM como Cloud Service:

* Creación y administración de nuevos programas. Consulte [Explicación de los Programas y tipos de Programas](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) para obtener más detalles.

* Crear y administrar los entornos de AEM dentro de estos programas. Consulte [Administración de Entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener más detalles.

* Creación y administración de las tuberías para implementar el código del cliente y la configuración relacionada en un entorno específico. Consulte [Configuración de la canalización CI-CD](/help/implementing/cloud-manager/configure-pipeline.md) para obtener más detalles.

* Recibir notificaciones de eventos importantes del ciclo vital para estos componentes (por ejemplo, actualizaciones de productos).

Actualmente, Cloud Manager puede crear entornos en 3 regiones geográficas (con más regiones a continuación):

* EE.UU. (Este)

* EMEA (Países Bajos)

* APAC (Australia)

>[!NOTE]
>Consulte [Acceso a Experience Manager como Cloud Service](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md) para empezar a usar Cloud Manager en AEM como Cloud Service.

## Incorporación {#onboarding}

>[!NOTE]
>
>Para obtener más información, consulte [Inicio](/help/onboarding/home.md).

El inicio y la administración de un proyecto AEM es sencillo cuando el uso de AEM como servicio de nube como Adobe es responsable de muchos aspectos:

* Las imágenes de AEM de línea de base están optimizadas para casos de uso específicos.

* Muchas de las tareas de configuración manual se han vuelto redundantes.

También es significativamente diferente, como ahora lo es:

* Una fase de evaluación para asegurar que se hayan cumplido todos los requisitos previos; incluyendo, por ejemplo:

   * Requisitos legales

   * Acuerdos contractuales

   * Requisitos técnicos para cualquier contenido existente o código personalizado por el cliente

* Requisitos de implementación:

   * Actualizaciones de código; cualquier aplicación para clientes desarrollada para una versión anterior de AEM deberá ser revisada y posiblemente actualizada.

   * Migración de contenido

## Desarrollo de {#developing}

>[!NOTE]
>
>Para obtener más información, puede consultar el inicio con [Development Guidelines](/help/implementing/developing/introduction/development-guidelines.md) y [Developing - The WKND Tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

La nueva arquitectura que admite AEM como Cloud Service implica algunos cambios clave en la experiencia general del desarrollador. Uno de los principales objetivos de AEM como Cloud Service es permitir que los clientes con experiencia (que han utilizado AEM in situ o en el contexto de los servicios gestionados de Adobe) migren a AEM como Cloud Service lo antes posible, sin tener que reescribir la mayor parte de su código personalizado. Sin embargo, es posible que aún sean necesarios algunos ajustes.

### Desarrollo de nube {#aem-as-a-cloud-service-developing-cloud-development}

Para que las aplicaciones AEM existentes se ejecuten en AEM como Cloud Service, se esperan los siguientes pasos:

* El código y la configuración de la aplicación deben almacenarse en el repositorio de código Git del programa de Cloud Manager asociado.
* El código y la configuración de la aplicación deben ser compatibles con la última versión de la imagen de AEM de línea base (que puede estar cambiando diariamente).
   * La aplicación del cliente debe crearse e implementarse mediante la canalización de Cloud Manager asociada al entorno de Cloud Manager.
* La aplicación cliente debe pasar todas las puertas de calidad, seguridad y rendimiento del código que se apliquen en la canalización.
* Las imágenes creadas para la aplicación del cliente deben implementarse mediante la canalización de Cloud Manager.

Este proceso se conoce comúnmente como desarrollo primerizado en la nube. Dado que se espera que la duración de extremo a extremo tome minutos (de 20 a 50 según la complejidad de la aplicación), es necesario adoptar metodologías de desarrollo rápido antes de que se intenten los cambios de código y configuración pendientes en la nube.

La consola web, en la que se administran los paquetes OSGI y su configuración asociada, y que anteriormente formaba parte de AEM QuickStart, ya no es accesible directamente para los usuarios de un AEM como entorno de Cloud Service. Se puede acceder a esta interfaz en modo de solo lectura mediante una nueva consola para desarrolladores. Con esta consola, los desarrolladores pueden seleccionar e iniciar sesión directamente en cualquier nodo concreto de un autor o servicio de publicación y, a continuación, acceder a las áreas bloqueadas de forma predeterminada.

>[!NOTE]
>
>Consulte también [Configuración de OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Otro requisito común para los desarrolladores es el acceso rápido a los archivos de registro de los distintos entornos. Con AEM como Cloud Service, los archivos de registro de los diferentes nodos de los nodos de creación y publicación están disponibles a través del Administrador de nube, ya sea en forma de archivos que se pueden descargar o mediante API.

Debido a la clara separación de código y contenido, los desarrolladores pueden utilizar un proceso particular para actualizar el contenido como parte de una implementación. Los casos de uso típicos del contenido mutable son:

* Contenido *predeterminado* estándar que forma parte del proyecto del cliente (por ejemplo, carpetas, plantillas, flujos de trabajo, etc.)

* Definiciones de índice de búsqueda

* ACL y permisos

* Usuarios de servicios y grupos de usuarios

### Desarrollo local {#aem-as-a-cloud-service-developing-local-development}

A fin de apoyar las iteraciones y el desarrollo rápidos, también es posible desarrollar aplicaciones AEM fuera del AEM como contexto Cloud Service. Con este fin, los desarrolladores pueden acceder a los siguientes artefactos:

* El AEM como Cloud Service QuickStart: un instalador independiente basado en `.jar` de la base de código de AEM más reciente, con la misma superficie funcional y API.

* El AEM como Cloud Service Dispatcher SDK: un proceso basado en imágenes para probar y validar localmente las configuraciones de Dispatcher

>[!NOTE]
>
>Debe tenerse en cuenta que el inicio rápido de la nube no permite todas las funcionalidades de AEM Sites y AEM Assets. Consiste en un simple entorno de autor en el que la mayoría de las extensiones se pueden desarrollar y probar.

## Operaciones y rendimiento {#operations-and-performance}

>[!NOTE]
>
>Para obtener más información, comience con [Copia de seguridad](/help/operations/backup.md), [Indexación](/help/operations/indexing.md) y [Otras tareas de mantenimiento](/help/operations/maintenance.md).

Con AEM como Cloud Service, estas operaciones se automatizan para que ya no sea necesaria la interrupción del servicio.

En estas áreas:

* Se han automatizado muchas tareas.

* Las topologías están optimizadas para lograr la máxima resiliencia y eficiencia; por ejemplo, la replicación sin binarios es la predeterminada.

* Las tareas de gran carga, como colas, trabajos y tareas de procesamiento masivo, se han trasladado de la instancia central de AEM para que se gestionen mediante microservicios compartidos y dedicados.

Las operaciones para AEM como Cloud Service también están respaldadas por una nueva infraestructura de monitoreo, sistema de informes y alerta. Esto permite que los SREs de Adobe (Ingenieros de Fiabilidad del Sitio) mantengan el servicio de forma proactiva y saludable. Los diferentes elementos de la arquitectura están equipados con una gran variedad de controles sanitarios. Si, por alguna razón, un nodo particular de la arquitectura se considera insalubre, entonces se elimina del servicio y se reemplaza silenciosamente por uno nuevo y saludable.

## Administración de identidades {#identity-management}

>[!NOTE]
>
>Para obtener más información, consulte [Seguridad: Soporte de IMS](/help/security/ims-support.md).

Un cambio importante en AEM como Cloud Service es el uso completamente integrado de ID de Adobe para acceder al nivel de autor.

Esto requiere el uso de la [Consola de administración de Adobe](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. Las cuentas de usuario permiten a los usuarios acceder a los productos y servicios de Adobe, ya que la información de perfil de usuario está centralizada en el sistema Identity Management de Adobe (IMS) para compartirse en todos los servicios de nube. Una vez asignado el acceso a AEM, se puede hacer referencia a las cuentas de usuario en AEM como Cloud Service (como antes); por ejemplo, para definir funciones y permisos desde las interfaces de usuario de AEM Security.

Esto combina las ventajas de:

* Uso del sistema Identity Management de Adobe (IMS) para proporcionar el inicio de sesión único en todas las aplicaciones de nube de Adobe.

* Las preferencias del usuario permanecen locales en cada instancia concreta de AEM como Cloud Service.

## Creación de la interfaz de usuario {#authoring-user-interface}

>[!NOTE]
>
>Para obtener más información, la [Administración básica](/help/sites-cloud/authoring/getting-started/basic-handling.md) es un buen punto de partida.

Los principios básicos de la interfaz de usuario (IU) de creación, tanto para Sitios como para Recursos, resultarán muy familiares para cualquiera que haya utilizado AEM en el pasado.

La principal diferencia es que la interfaz de usuario está habilitada exclusivamente para la función táctil; la IU clásica ya no está disponible. De lo contrario, los conceptos básicos permanecen inalterados y sólo se observan pequeños cambios.

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites como Cloud Service le permite ofrecer a sus clientes experiencias personalizadas y basadas en el contenido, combinando la potencia del sistema Gestor de contenido AEM con la administración AEM de activos digitales.

Para obtener más información, consulte la descripción general de [Cambios en sitios](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets como Cloud Service oferta una solución SaaS nativa de la nube para que las empresas no solo realicen sus operaciones de administración de activos digitales y de Dynamic Media con rapidez e impacto, sino que también utilicen las funciones inteligentes de próxima generación, como AI/ML, desde un sistema siempre actual, siempre disponible y siempre en aprendizaje.

La oferta de recursos incluye el procesamiento de recursos de próxima generación en la nube y la búsqueda y la ingesta de recursos de alto rendimiento.

Para obtener más información, consulte [información general e introducción a Assets como Cloud Service](/help/assets/overview.md).

## Cómo conocer Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Para obtener más información, consulte:

* [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* La [arquitectura](/help/core-concepts/architecture.md) de Adobe Experience Manager as a Cloud Service
* [Cambios importantes en AEM as a Cloud Service (Notas de la versión)](/help/release-notes/aem-cloud-changes.md)
* [Cambios importantes en AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Cambios importantes en AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Introducción a AEM Assets como Cloud Service](/help/assets/overview.md)
* [Tutoriales de Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-learn/cloud-service/overview.html)
