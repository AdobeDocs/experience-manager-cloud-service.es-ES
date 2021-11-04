---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.11.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.11.0
feature: Release Information
exl-id: null
source-git-commit: e8ceeb0eb4fb26553683ced74a2e20628fc2952e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.11.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.11.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.11.0 es el 4 de noviembre de 2021.
La próxima versión está planificada para el 9 de diciembre de 2021.

### Novedades {#what-is-new}

* Los usuarios ahora pueden aprovechar las nuevas canalizaciones front-end para implementar exclusivamente el código front-end de forma acelerada. Consulte [Canalizaciones principales de Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obtener más información.

   >[!IMPORTANT]
   >Debe estar en AEM versión `2021.10.5933.20211012T154732Z` para aprovechar las nuevas canalizaciones front-end.

* La duración de la canalización Calidad del código se reduce significativamente al realizar el análisis del código de una manera más eficiente sin necesidad de crear una imagen AEM completa. Este cambio se implementará progresivamente durante las semanas siguientes a la publicación.

* El ID de confirmación de Git ahora se mostrará en los detalles de ejecución de la canalización, lo que facilita el seguimiento del código creado.

* La creación de programas ya está disponible a través de una API expuesta públicamente.

* La creación de entornos ya está disponible a través de una API expuesta públicamente.

* La variable `x-request-id` el encabezado de respuesta ahora está visible en API Playground en [www.adobe.io](https://www.adobe.io/). Este encabezado es útil cuando se envían problemas de atención al cliente para la resolución de problemas.

* Como usuario, veo que la tarjeta de canalización con cero canalizaciones me proporciona la guía adecuada.

* Ya está disponible una nueva página de actividad donde se pueden ver actividades como las ejecuciones de canalización y código junto con los detalles asociados. Con el tiempo, las actividades enumeradas en esta página se ampliarán en alcance junto con los detalles proporcionados.

* Ya está disponible una nueva página de canalizaciones con una ventana emergente de estado al pasar el ratón por encima para facilitar la vista del resumen de detalles. Las ejecuciones de canalización se pueden ver junto con los detalles asociados.

* La API Editar canalización ahora admite el cambio del entorno utilizado en las fases de implementación.

* Se ha introducido una optimización en el proceso de digitalización de OakPal para paquetes grandes.

* El archivo CSV del problema de calidad ahora contendrá la marca de tiempo para cada problema de calidad.

### Corrección de errores {#bug-fixes}

* Algunas configuraciones de compilación no ortodoxas tuvieron como resultado que se almacenaran archivos innecesarios en la caché de artefactos Maven de la canalización, lo que resultó en E/S de red superfluas al iniciar y detener el contenedor de compilación.

* La API del PATCH de canalización falla si la fase de implementación no existe.

* La variable `ClientlibProxyResourceCheck` la regla de calidad producía problemas falsos positivos cuando había bibliotecas cliente con rutas base comunes.

* El mensaje de error cuando se ha alcanzado el número máximo de repositorios no especificaba el motivo del error.

* En casos excepcionales, las canalizaciones fallaban debido a la gestión inadecuada de reintentos de ciertos códigos de respuesta.

