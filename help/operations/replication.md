---
title: Replicación
description: Obtenga información acerca de la distribución y la resolución de problemas de replicación en AEM as a Cloud Service.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
feature: Operations
role: Admin
source-git-commit: d6555eebfa13a400f084ef4edefb92b4471adcac
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 13%

---

# Replicación {#replication}

Adobe Experience Manager as a Cloud Service usa la capacidad [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) para mover el contenido que se va a replicar a un servicio de canalización que se ejecute en Adobe Developer que esté fuera del tiempo de ejecución de AEM.

>[!NOTE]
>
>Lectura [Distribución](/help/overview/architecture.md#content-distribution) para obtener más información.

## Métodos de publicación de contenido {#methods-of-publishing-content}

>[!NOTE]
>
>Si le interesa publicar contenido en lotes, cree un flujo de trabajo con el [Paso del flujo de trabajo de activación de árbol](/help/operations/tree-replication-workflows.md#tree-activation), que puede administrar de manera eficiente las cargas útiles grandes.
>No se recomienda crear su propio código personalizado de publicación en lotes.
>Si debe personalizar por cualquier motivo, puede almacenar en déclencheur un flujo de trabajo con este paso mediante las API de flujo de trabajo existentes.
>Siempre es recomendable publicar solo el contenido que se debe publicar. Y sea prudente al no intentar publicar grandes cantidades de contenido, si no es necesario. Sin embargo, no hay límites en cuanto a la cantidad de contenido que se puede enviar a través de flujos de trabajo con el paso de flujo de trabajo de activación de árbol.

### Cancelación/publicación rápida: cancelación/publicación planeada {#publish-unpublish}

Esta función le permite publicar las páginas seleccionadas inmediatamente, sin las opciones adicionales posibles a través del enfoque Administrar publicación.

Para obtener más información, consulte [Administrar publicación](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### Horas de activación y desactivación: configuración del activador {#on-and-off-times-trigger-configuration}

Las posibilidades adicionales de **Tiempo de activación** y **Tiempo de inactividad** están disponibles en la [Pestaña básica de propiedades de página](/help/sites-cloud/authoring/sites-console/page-properties.md#basic).

Para realizar la replicación automática de esta característica, habilite **Replicar automáticamente** en la [configuración OSGi](/help/implementing/deploying/configuring-osgi.md) **Configuración del Déclencheur de activación/desactivación**:

![Configuración del activador de activación de OSGi](/help/operations/assets/replication-on-off-trigger.png)

### Administrar publicación {#manage-publication}

Administrar publicación ofrece más opciones que Publicación rápida, pues permite incluir páginas secundarias, personalizar las referencias e iniciar cualquier flujo de trabajo aplicable, además de poder publicar más adelante.

Al incluir los elementos secundarios de una carpeta para la opción &quot;publicar más tarde&quot; se invoca el flujo de trabajo Publicar árbol de contenido, descrito en [Flujos de trabajo de replicación de árbol](/help/operations/tree-replication-workflows.md#publish-content-tree-workflow).

Puede encontrar información más detallada sobre Administrar publicación en la [Documentación de aspectos básicos de la publicación](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

Para replicar jerarquías de contenido profundo de forma masiva, utilice un método basado en flujos de trabajo. Consulte [Flujos de trabajo de replicación de árbol](/help/operations/tree-replication-workflows.md) para ver el paso recomendado del flujo de trabajo de activación de árbol, los parámetros de configuración y las instrucciones de supervisión. El flujo de trabajo obsoleto Publicar árbol de contenido también se documenta allí como referencia.

### API de replicación {#replication-api}

Puede publicar contenido mediante la API de replicación que aparece en AEM as a Cloud Service.

Para obtener más información, consulte la [Documentación de la API](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

**Uso básico de la API**

```
@Reference
Replicator replicator;
@Reference
ReplicationStatusProvider replicationStatusProvider;

....
Session session = ...
// Activate a single page to all agents, which are active by default
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en");
// Activate multiple pages (but try to limit it to approx 100 at max)
replicator.replicate(session,ReplicationActionType.ACTIVATE, new String[]{"/content/we-retail/en","/content/we-retail/de"});

// ways to get the replication status
Resource enResource = resourceResolver.getResource("/content/we-retail/en");
Resource deResource = resourceResolver.getResource("/content/we-retail/de");
ReplicationStatus enStatus = enResource.adaptTo(ReplicationStatus.class);
// if you need to get the status for more than 1 resource at once, this approach is more performant
Map<String,ReplicationStatus> allStatus = replicationStatusProvider.getBatchReplicationStatus(enResource,deResource);
```

**Agentes de replicación**

AEM as a Cloud Service proporciona dos agentes de replicación predefinidos que enrutan el contenido de autor a un nivel de destino a través de Sling Content Distribution:

* **publicar**: replica el contenido activado en el nivel de publicación activa. Este agente está habilitado de forma predeterminada y se utiliza al publicar desde la interfaz de usuario, los flujos de trabajo o la API de replicación, a menos que especifique lo contrario.
* **preview**: replica el contenido en el nivel de vista previa para que los autores puedan revisar los cambios antes de que se activen. Este agente no está habilitado de forma predeterminada.

Puede ver y supervisar ambos agentes desde **Herramientas** > **Implementación** > **Distribución**:

![Agentes de distribución que muestran publicación y previsualización](/help/operations/assets/replication-agents.png "Agentes de distribución")

Al seleccionar una tarjeta de agente, se abre su estado, los registros y [detalles de la cola](#replication-queues).

**Replicación con agentes específicos**

Al replicar con la API como se muestra arriba, solo se usan los agentes habilitados de forma predeterminada; es decir, solo **publicar** en AEM as a Cloud Service. Para replicar exclusivamente en el nivel de vista previa, pase un `AgentFilter` que seleccione el agente de vista previa:

Consulte el siguiente ejemplo:

```
private static final String PREVIEW_AGENT = "preview";

ReplicationStatus beforeStatus = enResource.adaptTo(ReplicationStatus.class); // beforeStatus.isActivated == false

ReplicationOptions options = new ReplicationOptions();
options.setFilter(new AgentFilter() {
  @Override
  public boolean isIncluded (Agent agent) {
    return agent.getId().equals(PREVIEW_AGENT);
  }
});
// will replicate only to preview
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en", options);

ReplicationStatus afterStatus = enResource.adaptTo(ReplicationStatus.class); // afterStatus.isActivated == false
ReplicationStatus previewStatus = afterStatus.getStatusForAgent(PREVIEW_AGENT); // previewStatus.isActivated == true
```

Si replica sin `AgentFilter`, solo se usa **publish** y el nivel de vista previa no se ve afectado.

El `ReplicationStatus` general de un recurso se actualiza solamente cuando la replicación incluye al menos un agente habilitado de manera predeterminada. En el ejemplo anterior, solo se usó **preview**, de modo que `ReplicationStatus.isActivated` permanece `false`. Use `getStatusForAgent()` para comprobar el estado de un agente específico; por ejemplo, `getStatusForAgent("preview")` después de una replicación de solo vista previa o `getStatusForAgent("publish")` para el nivel de publicación activa.

### Métodos de invalidación de contenido {#invalidating-content}

Puede invalidar contenido directamente utilizando Invalidación de contenido de Sling (SCD) del autor (el método preferido) o utilizando la API de replicación para invocar el agente de replicación de vaciado de Dispatcher de publicación. Consulte la página [Almacenamiento en caché](/help/implementing/dispatcher/caching.md) para obtener más información.

**Límites de capacidad de API de replicación**

Repita menos de 100 rutas a la vez, siendo 500 el límite. Por encima del límite, se arroja un `ReplicationException`.
Si la lógica de la aplicación no requiere replicación atómica, este límite se puede superar configurando `ReplicationOptions.setUseAtomicCalls` como false, que acepta cualquier número de rutas, pero crea bloques internamente para permanecer por debajo de este límite.

El tamaño del contenido transmitido por llamada de replicación no debe superar `10 MB`. Esta regla incluye los nodos y las propiedades, pero no ningún binario (los paquetes de flujo de trabajo y los paquetes de contenido se consideran binarios).


## Colas de replicación {#replication-queues}

Cada agente de replicación muestra dos colas de replicación. AEM as a Cloud Service ya no muestra una cola independiente para cada pod de publicación: el nivel de publicación se adapta automáticamente, por lo que las colas por pod añaden complejidad sin ninguna ventaja práctica. El estado de la cola se consolida de la siguiente manera:

* **persistente**: el cambio se almacena de forma duradera en el nivel de publicación. Una vez que un elemento borra esta cola, el contenido se mantiene; las instancias de publicación alcanzan un estado coherente a lo largo del tiempo.
* **publicado completamente**: el cambio está activo en todos los pods de publicación y la caché de Dispatcher se borra para las rutas afectadas. Cuando un elemento borra esta cola, los visitantes reciben el contenido actualizado.

### Supervisar colas de replicación {#monitor-replication-queues}

1. Desde la [navegación global](/help/sites-cloud/authoring/basic-handling.md#global-navigation) de AEM, vaya a **Herramientas** > **Implementación**.

   ![Navegar a Distribución desde Herramientas](/help/operations/assets/replication-agent-navigation.png "Navegación de distribución")

1. Seleccione **Distribución** y, a continuación, abra la tarjeta del agente **publicar** o **previsualizar**.

1. En la ficha **Estado**, compruebe que todas las colas tengan un estado correcto. Revisa **elementos pendientes** para el trabajo que está a la espera de procesarse y **Último elemento procesado** para la actividad reciente.

   ![Colas de replicación que muestran persistentes y totalmente publicadas](/help/operations/assets/replication-queues.png "Colas de replicación")

1. Seleccione **Probar conexión** para comprobar que el agente puede contactar con el servicio de distribución.
1. Seleccione la ficha **Registros** para ver el historial de publicaciones de contenido.

   ![Registros de replicación](/help/operations/assets/publish-logs.png "Registros")

## Resolución de problemas {#troubleshooting}

Si el contenido no se puede publicar, la publicación se revierte desde el servicio de publicación de AEM. Use [Supervisar colas de replicación](#monitor-replication-queues) para abrir la ficha **Estado** del agente e identificar la cola afectada.

Cuando una cola muestra un estado rojo, revise sus elementos pendientes para averiguar la causa del error. Seleccione la cola para ver los elementos pendientes y, a continuación, borre los elementos individuales o toda la cola si es necesario.
