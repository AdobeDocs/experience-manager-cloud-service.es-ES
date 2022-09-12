---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.5.0
description: Notas de la versión de Experience Manager para 2020.5.0
exl-id: 8570d2c3-6d55-4914-94b2-f5d162e0c285
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 100%

---

# Notas de la versión de AEM as a Cloud Service 2020.5.0 {#release-notes}

Esta página describe las notas de la versión generales de Experience Manager as a Cloud Service 2020.5.0.

## Fecha de la versión {#release-date}

La fecha de la versión de [!DNL Experience Manager] as a Cloud Service 2020.5.0 es el 7 de mayo de 2020.

## Novedades en AEM Sites {#aem-sites}

Siga esta sección para conocer las novedades y las actualizaciones de AEM Sites en AEM as a Cloud Service versión 2020.5.0.

* La información detallada del trabajo ahora está disponible después de procesar los movimientos y despliegues de página masiva como trabajos asincrónicos.
* Al copiar/pegar un árbol de páginas, ahora ofrece la opción de pegar solo la página raíz o también las subpáginas del árbol.
* Los fragmentos de experiencias de AEM exportados a espacios de trabajo de Adobe Target ahora aparecen como tipos de oferta únicos y fuentes de oferta en Target.
* MSM: al usar el activador de *publicación* ahora despliega correctamente eventos de eliminación para los componentes del origen de Live Copy, es decir, elimina componentes de una Live Copy que se eliminaron del origen de Live Copy.
* MSM: ahora se cambia el nombre de los componentes de Live Copy a *_msm_move* después del mismo despliegue de componente desde el origen de Live Copy.


## Novedades de Cloud Manager {#cloud-manager}

Siga esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.5.0.

### Novedades {#what-is-new}

* Se han agregado seis reglas de calidad de código adicionales para ayudar a los clientes a identificar posibles problemas al planificar una migración a Cloud Service,
* Se ha añadido una nueva métrica *Compatibilidad de Cloud Service* para resumir el número de problemas relacionados con la compatibilidad.
* Los entornos que no se hayan podido crear ahora se eliminarán automáticamente, aproximadamente 24 horas después del error de creación, a menos que ya se hayan eliminado.
* Se ha mejorado el rendimiento de la página de Actividad y de la API de Lista de ejecuciones de canalización.
* El registro de calidad del código ahora contiene todos los seguimientos de pila para excepciones.

### Correcciones de errores  {#bug-fixes}

* Se mostraba una tarjeta engañosa en la página de información general mientras se ejecutaba la canalización de producción.
* La regla de calidad del código *DontImplementeOrExtendProviderTypesPomCheck* puede producir a veces una excepción de puntero nulo.
* Algunos vínculos de documentación de la página de información general no funcionaban correctamente.
* El cuadro de diálogo Crear Entorno no se mostraba correctamente en Safari.
* Algunas tarjetas de la página de información general no mostraban correctamente los nombres de entidades.
* En algunos casos, Generar imagen no descargaba correctamente los paquetes de clientes.
