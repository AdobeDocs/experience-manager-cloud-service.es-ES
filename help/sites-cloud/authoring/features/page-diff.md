---
title: 'Diferencias de página  '
description: La función Diferencias de página permite realizar una cómoda comparación en paralelo de dos páginas con las diferencias resaltadas.
translation-type: tm+mt
source-git-commit: b405e49cd883df1e2e9768bb9e4d6908afc443e2
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 97%

---


# Diferencias de página   {#page-diff}

## Introducción {#introduction}

La creación de contenido es un proceso iterativo. La creación con eficiencia de contenido requiere poder ver qué ha cambiado de una iteración a otra. Visualizar una versión de la página y luego otra es un proceso poco eficaz y propenso a errores. Un autor desea poder comparar fácilmente la página actual en paralelo con otra versión.

La función Diferencias de página permite realizar una cómoda comparación en paralelo de dos páginas con las diferencias resaltadas.

>[!NOTE]
>
>El usuario debe tener el permiso para **Modificar/Crear/Eliminar** en el nodo `/content/versionhistory` para poder utilizar la función.
>
>Consulte [Desarrollo y diferencia de página](/help/implementing/developing/introduction/page-diff.md#operation-details) para obtener más información técnica sobre esta función.

## Uso {#use}

La comparación de diferencias en paralelo permite comparar lo siguiente:

* [Versiones](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page): versión anterior de una página con el estado actual.
* Live Copies: Live Copy con su modelo.<!-- [Live Copies](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live Copy with its Blueprint-->
* [Lanzamientos](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page): lanzamiento con su origen.
* Copias de idioma: una página antes y después de la traducción.<!-- [Language Copies](/help/sites-administering/tc-manage.md#comparing-language-copies) - A page before and after (re-)translation-->

Consulte los temas correspondientes sobre cómo iniciar la comparación de diferencias en esos contextos.

### Presentación de diferencias    {#presentation-of-differences}

Independientemente del contenido que se va a comparar, la presentación de las diferencias sigue siendo la misma.

* El contenido seleccionado al iniciar la comparación de diferencias se muestra a la izquierda (punto de entrada de las diferencias).
* El contenido con el que se va a comparar se muestra a la derecha (elemento con el que se compara el contenido seleccionado).

Por ejemplo, si se comparan versiones, la versión actual se muestra a la izquierda y la versión anterior se muestra a la derecha.

El origen de ambas páginas se muestra claramente en la barra de encabezado de la parte superior de la ventana del navegador.

![Versiones en paralelo](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

La comparación de diferencias detecta los cambios en el nivel de componente y de HTML. Los elementos modificados se resaltan con colores diferentes.

**Cambios en los componentes** 

* Verde claro: componente añadido
* Rosa: componente eliminado

**Cambios en HTML** 

* Verde oscuro: HTML añadido
* Rojo: HTML eliminado

>[!NOTE]
>
>Al comparar copias de idioma, el resaltado está desactivado, ya que en una traducción cambia todo y el resaltado no proporcionará ninguna ventaja.

### Pantalla completa y salida    {#fullscreen-and-exiting}

Para centrarse en un contenido específico, puede hacer clic en el icono de pantalla completa para que cualquier &quot;lado&quot; de la comparación de diferencias en paralelo se amplíe en la ventana completa del navegador.

![Botón Pantalla completa](/help/sites-cloud/authoring/assets/versions-full-screen.png)

El lado seleccionado llenará toda la ventana, pero la barra permanecerá en la parte superior para que pueda cambiar entre las dos páginas.

![Modo de pantalla completa](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>Si el ancho del explorador no puede incluir ambos nombres de página en la vista de pantalla completa, solo se muestra el nombre de la página que aparece y el otro está disponible tras acceder al menú en los puntos suspensivos.

También puede cerrar la vista de pantalla completa haciendo clic en el icono para salir del modo de pantalla completa.

![Salir del modo de pantalla completa](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

Puede salir de la comparación de diferencias en paralelo en cualquier momento haciendo clic en el botón Cerrar del encabezado.

## Restricciones    {#limitations}

Hay algunas situaciones en las que la comparación de diferencias de la página quizás no detecte una diferencia de la forma esperada.

* Al realizar la comparación de diferencias de versiones y lanzamientos, no se tienen en cuenta componentes dinámicos como rutas de exploración, menús, listas de productos o logotipos (componentes que se basan en la estructura del sitio para procesar su contenido).
* Para las versiones, la diferencia no vuelve a crear la directiva de control de acceso ni las relaciones de Live Copy.
* Si se mueve una página, ya no se puede realizar una diferencia con ninguna versión hecha antes del movimiento.
   * Si tiene problemas con una diferencia, compruebe la [línea de tiempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) para ver si la página se ha movido.

>[!NOTE]
>
>Las versiones no se pueden comparar entre sí. Solo la versión actual se puede comparar con otras versiones de la página. La versión actual siempre es la versión que se resalta con los cambios.

>[!NOTE]
>
>Para obtener más información sobre cómo funciona el mecanismo de diferencia de página, así como las limitaciones que pueden afectar a dicho mecanismo, consulte la [documentación para desarrolladores](/help/implementing/developing/introduction/page-diff.md) de esta función.
