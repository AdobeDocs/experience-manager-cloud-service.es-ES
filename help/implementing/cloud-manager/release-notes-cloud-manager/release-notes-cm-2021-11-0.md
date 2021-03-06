---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.11.0
description: Estas son las notas de la versión de Cloud Manager en AEM versión as a Cloud Service 2021.11.0
feature: Release Information
exl-id: 98fd6d8a-ddc2-4f53-9dfc-d8e21af0c14d
source-git-commit: 4505f703754fa46cd746ae4794a3cab65cb19976
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 77%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.11.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.11.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager en AEM as a Cloud Service 2021.11.0 es el 4 de noviembre de 2021.
La próxima versión está planificada para el 16 de diciembre de 2021.

## Novedades {#what-is-new}

* Los usuarios ahora pueden aprovechar las nuevas canalizaciones front-end para implementar exclusivamente el código front-end de forma acelerada. Consulte [Canalizaciones principales de Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obtener más información.

   >[!IMPORTANT]
   >Debe estar en AEM versión `2021.10.5933.20211012T154732Z` para aprovechar las nuevas canalizaciones front-end.

* La duración de la canalización Calidad del código se reduce significativamente al realizar el análisis del código de una manera más eficiente sin necesidad de crear una imagen de AEM completa. Este cambio se implementará progresivamente durante las semanas siguientes a la publicación.

* El ID de confirmación de Git ahora se mostrará en los detalles de ejecución de la canalización, lo que facilita el seguimiento del código creado.

* La creación de programas ya está disponible a través de una API expuesta públicamente.

* La creación de entornos ya está disponible a través de una API expuesta públicamente.

* El encabezado de respuesta `x-request-id` ahora está visible en el sitio de pruebas de API en [www.adobe.io](https://www.adobe.io/). Este encabezado es útil cuando se envían problemas de servicio de atención al cliente para la resolución de problemas.

* Como usuario, veo que la tarjeta de canalización con cero canalizaciones me proporciona la guía adecuada.

* Ya está disponible una nueva página Actividad donde se pueden ver actividades como las ejecuciones de canalización y código junto con los detalles asociados. Con el tiempo, las actividades enumeradas en esta página se ampliarán en alcance junto con los detalles proporcionados.

* Ya está disponible una nueva página de canalizaciones con una ventana emergente de estado al pasar el ratón por encima para facilitar la vista del resumen de detalles. Las ejecuciones de canalización se pueden ver junto con los detalles asociados.

* La API Editar canalización ahora admite el cambio del entorno utilizado en las fases de implementación.

* Se ha introducido una optimización en el proceso de digitalización de OakPal para paquetes grandes.

* El archivo CSV del problema de calidad ahora contendrá la marca de tiempo para cada problema de calidad.

## Corrección de errores {#bug-fixes}

* Algunas configuraciones de compilación no ortodoxas tuvieron como resultado que se almacenaran archivos innecesarios en la caché de artefactos Maven de la canalización, lo que resultó en I/O de red superfluas al iniciar y detener el contenedor de compilación.

* La API PATCH de canalización falla si la fase de implementación no existe.

* La regla de calidad `ClientlibProxyResourceCheck` producía problemas de falsos positivos cuando había bibliotecas de cliente con rutas base comunes.

* El mensaje de error cuando se ha alcanzado el número máximo de repositorios no especificaba el motivo del error.

* En casos excepcionales, las canalizaciones fallaban debido a la gestión inadecuada de reintentos de ciertos códigos de respuesta.
