---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.5.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.5.0
feature: Release Information
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 3%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.5.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.5.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.5.0 es el 6 de mayo de 2021.

### Novedades {#what-is-new}

* La regla de calidad PackageOverlaps ahora detecta casos en los que el mismo paquete se implementó varias veces, es decir, en varias ubicaciones incrustadas, en el mismo conjunto de paquetes implementado.

* El extremo del repositorio en la API pública ahora incluye la URL de Git.

* El registro de implementación descargado por un usuario de Cloud Manager será más profundo y ahora incluirá detalles sobre errores y escenarios de éxito.

* Se han resuelto errores intermitentes encontrados al insertar el código en el Git de Adobe.

* Ahora, el complemento Commerce se puede aplicar a los programas de Sandbox durante el flujo de trabajo Editar programa .

* La variable *Editar programa* se ha actualizado la experiencia.

* La tabla Nombres de dominio de la página Detalles del entorno mostrará hasta 250 nombres de dominio a través de la paginación.

* La variable **Soluciones y complementos** en **Agregar programa** y **Editar programa** los flujos de trabajo mostrarán la solución, aunque solo haya una solución disponible para el programa.

* El mensaje de error en el registro de pasos de compilación cuando la compilación no produjo ningún paquete de contenido implementado no estaba claro.

### Corrección de errores {#bug-fixes}

* En ocasiones, el usuario puede ver un estado &quot;activo&quot; verde junto a una Lista de permitidos IP incluso cuando esa configuración no se implementó.

* En lugar de eliminar las variables &quot;eliminadas&quot;, la API de variables de canalización solo las marcaría con estado **ELIMINADO**.

* Algunos problemas de calidad del tipo de hueso de código impactaban incorrectamente en la clasificación de fiabilidad.

* Dado que los dominios comodín no son compatibles, la interfaz de usuario no permitirá que el usuario envíe un dominio comodín.

* Cuando se inició la ejecución de una canalización entre la medianoche y la 01:00 UTC, la versión del artefacto generada por Cloud Manager no estaba buena a la versión creada el día anterior.

* Durante la configuración del programa de espacio aislado, una vez que el proyecto con código de muestra se haya creado correctamente, Administrar Git aparecerá como un vínculo desde la tarjeta promocional en la página Información general .
