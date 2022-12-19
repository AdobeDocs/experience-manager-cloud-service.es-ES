---
title: Directrices y prácticas recomendadas para el uso de la herramienta de transferencia de contenido
description: Directrices y prácticas recomendadas para el uso de la herramienta de transferencia de contenido
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: b0d219f712b1dbbfa70d66ac14c0a66dc89ebbab
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 19%

---

# Directrices y prácticas recomendadas para el uso de la herramienta de transferencia de contenido {#guidelines}

## Directrices y prácticas recomendadas {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Directrices y prácticas recomendadas"
>abstract="Revise las directrices y las prácticas recomendadas para utilizar la herramienta de transferencia de contenido, incluidas las tareas de limpieza de revisiones, consideraciones sobre el espacio en disco y más."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Consideraciones importantes sobre el uso de la herramienta de asignación de usuarios"

Hay disponible una nueva versión de la herramienta de transferencia de contenido que integra el proceso de transferencia de contenido con Cloud Acceleration Manager. Se recomienda cambiar a esta nueva versión para aprovechar todas las ventajas que ofrece:

* Forma de autoservicio de extraer un conjunto de migración una vez e introducirlo en varios entornos en paralelo
* Experiencia del usuario mejorada mediante mejores estados de carga, protecciones y gestión de errores
* Los registros de ingesta se mantienen y siempre están disponibles para la resolución de problemas

Para empezar a utilizar la nueva versión, deberá desinstalar las versiones anteriores de la herramienta de transferencia de contenido. Esto es necesario porque la nueva versión viene con un cambio arquitectónico importante. Con la versión 2.0.10, deberá crear nuevos conjuntos de migración y volver a ejecutar la extracción y la ingesta en los nuevos conjuntos de migración. Si la migración ya está en curso, puede seguir utilizando la versión anterior de CTT hasta que se complete.

Las siguientes directrices y prácticas recomendadas se aplican a la nueva versión de la herramienta de transferencia de contenido:

* Es aconsejable ejecutar [Revision Cleanup](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) y [las comprobaciones de coherencia del almacén de datos](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) en el repositorio de **origen** para identificar posibles problemas y reducir el tamaño del repositorio.

* En la fase de ingesta se recomienda ejecutarla mediante el modo de *borrado* activado, en el que el repositorio existente (autor o publicación) en el entorno de Cloud Service de AEM de destinatario se eliminará por completo y, a continuación, se actualizará con los datos del conjunto de migración. Este modo es mucho más rápido que el modo sin borrado, donde el conjunto de migración se aplica sobre el contenido  existente.

* Una vez completada la actividad de transferencia de contenido, se requiere la estructura de proyecto correcta en el entorno de Cloud Service para garantizar que el contenido se procese correctamente en el entorno de Cloud Service.

* Antes de ejecutar la herramienta de transferencia de contenido, debe asegurarse de que haya suficiente espacio en disco en el `crx-quickstart` subdirectorio de la instancia de origen de AEM. Esto se debe a que la herramienta de transferencia de contenido crea una copia local del repositorio que se carga posteriormente en el conjunto de migración.
La fórmula general para calcular el espacio en disco necesario es la siguiente:
   `data store size + node store size * 1.5`

   * *tamaño del almacén de datos*: la herramienta de transferencia de contenido utiliza 64 GB, incluso si el almacén de datos real es más grande.
   * *tamaño del almacén de nodos*: el tamaño del directorio del almacén de segmentos o el tamaño de la base de datos MongoDB.
Por lo tanto, para un tamaño de almacén de segmentos de 20 GB, el espacio libre requerido en disco sería de 94 GB.

* Es necesario mantener un conjunto de migraciones a lo largo de toda la actividad de transferencia de contenido para que admita las recargas de contenido. Se puede crear y mantener un máximo de cinco conjuntos de migración por proyecto en Cloud Acceleration Manager a la vez durante la actividad de transferencia de contenido. Si se necesitan más de cinco conjuntos de migración, deberá crear un segundo proyecto en Cloud Acceleration Manager. Sin embargo, esto requerirá administración de proyectos adicional y control fuera del producto para evitar que varios usuarios sobrescriban el contenido en el destino.

## Consideraciones importantes antes de usar la herramienta de transferencia de contenido {#important-considerations}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar la herramienta de transferencia de contenido:

* El requisito mínimo del sistema para la herramienta de transferencia de contenido es AEM 6.3+ y JAVA 8. Si su versión de AEM es anterior, debe actualizar el repositorio de contenido a AEM 6.5 para utilizar la herramienta de transferencia de contenido.

* Java debe configurarse en el entorno AEM para que la variable `java` puede ejecutarlo el usuario que inicia AEM.

* La herramienta de transferencia de contenido se puede utilizar con los siguientes tipos de almacén de datos: Almacén de datos de archivos, almacén de datos S3, almacén de datos compartido S3 y almacén de datos del blob de Azure.

* Si está utilizando un *Entorno de espacio aislado*, compruebe que su entorno esté actualizado y actualizado a la versión más reciente. Si utiliza un *Entorno de producción*, se actualiza automáticamente.

* Para iniciar una ingesta, debe pertenecer a la AEM local **administradores** en la instancia de Cloud Service a la que está transfiriendo el contenido. Los usuarios sin privilegios no podrán iniciar las ingestas sin proporcionar manualmente el token de migración.

* Si la configuración **Borrar el contenido existente en la instancia de Cloud antes de la ingesta** está activada, elimina todo el repositorio existente y crea un nuevo repositorio en el que introducir contenido. Esto significa que restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino. Esto también se aplica a los usuarios administradores agregados a la variable **administradores** grupo. El usuario debe añadirse de nuevo al **administradores** para recuperar el token de acceso para la herramienta de transferencia de contenido.

* Las entradas no admiten la combinación de contenido de varios orígenes en la instancia de Cloud Service de destino si el contenido de los dos orígenes se mueve a las mismas rutas en el destino. Para mover contenido de varias fuentes a una sola instancia de Cloud Service de destino, debe asegurarse de que no haya superposición de las rutas de contenido de las fuentes.

* La clave de extracción es válida durante 14 días desde el momento en que se creó o renovó. Se puede renovar en cualquier momento. Si la clave de extracción ha caducado, no podrá realizar una extracción.

* La herramienta de transferencia de contenido (CTT) no realiza ningún tipo de análisis de contenido antes de transferir contenido de la instancia de origen a la instancia de destino. Por ejemplo, CTT no diferencia entre contenido publicado y no publicado al ingerir contenido en un entorno de publicación. Sea cual sea el contenido especificado en el conjunto de migración, se incorporará en la instancia de destino elegida. El usuario tiene la capacidad de ingerir un conjunto de migración en una instancia de Autor, una instancia de Publicación o ambas. Se recomienda que, al mover contenido a una instancia de Producción, CTT se instale en la instancia de Autor de origen para mover contenido a la instancia de Autor de destino y, de manera similar, instale CTT en la instancia de Publicación de origen para mover contenido a la instancia de Publicación de destino. Consulte [Ejecución de la herramienta de transferencia de contenido en una instancia de publicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) para obtener más información.

* Los usuarios y grupos que transfiere la herramienta de transferencia de contenido son solo aquellos que necesita el contenido para satisfacer los permisos. La variable *Extracción* el proceso copia todo el `/home` en el conjunto de migración y en la variable *Ingesta* El proceso copia todos los usuarios y grupos a los que se hace referencia en las ACL de contenido migrado. Para asignar automáticamente los usuarios existentes a sus ID de IMS, consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=es#cloud-migration).

* Durante la fase de extracción, la herramienta de transferencia de contenido se ejecuta en una instancia de origen de AEM activa.

* Después de completar la *Extracción* fase del proceso de transferencia de contenido y antes de iniciar el *Fase de ingesta* para ingerir contenido en el AEM as a Cloud Service *Prueba* o *Producción* , deberá registrar un ticket de asistencia para notificar al Adobe de su intención de ejecutar *Ingesta* para que el Adobe pueda garantizar que no se produzcan interrupciones durante el *Ingesta* proceso. Tendrá que registrar el ticket de asistencia 1 semana antes de la semana planificada *Ingesta* fecha. Una vez que haya enviado el ticket de soporte, el equipo de soporte le proporcionará instrucciones sobre los pasos siguientes. Puede registrar un vale de soporte con los siguientes detalles:

   * Fecha exacta y hora estimada (con su zona horaria) en la que planea iniciar la variable *Ingesta* fase.
   * Tipo de entorno (fase o producción) en el que planea introducir datos.
   * ID del programa.

* La variable *Fase de ingesta* para el autor, reduce la implementación de todo el autor. Esto significa que el autor de AEM no estará disponible durante todo el proceso de inserción. Asegúrese también de que no se ejecutan canalizaciones de Cloud Manager mientras está ejecutando el *Ingesta* fase.

* Al usar `Amazon S3` o `Azure` como almacén de datos en el sistema de AEM de origen, el almacén de datos debe configurarse de modo que los blobs almacenados no se puedan eliminar (se recopiló la basura). Esto garantiza la integridad de los datos de índice y si no se configuran de esta manera, pueden producirse extracciones fallidas debido a la falta de integridad de estos datos de índice.

* Si está utilizando índices personalizados, debe asegurarse de configurar los índices personalizados con `tika` antes de ejecutar la herramienta de transferencia de contenido. Consulte [Preparación de la nueva definición de índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) para obtener más información.

* Si tiene intención de realizar recargas, es esencial que la estructura de contenido del contenido existente no cambie desde el momento en que se toma la extracción inicial hasta cuando se ejecuta la extracción superior. Las superposiciones no se pueden ejecutar en contenido cuya estructura haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

* Si tiene intención de incluir versiones como parte de un conjunto de migración y realiza complementos con `wipe=false`, debe desactivar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.

## Siguientes pasos {#whats-next}

Una vez que conozca las directrices, las prácticas recomendadas y las consideraciones importantes sobre el uso de la herramienta de transferencia de contenido, ya estará listo para instalar y utilizar la herramienta, empezando por la creación de un conjunto de migración. Consulte [Introducción a la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) para obtener más información.
