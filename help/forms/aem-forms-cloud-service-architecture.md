---
title: Experience Manager [!DNL AEM Forms] Arquitectura as a Cloud Service
description: Comprender la arquitectura de [!DNL AEM Forms] as a Cloud Service para conocer los aspectos de escalabilidad, resiliencia y rendimiento de la plataforma.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 6%

---


# [!DNL AEM] arquitectura as a Cloud Service {#architecture}

[!DNL AEM Forms] as a Cloud Service estandariza la arquitectura de implementación para todos los clientes, con el objetivo de liberar completamente a los clientes de las consideraciones arquitectónicas. Por ejemplo, mientras que la nueva arquitectura as a Cloud Service AEM sigue basándose en el concepto de micro-núcleos para la persistencia, los clientes no necesitan preocuparse acerca del micronúcleo del que elegir. Los microkernels utilizados en el autor y en el lado de publicación son exclusivos de [!DNL AEM Cloud Service] y, de lo contrario, no están disponibles para los clientes para instalaciones locales.

AEM as a Cloud Service tiene una arquitectura dinámica con un número variable de instancias de AEM. Proporciona entornos de desarrollo, fase, producción y demostración. Proporciona herramientas para administrar instancias de AEM (Cloud Manager), mantener usuarios y autenticaciones (sistema Admin Console e IMS (administración de identidades de Adobe)), configurar el almacenamiento en caché (CDN de FIENTE) y el entorno de desarrollo nativo de la nube. Para obtener más información sobre la arquitectura, consulte [Introducción a la arquitectura de [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=en).

## Cloud Manager{#cloud-manager}

Cloud Manager es un componente esencial para [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Cada nuevo inquilino de la variable [!DNL AEM Forms] as a Cloud Service se aprovisiona primero para el acceso a Cloud Manager. Cloud Manager es el punto de entrada único para las operaciones y el desarrollador de nuestros clientes. Es el lugar desde donde se pueden administrar los programas y entornos AEM. Cloud Manager ha evolucionado como un portal de autoservicio en el que se pueden crear y configurar los componentes principales del AEM as a Cloud Service:

* Creación y administración de programas
* Creación y administración de los entornos AEM dentro de los programas
* Creación y administración de canalizaciones para implementar el código del cliente y la configuración en un entorno en particular
* Obtención de notificaciones de eventos de ciclo vital importantes para estos componentes (p. ej., actualizaciones de productos) Para obtener más información sobre Cloud Manager, consulte [Comprender Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) y [Introducción a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es).

## Usuarios y autenticación {#users-and-authentication}

AEM as a Cloud Service incluye compatibilidad con Admin Console para instancias AEM y autenticación basada en el sistema Identity Management de Adobe (IMS). Admin Console permite a los administradores gestionar de forma centralizada todos los usuarios de Experience Cloud. Los usuarios y grupos pueden asignarse a perfiles de producto asociados a instancias de AEM as a Cloud Service, lo que les permite iniciar sesión en esa instancia. Para obtener más información sobre los usuarios, la autenticación y, y el acceso a una instancia de AEM as a Cloud Service, consulte [Compatibilidad con IMS para [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Varias personas participan en una [!DNL AEM Forms] proyecto. Después de iniciar sesión en su [!DNL AEM Forms] instancia as a Cloud Service, puede [agregar usuarios en admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=es) para personas aplicables a su organización o proyecto y [asignar usuarios a grupos integrados](forms-groups-privileges-tasks.md) para proporcionarles los privilegios necesarios.

Para aprender a utilizar los distintos elementos integrados [!DNL AEM Forms] grupos de usuarios específicos y privilegios disponibles en [!DNL AEM Forms] como instancia de Cloud Services, consulte [Configuración, usuario, funciones y grupos](forms-groups-privileges-tasks.md).

## Experiencia del desarrollador {#developer-experience}

La nueva arquitectura que admite AEM as a Cloud Service aporta algunos cambios clave a la experiencia general del desarrollador. Uno de los objetivos principales de los cambios en la experiencia del desarrollador es permitir que la migración a AEM as a Cloud Service lo antes posible, con pocas modificaciones en el código personalizado existente.

## Desarrollo en la nube {#cloud-development}

Estas son las directrices para ejecutar el código existente sin problemas en AEM entorno as a Cloud Service:

* Almacene el código y las configuraciones en el repositorio Git del programa Cloud Manager asociado. Hace que la gestión e integración del código con CI/CD sea una brisa.
* Hacer que el código y la configuración de la aplicación sean compatibles con la línea base [!DNL AEM Forms] imágenes. El uso de las API más recientes ayuda a crear aplicaciones más rápidas y seguras.
* Utilice la canalización de Cloud Manager asociada al entorno de Cloud Manager para crear e implementar aplicaciones. Le ayuda a traer las últimas funciones y a corregir el error de [!DNL AEM Forms] as a Cloud Service para su entorno.
* Pruebe que sus aplicaciones personalizadas pasen todas las puertas de calidad, seguridad y rendimiento del código impuestas en la canalización. Ayuda a crear aplicaciones seguras y de mejor rendimiento, lo que mejora la experiencia del cliente. Siempre puede utilizar la interfaz de usuario de Cloud Manager para omitir algunas comprobaciones.
Este proceso se conoce comúnmente como desarrollo en la nube. [!DNL AEM Forms] as a Cloud Service también proporciona un SDK para admitir un desarrollo rápido antes de que se intenten en la nube los cambios de código y configuración pendientes.
Algunas interfaces que anteriormente formaban parte de AEM QuickStart ya no están disponibles para los usuarios del entorno as a Cloud Service AEM. Por ejemplo, la consola web donde se administran los paquetes OSGI y su configuración asociada. El navegador del repositorio de contenido del CRXDE Lite solo es accesible en los tipos de entorno que no sean de producción. Un subconjunto de las funcionalidades de la consola web que los desarrolladores necesitan, especialmente en lo que respecta a diagnósticos y estados, está disponible a través de una nueva consola para desarrolladores.
Además, uno de los requisitos más comunes para los desarrolladores es el acceso rápido a los archivos de registro de los distintos entornos. con [!DNL AEM Cloud Service], los archivos de registro de los diferentes nodos del Autor, Publish están disponibles a través de Cloud Manager, ya sea en forma de archivos que se pueden descargar o a través de API para adaptar los registros. Debido a la clara separación de código y contenido, los desarrolladores pueden aprovechar un proceso particular para actualizar contenido como parte de una implementación. Los casos de uso habituales del contenido mutable son:
* Contenido &quot;predeterminado&quot; estándar que forma parte del proyecto del cliente (p. ej., carpetas, plantillas, flujos de trabajo...)
* Definiciones de índices de búsqueda
* ACL y permisos
* Usuarios y grupos de usuarios de servicios
Configure su entorno de desarrollo. [Configurar la canalización de CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)y aprenda a [implementar el código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) en el entorno.

## Desarrollo local {#local-development}

Al configurar y configurar un [!DNL AEM Forms] entorno as a Cloud Service, puede configurar entornos de desarrollo, ensayo y producción. Además, configure un entorno de desarrollo local para realizar iteraciones y procesos de desarrollo rápidos. Puede descargar y configurar AEM SDK y [!DNL AEM Forms] archivo de funciones de complemento para configurar un [!DNL Forms] Entorno de desarrollo as a Cloud Service.  Para obtener instrucciones detalladas, consulte [Configuración de un entorno de desarrollo local](setup-local-development-environment.md).

## Depuración {#debugging}

AEM se ejecuta en infraestructura de nube con capacidad de autoservicio, escalable y de autoservicio. Requiere que los desarrolladores de AEM entiendan y depuren varias facetas de AEM as a Cloud Service, desde la compilación y la implementación hasta la obtención de detalles de la ejecución de aplicaciones de AEM. Para obtener información detallada, consulte [Depuración AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en).
