---
title: Uso del panel del sitio para administrar el tema del sitio
description: Conozca las potentes funciones del panel del sitio para ayudarle a personalizar y administrar fácilmente el tema del sitio.
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
solution: Experience Manager Sites
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 31%

---


# Uso del panel del sitio para administrar el tema del sitio {#site-panel}

{{traditional-aem}}

Conozca las potentes funciones del panel del sitio para ayudarle a personalizar y administrar fácilmente el tema del sitio.

## Información general {#overview}

El panel Sitio permite administrar los recursos de tema y plantilla del sitio. [Al igual que otros paneles](/help/sites-cloud/authoring/sites-console/console-side-panel.md), como el Árbol de contenido, Referencias o Línea de tiempo, el panel Sitio se muestra como el panel situado más a la izquierda en la consola Sitios y muestra información sobre el elemento seleccionado. A diferencia de otros paneles, el panel Sitio solo se aplica a las raíces del sitio.

El panel Sitio se utiliza para administrar la información relacionada con el tema y la plantilla para el sitio, que incluye:

* [Descarga de fuentes de temas](#downloading-theme-sources)
* [Descarga de recursos de plantilla, como mallas metálicas](#downloading-template-resources)
* [Visualización y cambio de versiones de temas](#theme-vrsions)
* [Activación de la canalización front-end](#enabling-the-front-end-pipeline)

>[!TIP]
>
>Consulte el [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para familiarizarse con la herramienta de creación rápida del sitio y la canalización de front-end con el fin de personalizar fácilmente el tema del sitio.

## Descarga de fuentes de temas {#downloading-theme-sources}

Cuando crea un sitio en AEM basado en una [plantilla del sitio](site-templates.md), puede descargar el [tema del sitio](site-themes.md) mediante el panel Sitio.

Con el panel Sitio en la consola Sitios, seleccione la raíz del sitio para mostrar la información del tema sobre el sitio.

![Descarga de fuentes de temas](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Seleccione **Descargar fuentes de temas** para descargar una copia local del tema del sitio como archivo `.zip` con fines de personalización.

## Descarga de recursos de plantilla {#downloading-template-resources}

[Plantillas de sitio](site-templates.md) pueden contener información además de la estructura de contenido del sitio y el [tema del sitio](site-themes.md). Las plantillas de sitio pueden contener diseños de malla metálica u otros archivos relacionados con el sitio, por ejemplo.

Si el sitio se basa en una plantilla de sitio, y el panel Sitio se muestra en la consola Sitios, seleccione la raíz del sitio para mostrar la información del tema sobre el sitio, incluidos los recursos del sitio adicionales.

![Descarga de fuentes de temas](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Seleccione el botón o los botones situados debajo del encabezado **Descargar recursos de plantilla adicionales** para descargar una copia local de los archivos disponibles.

## Visualización y cambio de versiones de temas {#them-versions}

Si el sitio se basa en una plantilla de sitio, es posible que su tema ya haya sido personalizado por el desarrollador del front-end. Con el panel Sitio, puede ver qué versión del tema del sitio está implementada actualmente y cambiar a versiones anteriores.

Con el panel Sitio en la consola Sitios, seleccione la raíz del sitio para mostrar la información del tema sobre el sitio.

![Versiones del sitio en el panel](/help/sites-cloud/administering/assets/theme-versions.png)

La versión actual del tema se muestra con su hash de compromiso junto con la marca de tiempo de su última actualización del estado.

Seleccione **Seleccionar versión** para ver las versiones anteriores del tema.

![Seleccionar la versión del tema](/help/sites-cloud/administering/assets/select-theme-versions.png)

Seleccione la versión a la que desee cambiar y, a continuación, seleccione **Aplicar** para realizar el cambio.

Si AEM detecta que se ha implementado una versión más reciente del tema a través de la canalización front-end, pero no se ha aplicado a su sitio, se mostrará un icono de notificación.

![Versión más reciente del indicador del tema](/help/sites-cloud/administering/assets/new-theme-version.png)

Puede usar el botón **Seleccionar versión** para actualizar a la nueva versión del tema.

## Activación de la canalización front-end {#enabling-front-end-pipeline}

Si el sitio no se creó con una plantilla de sitio, no es posible utilizar la canalización de front-end para personalizar e implementar su tema.

Sin embargo, puede habilitar la canalización front-end para su sitio mediante el panel Sitio.

Con el panel Sitio en la consola Sitios, seleccione la raíz del sitio para mostrar la información del tema sobre el sitio y, a continuación, seleccione **Habilitar canalización front-end**.

![Habilitar canalización front-end](/help/sites-cloud/administering/assets/enable-fep.png)

Para obtener más información, consulte el documento [Habilitar la canalización front-end](enable-front-end-pipeline.md).
