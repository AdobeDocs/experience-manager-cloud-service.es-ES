---
title: El componente RemotePage
description: SPA AEM El componente RemotePage es un componente de página personalizado para editar el grupo de informes de React de forma remota dentro de los grupos de informes de.
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# El componente RemotePage {#remote-page-component}

Al decidir [qué nivel de integración](/help/implementing/developing/headful-headless.md) SPA AEM SPA AEM Si desea tener entre el recurso externo y el de la, a menudo resulta claro que necesita poder ver y editar el recurso de la en el propio usuario de la aplicación. El componente RemotePage es un componente de página personalizado solo para este propósito.

## Información general {#overview}

El componente RemotePage obtiene todos los recursos necesarios del contenido generado por la aplicación `asset-manifest.json` SPA AEM y utiliza esto para procesar los dentro de la.

* SPA AEM RemotePage permite insertar los scripts y las hojas de estilo de una página en el cuerpo de un componente de página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la aplicación.
* AEM SPA Los componentes de front-end virtuales permiten marcar secciones como editables en el editor de.
* SPA AEM Juntos, un alojado en un dominio diferente se puede convertir en editable en el espacio de trabajo de la aplicación de la versión de.

Consulte el artículo [SPA AEM Edición de una externa dentro de un grupo de informes](editing-external-spa.md) SPA AEM para obtener más información sobre las funciones editables y externas, haga clic en.

## Requisitos  {#requirements}

* Habilitar CORS en desarrollo
* Configurar URL remota en Propiedades de página
* SPA AEM Procesar la en el
* La aplicación web debe utilizar un manifiesto de recurso de paquete como uno de los siguientes y exponer un `asset-manifest.json` archivo en la raíz de dominio que enumera en un `entrypoints property` todos los archivos CSS y JS que se van a cargar:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
     ![ejemplo de propiedad entrypoints](assets/asset-manifest-entrypoints.png)
* La aplicación debe poder inicializarse en un `<div id="root"></div>` debajo del `body` Elemento. Si se espera un marcado diferente para que la aplicación cree una instancia, esto debe ajustarse en consecuencia en los scripts HTL del componente proxy que tenga un `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Restricciones {#limitations}

* El componente RemotePage espera que la implementación proporcione un manifiesto de recurso como el siguiente [encontrado aquí.](https://github.com/shellscape/webpack-manifest-plugin) Sin embargo, el componente RemotePage solo se ha probado para que funcione con el marco de React (y Next.js mediante el componente remote-page-next) y, por lo tanto, no admite la carga remota de aplicaciones desde otros marcos, como el Angular.
* El CSS interno definido en el archivo HTML AEM raíz de la aplicación y el CSS en línea en el nodo DOM raíz no estarán disponibles al realizar el procesamiento remoto en el.

## Detalles técnicos {#technical-details}

AEM SPA Al igual que el resto del proyecto de, el componente RemotePage es de código abierto. Para obtener todos los detalles técnicos del componente RemotePage, [consulte el repositorio de GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
