---
title: Diagnóstico de ContextHub
description: ContextHub proporciona una página de diagnóstico en la que puede ver información general sobre el marco de ContextHub
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# Diagnóstico de ContextHub {#contexthub-diagnostics}

ContextHub proporciona una página de diagnóstico en la que puede ver información general del marco de ContextHub. Para abrir la página, vaya a `contexthub.diagnostics.html` de la instancia de autor de AEM, por ejemplo:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

La página Diagnósticos de ContextHub proporciona información sobre las tiendas y los módulos de interfaz de usuario que se han creado, las carpetas de la biblioteca de cliente que se han cargado y los vínculos a páginas útiles.

>[!NOTE]
>
>Para que se devuelva la información de diagnóstico, el modo de depuración debe estar habilitado; de lo contrario, la página de diagnóstico estará en blanco. Consulte [este documento](configuring-contexthub.md#debugging-contexthub) para obtener más información sobre cómo habilitar el modo de depuración.

## Almacenes {#stores}

La sección Almacenes enumera todos los almacenes de ContextHub configurados. Cada elemento de la lista consta de la siguiente información:

* **Título:** La variable [tipo de tienda](sample-stores.md) en el que se basa la tienda.
* **ruta:** Ruta al nodo del repositorio que contiene la configuración.
* **resourceType:** Ruta del nodo del repositorio donde se define el tipo de almacén.
* **clientlibs:** Las categorías de bibliotecas de cliente que se cargan que implementan el tipo de tienda.

## Módulos {#modules}

La sección Módulos enumera todos los módulos de IU de ContextHub que se han configurado. Cada elemento de la lista consta de la siguiente información:

* **Título:** La variable [Tipo de módulo de interfaz de usuario](sample-modules.md) en el que se basa el módulo de IU.
* **ruta:** Ruta al nodo del repositorio que contiene la configuración.
* **resourceType:** Ruta del nodo del repositorio donde se define el tipo de módulo de interfaz de usuario.
* **clientlibs:** Las categorías de bibliotecas de cliente que se cargan que implementan el tipo de módulo de interfaz de usuario.

## Clientlibs {#clientlibs}

La sección Clientlibs enumera todas las [carpetas de bibliotecas de cliente](/help/implementing/developing/introduction/clientlibs.md) que ha cargado ContextHub. Las bibliotecas de cliente se categorizan de la siguiente manera:

* **kernel.js:** Bibliotecas de cliente que implementan el marco de ContextHub, el motor de segmentos y los tipos de almacén.
* **ui.js:** Bibliotecas de cliente que implementan los tipos de módulos UI y UI de ContextHub.
* **style.css:** Archivos CSS que se cargan desde bibliotecas de cliente.

## URL {#urls}

La sección URL contiene vínculos a las funciones de ContextHub:

* **Editor de configuración:** Abre el [Página de configuración de ContextHub](configuring-contexthub.md) donde puede configurar tiendas, modos de IU y módulos de IU.
* **Configuración de los módulos de ContextHub:** Abre el `/etc/cloudsettings/default/contexthub.config.kernel.js` , que contiene la representación de objeto Javascript de las configuraciones de almacén de ContextHub.
* **Configuración de la interfaz de usuario de ContextHub:** Abre el `/etc/cloudsettings/default/contexthub.config.ui.js` , que contiene la representación de objeto Javascript de las configuraciones de modo de interfaz de usuario de ContextHub.
* **kernel.js:** Abre el `/etc/cloudsettings/default/contexthub.kernel.js` , que contiene el código fuente de las bibliotecas de cliente que implementan el marco de ContextHub, el motor de segmentos y los tipos de almacén.
* **ui.js:** Abre el `/etc/cloudsettings/default/contexthub.ui.js` , que contiene el código fuente de las bibliotecas de cliente que implementan los tipos de módulo de interfaz de usuario y de ContextHub.
* **style.css:** Abre el `/etc/cloudsettings/default/contexthub.styles.css` , que contiene los estilos CSS para los módulos de IU y IU de ContextHub.
