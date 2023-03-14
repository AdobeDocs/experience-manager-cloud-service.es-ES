---
title: Actualizaciones de la versión de AEM
description: Actualizaciones de la versión de AEM
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: f977c6d8fa3ebd4b082e48da8b248178f9a2f34b
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 30%

---


# Actualizaciones de la versión de AEM {#aem-version-updates}

## Introducción {#introduction}

AEM as a Cloud Service ahora utiliza la integración y la entrega continua (CI/CD) para garantizar que sus proyectos se encuentren en la versión de AEM más actual. AEM Esto significa que las instancias de producción y ensayo se actualizan a la última versión de la aplicación sin interrupciones del servicio para los usuarios de.

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

AEM Las actualizaciones de los productos pasan por un proceso de validación de productos intenso y totalmente automatizado que incluye varios pasos, lo que garantiza que no se interrumpa el servicio de ningún sistema en producción. Las comprobaciones de estado se utilizan para supervisar el estado de la aplicación. AEM Si estas comprobaciones fallan durante una actualización as a Cloud Service del estado, la versión no continúa y el Adobe investigará por qué la actualización ha provocado este comportamiento inesperado.

[Pruebas de productos y pruebas funcionales de clientes,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) AEM que evitan que las actualizaciones de productos y las inserciones de código de cliente rompan los sistemas de producción, también se validan durante una actualización de versión de la.

>[!NOTE]
>
>AEM Si el código personalizado se insertó en el ensayo y no en la producción, la siguiente actualización de la eliminará esos cambios para reflejar la etiqueta de Git de la última versión correcta del cliente en producción. Por lo tanto, el código personalizado que solo estaba disponible en el ensayo deberá implementarse de nuevo.

## Almacén de nodos compuestos {#composite-node-store}

Las actualizaciones en la mayoría de los casos no implican ningún tiempo de inactividad, incluida la instancia de creación, que es un clúster de nodos. Las actualizaciones móviles son posibles debido a la función de almacén de nodos compuestos en Oak.

AEM Esta función permite a los usuarios hacer referencia a varios repositorios de forma simultánea. AEM En una implementación móvil, la nueva versión de la aplicación en color verde contiene la suya propia `/libs` AEM (el repositorio inmutable basado en TarMK), distinto de la versión anterior de la versión azul de la, aunque ambos hacen referencia a un repositorio mutable basado en DocumentMK compartido que contiene áreas como `/content` , `/conf` , `/etc` y otros. Porque tanto el azul como el verde tienen sus propias versiones de `/libs`, ambos pueden estar activos durante la actualización móvil, y activar el tráfico hasta que el azul se sustituya completamente por el verde.
