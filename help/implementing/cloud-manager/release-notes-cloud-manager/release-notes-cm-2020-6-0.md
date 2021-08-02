---
title: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2020.6.0
description: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2020.6.0
feature: Información de la versión
exl-id: 879a5025-f94f-4549-bf6e-e1cc6b6a7b58
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 83%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2020.6.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2020.6.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2020.6.0 es el 4 de junio de 2020.

## Novedades {#whats-new-cloud-manager}

* Un usuario con la función *Propietario empresarial* en Cloud Manager ahora puede eliminar un programa de espacio aislado para pruebas de la página de aterrizaje (con el botón de acción rápida en tarjeta de programa) o desde el programa.

   Consulte [Eliminación de un programa de espacio aislado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) para obtener más información.

* Un usuario de programa de espacio aislado en la función *Propietario empresarial* o *Administrador de implementación* en Cloud Manager ahora puede eliminar su conjunto de entornos de producción y ensayo en la interfaz de usuario de Cloud Manager. La opción Eliminar ya está disponible en la tarjeta de entorno de la página **Información general de Programas** y en la página **Entornos**. Al seleccionar la opción de eliminación en producción o fase también se eliminan las otras del conjunto.

   Consulte [Eliminación de un programa de espacio aislado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) para obtener más información.

* Marcas de entrenador en la página de aterrizaje para informar e instruir al usuario sobre la navegación básica.

* Marcas de entrenador en la página de **Información general de Programa** para informar e instruir al usuario sobre la navegación básica dentro de Cloud Manager para los primeros pasos.

* Ahora hay disponible una página **LEARN** en Cloud Manager, a la que se puede acceder desde la barra de navegación superior. Esta página incluye recursos para ayudar a los usuarios a conocer los flujos de trabajo utilizados con más frecuencia según su función asignada en Cloud Manager.

* Los Programas de espacio aislado ahora se identifican mediante un distintivo de **Espacio aislado** que se mostrará en la tarjeta de programa de la página de aterrizaje junto al nombre del programa en la página **Información general del Programa**.

* Un usuario con la función SysAdmin ahora tiene acceso con un solo clic a la ubicación de Admin Console desde la que se pueden administrar las funciones de los usuarios o los permisos de Cloud Manager. Ahora está disponible el botón **Administrar acceso** en la página de aterrizaje junto al botón **Añadir Programa**.

   Consulte [Tareas de SysAdmin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) para obtener más información.

* Un usuario con la función SysAdmin ahora tiene acceso con un solo clic a la instancia de autor directamente desde Cloud Manager.

   Consulte [Administración del acceso a la instancia de autor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) para obtener más información.

* El registro de compilación ahora incluye la lista de artefactos descubiertos, incluidos los paquetes de contenido omitido.

* El paso Generar ahora valida que todos los paquetes de contenido generados incluyen todas las propiedades obligatorias: nombre, grupo y versión.

* El paso Generar ahora valida que la compilación produjo al menos un paquete de contenido.

### Corrección de errores {#bug-fixes-cm}

* En determinadas situaciones, los iconos del cuadro de diálogo **Crear Programa** estaban desalineados.

* El identificador de la versión de AEM no se mostraba de forma coherente en la página **Información general de Programas**.

* Al configurar la canalización de producción, la opción **Implementación programada** no estaba visible para algunos clientes.

### Problemas conocidos {#known-issues-cm}

* Los Entornos dentro de un programa de espacio aislado hibernarán cuando no se detecte ninguna actividad durante un tiempo determinado. Este estado no se observa en Cloud Manager. Sin embargo, el estado se puede observar a través de Developer Console. Esto se solucionará en una próxima versión.

* El vínculo a Developer Console directamente desde Cloud Manager no mostrará la opción de anular la hibernación o hibernar el entorno de un programa de espacio aislado para pruebas. Para solucionarlo, una vez en Developer Console, añada el patrón `#release-cm-p1234-e5678` al final de la dirección URL, donde *1234* es el ID de Programa y *5678* es el ID del entorno. Esto se solucionará en una próxima versión.
