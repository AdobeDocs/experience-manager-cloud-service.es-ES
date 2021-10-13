---
title: Uso de la herramienta de transferencia de contenido
description: Uso de la herramienta de transferencia de contenido
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 57%

---

# Uso de la herramienta de transferencia de contenido {#using-content-transfer-tool}

## Ejecución de la herramienta de transferencia de contenido en una instancia de publicación {#running-ctt-on-publish}

Se recomienda que, al mover contenido a una instancia de Publish, CTT se instale en la instancia de Publish de origen para mover contenido a la instancia de Publish de destino. Siga el enfoque recomendado como se describe a continuación:

* Utilice la misma versión del CTT que se utilizó en la instancia de autor.

* Solo es necesario migrar un nodo de publicación único. Debe eliminarse del equilibrador de carga antes de comenzar la extracción.

* Al crear el conjunto de migración, utilice la URL del entorno AEMaaCS de autor.

* Durante la ingesta para publicar, el nivel de publicación NO se reducirá (a diferencia del autor). Como precaución, evite cualquier operación de escritura iniciada por el usuario, como:

   * Distribución de contenido de AEMaaCS Author para publicar en ese entorno
   * Sincronización de usuarios entre instancias de publicación


## Solución de problemas {#troubleshooting}

### ID de blob faltantes {#missing-blobs}

Si se notifican identificaciones de blob faltantes como se menciona a continuación, entonces es necesario ejecutar una prueba de consistencia en el repositorio existente y restaurar los blobs que faltan.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Se ejecuta el siguiente comando:

>[!NOTE]
>
>`--verbose` se necesita el indicador para informar de las rutas de nodos desde donde se hace referencia a los blobs.

**Para repositorios AEM 6.5 (Oak 1.8 y posteriores)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Para repositorios con Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Consulte [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para obtener más detalles.

Los archivos creados en *OUT_DIR* especificados anteriormente para mantener la consistencia se pueden comprobar en busca de rutas en las que falten binarios y acciones adecuadas como restaurar desde una copia de seguridad, eliminar las rutas, volver a indexar, etc.


### Comportamiento de la IU {#ui-behavior}

Como usuario, es posible que vea los siguientes cambios de comportamiento en la IU (IU) para la herramienta de transferencia de contenido:

* Es posible que los iconos de la IU de la herramienta de transferencia de contenido sean diferentes de las capturas de pantalla que se muestran en esta guía o que no se muestren en absoluto según la versión de la instancia de origen de AEM.
