---
title: Diagnósticos de ContextHub
description: ContextHub proporciona una página de diagnóstico en la que puede ver una descripción general del marco de ContextHub
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Diagnósticos de ContextHub {#contexthub-diagnostics}

ContextHub proporciona una página de diagnóstico donde puede ver una descripción general del marco de ContextHub. Para abrir la página, vaya a la `contexthub.diagnostics.html` página de la instancia de creación de AEM, por ejemplo:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

La página Diagnósticos de ContextHub proporciona información sobre las tiendas y los módulos de interfaz de usuario que se han creado, las carpetas de la biblioteca de cliente que se han cargado y los vínculos a páginas útiles.

>[!NOTE]
>
>Para que se devuelva la información de diagnóstico, se debe habilitar el modo de depuración; de lo contrario, la página de diagnóstico estará en blanco. Consulte [este documento](configuring-contexthub.md#debugging-contexthub) para obtener detalles sobre cómo habilitar el modo de depuración.

## Tiendas {#stores}

La sección Tiendas lista todos los almacenes de ContextHub configurados. Cada elemento de la lista consta de la siguiente información:

* **Título:** Tipo [de](sample-stores.md) tienda en el que se basa la tienda.
* **path:** Ruta al nodo del repositorio que contiene la configuración.
* **resourceType:** Ruta del nodo del repositorio donde se define el tipo de almacén.
* **clientlibs:** Las categorías de las bibliotecas de cliente que se cargan y que implementan el tipo de almacén.

## Módulos {#modules}

La sección Módulos lista todos los módulos de interfaz de usuario de ContextHub configurados. Cada elemento de la lista consta de la siguiente información:

* **Título:** Tipo [de módulo de](sample-modules.md) interfaz de usuario en el que se basa el módulo de interfaz de usuario.
* **path:** Ruta al nodo del repositorio que contiene la configuración.
* **resourceType:** Ruta del nodo del repositorio donde se define el tipo de módulo de interfaz de usuario.
* **clientlibs:** Las categorías de las bibliotecas de cliente que se cargan que implementan el tipo de módulo de interfaz de usuario.

## Clientlibs {#clientlibs}

La sección Clientlibs lista todas las carpetas [de la biblioteca de](/help/implementing/developing/introduction/clientlibs.md) cliente que ha cargado ContextHub. Las bibliotecas cliente se clasifican de la siguiente manera:

* **kernel.js:** Bibliotecas de clientes que implementan el marco de ContextHub, el motor de segmentos y los tipos de tiendas.
* **ui.js:** Bibliotecas de clientes que implementan los tipos de módulos UI y UI de ContextHub.
* **style.css:** Archivos CSS que se cargan desde bibliotecas de cliente.

## URL {#urls}

La sección de direcciones URL contiene vínculos a las funciones de ContextHub:

* **Editor de configuración:** Abre la página [de configuración de](configuring-contexthub.md) ContextHub, donde puede configurar tiendas, modos de interfaz de usuario y módulos de interfaz de usuario.
* **Configuración de los módulos de ContextHub:** Abre el `/etc/cloudsettings/default/contexthub.config.kernel.js` archivo, que contiene la representación del objeto Javascript de las configuraciones de la tienda de ContextHub.
* **Configuración de la interfaz de usuario de ContextHub:** Abre el `/etc/cloudsettings/default/contexthub.config.ui.js` archivo, que contiene la representación del objeto Javascript de las configuraciones del modo de interfaz de usuario de ContextHub.
* **kernel.js:** Abre el `/etc/cloudsettings/default/contexthub.kernel.js` archivo, que contiene el código fuente de las bibliotecas cliente que implementan el marco de ContextHub, el motor de segmentos y los tipos de tienda.
* **ui.js:** Abre el `/etc/cloudsettings/default/contexthub.ui.js` archivo, que contiene el código fuente de las bibliotecas cliente que implementan los tipos de módulos UI y UI de ContextHub.
* **style.css:** Abre el `/etc/cloudsettings/default/contexthub.styles.css` archivo, que contiene los estilos CSS de la interfaz de usuario y los módulos de interfaz de usuario de ContextHub.
