---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.2.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.2.0
exl-id: 281f9523-dec2-44f1-9459-5a45d48489d9
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.2.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.2.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.2.0 es el 11 de febrero de 2021.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* Los clientes de Assets ahora podrán elegir cuándo y dónde implementar su instancia de Brand Portal de forma autoservicio mediante la interfaz de usuario de Cloud Manager. Para un programa normal (que no sea de simulación de pruebas) con la solución Assets, Brand Portal ahora se puede aprovisionar en el entorno de producción. El aprovisionamiento solo se puede realizar una vez en el entorno de producción.

* El tipo de archivo del proyecto AEM utilizado en la creación de proyectos y entornos limitados se ha actualizado a la versión 25.

* La lista de API obsoletas identificadas durante la digitalización del código se ha refinado para incluir clases y métodos adicionales que ya no se utilizan en las últimas versiones del SDK de Cloud Service.

* El perfil de SonarQube para Cloud Manager se ha actualizado para eliminar la regla Sonar squid:S2142. Esto ya no entrará en conflicto con las comprobaciones de Interrupción de subprocesos.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda añadir o actualizar temporalmente el nombre de dominio porque el entorno asociado tiene una canalización en ejecución conectada a él o está en espera del paso de aprobación.

* Propiedades establecidas en el cliente `pom.xml` los archivos con el prefijo sonar ahora se eliminarán dinámicamente para evitar errores de análisis de calidad y compilación.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda seleccionar temporalmente un certificado SSL si lo está utilizando un nombre de dominio que se esté implementando actualmente.

* Se han agregado reglas de calidad de código adicionales para cubrir los problemas de compatibilidad con el Cloud Service.

### Correcciones de errores  {#bug-fixes}

* La coincidencia del certificado SSL con un nombre de dominio ya no distingue entre mayúsculas y minúsculas.

* La interfaz de usuario de Cloud Manager informará a un usuario si las claves privadas del certificado no cumplen el límite de 2048 bits con un mensaje de error apropiado.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda seleccionar temporalmente un certificado SSL si lo está utilizando un nombre de dominio que se esté implementando actualmente.

* En algunos casos, un problema interno puede provocar que la eliminación del entorno se bloquee.

* Algunos errores de canalización se notificaron incorrectamente como errores de canalización.
