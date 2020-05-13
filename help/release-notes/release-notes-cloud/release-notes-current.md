---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.5.0
description: Notas de la versión de Experience Manager para 2020.5.0
translation-type: tm+mt
source-git-commit: 94a732f56929ad4af23855152e258f82ad61ee2c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 29%

---


# Notas de la versión de AEM as a Cloud Service 2020.5.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.5.0.

## Cloud Manager {#cloud-manager}

Siga esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.5.0.

### Novedades {#what-is-new}

* Se han agregado seis reglas de calidad de código adicionales para ayudar a los clientes a identificar posibles problemas al planificar una migración a Cloud Service.
* Se ha añadido una nueva métrica Compatibilidad *de servicio de* nube para resumir el número de problemas relacionados con la compatibilidad.
* Los Entornos que no se hayan podido crear ahora se eliminarán automáticamente aproximadamente 24 horas después del error de creación, a menos que ya se hayan eliminado.
* Se ha mejorado el rendimiento de la página de Actividad y de la API de Lista de las ejecuciones de tubería.
* El registro de calidad del código ahora contiene todos los seguimientos de pila para excepciones.

### Corrección de errores {#bug-fixes}

* Se mostraba una tarjeta engañosa en la página de información general mientras se ejecutaba la canalización de producción.
* La regla de calidad del código *DontImplementeOrExtendProviderTypesPomCheck* puede producir a veces una excepción de puntero nulo.
* Algunos vínculos de documentación de la página de información general no funcionaban correctamente.
* El cuadro de diálogo Crear Entorno no se representaba correctamente en Safari.
* Algunas tarjetas de la página de información general no mostraban correctamente los nombres de entidades.
* En algunos casos, la imagen de compilación no puede descargar correctamente los paquetes de clientes.

