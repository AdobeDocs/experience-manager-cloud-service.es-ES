---
title: Uso del carril del sitio para administrar el tema del sitio
description: Conozca las potentes funciones del carril del sitio para ayudarle a personalizar y administrar fácilmente el tema del sitio.
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 95%

---

# Uso del carril del sitio para administrar el tema del sitio {#site-rail}

Conozca las potentes funciones del carril del sitio para ayudarle a personalizar y administrar fácilmente el tema del sitio.

## Información general {#overview}

El carril del sitio permite administrar los recursos de tema y plantilla del sitio. [Como otros raíles](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) como el árbol de contenido, las referencias o los raíles de cronología, el carril del sitio se muestra como el panel situado más a la izquierda en la consola Sitios y muestra información sobre el elemento seleccionado. A diferencia de otros carriles, el carril del sitio solo se aplica a las raíces del sitio.

El carril del sitio se utiliza para administrar la información relacionada con el tema y la plantilla para su sitio, que incluye:

* [Descarga de fuentes de temas](#downloading-theme-sources)
* [Descarga de recursos de plantilla, como mallas metálicas](#downloading-template-resources)
* [Visualización y cambio de versiones de temas](#theme-vrsions)
* [Activación de la canalización front-end](#enabling-the-front-end-pipeline)

>[!TIP]
>
>Consulte el [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para familiarizarse con la herramienta de creación rápida del sitio y la canalización de front-end con el fin de personalizar fácilmente el tema del sitio.

## Descarga de fuentes de temas {#downloading-theme-sources}

Cuando crea un sitio en AEM basado en una [plantilla de sitio,](site-templates.md) puede descargar su [tema del sitio](site-themes.md) mediante el carril del sitio.

Con el carril del sitio en la consola Sitios, seleccione la raíz del sitio para mostrar la información del tema sobre el sitio.

![Descargar fuentes de temas](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Toque o haga clic en **Descargar fuentes de temas** para descargar una copia local del tema del sitio como `.zip` archivo para fines de personalización.

## Descarga de recursos de plantilla {#downloading-template-resources}

[Plantillas de sitio](site-templates.md) puede contener información además de la estructura de contenido del sitio y [tema del sitio.](site-themes.md) Las plantillas de sitio pueden contener diseños de malla metálica u otros archivos relacionados con el sitio, por ejemplo.

Si el sitio se basa en una plantilla de sitio, y el carril del sitio se muestra en la consola Sitios, seleccione la raíz del sitio para mostrar la información del tema sobre el sitio, incluidos los recursos del sitio adicionales.

![Descargar fuentes de temas](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Toque o haga clic en los botones situados debajo del encabezado **Descargar recursos de plantilla adicionales** para descargar una copia local de los archivos disponibles.

## Visualización y cambio de versiones de temas {#them-versions}

Si el sitio se basa en una plantilla de sitio, es posible que su tema ya haya sido personalizado por el desarrollador del front-end. Con el carril del sitio, puede ver qué versión del tema del sitio está implementada actualmente y cambiar a versiones anteriores.

Con el carril del sitio en la consola Sitios, seleccione la raíz del sitio para mostrar la información del tema sobre el sitio.

![Versiones del sitio en el carril](/help/sites-cloud/administering/assets/theme-versions.png)

La versión actual del tema se muestra con su hash de compromiso junto con la marca de tiempo de su última actualización del estado.

Haga clic o pulse **Seleccionar versión** para ver las versiones anteriores de la temática.

![Seleccionar la versión del tema](/help/sites-cloud/administering/assets/select-theme-versions.png)

Toque o haga clic en la versión a la que desee cambiar y, a continuación, toque o haga clic en **Aplicar** para realizar el cambio.

Si AEM detecta que se ha implementado una versión más reciente del tema a través de la canalización front-end, pero no se ha aplicado a su sitio, se mostrará un icono de notificación.

![Versión más reciente del indicador del tema](/help/sites-cloud/administering/assets/new-theme-version.png)

Puede usar el botón **Seleccionar versión** para actualizar a la nueva versión del tema.

## Activación de la canalización front-end {#enabling-front-end-pipeline}

Si el sitio no se creó con una plantilla de sitio, no es posible utilizar la canalización de front-end para personalizar e implementar su tema.

Sin embargo, puede habilitar la canalización front-end para su sitio mediante el carril del sitio.

Con el carril del sitio en la consola Sitios, seleccione la raíz del sitio para mostrar la información del tema sobre el sitio y, a continuación, toque o haga clic en **Habilitar canalización front-end**.

![Habilitar canalización front-end](/help/sites-cloud/administering/assets/enable-fep.png)

Para obtener más información, consulte el documento [Activación de la canalización front-end.](enable-front-end-pipeline.md)
