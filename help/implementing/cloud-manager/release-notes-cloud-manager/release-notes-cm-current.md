---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2022.01.0
description: Estas son las notas de la versión de Cloud Manager de AEM versión as a Cloud Service 2022.01.0.
feature: Release Information
source-git-commit: 8da3976250c94d5858d07a83b0eb395fab9a3eda
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---


# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2022.01.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2022.01.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager en AEM as a Cloud Service 2022.01.0 es el 20 de enero de 2022. La próxima versión está prevista para el 10 de febrero de 2022.

## Novedades {#what-is-new}

* Cloud Manager [evite la reconstrucción del código base cuando detecte que se utiliza la misma confirmación git](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) en varias ejecuciones de canalización de pila completa.
* El acceso al registro de entorno de AEM ahora requiere la variable **Administrador de implementación** perfil de producto. Los usuarios sin este perfil verán un botón deshabilitado en la interfaz de usuario.
* La interfaz de usuario no permitirá la configuración de canalización de front-end para un programa en el que Sites no esté habilitado como solución.
* Al generar una contraseña de git, se muestra la fecha de caducidad.

## Corrección de errores {#bug-fixes}

* Se han corregido las excepciones de puntero nulo encontradas en algunas implementaciones de canalización de front-end.
* Ahora se pueden agregar, actualizar y eliminar variables de entorno cuando un entorno ejecuta una versión obsoleta de AEM.
* El paso crear imagen ya no se marcará como ERROR para las canalizaciones que usaron el paso programado en algunos casos excepcionales.
* Para los programas con un solo repositorio, la pantalla de ejecución de la canalización ahora mostrará el nombre del repositorio.
