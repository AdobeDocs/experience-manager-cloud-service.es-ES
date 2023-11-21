---
title: Creación de componentes
description: AEM Los componentes de se utilizan para mantener, dar formato y representar el contenido disponible en las páginas web. Siga esta página para obtener más información sobre la creación de canales y el procesamiento de componentes.
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 3%

---

# Creación de componentes {#creating-components}

AEM Los componentes de se utilizan para mantener, dar formato y representar el contenido disponible en las páginas web.

## Creación de canales {#authoring-channels}

El canal es el objeto central del contenido enviado a un conjunto de pantallas. Por lo tanto, un autor de contenido suele abrir un canal en el editor para agregar o modificar contenido. Dado que el canal es un ***cq:Page*** seguirá el mismo patrón de experiencia de usuario tradicional para añadir y cambiar componentes en el canal.

Sin embargo, dado que los componentes de un canal suelen procesarse a pantalla completa, la experiencia de creación se verá afectada al intentar editar componentes únicos o componer nuevos pedidos. Por lo tanto, el canal dependerá de los selectores para procesar diferentes vistas de los componentes. El entorno de creación utiliza el selector de edición para activar el procesamiento del canal personalizado.

Por ejemplo, `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

El usuario no tiene que encargarse de añadir el selector a la URL durante la edición. Una lógica del lado del cliente escucha el evento del conmutador de capa y agrega el selector si el canal tiene el tipo de recurso dedicado *screens/core/components/channel.*

## Componentes de procesamiento {#rendering-components}

Para permitir una creación adecuada, los componentes deben proporcionar las dos representaciones siguientes:

| **Componente** | **Representaciones** |
|---|---|
| *my-component/my-component.html* | renderización de producción |
| *my-component/edit.html* | edición del procesamiento en una vista más pequeña |

Los componentes integrados utilizan las siguientes categorías de biblioteca de cliente:

| **Componente** | **Biblioteca de cliente** |
|---|---|
| *cq.screens.components.edit* | CSS y JS que deben cargarse durante la creación |
| *cq.screens.components.production* | CSS y JS que deben cargarse cuando se está ejecutando el canal |
| *cq.screens.components* | CSS y JS compartidos |

>[!NOTE]
>
>Para desarrollar componentes personalizados, utilice el ***[Plantilla de componente de muestra de AEM Screens](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***.
