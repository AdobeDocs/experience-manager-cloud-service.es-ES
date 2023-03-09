---
title: Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido (heredada)
description: Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido
hide: true
hidefromtoc: true
exl-id: 03449606-0fb4-4a9f-9abb-6b17c27a6046
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 14%

---

# Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido (heredada) {#guidelines}

## Directrices y prácticas recomendadas {#best-practices}

Siga esta sección para conocer las directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido:

* Ejecutar [Limpieza de revisión](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) y [comprobaciones de coherencia del almacén de datos](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=en) en el **origen** para identificar posibles problemas y reducir el tamaño del repositorio.

* AEM Si la configuración de la red de distribución de contenido (CDN) del Autor de la nube de está configurada para tener una lista de permitidos de direcciones IP, asegúrese de que las direcciones IP de entorno de origen también se añadan a la lista de permitidos. AEM Al hacerlo, se asegura de que el entorno de origen y el entorno de nube de puedan comunicarse entre sí.

* Ejecute la ingesta utilizando *barrido* modo habilitado en el que el repositorio existente (autor o publicación) en el entorno de AEM Cloud Service de destino se eliminará y luego se actualizará con los datos del conjunto de migración. Este modo es mucho más rápido que el modo sin borrado, donde el conjunto de migración se aplica sobre el contenido  existente.

* Una vez completada la actividad de transferencia de contenido, se requiere la estructura de proyecto correcta en el entorno de Cloud Service para garantizar que el contenido se procese correctamente en el entorno de Cloud Service.

* Antes de ejecutar la herramienta de transferencia de contenido, debe asegurarse de que haya suficiente espacio en disco en el `crx-quickstart` subdirectorio de la instancia de origen de AEM. Esto se debe a que la herramienta de transferencia de contenido crea una copia local del repositorio que se carga posteriormente en el conjunto de migración.
La fórmula general para calcular el espacio libre necesario en disco es la siguiente:
   `data store size + node store size * 1.5`

   * *tamaño del almacén de datos*: la herramienta de transferencia de contenido utiliza 64 GB, incluso si el almacén de datos real es más grande.
   * *tamaño del almacén de nodos*: el tamaño del directorio del almacén de segmentos o el tamaño de la base de datos MongoDB.
Por lo tanto, para un tamaño de almacén de segmentos de 20 GB, el espacio libre requerido en disco sería de 94 GB.

* Se debe mantener un conjunto de migración a lo largo de la actividad de transferencia de contenido para admitir recargas de contenido. Dado que se pueden crear y mantener un máximo de diez conjuntos de migración a la vez durante la actividad de transferencia de contenido, se recomienda dividir el repositorio de contenido en consecuencia. Al hacerlo, se asegura de que no se quede sin conjuntos de migración.

## Consideraciones importantes antes de utilizar la herramienta de transferencia de contenido {#important-considerations}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar la herramienta de transferencia de contenido:

* AEM El requisito mínimo del sistema para la herramienta de transferencia de contenido es de 6.3+ y Java™ 8, respectivamente. AEM AEM Si su versión es menor, debe actualizar el repositorio de contenido a la versión 6.5 para usar la herramienta de transferencia de contenido, que se encuentra en la versión 6.5.

* AEM Java™ debe configurarse en el entorno de para que la variable `java` AEM El comando lo puede ejecutar el usuario que lo inicia

* Desinstale las versiones anteriores de la herramienta de transferencia de contenido al instalar la versión 1.3.0 porque se ha producido un cambio importante de arquitectura en la herramienta. Con 1.3.0, también debe crear conjuntos de migración y volver a ejecutar la extracción y la ingesta en los nuevos conjuntos de migración.

* La herramienta Content Transfer Tool se puede utilizar con los siguientes tipos de almacén de datos: almacén de datos de archivos, almacén de datos S3, almacén de datos compartido S3 y almacén de datos del almacén de Azure Blob.

* Si utiliza un *Entorno de zona protegida*, asegúrese de que su entorno esté actualizado y actualizado a la última versión. Si utiliza un *Entorno de producción*, se actualiza automáticamente.

* AEM Para utilizar la herramienta de transferencia de contenido, debe ser un usuario administrador en su instancia de origen y pertenecer al grupo de trabajo local de la instancia de la instancia de la **administradores** en la instancia de Cloud Service a la que está transfiriendo el contenido. Los usuarios sin privilegios no pueden recuperar el token de acceso para utilizar la herramienta de transferencia de contenido.

* Si la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está activada, elimina todo el repositorio existente y crea un repositorio en el que introducir contenido. Este flujo de trabajo significa que restablece todos los ajustes, incluidos los permisos, en la instancia del Cloud Service de destino. Este resultado es verdadero incluso para un usuario administrador que se añade a **del administrador** grupo. El usuario debe leerse en el **del administrador** para recuperar el token de acceso para la herramienta de transferencia de contenido.

* La herramienta de transferencia de contenido no admite la combinación de contenido de varias fuentes en la instancia del Cloud Service de destino si el contenido de las dos fuentes se mueve a las mismas rutas en el destino. Para mover contenido de varias fuentes a una sola instancia de Cloud Service de destino, debe asegurarse de que no haya superposición de las rutas de contenido de las fuentes.

* El token de acceso puede caducar periódicamente después de un período de tiempo específico o después de que se haya actualizado el entorno del Cloud Service. Si el token de acceso ha caducado, no puede conectarse a la instancia de Cloud Service. En este caso, debe recuperar el nuevo token de acceso. El icono de estado asociado a un conjunto de migración existente cambia a una nube roja y muestra un mensaje cuando pasa el ratón por encima.

* La herramienta de transferencia de contenido (CTT) no realiza ningún tipo de análisis de contenido antes de transferir contenido de la instancia de origen a la instancia de destino. Por ejemplo, CTT no diferencia entre contenido publicado y no publicado al ingerir contenido en un entorno de publicación. Independientemente del contenido especificado en el conjunto de migración, este se incorpora en la instancia de destino elegida. El usuario puede introducir un conjunto de migración en una instancia de autor, una instancia de publicación o ambas. Al mover contenido a una instancia de producción, instale CTT en la instancia de autor de origen para mover contenido a la instancia de autor de destino. Del mismo modo, instale CTT en la instancia de publicación de origen para mover contenido a la instancia de publicación de destino. Consulte [Ejecución de la herramienta de transferencia de contenido en una instancia de publicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) para obtener más información.

* Los usuarios y grupos transferidos por la herramienta de transferencia de contenido son solo aquellos que el contenido requiere para satisfacer los permisos. El *Extracción* El proceso copia el `/home` en el conjunto de migración y la *Ingesta* process copia todos los usuarios y grupos a los que se hace referencia en las ACL de contenido migradas. Para asignar automáticamente los usuarios y grupos existentes a sus ID de IMS, consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).

* Durante la fase de extracción, la herramienta de transferencia de contenido se ejecuta en una instancia de origen de AEM activa.

* Después de completar la *Extracción* fase del proceso de transferencia de contenido y antes de iniciar la *Fase de ingesta* AEM para introducir contenido en el archivo as a Cloud Service de la *Fase* o *Producción* instancias, registre un ticket de asistencia. Notificar al Adobe de su intención de ejecutar *Ingesta* para que el Adobe pueda garantizar que no se produzcan interrupciones durante la *Ingesta* proceso. Registre el ticket de asistencia una semana antes de lo planeado *Ingesta* fecha. Una vez enviado el vale de soporte, el equipo de asistencia le indicará los pasos siguientes. Registre un ticket de asistencia con los siguientes detalles:

   * Fecha exacta y hora estimada (con su zona horaria) en que planea iniciar la *Ingesta* fase.
   * Tipo de entorno (fase o producción) en el que planea introducir los datos.
   * ID de programa.

* El *Fase de ingesta* para el autor reduce la implementación de todo el autor. AEM Este proceso significa que el autor no está disponible durante todo el proceso de ingesta de datos. Asegúrese también de que no se ejecuten canalizaciones de Cloud Manager mientras ejecuta *Ingesta* fase.

* Al utilizar `Amazon S3` o `Azure` AEM al igual que el almacén de datos en el sistema de fuentes de datos, el almacén de datos debe configurarse para que los blobs almacenados no se puedan eliminar (recolección de basura). Esto garantiza la integridad de los datos de índice y si no se configura de esta manera, pueden producirse extracciones fallidas debido a la falta de integridad de estos datos de índice.

* Si utiliza índices personalizados, debe asegurarse de configurar los índices personalizados con `tika` antes de ejecutar la herramienta de transferencia de contenido. Consulte [Preparación de la nueva definición de índice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en#preparing-the-new-index-definition) para obtener más información.

* Si tiene intención de realizar recargas, asegúrese de que la estructura de contenido del contenido existente no cambie desde el momento en que se realiza la extracción inicial hasta el momento en que se ejecuta la extracción superior. Las recargas no se pueden ejecutar en contenido cuya estructura se haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

* Si tiene intención de incluir versiones como parte de un conjunto de migración y realiza recargas con `wipe=false`, debe deshabilitar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.

## Siguientes pasos {#whats-next}

Una vez que haya aprendido las directrices, las prácticas recomendadas y las consideraciones importantes para utilizar la herramienta de transferencia de contenido, ya puede instalarla y utilizarla, empezando por la creación de un conjunto de migración. Consulte [Introducción a la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es) para obtener más información.
