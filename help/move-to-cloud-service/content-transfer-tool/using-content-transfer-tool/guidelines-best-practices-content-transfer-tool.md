---
title: Directrices y prácticas recomendadas para el uso de la herramienta de transferencia de contenido
description: Directrices y prácticas recomendadas para el uso de la herramienta de transferencia de contenido
source-git-commit: b421cc5e6078112adecb856d723a1bae628d8ec7
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 25%

---


# Directrices y prácticas recomendadas para el uso de la herramienta de transferencia de contenido {#guidelines}

## Directrices y prácticas recomendadas {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Directrices y prácticas recomendadas"
>abstract="Revise las directrices y las prácticas recomendadas para utilizar la herramienta de transferencia de contenido, incluidas las tareas de limpieza de revisiones, consideraciones sobre el espacio en disco y más."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Consideraciones importantes sobre el uso de la herramienta de asignación de usuarios"

Siga esta sección para conocer las directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido:

* Es aconsejable ejecutar [Revision Cleanup](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) y [las comprobaciones de coherencia del almacén de datos](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) en el repositorio de **origen** para identificar posibles problemas y reducir el tamaño del repositorio.

* Si la configuración de la red de distribución de contenido (CDN) del Autor de AEM Cloud está configurada para tener una lista blanca de direcciones IP, debe asegurarse de que las direcciones IP de entorno de origen también se incluyan en la lista de permitidos para que el entorno de origen y el entorno de AEM Cloud puedan comunicarse entre sí.

* En la fase de ingesta se recomienda ejecutarla mediante el modo de *borrado* activado, en el que el repositorio existente (autor o publicación) en el entorno de Cloud Service de AEM de destinatario se eliminará por completo y, a continuación, se actualizará con los datos del conjunto de migración. Este modo es mucho más rápido que el modo sin borrado, donde el conjunto de migración se aplica sobre el contenido  existente.

* Una vez completada la actividad de transferencia de contenido, se requiere la estructura de proyecto correcta en el entorno de Cloud Service para garantizar que el contenido se procese correctamente en el entorno de Cloud Service.

* Antes de ejecutar la herramienta de transferencia de contenido, debe asegurarse de que haya suficiente espacio en disco en el `crx-quickstart` subdirectorio de la instancia de origen de AEM. Esto se debe a que la herramienta de transferencia de contenido crea una copia local del repositorio que se carga posteriormente en el conjunto de migración.
La fórmula general para calcular el espacio en disco necesario es la siguiente:
   `data store size + node store size * 1.5`

   * *tamaño del almacén de datos*: la herramienta de transferencia de contenido utiliza 64 GB, incluso si el almacén de datos real es más grande.
   * *tamaño del almacén de nodos*: el tamaño del directorio del almacén de segmentos o el tamaño de la base de datos MongoDB.
Por lo tanto, para un tamaño de almacén de segmentos de 20 GB, el espacio libre requerido en disco sería de 94 GB.

* Es necesario mantener un conjunto de migraciones a lo largo de toda la actividad de transferencia de contenido para que admita las recargas de contenido. Dado que se puede crear y mantener un máximo de diez conjuntos de migración a la vez durante la actividad de transferencia de contenido, se recomienda dividir el repositorio de contenido en consecuencia para garantizar que no se queden sin conjuntos de migración.

## Consideraciones importantes antes de usar la herramienta de transferencia de contenido {#important-considerations}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar la herramienta de transferencia de contenido:

* El requisito mínimo del sistema para la herramienta de transferencia de contenido es AEM 6.3+ y JAVA 8. Si su versión de AEM es anterior, debe actualizar el repositorio de contenido a AEM 6.5 para utilizar la herramienta de transferencia de contenido.

* Java debe configurarse en el entorno de AEM para que el usuario que inicia AEM pueda ejecutar el comando `java`.

* Se recomienda desinstalar las versiones anteriores de la herramienta de transferencia de contenido al instalar la versión 1.3.0, ya que se ha producido un cambio importante en la arquitectura de la herramienta. Con 1.3.0, también debe crear nuevos conjuntos de migración y volver a ejecutar la extracción y la ingesta en los nuevos conjuntos de migración.

* La herramienta de transferencia de contenido se puede utilizar con los siguientes tipos de almacén de datos: Almacén de datos de archivos, almacén de datos S3, almacén de datos compartido S3 y almacén de datos del blob de Azure.

* Si utiliza un *Entorno de espacio aislado*, asegúrese de que su entorno esté actualizado y actualizado a la última versión. Si utiliza un *Entorno de producción*, se actualiza automáticamente.

* Para utilizar la herramienta de transferencia de contenido, debe ser un usuario administrador en la instancia de origen y pertenecer al grupo local de AEM **administradores** en la instancia de Cloud Service a la que esté transfiriendo el contenido. Los usuarios sin privilegios no podrán recuperar el token de acceso para utilizar la herramienta de transferencia de contenido.

* Si la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está habilitada, elimina todo el repositorio existente y crea un nuevo repositorio en el que introducir contenido. Esto significa que restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino. Esto también se aplica a los usuarios administradores agregados al grupo **administradores**. Para recuperar el token de acceso para CTT, el usuario debe volver a agregarse al grupo **administradores** .

* El token de acceso puede caducar periódicamente después de un período de tiempo específico o después de actualizar el entorno del Cloud Service. Si el token de acceso ha caducado, no podrá conectarse a la instancia de Cloud Service y deberá recuperar el nuevo token de acceso. El icono de estado asociado con un conjunto de migración existente cambiará a una nube roja y mostrará un mensaje cuando pase el ratón por encima de él.

* La herramienta de transferencia de contenido (CTT) no realiza ningún tipo de análisis de contenido antes de transferir contenido de la instancia de origen a la instancia de destino. Por ejemplo, CTT no diferencia entre contenido publicado y no publicado al ingerir contenido en un entorno de publicación. Sea cual sea el contenido especificado en el conjunto de migración, se incorporará en la instancia de destino elegida. El usuario tiene la capacidad de ingerir un conjunto de migración en una instancia de Autor, una instancia de Publicación o ambas. Se recomienda que, al mover contenido a una instancia de Producción, CTT se instale en la instancia de Autor de origen para mover contenido a la instancia de Autor de destino y, de manera similar, instale CTT en la instancia de Publicación de origen para mover contenido a la instancia de Publicación de destino. Consulte [Ejecución de la herramienta de transferencia de contenido en una instancia de publicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) para obtener más información.

* Los usuarios y grupos que transfiere la herramienta de transferencia de contenido son solo aquellos que necesita el contenido para satisfacer los permisos. El proceso *Extraction* copia todo el `/home` en el conjunto de migración y el proceso *Ingestion* copia todos los usuarios y grupos a los que se hace referencia en las ACL de contenido migrado. Para asignar automáticamente los usuarios y grupos existentes a sus ID de IMS, consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Durante la fase de extracción, la herramienta de transferencia de contenido se ejecuta en una instancia de origen de AEM activa.

* Después de completar la fase *Extraction* del proceso de transferencia de contenido y antes de iniciar la *Fase de ingesta* para introducir contenido en las instancias as a Cloud Service de *Stage* o *Production* de AEM, deberá registrar un ticket de asistencia para notificar al Adobe su intención de ejecutar la *Ingesta* para que el Adobe pueda garantizar que no se produzcan interrupciones durante el proceso *Ingestion*. Tendrá que registrar el ticket de soporte 1 semana antes de la fecha planificada *Ingesta*. Una vez que haya enviado el ticket de soporte, el equipo de soporte le proporcionará instrucciones sobre los pasos siguientes. Puede registrar un vale de soporte con los siguientes detalles:

   * Fecha exacta y hora estimada (con su zona horaria) en la que planea iniciar la fase *Ingesta*.
   * Tipo de entorno (fase o producción) en el que planea introducir datos.
   * ID del programa.

* La *Fase de ingesta* para el autor reduce la implementación de todo el autor. Esto significa que el autor de AEM no estará disponible durante todo el proceso de inserción. Asegúrese también de que no se ejecutan canalizaciones de Cloud Manager mientras está ejecutando la fase *Ingesta*.

* Al utilizar `Amazon S3` o `Azure` como almacén de datos en el sistema de AEM de origen, el almacén de datos debe configurarse de modo que los blobs almacenados no se puedan eliminar (se recopilará la basura). Esto garantiza la integridad de los datos de índice y si no se configuran de esta manera, pueden producirse extracciones fallidas debido a la falta de integridad de estos datos de índice.

* Si está utilizando índices personalizados, debe asegurarse de configurar los índices personalizados con el nodo `tika` antes de ejecutar la herramienta de transferencia de contenido. Consulte [Preparación de la nueva definición del índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) para obtener más información.

* Si tiene intención de realizar recargas, es esencial que la estructura de contenido del contenido existente no cambie desde el momento en que se toma la extracción inicial hasta cuando se ejecuta la extracción superior. Las superposiciones no se pueden ejecutar en contenido cuya estructura haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

* Si tiene intención de incluir versiones como parte de un conjunto de migración y realiza complementos con `wipe=false`, debe desactivar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.

## Siguientes pasos {#whats-next}

Una vez que conozca las directrices, las prácticas recomendadas y las consideraciones importantes sobre el uso de la herramienta de transferencia de contenido, ya estará listo para instalar y utilizar la herramienta, empezando por la creación de un conjunto de migración. Consulte [Introducción a la transferencia de contenido a](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) para obtener más información.
