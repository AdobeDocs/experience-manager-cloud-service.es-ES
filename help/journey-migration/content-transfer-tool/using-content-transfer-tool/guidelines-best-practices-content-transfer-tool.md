---
title: Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido
description: Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 2c53d1cce6b1e889a0e49254621d02bd152bfbbf
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 19%

---

# Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido {#guidelines}

## Directrices y prácticas recomendadas {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.md#important-considerations" text="Important Considerations when Mapping and Migrating Users" 

-->

Hay disponible una nueva versión de la herramienta de transferencia de contenido que integra el proceso de transferencia de contenido con Cloud Acceleration Manager. Se recomienda encarecidamente cambiar a esta nueva versión para aprovechar todas las ventajas que ofrece:

* Forma de autoservicio de extraer un conjunto de migración una vez e introducirlo en varios entornos en paralelo
* Experiencia del usuario mejorada mediante mejores estados de carga, protecciones y administración de errores
* Los registros de ingesta se mantienen y siempre están disponibles para la resolución de problemas

Para empezar a utilizar la nueva versión, deberá desinstalar las versiones anteriores de la herramienta de transferencia de contenido. Esto es necesario porque la nueva versión viene con un cambio arquitectónico importante. Con la versión 2.x, deberá crear nuevos conjuntos de migración y volver a ejecutar la extracción y la ingesta en los nuevos conjuntos de migración.
Las versiones anteriores a la 2.0.0 ya no serán compatibles y es aconsejable utilizar la versión más reciente.

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

* Es necesario mantener un conjunto de migración a lo largo de la actividad de transferencia de contenido para admitir recargas de contenido. Se puede crear y mantener un máximo de cinco conjuntos de migración por proyecto en Cloud Acceleration Manager a la vez durante la actividad de transferencia de contenido. Si se necesitan más de cinco conjuntos de migración, deberá crear un segundo proyecto en Cloud Acceleration Manager. Sin embargo, esto requerirá una administración de proyectos adicional y un control fuera del producto para evitar que varios usuarios sobrescriban contenido en el destino.

## Consideraciones importantes antes de utilizar la herramienta de transferencia de contenido {#important-considerations}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar la herramienta de transferencia de contenido:

* El requisito mínimo del sistema para la herramienta de transferencia de contenido es AEM 6.3+ y JAVA 8. AEM AEM Si su versión es menor, debe actualizar el repositorio de contenido a la versión 6.5 para usar la herramienta de transferencia de contenido, que se encuentra en la versión 6.5.

* AEM Java debe configurarse en el entorno de la, de modo que la variable `java` AEM El comando lo puede ejecutar el usuario que lo inicia

* La herramienta Content Transfer Tool se puede utilizar con los siguientes tipos de almacén de datos: almacén de datos de archivos, almacén de datos S3, almacén de datos compartido S3 y almacén de datos del almacén de Azure Blob.

* Si utiliza un *Entorno de zona protegida*, asegúrese de que su entorno esté actualizado y actualizado a la última versión. Si utiliza un *Entorno de producción*, se actualiza automáticamente.

* AEM Para iniciar una ingesta, debe pertenecer a la comunidad de usuarios de la **administradores** en la instancia de Cloud Service a la que está transfiriendo el contenido. Los usuarios sin privilegios no podrán iniciar ingestas sin proporcionar manualmente el token de migración.

* Si la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está activada, elimina todo el repositorio existente y crea un nuevo repositorio para introducir contenido en. Esto significa que restablece todos los ajustes, incluidos los permisos en la instancia del Cloud Service de destino. Esto también se aplica a un usuario administrador añadido a **administradores** grupo. El usuario debe volver a agregarse al **administradores** para recuperar el token de acceso para la herramienta de transferencia de contenido.

* Las ingestas no admiten la combinación de contenido de varias fuentes en la instancia del Cloud Service de destino si el contenido de las dos fuentes se mueve a las mismas rutas en el destino. Para mover contenido de varias fuentes a una sola instancia de Cloud Service de destino, debe asegurarse de que no haya superposición de las rutas de contenido de las fuentes.

* La clave de extracción es válida durante 14 días desde el momento en que se creó o renovó. Se puede renovar en cualquier momento. Si la clave de extracción ha caducado, no podrá realizar una extracción.

* La herramienta de transferencia de contenido (CTT) no realiza ningún tipo de análisis de contenido antes de transferir contenido de la instancia de origen a la instancia de destino. Por ejemplo, CTT no diferencia entre contenido publicado y no publicado al ingerir contenido en un entorno de publicación. El contenido especificado en el conjunto de migración se ingestará en la instancia de destino elegida. El usuario tiene la capacidad de introducir un conjunto de migración en una instancia de autor, una instancia de publicación o ambas. Se recomienda que, al mover contenido a una instancia de producción, CTT se instale en la instancia de autor de origen para mover contenido a la instancia de autor de destino y, de forma similar, instale CTT en la instancia de publicación de origen para mover contenido a la instancia de publicación de destino. Consulte [Ejecución de la herramienta de transferencia de contenido en una instancia de publicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.md?lang=en#running-ctt-on-publish) para obtener más información.

* Los usuarios y grupos transferidos por la herramienta de transferencia de contenido son solo aquellos que el contenido requiere para satisfacer los permisos. El _Extracción_ El proceso copia el `/home` al conjunto de migración y realiza Asignación de usuarios agregando un campo creado a partir de la dirección de correo electrónico de cada usuario. Para obtener más información, consulte [Asignación de usuarios y migración de principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).  El _Ingesta_ process copia todos los usuarios y grupos a los que se hace referencia en las ACL de contenido migradas.

* Durante la fase de extracción, la herramienta de transferencia de contenido se ejecuta en una instancia de origen de AEM activa.

* Después de completar la *Extracción* fase del proceso de transferencia de contenido y antes de iniciar la *Fase de ingesta* AEM para introducir contenido en el archivo as a Cloud Service de la *Fase* o *Producción* En algunos casos, deberá registrar un ticket de asistencia técnica para notificar al Adobe de su intención de ejecutar *Ingesta* para que el Adobe pueda garantizar que no se produzcan interrupciones durante la *Ingesta* proceso. Deberá registrar el ticket de asistencia 1 semana antes de lo previsto *Ingesta* fecha. Una vez que haya enviado la solicitud de asistencia, el equipo de asistencia le proporcionará instrucciones sobre los pasos siguientes. Puede registrar un ticket de asistencia técnica con los siguientes detalles:

   * Fecha exacta y hora estimada (con su zona horaria) en que planea iniciar la *Ingesta* fase.
   * Tipo de entorno (fase o producción) en el que planea introducir los datos.
   * ID de programa.

* El *Fase de ingesta* para el autor reduce la implementación de todo el autor. Esto significa que el autor de AEM no estará disponible durante todo el proceso de inserción. Asegúrese también de que no se ejecuten canalizaciones de Cloud Manager mientras ejecuta *Ingesta* fase.

* Al utilizar `Amazon S3` o `Azure` AEM al igual que el almacén de datos en el sistema de fuentes de datos, el almacén de datos debe configurarse para que los blobs almacenados no se puedan eliminar (recolección de basura). Esto garantiza la integridad de los datos de índice y si no se configura de esta manera, pueden producirse extracciones fallidas debido a la falta de integridad de estos datos de índice.

* Si utiliza índices personalizados, debe asegurarse de configurar los índices personalizados con `tika` antes de ejecutar la herramienta de transferencia de contenido. Consulte [Preparación de la nueva definición de índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=es#preparing-the-new-index-definition) para obtener más información.

* Si tiene intención de realizar recargas, es esencial que la estructura de contenido del contenido existente no cambie desde el momento en que se realiza la extracción inicial hasta el momento en que se ejecuta la extracción superior. Las recargas no se pueden ejecutar en contenido cuya estructura se haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

* Si tiene intención de incluir versiones como parte de un conjunto de migración y realiza recargas con `wipe=false`, debe deshabilitar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.

* Un conjunto de migración caducará después de un período prolongado de inactividad, después del cual sus datos ya no estarán disponibles. Consulte las [Caducidad del conjunto de migración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) para obtener más información.

## Siguientes pasos {#whats-next}

Una vez que haya aprendido las directrices, las prácticas recomendadas y las consideraciones importantes para utilizar la herramienta de transferencia de contenido, ya puede instalarla y utilizarla, empezando por la creación de un conjunto de migración. Consulte [Introducción a la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) para obtener más información.
