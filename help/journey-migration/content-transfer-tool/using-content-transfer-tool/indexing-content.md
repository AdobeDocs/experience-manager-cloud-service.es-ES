---
title: Indexación después de migrar contenido
description: Descubra cómo el proceso de migración indexará el contenido ingerido en la instancia del Cloud Service de destino.
exl-id: a13d5df4-b351-410a-9336-1b34a8af21b6
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 9%

---

# Indexación después de migrar contenido {#Indexing-content}

## Indexación {#aem-indexing-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_indexing"
>title="Indexación de contenido"
>abstract="La indexación de AEM hace referencia a la indexación del contenido en la instancia de Cloud Service después de migrar el contenido a ella. La indexación es necesaria para permitir la búsqueda de contenido en esa instancia."

Una vez que Cloud Acceleration Manager haya completado la ingesta de contenido en la instancia de Cloud Service, estará listo para utilizarse. Inicialmente, el contenido no se indexa, lo que probablemente resulte en un entorno inestable en el que se pueden esperar problemas como contenido inexplorable y rendimiento degradado. Para obtener un rendimiento óptimo en la instancia, el proceso de migración iniciará automáticamente la indexación del contenido. No hay nada que hacer, excepto monitorizar el progreso de indexación.

> Para obtener información sobre cómo iniciar una ingesta, consulte [Ingesta de contenido en el Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

Los siguientes pasos muestran el flujo general que puede esperar ver en la interfaz de usuario durante la indexación. Algunas etiquetas proporcionan un contexto útil en la información sobre herramientas, por lo que asegúrese de pasar el ratón por encima de los elementos para obtener más información sobre el estado de indexación actual.

Para empezar, vaya a Cloud Acceleration Manager. Haga clic en la tarjeta del proyecto y, a continuación, en la tarjeta Transferencia de contenido. Vaya a **Trabajos de ingesta** y vea los trabajos enumerados.

>[!NOTE]
>Puede ver o descargar los registros de indexación mediante las acciones del trabajo de ingesta, utilizando la lista desplegable ... . Los registros estarán disponibles en el
> Sección de acciones &quot;Registro de indexación&quot;, una vez completado el trabajo de indexación

### Pendiente

Así es como aparecerá la fila del trabajo de ingesta cuando se esté ejecutando, antes de que se haya iniciado el trabajo de indexación. No se requiere ninguna acción por parte del usuario. Si la ingesta falla por cualquier motivo, la cola del trabajo de índice se rescindirá y no se iniciará.

![imagen](/help/journey-migration/content-transfer-tool/assets-indexing/pending.png)

### En ejecución

Cuando la ingesta se realiza correctamente, el trabajo de indexación se inicia automáticamente. AEM La fila del trabajo de ingesta mostrará un icono de progreso para el estado de indexación de la. Puede abrir el cuadro de diálogo de duración para ver el progreso del trabajo.

![imagen](/help/journey-migration/content-transfer-tool/assets-indexing/running.png)

### Completado

Cuando el trabajo de indexación se realiza correctamente, la instancia está lista para utilizarse con un rendimiento óptimo. En este punto, los registros del trabajo de indexación están disponibles para verlos o descargarlos para inspeccionarlos.

![imagen](/help/journey-migration/content-transfer-tool/assets-indexing/complete.png)

### Errores

La indexación de la instancia del Cloud Service de destino muy probablemente se realizará correctamente. En algunos casos, puede fallar y la fila del trabajo de ingesta aparecerá de la siguiente manera. En todos los casos, puede encontrar algunos detalles del error pasando el ratón por encima del estado del error y puede proporcionar más información para ayudarle a determinar los pasos siguientes. En este punto, los registros del trabajo de indexación están disponibles para verlos o descargarlos para descubrir el origen del error. Si el siguiente paso no está claro, póngase en contacto con el Soporte técnico de Adobe e incluya detalles sobre la ingesta y el registro de indexación.

>[!TIP]
>
> Si el trabajo de indexación parece estar ejecutándose demasiado tiempo, asegúrese de que no se haya aplicado una Lista de permitidos [IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) a través de Cloud Manager, ya que impide que Cloud Acceleration Manager llegue al servicio de migración.

![imagen](/help/journey-migration/content-transfer-tool/assets-indexing/failed.png)

## Siguientes pasos {#whats-next}

Una vez indexada la instancia del servicio en la nube de destino, puede ver los registros de los trabajos de indexación y buscar detalles y errores.

La migración se ha completado. Pueden comenzar las pruebas y la validación de la instancia del servicio en la nube de destino.
