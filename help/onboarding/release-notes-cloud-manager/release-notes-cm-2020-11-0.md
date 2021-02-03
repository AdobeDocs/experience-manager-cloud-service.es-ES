---
title: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.11.0
description: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.11.0
translation-type: tm+mt
source-git-commit: 79af82d1589108e7a8953e29a5d0f0169920585c
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---


# Notas de la versión de Cloud Manager en Adobe Experience Manager como Cloud Service 2020.11.0 {#release-notes}

Esta página describe las Notas de la versión de Cloud Manager en AEM como Cloud Service 2020.11.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.11.0 es el 12 de noviembre de 2020.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* Ahora los usuarios pueden acceder a una nueva opción de menú **Inicio de sesión local** desde las opciones del menú entorno de las páginas de resumen de Entornos y tarjetas de Entorno.
Consulte [Administración de Entornos](/help/implementing/cloud-manager/manage-environments.md#login-locally) para obtener más detalles.

* La ficha **Learn** de Cloud Manager se ha actualizado con nuevas imágenes en la interfaz de usuario.

### Corrección de errores {#bug-fixes-cloud-manager}

* La carga de dependencias realizada antes de la ejecución de la compilación requería la descarga de un complemento de Maven.
* El vínculo del pie de página del Administrador de nubes para seleccionar un idioma ahora se desplazará a la ubicación correcta.
* A veces, durante la digitalización del código, el proceso SonarQube no se inicio. Esto se detectará automáticamente y se intentará reiniciar.
* Todas las tuberías de producción existentes se habilitarán automáticamente con el paso Auditoría de experiencias.
