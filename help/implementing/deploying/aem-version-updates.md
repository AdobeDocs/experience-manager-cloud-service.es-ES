---
title: Actualizaciones de la versión de AEM
description: Actualizaciones de la versión de AEM
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: becc07c0042cdfb5de86dc8895801c00c882f8a1
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 4%

---


# Actualizaciones de la versión de AEM {#aem-version-updates}

## Introducción {#introduction}

AEM as a Cloud Service ahora utiliza la integración continua y el envío continuo (CI/CD) para garantizar que sus proyectos se encuentren en la versión de AEM más actual. Esto significa que las instancias de producción y de ensayo se actualizan a la última versión de AEM sin interrupciones del servicio para los usuarios.

>[!NOTE]
>
>Si la actualización al entorno de producción falla, Cloud Manager restaurará automáticamente el entorno de ensayo. Esto se hace automáticamente para asegurarse de que, después de que se complete una actualización, tanto los entornos de ensayo como de producción estén en la misma versión AEM.

Existen dos tipos de actualizaciones de AEM versión:

* **Actualizaciones de mantenimiento de AEM**

   * Se puede publicar diariamente.
   * Se utilizan principalmente para fines de mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.
   * Tienen un impacto mínimo, ya que los cambios se aplican con regularidad.

* **Nuevas actualizaciones de funciones**

   * Se publican mediante un calendario mensual predecible.

AEM actualizaciones pasan por un proceso de validación de productos intenso y totalmente automatizado, que incluye varios pasos, lo que garantiza que no se interrumpa el servicio de ningún sistema en producción. Los controles sanitarios se utilizan para controlar el estado de la aplicación. Si estas comprobaciones fallan durante una actualización as a Cloud Service AEM, la versión no se realizará y el Adobe investigará por qué la actualización provocó este comportamiento inesperado.

[Pruebas de producto y pruebas funcionales del cliente,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) que impiden que las actualizaciones de productos y los impulsos de código de cliente rompan los sistemas de producción, también se validan durante una actualización de versión de AEM.

>[!NOTE]
>
>Si el código personalizado se insertó en el entorno de ensayo y no en la producción, la siguiente actualización de AEM eliminará esos cambios para reflejar la etiqueta git de la última versión correcta del cliente en la producción. Por lo tanto, el código personalizado que solo estaba disponible en el entorno de ensayo tendrá que volver a implementarse.

## Almacenamiento de nodos compuestos {#composite-node-store}

Las actualizaciones en la mayoría de los casos no tendrán tiempo de inactividad, incluido para la instancia de creación, que es un clúster de nodos. Las actualizaciones móviles son posibles debido a la función de almacén de nodos compuestos en Oak.

Esta función permite AEM varios repositorios simultáneamente. En una implementación móvil, la nueva versión verde AEM contiene su propia versión `/libs` (el repositorio inmutable basado en TarMK), distinto de la versión azul AEM anterior, aunque ambos hacen referencia a un repositorio mutable compartido basado en DocumentMK que contiene áreas como `/content` , `/conf` , `/etc` y otros. Porque tanto el azul como el verde tienen sus propias versiones de `/libs`, ambos pueden estar activos durante la actualización móvil, lo que hace que el tráfico pase hasta que el azul se sustituya por el verde.
