---
title: Actualizaciones de la versión de AEM
description: 'Actualizaciones de la versión de AEM '
translation-type: tm+mt
source-git-commit: 78c0802a0703e81941013347a3f4b57cb106c927
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Actualizaciones de la versión de AEM {#aem-version-updates}

## Introducción {#introduction}

AEM como Cloud Service ahora utiliza la integración continua y el Envío continuo (CI/CD) para garantizar que los proyectos se encuentren en la versión AEM más actual. Esto significa que las instancias de Producción y Fase se actualizan a la última versión de AEM sin interrupción del servicio para los usuarios.

>[!NOTE]
>Si falla la actualización al entorno de producción, Cloud Manager invertirá automáticamente el entorno del escenario. Esto se realiza automáticamente para asegurarse de que, una vez finalizada la actualización, tanto los entornos de fase como de producción se encuentren en la misma versión AEM.

AEM actualizaciones de versión son de dos tipos:

* **AEM actualizaciones push**

   * Se puede liberar diariamente.

   * Principalmente mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.

      A medida que los cambios se aplican con regularidad, el impacto es incremental, lo que reduce el impacto en el servicio.

* **Nuevas actualizaciones de funciones**

   * Publicado mediante un programa mensual predecible.

AEM actualizaciones pasan por un proceso de validación de productos intensivo y completamente automatizado, que implica varios pasos para garantizar que no se interrumpa el servicio para ningún sistema en producción. Los controles de estado se utilizan para supervisar el estado de la aplicación. Si estas comprobaciones fallan durante una AEM como actualización de Cloud Service, la versión no continuará y Adobe investigará por qué la actualización provocó este comportamiento inesperado.

[Las pruebas del producto y ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) las pruebas funcionales del cliente que impiden que las actualizaciones del producto y los impulsos del código del cliente rompan la producción también se validan durante una actualización de la versión de AEM.

>[!NOTE]
>
>Si el código personalizado se insertó en el entorno de ensayo y luego fue rechazado por usted, la siguiente actualización de AEM eliminará esos cambios para reflejar la etiqueta git de la última versión correcta del cliente a producción.

## Almacenamiento de nodos compuestos {#composite-node-store}

Como se mencionó anteriormente, las actualizaciones en la mayoría de los casos no producirán ningún tiempo de inactividad, incluso para el autor, que es un clúster de nodos. Las actualizaciones móviles son posibles debido a la función *almacén de nodos compuestos* en Oak.

Esta función permite AEM varios repositorios a la vez. En una implementación móvil, la nueva versión de Green AEM contiene su propio `/libs` (repositorio inmutable basado en TarMK), distinto de la versión anterior de Blue AEM, aunque ambos hacen referencia a un repositorio mutable basado en DocumentMK compartido que contiene áreas como `/content` , `/conf` , `/etc` y otras. Dado que tanto el Azul como el Verde tienen sus propias versiones de `/libs`, ambos pueden estar activos durante la actualización móvil, lo que provoca tráfico hasta que el azul se reemplaza por el verde.

