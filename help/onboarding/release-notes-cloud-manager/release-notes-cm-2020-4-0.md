---
title: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.4.0
description: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.4.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 77%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

Esta página describe las Notas de la versión de Cloud Manager en AEM como Cloud Service 2020.4.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.4.0 es el 9 de abril de 2020.

## Novedades {#whats-new-cloud-manager}

* Las URL de Publisher ya están disponibles en la página de Entorno de la interfaz de usuario de Cloud Manager.
* Cambios en la navegación para permitir que el usuario edite, cambie o agregue un programa desde la página de información general de Cloud Manager.
* Cambios que permiten al usuario editar programas desde la tarjeta de programa en la página de aterrizaje de Cloud Manager.
* Se muestra el nuevo estado de **Canalización ejecutándose** en el entorno con el que está asociada.
* Mejoras en la comprensión de la página de ejecución de la canalización. Esto incluye la visualización del nombre de la canalización (solo para la canalización que no es de producción) y el tipo, y un distintivo para indicar si el estado de la canalización está en curso/cancelada/con error.
* Información sobre las herramientas para mejorar la experiencia del usuario y la comprensión de por qué se desactiva el botón Añadir Programa/Entorno.
* Los entornos con error ahora se pueden eliminar a través de la interfaz de usuario y la API.
* El proceso utilizado para generar contraseñas de git se ha vuelto más resistente a los problemas en la capa de servicio subyacente.

### Corrección de errores {#bug-fixes-cloud-manager}

* Los vínculos al entorno de ensayo en la página de detalles de la ejecución de la canalización no navegaban de manera consistente a la ubicación correcta.
* Los pasos individuales dentro del proceso de creación de entornos agotarían el tiempo de espera antes de lo necesario, lo que causaría fallas en el proceso.
* La configuración Maven utilizada en el contenedor de compilación se actualizó para evitar interbloqueos al descargar metadatos de artefactos.
* En algunos casos, el paso Generar imagen no puede descargar correctamente los paquetes de clientes.
* Algunas condiciones poco frecuentes evitarían que se eliminaran entornos.
* Las notificaciones de Experience Cloud no se recibían de forma coherente.

