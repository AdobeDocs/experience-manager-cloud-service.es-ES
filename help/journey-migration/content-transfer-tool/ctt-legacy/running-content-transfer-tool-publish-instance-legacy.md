---
title: Ejecución de la herramienta de transferencia de contenido en una instancia de publicación (heredada)
description: Ejecución de la herramienta de transferencia de contenido en una instancia de publicación
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 4%

---

# Ejecución de la herramienta de transferencia de contenido en una instancia de publicación (heredada) {#run-content-transfer-tool-publish-instance}

## Introducción {#introduction}

La herramienta de transferencia de contenido (CTT) no realiza ningún tipo de análisis de contenido antes de transferir contenido de la instancia de origen a la instancia de destino. Por ejemplo, CTT no diferencia entre contenido publicado y no publicado al ingerir contenido en un entorno de publicación. Sea cual sea el contenido especificado en el conjunto de migración, se incorporará en la instancia de destino elegida. El usuario tiene la capacidad de ingerir un conjunto de migración en una instancia de Autor, una instancia de Publicación o ambas.

>[!NOTE]
>Se recomienda que, al mover contenido a una instancia de producción, la herramienta de transferencia de contenido se instale en la instancia de autor de origen para mover contenido a la instancia de autor de destino y, de manera similar, instalar la herramienta de transferencia de contenido en la instancia de publicación de origen para mover contenido a la instancia de publicación de destino. Consulte [Enfoque recomendado](#recommended-approach) para obtener más información.

## Enfoque recomendado {#recommended-approach}

Siga el enfoque recomendado como se describe a continuación:

* Utilice la misma versión de la herramienta de transferencia de contenido que se utilizó en la instancia de autor.

* Solo es necesario migrar un nodo de publicación único. Debe eliminarse del equilibrador de carga antes de comenzar la extracción.

* Al crear el conjunto de migración, utilice la URL del entorno as a Cloud Service AEM autor.

* Durante la ingesta para publicar, el nivel de publicación no se reducirá (a diferencia del autor).

   >[!IMPORTANT]
   >Como precaución, evite cualquier operación de escritura iniciada por el usuario, como:
   > * Distribución de contenido de AEM Autor as a Cloud Service a Publicar en ese entorno
   > * Sincronización de usuarios entre instancias de publicación

