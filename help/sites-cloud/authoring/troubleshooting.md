---
title: Resolución de problemas de AEM durante la creación
description: AEM Algunos problemas que pueden producirse al utilizar el servicio de asistencia de
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 66%

---

# Resolución de problemas de AEM durante la creación {#troubleshooting-aem-when-authoring}

La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.

## La versión anterior de la página sigue en el sitio publicado {#old-page-version-still-on-published-site}

* **Problema**:
   * Ha realizado cambios en una página y publicado la página en el sitio de publicación, pero la versión *antigua* de la página todavía se muestra en el sitio de publicación.
* **Motivo**:
   * Esto puede tener varias causas, la mayoría de las veces la caché (el explorador local o Dispatcher), aunque a veces puede ser un problema con la cola de replicación.
* **Soluciones**:
   * Aquí hay varias posibilidades:
   * Confirme que la página se ha duplicado correctamente. Compruebe el estado de la página y, si es necesario, el estado de la cola de replicación.
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
