---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2020.11.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2020.11.0
feature: Release Information
exl-id: e2acf515-d339-4d2b-9b62-09c1dab1ffac
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 8%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2020.11.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2020.11.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2020.11.0 es el 12 de noviembre de 2020.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* Una nueva opción de menú **Inicio de sesión local** ahora está disponible para los usuarios desde las opciones de menú de entorno de las páginas de tarjeta de entorno y Resumen de entornos .
Consulte [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md#login-locally) para obtener más información.

* La variable **Más información** en Cloud Manager se ha actualizado con nuevas imágenes en la interfaz de usuario.

### Correcciones de errores {#bug-fixes-cloud-manager}

* La carga de dependencias realizada antes de la ejecución de la compilación requería la descarga de un complemento de Maven.
* El vínculo del pie de página de Cloud Manager para seleccionar un idioma ahora se desplaza a la ubicación correcta.
* A veces, durante la digitalización del código, el proceso SonarQube no se iniciaba. Esto se detectará automáticamente y se intentará reiniciar.
* Todas las canalizaciones de producción existentes se habilitarán automáticamente con el paso Auditoría de experiencias .
