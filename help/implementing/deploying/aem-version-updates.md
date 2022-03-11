---
title: Actualizaciones de la versión de AEM
description: 'Actualizaciones de la versión de AEM '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 36%

---

# Actualizaciones de la versión de AEM {#aem-version-updates}

## Introducción {#introduction}

AEM as a Cloud Service ahora utiliza la integración continua y la entrega continua (CI/CD) para garantizar que sus proyectos se encuentren en la versión de AEM más actual. Esto significa que las instancias Producción y Ensayo se actualizan a la última versión de AEM sin interrupciones del servicio para los usuarios.

>[!NOTE]
>Si la actualización al entorno de producción falla, Cloud Manager invertirá automáticamente el entorno de ensayo. Esto se realiza automáticamente para garantizar que, después de completarse una actualización, tanto los entornos de ensayo como de producción estén en la misma versión de AEM.

Las actualizaciones de versión de AEM son de dos tipos:

* **Actualizaciones de AEM push**

   * Se puede publicar diariamente.

   * Principalmente, son de mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.

      Como los cambios se aplican regularmente, el impacto es incremental, lo que reduce el impacto en su servicio.

* **Nuevas actualizaciones de funciones**

   * Publicadas mediante un calendario mensual predecible.

AEM actualizaciones pasan por un proceso de validación de productos intensivo y totalmente automatizado, que incluye varios pasos que garantizan que no se interrumpa el servicio para ningún sistema en producción. Los controles sanitarios se utilizan para controlar el estado de la aplicación. Si estas comprobaciones fallan durante una actualización as a Cloud Service AEM, la versión no se realizará y el Adobe investigará por qué la actualización provocó este comportamiento inesperado.

[Pruebas de producto y pruebas funcionales de cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) que impiden que las actualizaciones de productos y los mensajes de código de cliente rompan la producción también se validan durante una actualización de versión de AEM.

>[!NOTE]
>
>Si el código personalizado se insertó en el entorno de ensayo y luego fue rechazado por usted, la siguiente actualización de AEM eliminará esos cambios para reflejar la etiqueta de git de la última versión de cliente en producción que se realizó correctamente.

## Almacenamiento de nodos compuestos {#composite-node-store}

Como se ha mencionado anteriormente, las actualizaciones en la mayoría de los casos no tendrán tiempo de inactividad, incluso para el autor, que es un clúster de nodos. Las actualizaciones móviles son posibles debido al *almacén de nodos compuestos* en Oak.

Esta función permite AEM varios repositorios simultáneamente. En una implementación móvil, la nueva versión de Green AEM contiene su propia versión `/libs` (el repositorio inmutable basado en TarMK), distinto de la versión anterior de Blue AEM, aunque ambos hacen referencia a un repositorio mutable compartido basado en DocumentMK que contiene áreas como `/content` , `/conf` , `/etc` y otros. Porque tanto el Azul como el Verde tienen sus propias versiones de `/libs`, ambos pueden estar activos durante la actualización móvil, lo que hace que el tráfico pase hasta que el azul se sustituya por el verde.
