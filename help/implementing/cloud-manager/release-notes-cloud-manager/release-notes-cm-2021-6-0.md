---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.6.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.5.0
feature: Release Information
exl-id: 9a0a53d3-31d4-493d-ba2e-b4bb22f60351
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 3%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.6.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.6.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.6.0 es el 10 de junio de 2021.

### Novedades {#what-is-new}

* El servicio de vista previa se implementará progresivamente en todos los programas. Se notificará al producto a los clientes cuando su programa esté habilitado para el servicio de vista previa. Consulte [Acceso al servicio de vista previa](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) para obtener más información.

* Las dependencias de Maven descargadas durante el paso de compilación ahora se almacenan en caché entre ejecuciones de canalización. Esta función se habilitará para los clientes en las próximas semanas.

* El nombre del programa ahora se puede editar mediante el cuadro de diálogo editar programa .

* El nombre de rama predeterminado utilizado durante la creación del proyecto y en el comando push predeterminado mediante la gestión de flujos de trabajo de Git se ha cambiado a `main`.

* Se ha actualizado la edición de la experiencia del programa en la interfaz de usuario.

* La regla de calidad `ImmutableMutableMixCheck` se ha actualizado para clasificar `/oak:index` como inmutables.

* Las reglas de calidad `CQBP-84` y `CQBP-84--dependencies` se han consolidado en una única regla. Como parte de esta consolidación, el análisis de dependencias identifica con mayor precisión los problemas en dependencias de terceros que se están implementando en el tiempo de ejecución de AEM.

* Para evitar confusiones, se han consolidado las filas de segmento Publicar AEM y Publicar Dispatcher en la página Detalles del entorno .

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* Se ha añadido una nueva regla de calidad de código para validar la estructura de `damAssetLucene` índices. Consulte [Índices Oak de DAM Asset Lucene personalizados](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) para obtener más información.

* La página de detalles del entorno ahora mostrará varios nombres de dominio para los servicios de publicación y vista previa (según corresponda). Consulte [Detalles del entorno](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#viewing-environment) para obtener más información.

### Corrección de errores {#bug-fixes}

* Las definiciones de nodo JCR que contenían una nueva línea después del nombre del elemento raíz no se analizaron correctamente.

* La API de repositorios de lista no filtraba los repositorios eliminados.

* Se mostraba un mensaje de error incorrecto cuando se proporcionaba un valor no válido para el paso de programación.

* En ocasiones, el usuario puede ver un verde *active* junto a una Lista de permitidos IP incluso cuando esa configuración no se haya implementado.

* Algunas secuencias de edición de programas podrían resultar en la incapacidad de crear o editar la canalización de producción.

* Algunas secuencias de edición de programas podrían dar como resultado la variable **Información general** que muestra un mensaje engañoso para volver a ejecutar la configuración del programa.
