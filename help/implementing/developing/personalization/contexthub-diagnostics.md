---
title: Diagnóstico de ContextHub
description: ContextHub proporciona una página de diagnóstico en la que puede ver una descripción general del marco de trabajo de ContextHub
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Diagnóstico de ContextHub {#contexthub-diagnostics}

ContextHub proporciona una página de diagnóstico en la que puede ver una descripción general del marco de trabajo de ContextHub. Para abrir la página, vaya a `contexthub.diagnostics.html` AEM de la instancia de autor de la, por ejemplo:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

La página Diagnósticos de ContextHub proporciona información sobre los almacenes y los módulos de interfaz de usuario que se han creado, las carpetas de la biblioteca de cliente que se cargan y los vínculos a páginas útiles.

>[!NOTE]
>
>Para que se devuelva la información de diagnóstico, debe habilitarse el modo de depuración; de lo contrario, la página de diagnósticos está en blanco. Consulte [este documento](configuring-contexthub.md#debugging-contexthub) para obtener más información sobre cómo habilitar el modo de depuración.

## Tiendas {#stores}

La sección Tiendas enumera todas las tiendas de ContextHub que se han configurado. Cada elemento de la lista consta de la siguiente información:

* **Título:** El [tipo de tienda](sample-stores.md) en el que se basa el almacén.
* **ruta:** La ruta al nodo del repositorio que contiene la configuración.
* **resourceType:** Ruta del nodo del repositorio donde se define el tipo de almacén.
* **clientlibs:** Las categorías de las bibliotecas de cliente cargadas que implementan el tipo de almacén.

## Módulos {#modules}

La sección Módulos enumera todos los módulos de interfaz de usuario de ContextHub que se han configurado. Cada elemento de la lista consta de la siguiente información:

* **Título:** El [Tipo de módulo de IU](sample-modules.md) en el que se basa el módulo de interfaz de usuario.
* **ruta:** La ruta al nodo del repositorio que contiene la configuración.
* **resourceType:** Ruta del nodo del repositorio donde se define el tipo de módulo de interfaz de usuario.
* **clientlibs:** Las categorías de las bibliotecas de cliente cargadas que implementan el tipo de módulo de interfaz de usuario.

## Clientlibs {#clientlibs}

La sección Clientlibs lo enumera todo[carpetas de la biblioteca del cliente](/help/implementing/developing/introduction/clientlibs.md) que ContextHub ha cargado. Las bibliotecas de cliente se clasifican de la siguiente manera:

* **kernel.js:** Bibliotecas de cliente que implementan el marco de trabajo de ContextHub, el motor de segmentos y los tipos de almacén.
* **ui.js:** Bibliotecas de cliente que implementan los tipos de módulos de IU e IU de ContextHub.
* **style.css:** Archivos CSS cargados desde bibliotecas de cliente.

## URL {#urls}

La sección Direcciones URL contiene vínculos a funciones de ContextHub:

* **Editor de configuración:** Abre el [Página Configuración de ContextHub](configuring-contexthub.md) donde puede configurar tiendas, modos de interfaz de usuario y módulos de interfaz de usuario.
* **Configuración de los módulos de ContextHub:** Abre el `/etc/cloudsettings/default/contexthub.config.kernel.js` , que contiene la representación de objeto JavaScript de las configuraciones del almacén de ContextHub.
* **Configuración de la IU de ContextHub:** Abre el `/etc/cloudsettings/default/contexthub.config.ui.js` , que contiene la representación de objeto JavaScript de las configuraciones del modo de IU de ContextHub.
* **kernel.js:** Abre el `/etc/cloudsettings/default/contexthub.kernel.js` , que contiene el código fuente de las bibliotecas de cliente que implementan el marco de trabajo de ContextHub, el motor de segmentos y los tipos de almacén.
* **ui.js:** Abre el `/etc/cloudsettings/default/contexthub.ui.js` , que contiene el código fuente de las bibliotecas de cliente que implementan los tipos de módulos de IU e IU de ContextHub.
* **style.css:** Abre el `/etc/cloudsettings/default/contexthub.styles.css` , que contiene los estilos CSS para los módulos de IU e IU de ContextHub.
