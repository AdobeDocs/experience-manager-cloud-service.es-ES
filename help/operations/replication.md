---
title: Replicación
description: Distribución y Resolución de problemas de replicación.
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---


# Replicación {#replication}

Adobe Experience Manager como servicio de nube utiliza la capacidad [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) para mover el contenido que se va a replicar a un servicio de canalización que se ejecuta en Adobe I/O y que está fuera del tiempo de ejecución de AEM.

>[!NOTE]
>
> Lea [Distribución](/help/core-concepts/architecture.md#content-distribution) para obtener más información.

## Métodos de publicación de contenido {#methods-of-publishing-content}

### Cancelación/Publicación Rápida: Cancelación/Publicación Planificada {#publish-unpublish}

Estas funcionalidades estándar de AEM para los autores no cambian con el servicio de nube de AEM.

### Activación de árbol {#tree-activation}

Para realizar una activación de árbol:

1. En el menú Inicio de AEM, vaya a **Herramientas > Implementación > Distribución**
2. Seleccione la tarjeta **forwardPublisher**
3. Una vez en la interfaz de usuario de la consola web de forwardPublisher, **seleccione Distribuir**

   ![](assets/distribute.png "DistribuirDistribuir")
4. Seleccione la ruta en el explorador de rutas, elija agregar un nodo, árbol o eliminar según sea necesario y seleccione **Enviar**

## Solución de problemas {#troubleshooting}

Para solucionar problemas de replicación, vaya a las colas de replicación en la interfaz de usuario web de AEM Author Service:

1. En el menú Inicio de AEM, vaya a **Herramientas > Implementación > Distribución**
2. Seleccione la tarjeta **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Compruebe el estado de la cola, que debería ser verde
4. Puede probar la conexión al servicio de replicación
5. Seleccione la ficha **Registros** que muestra el historial de publicaciones de contenido

![](assets/logs.png "LogsLogs")

Si no se pudo publicar el contenido, toda la publicación se recupera del servicio de publicación de AEM.
En ese caso, las colas deben revisarse para identificar qué elementos causaron la cancelación de la publicación. Al hacer clic en una cola que muestra un estado rojo, se mostrará la cola con elementos pendientes, desde la cual se pueden borrar todos o uno de los elementos si es necesario.
