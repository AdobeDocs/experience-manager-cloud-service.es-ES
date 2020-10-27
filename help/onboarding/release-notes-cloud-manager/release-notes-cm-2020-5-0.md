---
title: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.5.0
description: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.5.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 71%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.5.0 {#release-notes}

Esta página describe las Notas de la versión de Cloud Manager en AEM como Cloud Service 2020.5.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.5.0 es el 7 de mayo de 2020.

## Novedades {#whats-new-cloud-manager}

* Se han agregado seis reglas de calidad de código adicionales para ayudar a los clientes a identificar posibles problemas al planificar una migración a Cloud Service,
* Se ha añadido una nueva métrica *Compatibilidad de Cloud Service* para resumir el número de problemas relacionados con la compatibilidad.
* Los entornos que no se hayan podido crear ahora se eliminarán automáticamente, aproximadamente 24 horas después del error de creación, a menos que ya se hayan eliminado.
* Se ha mejorado el rendimiento de la página de Actividad y de la API de Lista de ejecuciones de canalización.
* El registro de calidad del código ahora contiene todos los seguimientos de pila para excepciones.

### Corrección de errores {#bug-fixes}

* Se mostraba una tarjeta engañosa en la página de información general mientras se ejecutaba la canalización de producción.
* La regla de calidad del código *DontImplementeOrExtendProviderTypesPomCheck* puede producir a veces una excepción de puntero nulo.
* Algunos vínculos de documentación de la página de información general no funcionaban correctamente.
* El cuadro de diálogo Crear Entorno no se mostraba correctamente en Safari.
* Algunas tarjetas de la página de información general no mostraban correctamente los nombres de entidades.
* En algunos casos, Generar imagen no descargaba correctamente los paquetes de clientes.
