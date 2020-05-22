---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.5.0
description: Notas de la versión de Experience Manager para 2020.5.0
translation-type: tm+mt
source-git-commit: 8fe1f6f1c7c6a608ee1ca42836ee91e83487428d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 61%

---


# Notas de la versión de AEM as a Cloud Service 2020.5.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.5.0.

## Fecha de la versión {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.5.0 is May 07, 2020.

## What&#39;s New in AEM Sites {#aem-sites}

Siga esta sección para conocer las novedades y las actualizaciones de AEM Sites en AEM como una versión 2020.5.0 del servicio de nube.

* La información detallada del trabajo ahora está disponible después de procesar los movimientos de página masiva y los despliegues como trabajos asincrónicos.
* Al copiar/pegar un árbol de páginas, ahora ofrece la opción de pegar solo la página raíz o también las subpáginas del árbol.
* Los fragmentos de experiencia de AEM exportados a espacios de trabajo de Adobe Destinatario ahora aparecen como tipos de oferta únicos y fuentes de oferta en Destinatario.
* MSM: el uso del activador de *publicación* ahora despliega correctamente eventos de eliminación para los componentes del origen de Live Copy, es decir, eliminando componentes de una Live Copy que se eliminaron del origen de Live Copy.
* MSM: ahora se cambia el nombre de los componentes de Live Copy a *_msm_move* después de la misma implementación de componente desde el origen de Live Copy.


## Novedades de Cloud Manager {#cloud-manager}

Siga esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.5.0.

### Novedades {#what-is-new}

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

