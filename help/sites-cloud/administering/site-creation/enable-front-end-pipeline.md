---
title: Activación de la canalización front-end
description: Descubra cómo puede habilitar la canalización de front-end para sitios existentes a fin de aprovechar los temas del sitio para personalizar más rápidamente el sitio.
feature: Administering
role: Admin
source-git-commit: 002b95212d682c41a601a483df9b4365a553b669
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---


# Activación de la canalización front-end {#enable-front-end-pipeline}

Descubra cómo puede habilitar la canalización de front-end para sitios existentes a fin de aprovechar los temas del sitio para personalizar más rápidamente el sitio.

## Información general {#overview}

La canalización front-end es un mecanismo que puede implementar rápidamente solo el código front-end de sus sitios web en función de [temas del sitio](site-themes.md) y [plantillas de sitio.](site-templates.md)

En lugar de implementar la pila completa, solo el código front-end se gestiona mediante esta canalización, lo que hace que el proceso sea más rápido y permite a los desarrolladores de front-end personalizar su sitio de forma fácil y rápida sin tener conocimiento de AEM.

Los sitios basados en plantillas de sitio pueden aprovechar la canalización de front-end de forma predeterminada. Este documento describe cómo puede adaptar los sitios existentes para aprovechar la canalización de front-end.

>[!TIP]
>
>Si no está familiarizado con la canalización del front-end y con cómo implementar rápidamente sitios mediante ella y las plantillas de sitio, revise la [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para una introducción.

Si no ha creado el sitio existente en función de las plantillas y los temas del sitio, AEM configurar el sitio para cargar los temas que se implementan con la canalización de front-end sobre las bibliotecas de cliente existentes.

## Detalles técnicos {#technical-details}

Al activar la canalización del front-end para un sitio, AEM realiza los siguientes cambios en la estructura del sitio.

* Todas las páginas del sitio incluirán un archivo CSS y JS adicional, que se puede modificar mediante la implementación de actualizaciones a través de una canalización front-end de Cloud Manager dedicada.
* Los archivos CSS y JS añadidos inicialmente estarán vacíos, pero se puede descargar una carpeta de &quot;fuentes temáticas&quot; para arrancar la estructura de carpetas que permite implementar actualizaciones de código CSS y JS a través de esa canalización.
* Este cambio solo lo puede deshacer un desarrollador, eliminando la variable `SiteConfig` y `HtmlPageItemsConfig` nodos que esta operación crea a continuación `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Esta acción no convierte automáticamente las bibliotecas de cliente existentes del sitio para utilizar la canalización de fin de fuente. Mover estos orígenes de la carpeta de biblioteca del cliente a la carpeta de canalización del front-end es una tarea que requiere el trabajo manual de un desarrollador del front-end.

## Requisitos {#requirements}

AEM adaptar automáticamente el sitio existente para utilizar la canalización front-end. Para poder hacerlo, el sitio debe utilizar [v2 o posterior del componente de página de los componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## Activación de la canalización front-end {#enabling}

La activación del sitio se realiza desde la consola Sitios mediante la [Carril del sitio.](site-rail.md)

1. Inicie sesión en AEM y navegue hasta su sitio a través de **Navegación global** > **Sitios**.
1. Seleccione el sitio en la consola. Debe seleccionar la raíz del sitio y no cualquier página secundaria.
1. Con el sitio seleccionado, abra el [selector de raíl](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) a la izquierda y elija **Sitio**.
1. En el **Sitio** carril , haga clic en el botón . **Habilitar canalización front-end**.

   ![Habilitar canalización front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM le solicita que confirme con una descripción general de los cambios que se realizarán. Confirme y su sitio está adaptado.

Ahora su sitio está listo para usar la canalización front-end. Para obtener más información sobre la canalización front-end y la administración del tema del sitio, consulte:

* [Uso del carril del sitio para administrar el tema del sitio](site-rail.md)
* [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) : Este recorrido de documentación le ofrece una visión general de principio a fin del proceso de implementación rápida de un sitio mediante la canalización front-end y la herramienta de creación rápida del sitio.
* [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) : Este documento describe la canalización front-end en el contexto de las canalizaciones de pila completa y de nivel web.
