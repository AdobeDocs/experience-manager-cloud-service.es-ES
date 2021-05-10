---
title: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2021.4.0
description: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2021.4.0
feature: Información de la versión
translation-type: tm+mt
source-git-commit: e2d4bb7649fad3ee172c6f049ecfdedc71417ee2
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---


# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.4.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.4.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.4.0 es el 8 de abril de 2021.
La próxima versión está planificada para el 06 de mayo de 2021.

### Novedades {#what-is-new-april}

* Actualizaciones de la interfaz de usuario de los flujos de trabajo Añadir y editar programa para que sea más intuitivo.

* Un usuario con los permisos necesarios ahora puede enviar el punto final del comercio a través de la interfaz de usuario.

* Ahora, las variables de entorno se pueden vincular a un servicio específico, ya sea de autor o publicación. Requiere AEM versión `2021.03.5104.20210328T185548Z` o superior.

* El botón **Administrar Git** se muestra en la tarjeta Canalizaciones aunque no se hayan configurado canalizaciones.

* La versión del arquetipo de proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 27.

* Los proyectos de la consola de desarrollador de Adobe I/O creados por Cloud Manager ya no se pueden editar ni eliminar de forma involuntaria.

* Cuando un usuario agrega un nuevo entorno, se les informará de que una vez que se haya creado un entorno, no se puede mover a otra región.

* Ahora, las variables de entorno se pueden vincular a un servicio específico, ya sea de autor o publicación. Requiere AEM versión 2021.03.5104.20210328T185548Z o superior.

* Se ha aclarado el mensaje de error al iniciar una canalización cuando se eliminaba un entorno.

* Los paquetes OSGi proporcionados por los proyectos de Eclipse ahora se excluyen de la regla `CQBP-84--dependencies`.

### Corrección de errores {#bug-fixes-cm-april}

* Al editar la página Auditoría de experiencias de una canalización, una ruta de entrada que comience con una barra diagonal `( / )` ya no dará como resultado que el paso se bloquee en estado pendiente.

* Cuando se crea una nueva canalización de producción, si el usuario no agrega ninguna anulación de auditoría de contenido, la página principal predeterminada no se auditó.

* Los problemas para `CloudServiceIncompatibleWorkflowProcess` tenían la gravedad incorrecta en el archivo CSV del problema descargable.

* La comprobación `Runmode` estaba produciendo falsos positivos en nodos que no son de carpeta.