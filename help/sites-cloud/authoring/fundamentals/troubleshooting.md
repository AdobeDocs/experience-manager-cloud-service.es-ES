---
title: Resolución de problemas de AEM durante la creación
description: Algunos problemas que pueden producirse al utilizar AEM
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---

# Resolución de problemas de AEM durante la creación {#troubleshooting-aem-when-authoring}

La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.

## La versión anterior de la página sigue en el sitio publicado {#old-page-version-still-on-published-site}

* **Problema**:
   * Ha realizado cambios en una página y publicado la página en el sitio de publicación, pero la versión *antigua* de la página todavía se muestra en el sitio de publicación.
* **Motivo**:
   * Puede haber varios motivos. Normalmente es la caché (su navegador local o Dispatcher), aunque a veces puede haber un problema con la cola de replicación.
* **Soluciones**:
   * Hay varias posibilidades:
   * Confirme que la página se haya replicado correctamente. Compruebe el estado de la página y, si es necesario, el estado de la cola de replicación.
   * Borre la caché del navegador local y vuelva a acceder a la página.
   * Añada `?` al final de la URL de la página. Por ejemplo:
      * `http://<host>:<port>/sites.html/content?`
      * Esta acción solicitará la página directamente desde AEM y omitirá a Dispatcher. Si recibe la página actualizada quiere decir que debe borrar la caché de Dispatcher.
   * Póngase en contacto con el administrador del sistema si hay problemas con las colas de replicación.

## Acciones aplicables a los componentes no visibles en la barra de herramientas {#component-actions-not-visible-on-toolbar}

* **Problema**:
   * La gama completa de acciones aplicables a los componentes no aparece visible al editar una página de contenido en el entorno de creación. 
* **Motivo**:
   * En casos excepcionales, una acción anterior podría afectar a la barra de herramientas.
* **Solución**:
   * Actualice la página.
