---
title: Notas de la versión para Cloud Manager en la versión 2021.5.0 de AEM as a Cloud Service
description: Notas de la versión para Cloud Manager en la versión 2021.5.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 100%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.5.0 {#release-notes}

Esta página describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.5.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.5.0 es el 6 de mayo de 2021.

### Novedades {#what-is-new}

* La regla de calidad PackageOverlaps ahora detecta casos en los que el mismo paquete se implementó varias veces, es decir, en varias ubicaciones incrustadas, en el mismo conjunto de paquetes implementado.

* El extremo del repositorio en la API Public ahora incluye la URL de Git.

* El registro de implementación que descargue un usuario de Cloud Manager será más profundo y ahora incluirá detalles sobre errores y escenarios de éxito.

* Se han resuelto errores intermitentes encontrados al insertar el código en el Git de Adobe.

* Ahora, el complemento Commerce se puede aplicar a los programas de zonas protegidas durante el flujo de trabajo Editar programa.

* La experiencia *Editar programa* se ha actualizado.

* La tabla Nombres de dominio de la página Detalles del entorno mostrará hasta 250 nombres de dominio a través de las páginas.

* La pestaña **Soluciones y complementos** en los flujos de trabajo **Agregar programa** y **Editar programa** mostrarán la solución, aunque solo haya una solución disponible para el programa.

* El mensaje de error en el registro de pasos de generación cuando la generación no producía ningún paquete de contenido implementado no estaba claro.

### Correcciones de errores {#bug-fixes}

* En ocasiones, el usuario podía ver el estado “activo” verde junto a una Lista de IP permitidas incluso cuando esa configuración no se implementaba.

* En lugar de eliminar las variables “eliminadas”, la API de variables de canalización solo las marcaba con el estado **ELIMINADO**.

* Algunos problemas de calidad del código Smell-type impactaban incorrectamente en la clasificación de fiabilidad.

* Dado que los dominios comodín no son compatibles, la interfaz de usuario no permitía que el usuario enviase un dominio comodín.

* Cuando se iniciaba la ejecución de una canalización entre la medianoche y la 01:00 UTC, la versión del artefacto generada por Cloud Manager no se garantizaba que fuera mayor que la versión creada el día anterior.

* Durante la configuración del programa de zona protegida, una vez que el proyecto con código de muestra se haya creado correctamente, Administrar Git aparecerá como un vínculo desde la tarjeta Hero en la página Información general.
