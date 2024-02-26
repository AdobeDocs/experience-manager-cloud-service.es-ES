---
title: Limitaciones de Deshacer y Rehacer
description: AEM Obtenga información acerca de las limitaciones de las opciones Deshacer y Rehacer en el editor de páginas de la página de.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 92%

---


# Limitaciones de Deshacer y Rehacer {#undo-redo}

AEM almacena un historial de las acciones que realiza y la secuencia en que las realizó, de modo que puede deshacer varias acciones en el orden en que se realizaron y rehacerlas para volver a aplicar una o más acciones.

Si hay un elemento seleccionado en la página de contenido (por ejemplo, un componente de texto), el comando para deshacer o rehacer se aplica a dicho elemento.

El comportamiento de los comandos Deshacer y Rehacer es similar al de otros programas. Utilice los comandos para restaurar el estado reciente de la página web a medida que toma decisiones sobre el contenido. Por ejemplo, si mueve un párrafo de texto a una ubicación diferente en la página, puede usar el comando Deshacer para mover el párrafo a la posición original. Si más tarde decide que la posición anterior era mejor, use el comando rehacer para “deshacer la acción”.

Por ejemplo, puede:

* Rehacer acciones se usa siempre y cuando no haya realizado ninguna edición en la página desde que usó el comando Deshacer por última vez.
* Deshacer un máximo de 20 acciones de edición (configuración predeterminada).
* También utilice los [métodos abreviados del teclado](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) para deshacer y rehacer.

Puede usar los comandos Deshacer y Rehacer para los siguientes tipos de cambios de página:

* Añadir, editar, quitar y mover párrafos
* Editar contenido de párrafos in-situ
* Copiar, cortar y pegar elementos en una página

>[!NOTE]
>
>* Se necesitan permisos especiales para deshacer y rehacer cambios en archivos e imágenes.
>* El historial de cambios en archivos e imágenes dura un mínimo de diez horas. No obstante, pasado ese tiempo, no se garantiza que se puedan deshacer los cambios. El administrador puede modificar el plazo predeterminado de diez horas.
>* El administrador del sistema puede configurar varios aspectos de las funciones de Deshacer/Rehacer según los requisitos de la instancia.
