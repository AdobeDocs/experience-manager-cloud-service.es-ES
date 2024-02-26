---
title: Activación de la canalización front-end
description: Descubra cómo puede habilitar la canalización front-end para sitios existentes, a fin de utilizar los temas de sitios para personalizar más rápidamente el sitio.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 98%

---

# Activación de la canalización front-end {#enable-front-end-pipeline}

Descubra cómo puede habilitar la canalización front-end para sitios existentes, a fin de utilizar los temas de sitios para personalizar más rápidamente el sitio.

## Información general {#overview}

La canalización front-end es un mecanismo que puede implementar rápidamente solo el código front-end de sus sitios web en función de [temas de sitio](site-themes.md) y [plantillas de sitio.](site-templates.md)

En lugar de implementar el código full stack, solo el código front-end se gestiona mediante esta canalización, lo que hace que el proceso sea más rápido y permite a los desarrolladores de front-end personalizar su sitio de forma fácil y rápida sin tener conocimiento de AEM.

Los sitios basados en plantillas de sitio pueden utilizar la canalización front-end de forma predeterminada. Este documento describe cómo puede adaptar los sitios existentes para aprovechar la canalización front-end.

>[!TIP]
>
>Si no está familiarizado con la canalización front-end y con cómo implementar sitios rápidamente mediante ella y las plantillas de sitio, revise el [recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para una introducción.

Si no ha creado el sitio existente basado en plantillas y temas de sitio, AEM puede configurar el sitio para cargar los temas que se implementan con la canalización front-end por encima de las bibliotecas de cliente existentes.

## Detalles técnicos {#technical-details}

Al activar la canalización front-end para un sitio, AEM realiza los siguientes cambios en la estructura del sitio.

* Todas las páginas del sitio incluirán un archivo CSS y JS adicional, que se puede modificar mediante la implementación de actualizaciones a través de una canalización front-end de Cloud Manager dedicada.
* Los archivos CSS y JS añadidos inicialmente estarán vacíos, pero se puede descargar una carpeta de &quot;fuentes temáticas&quot; para arrancar la estructura de carpetas que permite implementar actualizaciones de código CSS y JS a través de esa canalización.
* Este cambio solo lo puede deshacer un desarrollador, eliminando los nodos `SiteConfig` y `HtmlPageItemsConfig` que esta operación crea debajo de `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Esta acción no convierte automáticamente las bibliotecas de cliente existentes del sitio para utilizar la canalización front-end. Mover estos orígenes de la carpeta de biblioteca del cliente a la carpeta de canalización front-end es una tarea que requiere el trabajo manual de un desarrollador de front-end.

## Requisitos  {#requirements}

AEM puede adaptar automáticamente el sitio existente para utilizar la canalización front-end. Para poder hacerlo, el sitio debe utilizar la versión [2 o posterior del componente de página de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html?lang=es).

## Activación de la canalización front-end {#enabling}

La activación del sitio se realiza desde la consola Sitios mediante el [carril del sitio.](site-rail.md)

1. Inicie sesión en AEM y navegue hasta su sitio a través de **Navegación global** > **Sitios**.
1. Seleccione el sitio en la consola. Seleccione la raíz del sitio y no cualquier página secundaria.
1. Con el sitio seleccionado, abra el [selector de carril](/help/sites-cloud/authoring/basic-handling.md#rail-selector) a la izquierda y elija **Sitio**.
1. En el carril del **sitio**, haga clic en el botón **Habilitar canalización front-end**.

   ![Habilitación de la canalización front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM le solicita que confirme los cambios que se realizarán con una descripción general. Confirme y su sitio estará adaptado.

Ahora su sitio está listo para usar la canalización front-end. Para obtener más información sobre la canalización front-end y la administración del tema del sitio, consulte lo siguiente:

* [Uso del carril del sitio para administrar el tema del sitio](site-rail.md)
* [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md): este recorrido de documentación le ofrece una visión general de principio a fin del proceso de implementación rápida de un sitio mediante la canalización front-end y la herramienta de creación rápida del sitio.
* [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end): este documento describe la canalización front-end en el contexto de las canalizaciones full-stack y de nivel web.
