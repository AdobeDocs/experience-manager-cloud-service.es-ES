---
title: Ejecución de la herramienta de transferencia de contenido en una instancia de publicación (heredada)
description: Ejecución de la herramienta de transferencia de contenido en una instancia de publicación
hide: true
hidefromtoc: true
exl-id: 0a699dc1-9977-4cf9-a1b0-7b503ea2fc69
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 4%

---

# Ejecución de la herramienta de transferencia de contenido en una instancia de publicación (heredada) {#run-content-transfer-tool-publish-instance}

## Introducción {#introduction}

La herramienta de transferencia de contenido (CTT) no realiza ningún tipo de análisis de contenido antes de transferir contenido de la instancia de origen a la instancia de destino. Por ejemplo, CTT no diferencia entre contenido publicado y no publicado al ingerir contenido en un entorno de publicación. El contenido especificado en el conjunto de migración se ingestará en la instancia de destino elegida. El usuario tiene la capacidad de introducir un conjunto de migración en una instancia de autor, una instancia de publicación o ambas.

>[!NOTE]
>Se recomienda que, al mover contenido a una instancia de Producción, la herramienta de transferencia de contenido se instale en la instancia de autor de origen para mover contenido a la instancia de autor de destino y, de forma similar, instale la herramienta de transferencia de contenido en la instancia de publicación de origen para mover contenido a la instancia de publicación de destino. Consulte [Enfoque recomendado](#recommended-approach) para obtener más información.

## Enfoque recomendado {#recommended-approach}

Siga el método recomendado como se describe a continuación:

* Utilice la misma versión de la herramienta de transferencia de contenido que se utilizó en la instancia de autor.

* Solo es necesario migrar un nodo de publicación único. Debe eliminarse del equilibrador de carga antes de comenzar la extracción.

* AEM Al crear el conjunto de migración, utilice la dirección URL del entorno as a Cloud Service de creación de la aplicación de.

* Durante la ingesta para publicar, el nivel de publicación no se reducirá (a diferencia del autor).

   >[!IMPORTANT]
   >Como precaución, evite cualquier operación de escritura iniciada por el usuario, como:
   > * AEM La distribución de contenido desde autor as a Cloud Service a Publish en ese entorno
   > * Sincronización de usuarios entre instancias de publicación

