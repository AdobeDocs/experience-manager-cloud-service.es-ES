---
title: Modo de desarrollador
seo-title: Developer Mode
description: El modo de desarrollador abre un panel lateral con varias pestañas que proporcionan a un desarrollador información sobre la página actual
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# Modo de desarrollador {#developer-mode}

Al editar páginas en AEM, varias [modos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) están disponibles, incluido el modo de desarrollador. El modo de desarrollador abre un panel lateral con varias pestañas que proporcionan a un desarrollador información técnica sobre la página actual.

Hay dos pestañas:

* **[Componentes](#components)** para ver la información de estructura y rendimiento.
* **[Errores](#errors)** para ver si se producen problemas.

Ayudan a los desarrolladores a:

* **Discover** composición de las páginas.
* **Depuración:** lo que está sucediendo donde y cuándo, lo que a su vez ayuda a resolver los problemas.

>[!NOTE]
>
>Modo de desarrollador:
>
>* No está disponible en dispositivos móviles o ventanas pequeñas en equipos de escritorio (debido a restricciones de espacio).
>  * Esto ocurre cuando la anchura es inferior a 1024 píxeles.
>* Solo está disponible para los usuarios que son miembros de la `administrators` grupo.


## Apertura del modo de desarrollador {#opening-developer-mode}

El modo de desarrollador se implementa como panel lateral en el editor de páginas. Para abrir el panel, seleccione **Desarrollador** desde el selector de modo en la barra de herramientas del editor de páginas:

![Apertura del modo de desarrollador](assets/developer-mode.png)

El panel se divide en dos pestañas:

* **[Componentes](#components)** : Muestra un árbol de componentes similar a la variable [árbol de contenido](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree) para autores
* **[Errores](#errors)** - Cuando se producen problemas, se muestran detalles de cada componente.

### Pestaña Componentes {#components}

![Ficha Componentes](assets/developer-mode-components-tab.png)

Muestra un árbol de componentes que:

* Describe la cadena de componentes y plantillas procesadas en la página. El árbol se puede expandir para mostrar el contexto dentro de la jerarquía.
* Muestra el tiempo de cálculo del lado del servidor necesario para procesar el componente.
* Permite expandir el árbol y seleccionar componentes específicos dentro del árbol. La selección proporciona acceso a los detalles del componente; como:
   * Ruta del repositorio
   * Vínculos a secuencias de comandos (se accede en el CRXDE Lite)
   * Detalles del componente como se ven en la sección [Consola Componentes](/help/sites-cloud/authoring/features/components-console.md)
* Los componentes seleccionados en el árbol se indican con un borde azul en el editor.

Esta pestaña de componentes ayuda a:

* Determine y compare el tiempo de procesamiento por componente.
* Consulte y comprenda la jerarquía.
* Comprenda y, a continuación, mejore el tiempo de carga de la página buscando componentes lentos.

Cada entrada de componente puede tener las siguientes opciones:

![Ejemplo de componente de modo de desarrollador](assets/developer-mode-component-example.png)

* **Ver detalles:** Vínculo a una lista que muestra:
   * Todos los scripts de componente utilizados para procesar el componente.
   * Ruta de contenido del repositorio para este componente específico.

      ![Ver detalles](assets/developer-mode-view-details.png)

* **Editar script:** Vínculo que abre el script de componente en CRXDE Lite.

* **Ver detalles del componente:** Abre los detalles del componente dentro del [Consola Componentes.](/help/sites-cloud/authoring/features/components-console.md)

La expansión de una entrada de componente tocando o haciendo clic en la cadena también puede mostrar:

    * La jerarquía dentro del componente seleccionado.
    * Tiempos de renderización para el componente seleccionado de forma aislada, cualquier componente individual anidado dentro de él y el total combinado.

### Ficha Errores {#errors}

![La pestaña errors](assets/developer-mode-errors-tab.png)

Con suerte, el **Errores** siempre estará vacía (como se ha indicado anteriormente), pero cuando se produzcan problemas, se podrán mostrar los siguientes detalles para cada componente:

* Una advertencia si el componente escribe una entrada en el registro de errores, junto con detalles del error y vínculos directos al código apropiado dentro del CRXDE Lite.
* Una advertencia si el componente abre una sesión de administrador.

Por ejemplo, si se llama a un método indefinido, el error resultante se mostrará en la variable **Errores** y la entrada de componente en el árbol del **Componentes** también se marcará con un indicador cuando se produzca un error.
