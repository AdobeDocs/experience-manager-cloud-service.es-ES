---
title: Actualizaciones en la versión AEM
description: 'Actualizaciones en la versión AEM '
feature: Implementación
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Actualizaciones de la versión de AEM {#aem-version-updates}

## Introducción {#introduction}

AEM como Cloud Service ahora utiliza la integración continua y la entrega continua (CI/CD) para garantizar que sus proyectos se encuentren en la versión de AEM más actual. Esto significa que las instancias Producción y Fase se actualizan a la última versión de AEM sin interrupciones del servicio para los usuarios.

>[!NOTE]
>Si la actualización al entorno de producción falla, Cloud Manager invertirá automáticamente el entorno de ensayo. Esto se realiza automáticamente para garantizar que, después de completarse una actualización, tanto los entornos de fase como de producción estén en la misma versión AEM.

AEM actualizaciones de versión son de dos tipos:

* **AEM actualizaciones push**

   * Se puede publicar diariamente.

   * Principalmente mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.

      Como los cambios se aplican regularmente, el impacto es incremental, lo que reduce el impacto en su servicio.

* **Nuevas actualizaciones de funciones**

   * Publicado mediante un calendario mensual predecible.

AEM actualizaciones pasan por un proceso de validación de productos intensivo y totalmente automatizado, que incluye varios pasos que garantizan que no se interrumpa el servicio para ningún sistema en producción. Los controles sanitarios se utilizan para controlar el estado de la aplicación. Si estas comprobaciones fallan durante una AEM como actualización de Cloud Service, la versión no se ejecuta y el Adobe investigará por qué la actualización provocó este comportamiento inesperado.

[Las pruebas de producto y las ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) pruebas funcionales de cliente que impiden que las actualizaciones de productos y los impulsos de código de cliente rompan la producción también se validan durante una actualización de versión de AEM.

>[!NOTE]
>
>Si el código personalizado se insertó en el entorno de ensayo y luego fue rechazado por usted, la siguiente actualización de AEM eliminará esos cambios para reflejar la etiqueta de git de la última versión de cliente en producción que se realizó correctamente.

## Almacenamiento de nodos compuestos {#composite-node-store}

Como se ha mencionado anteriormente, las actualizaciones en la mayoría de los casos no tendrán tiempo de inactividad, incluso para el autor, que es un clúster de nodos. Las actualizaciones móviles son posibles debido a la función *del almacén de nodos compuestos* en Oak.

Esta función permite AEM varios repositorios simultáneamente. En una implementación móvil, la nueva versión de Green AEM contiene su propio `/libs` (el repositorio inmutable basado en TarMK), distinto de la versión anterior de Blue AEM, aunque ambos hacen referencia a un repositorio mutable compartido basado en DocumentMK que contiene áreas como `/content` , `/conf` , `/etc` y otras. Dado que tanto el Azul como el Verde tienen sus propias versiones de `/libs`, ambos pueden estar activos durante la actualización móvil, lo que hace que el tráfico entre en vigor hasta que el azul se reemplace completamente por el verde.
