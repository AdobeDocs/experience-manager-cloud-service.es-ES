---
title: Ejecución de la herramienta de transferencia de contenido en una instancia de publicación
description: Ejecución de la herramienta de transferencia de contenido en una instancia de publicación
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 11%

---

# Ejecución de la herramienta de transferencia de contenido en una instancia de publicación {#run-content-transfer-tool-publish-instance}

## Introducción {#introduction}

La herramienta de transferencia de contenido (CTT) no realiza ningún tipo de análisis de contenido antes de transferir contenido de la instancia de origen a la instancia de destino. Por ejemplo, CTT no diferencia entre contenido publicado y no publicado al ingerir contenido en un entorno de publicación. Independientemente del contenido especificado en el conjunto de migración, este se incorpora en la instancia de destino elegida. El usuario tiene la capacidad de introducir un conjunto de migración en una instancia de autor, una instancia de publicación o ambas.

>[!NOTE]
>Se recomienda que, al mover contenido a una instancia de Producción, la herramienta de transferencia de contenido se instale en la instancia de autor de origen para mover contenido a la instancia de autor de destino y, de forma similar, instale la herramienta de transferencia de contenido en la instancia de publicación de origen para mover contenido a la instancia de publicación de destino. Consulte [Enfoque recomendado](#recommended-approach) para obtener más información.

## Enfoque recomendado {#recommended-approach}

Siga el método recomendado como se describe a continuación:

* Utilice la misma versión de la herramienta de transferencia de contenido que se utilizó en la instancia de autor.

* Solo es necesario migrar un nodo de publicación único. Debe eliminarse del equilibrador de carga antes de comenzar la extracción.

* Durante la ingesta para publicar, el nivel de publicación no se reducirá (a diferencia del autor).

  >[!IMPORTANT]
  >Como precaución, evite cualquier operación de escritura iniciada por el usuario, como:
  > * AEM La distribución de contenido desde autor as a Cloud Service a Publish en ese entorno
  > * Sincronización de usuarios entre instancias de publicación
