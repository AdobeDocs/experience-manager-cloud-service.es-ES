---
title: Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido
description: Conozca las directrices y las prácticas recomendadas para utilizar la herramienta de transferencia de contenido.
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
feature: Migration
role: Admin
source-git-commit: 943685ed9c33ba42c4dd1cb941b2eca1cce8bfe8
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 14%

---


# Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido {#guidelines}

## Directrices y prácticas recomendadas {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/group-migration.md#important-considerations" text="Important Considerations when Migrating Groups" 

-->

La herramienta de transferencia de contenido integra el proceso de transferencia de contenido con Cloud Acceleration Manager. Es necesario utilizar esta versión (2.0 o posterior, pero ahora se recomienda la versión 3.0) para obtener todas las ventajas que proporciona:

* Forma de autoservicio de extraer un conjunto de migración una vez e introducirlo en varios entornos en paralelo.
* Se ha mejorado la experiencia del usuario mediante mejores estados de carga, protecciones y gestión de errores
* Los registros de ingesta se mantienen y siempre están disponibles para la resolución de problemas.

Para empezar a utilizar la versión más reciente, desinstale las versiones anteriores de la herramienta de transferencia de contenido. Con la versión 2.0 y posteriores de, se crean conjuntos de migración y se vuelve a ejecutar la extracción y la ingesta en los conjuntos.
No se admiten versiones anteriores a la 2.0.0 y se recomienda utilizar la versión más reciente.

Las siguientes directrices y prácticas recomendadas se aplican a la nueva versión de la herramienta de transferencia de contenido:

* Ejecute [Limpieza de revisión](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=es) y [comprobaciones de coherencia del almacén de datos](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=es) en el repositorio de **origen** para que pueda identificar posibles problemas y reducir el tamaño del repositorio.

* En la fase de ingesta, Adobe recomienda que ejecute la ingesta utilizando el modo *wipe* habilitado en el que se elimina el repositorio existente (Author o Publish) en el entorno del Cloud Service de Adobe Experience Manager AEM de destino (). A continuación, actualice con los datos del conjunto de migración. Este modo es más rápido que el modo sin borrado, donde el conjunto de migración se aplica sobre el contenido actual.

* Una vez completada la actividad de transferencia de contenido, se requiere la estructura de proyecto correcta en el entorno de Cloud Service para garantizar que el contenido se procese correctamente en el entorno de Cloud Service.

* Antes de ejecutar la herramienta de transferencia de contenido, debe asegurarse de que haya suficiente espacio en disco en el `crx-quickstart` subdirectorio de la instancia de origen de AEM. Esto se debe a que la herramienta de transferencia de contenido crea una copia local del repositorio que se carga posteriormente en el conjunto de migración.
La fórmula general para calcular el espacio libre necesario en disco es la siguiente:
  `data store size + node store size * 1.5`

* *tamaño del almacén de datos*: la herramienta de transferencia de contenido utiliza 64 GB, incluso si el almacén de datos real es más grande.
* *tamaño del almacén de nodos*: el tamaño del directorio del almacén de segmentos o el tamaño de la base de datos MongoDB.
Por lo tanto, para un tamaño de almacén de segmentos de 20 GB, el espacio libre requerido en disco sería de 94 GB.

* Se debe mantener un conjunto de migración a lo largo de la actividad de transferencia de contenido para admitir recargas de contenido. Se puede crear y mantener un máximo de 10 conjuntos de migración por proyecto en Cloud Acceleration Manager a la vez durante la actividad de transferencia de contenido. Si se necesitan más de 10 conjuntos de migración, cree un segundo proyecto en Cloud Acceleration Manager. Sin embargo, esto requiere administración de proyectos adicional y administración externa al producto para evitar que varios usuarios sobrescriban contenido en el destino.

* Evite alterar el directorio de instalación de la herramienta CTT. De forma predeterminada, la instalación se realiza en la ruta crx-quickstart/cloud-migration. Otras bibliotecas utilizan internamente esta ubicación específica. Modificar esta ruta puede provocar problemas de extracción.

## Consideraciones importantes antes de utilizar la herramienta de transferencia de contenido {#important-considerations}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar la herramienta de transferencia de contenido:

* AEM El requisito mínimo del sistema para la herramienta de transferencia de contenido es de 6.3+ y Java™ 8, respectivamente. AEM AEM Si su versión es menor, actualice el repositorio de contenido a la versión 6.5 de la versión, que le permite usar la herramienta de transferencia de contenido. La versión es la siguiente:.

* AEM AEM Java™ debe configurarse en el entorno de la, de modo que el usuario que inicia el comando `java` pueda ejecutarlo de forma independiente. El usuario que inicia el proceso de ejecución del comando debe tener en cuenta lo siguiente

* La herramienta Content Transfer Tool se puede utilizar con los siguientes tipos de almacén de datos: almacén de datos de archivos, almacén de datos S3, almacén de datos compartido S3 y almacén de datos del almacén de Azure Blob.

* Si está usando un *Entorno de espacio aislado*, asegúrese de que su entorno esté actualizado y actualizado a la última versión. Si utiliza un *Entorno de producción*, se actualiza automáticamente.

* AEM Para iniciar una ingesta, debe pertenecer al grupo local de **administradores** de la instancia de Cloud Service a la que está transfiriendo el contenido. Los usuarios sin privilegios no pueden iniciar ingestas sin proporcionar manualmente el token de migración.

* Si la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está habilitada, se eliminará todo el repositorio existente y se creará un nuevo repositorio en el que introducir contenido. Esto significa que restablece todos los ajustes, incluidos los permisos en la instancia del Cloud Service de destino. También es verdadero para un usuario administrador agregado al grupo **administradores**. Se debe leer al usuario en el grupo **administradores** para recuperar el token de acceso para la herramienta de transferencia de contenido.

* La clave de extracción es válida durante 14 días desde el momento en que se creó o renovó. Se puede renovar en cualquier momento. Si la clave de extracción ha caducado, no se puede realizar una extracción.

* La herramienta de transferencia de contenido (CTT) no realiza ningún tipo de análisis de contenido antes de transferir contenido de la instancia de origen a la instancia de destino. Por ejemplo, CTT no diferencia entre contenido publicado y no publicado al introducir contenido en un entorno de Publish. Independientemente del contenido especificado en el conjunto de migración, este se incorpora en la instancia de destino elegida. Un usuario puede ingerir un conjunto de migración en una instancia de autor, en una instancia de Publish o en ambas. El Adobe recomienda que, al mover contenido a una instancia de Production, CTT se instale en la instancia de Author de origen para mover contenido a la instancia de Author de destino. Del mismo modo, instale CTT en la instancia de Publish de origen para mover contenido a la instancia de Publish de destino. Consulte [Ejecución de la herramienta de transferencia de contenido en una instancia de Publish](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es#running-tool) para obtener más información.

* Los grupos transferidos por la herramienta de transferencia de contenido son solo aquellos grupos que el contenido requiere para satisfacer los permisos. El proceso _Extracción_ copia todo el(la) `/home/groups` en el conjunto de migración. Para obtener más información, consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md). El proceso _Ingesta_ copia todos los grupos a los que se hace referencia en las ACL de contenido migradas. Consulte [Migración de grupos de usuarios cerrados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para obtener consideraciones adicionales para los grupos utilizados en una directiva de grupo de usuarios cerrados (CUG).

* Durante la fase de extracción, la herramienta de transferencia de contenido se ejecuta en una instancia de origen de AEM activa.

* La *fase de ingesta* para el autor reduce la implementación de todo el autor. AEM Esto significa que Author no está disponible durante todo el proceso de ingesta de datos. Asegúrese también de que no se ejecuten canalizaciones de Cloud Manager mientras está ejecutando la fase *Ingesta*.

* AEM Cuando se usa `Amazon S3` o `Azure` como almacén de datos en el sistema de almacenamiento de datos de origen, el almacén de datos debe configurarse para que los blobs almacenados no se puedan eliminar (recolección de elementos no utilizados). Esto garantiza la integridad de los datos de índice y si no se configura de esta manera, pueden producirse extracciones fallidas debido a la falta de integridad de estos datos de índice.

* Si utiliza índices personalizados, debe asegurarse de configurarlos con el nodo `tika` antes de ejecutar la herramienta de transferencia de contenido. Consulte [Preparación de la nueva definición de índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=es#preparing-the-new-index-definition) para obtener más información.

* Si tiene intención de realizar recargas, la estructura de contenido del contenido existente no debe cambiar desde el momento en que se realiza la extracción inicial hasta el momento en que se ejecuta la extracción superior. Las recargas no se pueden ejecutar en contenido cuya estructura se haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

* Si tiene intención de incluir versiones como parte de un conjunto de migración y está realizando recargas con `wipe=false`, debe deshabilitar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.

* La herramienta de transferencia de contenido (CTT) no admite las ingestas de combinación. Para consolidar contenido de varios sistemas en una única instancia de Cloud Service, solo se pueden migrar versiones de un sistema de origen. Este proceso requiere el uso de migraciones con el parámetro wipe=false, lo que puede resultar en tiempos de ingesta prolongados debido a la naturaleza incremental de la operación. Si es posible, consolide el contenido en un único sistema de origen antes de comenzar la migración para eliminar la necesidad de combinar contenido.

* Un conjunto de migración caduca después de un período prolongado de inactividad, después del cual sus datos ya no están disponibles. Revise [Expiración del conjunto de migración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es#migration-set-expiry) para obtener más detalles.

## Siguientes pasos {#whats-next}

Una vez que haya aprendido las directrices, las prácticas recomendadas y las consideraciones importantes para utilizar la herramienta de transferencia de contenido, ya puede instalarla y utilizarla, empezando por la creación de un conjunto de migración. Consulte [Introducción a la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).
