---
title: Actualizaciones de la versión de AEM
description: AEM Descubra cómo utiliza la integración y el envío continuos (CI/CD) para mantener sus proyectos en la versión más reciente de los que utiliza as a Cloud Service.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 23%

---


# Actualizaciones de la versión de AEM {#aem-version-updates}

AEM Descubra cómo utiliza la integración y el envío continuos (CI/CD) para mantener sus proyectos en la versión más reciente de los que utiliza as a Cloud Service.

## CI/CD {#ci-cd}

AEM as a Cloud Service AEM utiliza la integración y la entrega continuas (CI/CD) para garantizar que sus proyectos se encuentren en la versión de la aplicación más actual de la. Esto significa que las instancias de producción y de ensayo se actualizan a la última versión de AEM sin interrupciones del servicio para los usuarios.

Las actualizaciones de versión se aplican automáticamente solo a las instancias de producción y ensayo. [AEM Las actualizaciones de la versión se deben aplicar manualmente a todas las demás instancias](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).

## Tipo de actualizaciones {#update-types}

Existen dos tipos de actualizaciones versión de AEM:

* **Actualizaciones de mantenimiento de AEM**

   * Se pueden publicar diariamente.
   * Se utilizan principalmente para fines de mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.
   * Tienen un impacto mínimo, ya que los cambios se aplican con regularidad.

* **Nuevas actualizaciones de funciones**

   * Se lanzan el [un horario mensual predecible.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es)

## Error de actualización {#update-failure}

AEM Las actualizaciones de los productos pasan por un proceso de validación de productos intenso y totalmente automatizado que incluye varios pasos, lo que garantiza que no se interrumpa el servicio de ningún sistema en producción. Las comprobaciones de estado se utilizan para supervisar el estado de la aplicación. AEM Si estas comprobaciones fallan durante una actualización as a Cloud Service del estado, la versión no continúa y el Adobe investigará por qué la actualización ha provocado este comportamiento inesperado.

[Pruebas de productos y pruebas funcionales de clientes,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) AEM que evitan que las actualizaciones de productos y las inserciones de código de cliente rompan los sistemas de producción, también se validan durante una actualización de versión de la.

Si la actualización al entorno de producción falla, Cloud Manager restablecerá automáticamente el entorno de ensayo. Esto se realiza automáticamente para garantizar que, después de completarse una actualización, tanto los entornos de ensayo como de producción estén en la misma versión de AEM.

>[!NOTE]
>
>AEM Si el código personalizado se insertó en el ensayo y no en la producción, la siguiente actualización de la eliminará esos cambios para reflejar la etiqueta de Git de la última versión correcta del cliente en producción. Por lo tanto, el código personalizado que solo estaba disponible en el ensayo deberá implementarse de nuevo.

## Almacén de nodos compuestos {#composite-node-store}

En la mayoría de los casos, las actualizaciones no implican ningún tiempo de inactividad, incluida la instancia de creación, que es un clúster de nodos. Las actualizaciones móviles son posibles debido a [la función de almacén de nodos compuestos en Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

AEM Esta función permite a los usuarios hacer referencia a varios repositorios de forma simultánea. En un [implementación móvil,](/help/implementing/deploying/overview.md#how-rolling-deployments-work) AEM la nueva versión de la contiene su propio `/libs` AEM (el repositorio inmutable basado en TarMK), distinto de la versión más antigua, aunque ambos hacen referencia a un repositorio mutable basado en DocumentMK compartido que contiene áreas como `/content` , `/conf` , `/etc` y otros.

Porque tanto la versión antigua como la nueva tienen sus propias versiones de `/libs`Sin embargo, ambos pueden estar activos durante la actualización móvil y pueden asumir el tráfico hasta que el antiguo se sustituya completamente por el nuevo.
