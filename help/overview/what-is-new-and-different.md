---
title: 'Novedades y diferencias: Adobe Experience Manager as a Cloud Service'
description: 'Novedades y diferencias: Adobe Experience Manager (AEM) as a Cloud Service.'
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 97%

---

# Novedades y diferencias {#what-is-new-and-what-is-different}

Durante muchos años AEM ha estado disponible tanto:

* Local

* as a Managed Service

Hay diferencias intrínsecas entre estos enfoques anteriores y AEM as a Cloud Service:

* [Arquitectura](#architecture)
* [Actualizaciones](#upgrades)
* [Cloud Manager](#cloud-manager)
* [Incorporación](#onboarding)
* [Desarrollo de](#developing)
* [Operaciones y rendimiento](#operations-and-performance)
* [Administración de identidades](#identity-management)
* [Interfaz de usuario de creación](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>Estas descripciones generales no son exhaustivas, pero tienen por objeto proporcionar una introducción.

>[!NOTE]
>
>Para obtener más información sobre las versiones On-Premise y Managed Service, consulte el conjunto de documentación para [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es).

## Arquitectura {#architecture}

>[!NOTE]
>
>Para obtener más información, consulte [Arquitectura](/help/overview/architecture.md).

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

AEM as a Cloud Service ahora utiliza la integración y la entrega continua (CI/CD) para garantizar que sus proyectos se encuentren en la versión de AEM más actual. Esto significa que las instancias de producción y de ensayo se actualizan a la última versión de AEM sin interrupciones del servicio para los usuarios.

>[!NOTE]
>
>Si la actualización al entorno de producción falla, Cloud Manager restablecerá automáticamente el entorno de ensayo. Esto se realiza automáticamente para garantizar que, después de completarse una actualización, tanto los entornos de ensayo como de producción estén en la misma versión de AEM.

Existen dos tipos de actualizaciones versión de AEM:

* **Actualizaciones de mantenimiento de AEM**

   * Se pueden publicar diariamente.
   * Se utilizan principalmente para fines de mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.
   * Tienen un impacto mínimo, ya que los cambios se aplican con regularidad.

* **Nuevas actualizaciones de funciones**

   * Publicadas mediante una programación mensual predecible.

>[!TIP]
>
>Para obtener más información, consulte [Actualizaciones de la versión de AEM](/help/implementing/deploying/aem-version-updates.md).

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager es una parte integral del enfoque de actualización continua de AEM as a Cloud Service, ya que controla todas las actualizaciones de las instancias. Esto es obligatorio.

Las actualizaciones se pueden activar mediante Adobe cuando hay una nueva versión del servicio en la nube disponible. Como alternativa, puede activar las actualizaciones de la aplicación mediante las canalizaciones que Cloud Manager proporciona.

Cloud Manager:

* se utiliza para administrar programas y entornos de AEM,

* es un componente esencial de AEM as a Cloud Service; cada nuevo inquilino se aprovisiona primero para el acceso a Cloud Manager,

* es el punto de entrada único para su personal de operaciones y desarrollo.

En concreto, el número y el tipo de programas de AEM que se pueden crear desde Cloud Manager se derivan:

* del contrato de licencia de cliente,

* de agentes internos cuando AEM as a Cloud Service se utiliza para la habilitación o el aprendizaje,

* a partir de procesos impulsados por externos como ensayos iniciados desde Adobe.com.

Cloud Manager ha evolucionado como un portal de autoservicio donde se pueden crear y configurar los componentes principales de AEM as a Cloud Service:

* Creación y administración de nuevos programas. Consulte [Explicación de programas y tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para obtener más información.

* Creación y administración de entornos de AEM dentro de estos programas. Consulte [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener más información.

* Creación y administración de canalizaciones para implementar el código de cliente y la configuración relacionada en un entorno específico. Consulte [Configuración de la canalización de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información.

* Recepción de notificaciones de eventos de ciclo vital importantes para estos componentes (por ejemplo, actualizaciones de productos).

Cloud Manager crea entornos en centros de datos de muchas regiones geográficas, lo que proporciona una cobertura global. Los puntos de presencia (PoPs) de la red de distribución de contenido (CDN) garantizan una entrega de contenido con baja latencia para clientes ubicados en todo el mundo.


## Incorporación {#onboarding}

El inicio y la administración de un proyecto de AEM es sencillo al usar AEM as a Cloud Service, ya que Adobe es responsable de muchos aspectos:

* Las imágenes de AEM de línea de base están optimizadas para casos de uso específicos.

* Muchas de las tareas de configuración manual se han vuelto redundantes.

También es significativamente diferente, ya que ahora hay:

* Una fase de evaluación para garantizar que se hayan cumplido todos los requisitos previos; entre ellos, por ejemplo:

   * Requisitos legales

   * Acuerdos contractuales

   * Requisitos técnicos para cualquier contenido existente o código personalizado por el cliente

* Requisitos de implementación:

   * Actualizaciones de código; cualquier aplicación de cliente desarrollada para una versión anterior de AEM deberá revisarse y posiblemente actualizarse.

   * Migración de contenido

>[!TIP]
>
>Para obtener una descripción general completa del proceso de incorporación, consulte el [recorrido de incorporación.](/help/journey-onboarding/overview.md)

## Desarrollo de {#developing}

>[!NOTE]
>
>Para obtener más información, comience con [Directrices de desarrollo](/help/implementing/developing/introduction/development-guidelines.md) y [Desarrollo: tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

La nueva arquitectura que admite AEM as a Cloud Service implica algunos cambios clave en la experiencia general del desarrollador. Uno de los principales objetivos de AEM as a Cloud Service es permitir que los clientes con experiencia (que han utilizado AEM local o en el contexto de Adobe Managed Services) migren a AEM as a Cloud Service lo antes posible, sin tener que reescribir la mayor parte de su código personalizado. Sin embargo, es posible que todavía se necesiten algunos ajustes.

### Desarrollo en la nube {#aem-as-a-cloud-service-developing-cloud-development}

Para que las aplicaciones de AEM existentes se ejecuten en AEM as a Cloud Service, se esperan los siguientes pasos:

* El código y la configuración de la aplicación deben almacenarse en el repositorio de código Git del programa Cloud Manager asociado.
* El código y la configuración de la aplicación deben ser compatibles con la última versión de la imagen de AEM de línea de base (que puede estar cambiando diariamente).
   * La aplicación del cliente debe crearse e implementarse mediante la canalización de Cloud Manager asociada al entorno de Cloud Manager.
* La aplicación del cliente debe pasar todas las puertas de calidad, seguridad y rendimiento del código que se aplican en la canalización.
* Las imágenes creadas para la aplicación del cliente deben implementarse mediante la canalización de Cloud Manager.

Este proceso se conoce comúnmente como desarrollo con prioridad en la nube. Dado que se espera que la duración de extremo a extremo tarde unos cuantos minutos (de 20 a 50 según la complejidad de la aplicación), es necesario adoptar metodologías de desarrollo rápido antes de que se intenten en la nube los cambios de código y configuración pendientes.

La consola web, en la que se administran los paquetes OSGi y su configuración asociada, y que anteriormente formaba parte de QuickStart de AEM, ya no está disponible en AEM as a Cloud Service. La nueva consola para desarrolladores proporciona una interfaz de solo lectura para la mayoría de la información de tiempo de ejecución. Con esta consola, los desarrolladores pueden seleccionar e iniciar sesión directamente en cualquier nodo concreto de un autor o servicio de publicación y ver la información relevante.

>[!NOTE]
>
>Consulte también [Configuración de OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Otro requisito común para los desarrolladores es el acceso rápido a los archivos de registro de los distintos entornos. Con AEM as a Cloud Service, los archivos de registro de los diferentes nodos de los nodos de creación y publicación están disponibles mediante Cloud Manager, ya sea en forma de archivos que se pueden descargar o a través de API.

Debido a la clara separación de código y contenido, los desarrolladores pueden utilizar un proceso particular para actualizar contenido como parte de una implementación. Los casos de uso habituales del contenido mutable son:

* Contenido estándar *predeterminado* que forma parte del proyecto del cliente (por ejemplo, carpetas, plantillas, flujos de trabajo, etc.)

* Definiciones de índices de búsqueda

* ACL y permisos

* Usuarios y grupos de usuarios de servicios

### Desarrollo local {#aem-as-a-cloud-service-developing-local-development}

AEM AEM Para apoyar las iteraciones y el desarrollo rápidos, también es posible desarrollar aplicaciones de la fuera del contexto as a Cloud Service. Con este fin, se ponen a disposición de los desarrolladores los siguientes artefactos:

* Quickstart de AEM as a Cloud Service: un instalador independiente basado en `.jar` de la última base de código de AEM, con la misma superficie funcional y API.

* El SDK de Dispatcher de AEM as a Cloud Service: un proceso basado en imágenes para probar y validar configuraciones de Dispatcher localmente

>[!NOTE]
>
>Debe tenerse en cuenta que Quickstart de la nube no permite todas las funcionalidades de AEM Sites y AEM Assets. Consiste en un entorno de creación sencillo en el que la mayoría de las extensiones se pueden desarrollar y probar.

## Operaciones y rendimiento {#operations-and-performance}

>[!NOTE]
>
>Para obtener más información, comience con [Copia de seguridad](/help/operations/backup.md), [Indexación](/help/operations/indexing.md) y [Otras tareas de mantenimiento](/help/operations/maintenance.md).

Con AEM as a Cloud Service, esas operaciones se automatizan para que ya no sea necesaria ninguna interrupción del servicio.

En estas áreas:

* Se han automatizado muchas tareas.

* Las topologías están optimizadas para lograr la máxima resiliencia y eficiencia; por ejemplo, la replicación binaria es la predeterminada.

* Las tareas de carga pesada, como colas, trabajos y tareas de procesamiento masivo, se han movido fuera de la instancia de AEM principal para que se gestionen mediante microservicios compartidos y dedicados.

Las operaciones para AEM as a Cloud Service también están apoyadas por una nueva infraestructura de monitorización, creación de informes y alertas. Esto permite que los SRE (ingenieros de confiabilidad del sitio) de Adobe mantengan el servicio de forma proactiva en buen estado. Los diferentes elementos de la arquitectura están equipados con una variedad de controles de estado. Si, por alguna razón, un nodo particular de la arquitectura se considera no saludable, entonces se elimina del servicio y se reemplaza silenciosamente por uno nuevo y en perfectas condiciones.

## Administración de identidades {#identity-management}

>[!NOTE]
>
>Para obtener más información, consulte [Seguridad: compatibilidad con IMS](/help/security/ims-support.md).

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de los Adobe ID para acceder al nivel de creación.

Esto requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. Las cuentas de usuario permiten a los usuarios acceder a los productos y servicios de Adobe, ya que la información de perfil de usuario está centralizada en el Identity Management System (IMS) de Adobe para compartirse en todos los servicios de nube. Una vez asignado el acceso a AEM, se puede hacer referencia a las cuentas de usuario en AEM as a Cloud Service (como antes); por ejemplo, para definir funciones y permisos desde las interfaces de usuario de seguridad de AEM.

Esto combina las ventajas de:

* Usar el Identity Management System (IMS) de Adobe para proporcionar un inicio de sesión único en todas las aplicaciones de la nube de Adobe.

* El hecho de que las preferencias de usuario permanezcan locales en cada instancia concreta de AEM as a Cloud Service.

## Interfaz de usuario de creación {#authoring-user-interface}

>[!NOTE]
>
>Para obtener más información, la [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md) es un buen punto de partida.

AEM Los principios básicos de la interfaz de usuario (IU) de creación, tanto para Sites como para Assets, resultarán muy familiares para cualquiera que haya utilizado la interfaz de usuario (IU) en el pasado.

La principal diferencia es que la IU solo es táctil; la IU clásica ya no está disponible. Por lo demás, los conceptos básicos permanecen inalterados, con solo pequeños cambios aparentes.

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service le permite ofrecer a sus clientes experiencias personalizadas basadas en contenido, combinando la potencia del sistema de administración de contenido de AEM con la administración de activos digitales de AEM.

Para obtener más información, consulte la descripción general de [Cambios en Sites](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service ofrece una solución PaaS nativa de la nube para que las empresas no solo realicen sus operaciones de administración de activos digitales y medios dinámicos con rapidez e impacto, sino que también utilicen funciones inteligentes de próxima generación, como IA y aprendizaje automático, desde un sistema que siempre esté actualizado, disponible y aprendiendo.

La oferta de Assets incluye el procesamiento de recursos de próxima generación en la nube y la ingesta y búsqueda de recursos de alto rendimiento.

Para obtener más información, consulte [información general e introducción a Assets as a Cloud Service](/help/assets/overview.md).

## Cómo conocer Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Para obtener más información, consulte:

* [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* La [arquitectura](/help/overview/architecture.md) de Adobe Experience Manager as a Cloud Service
* [Cambios importantes en AEM as a Cloud Service (Notas de la versión)](/help/release-notes/aem-cloud-changes.md)
* [Cambios importantes en AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Cambios importantes en AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Presentación de AEM Assets as a Cloud Service](/help/assets/overview.md)
* [Tutoriales de Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=es)

>[!TIP]
>
>Una vez que tenga una visión general de AEM as a Cloud Service, podrá incorporarse rápidamente revisando el [Recorrido de incorporación](/help/journey-onboarding/overview.md).
>
>¿Ya incorporado o listo para sumergirse en las funciones de AEM de prueba? Instale el [complemento de demostraciones de referencia de AEM](/help/journey-sites/demos-add-on/overview.md) para explorar las potentes funciones de AEM con interesantes ejemplos.
