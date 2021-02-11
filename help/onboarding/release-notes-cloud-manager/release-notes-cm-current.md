---
title: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2021.2.0
description: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2021.2.0
translation-type: tm+mt
source-git-commit: d20a729712c1dbd48150f813419b57c49074b492
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# Notas de la versión de Cloud Manager en Adobe Experience Manager como Cloud Service 2021.2.0 {#release-notes}

Esta página describe las Notas de la versión de Cloud Manager en AEM como Cloud Service 2021.2.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2021.2.0 es el 11 de febrero de 2021.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* La canalización de producción de Cloud Manager ahora incluirá la capacidad de prueba de IU personalizada.

* Los clientes de Assets ahora podrán elegir cuándo y dónde implementar la instancia de Brand Portal de forma automática mediante la interfaz de usuario de Cloud Manager. Para un programa normal (sin simulación de pruebas) con la solución Assets, Brand Portal ahora se puede aprovisionar en el entorno de producción. El aprovisionamiento solo se puede realizar una vez en el entorno de producción.

* El arquetipo del proyecto AEM utilizado en la creación de proyectos y Simuladores para pruebas se ha actualizado a la versión 25.

* La lista de las API obsoletas identificadas durante el análisis de código se ha refinado para incluir clases y métodos adicionales que ya no se utilizan en las últimas versiones del SDK de Cloud Service.

* SonarQube perfil para Cloud Manager actualizado para eliminar Sonar rule squid:S2142. Esto ya no entrará en conflicto con las comprobaciones de interrupción del subproceso.

* La interfaz de usuario del Administrador de nube informará al usuario que no pueda agregar o actualizar temporalmente el nombre de dominio porque el entorno asociado tiene una canalización en ejecución conectada a él o está esperando el paso de aprobación.

* Las propiedades configuradas en los archivos `pom.xml` del cliente con el prefijo Sonar ahora se eliminarán dinámicamente para evitar errores de compilación y de exploración de calidad.

* La interfaz de usuario del Administrador de nube informará al usuario que no pueda seleccionar temporalmente un certificado SSL si está siendo utilizado por un nombre de dominio que se está implementando actualmente.


### Corrección de errores {#bug-fixes}

* El certificado SSL que coincide con un nombre de dominio ya no distingue entre mayúsculas y minúsculas.

* La interfaz de usuario del Administrador de nube ahora informará al usuario si las claves privadas del certificado no cumplen el límite de 2048 bits con un mensaje de error adecuado.

* La interfaz de usuario del Administrador de nube informará al usuario que no pueda seleccionar temporalmente un certificado SSL si está siendo utilizado por un nombre de dominio que se está implementando actualmente.

* En algunos casos, un problema interno puede hacer que la eliminación de entornos se quede atascada.

* Algunos errores de canalización se notificaron incorrectamente como errores de canalización.
