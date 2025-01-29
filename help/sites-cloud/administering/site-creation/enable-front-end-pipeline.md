---
title: Activación de la canalización front-end
description: Descubra cómo puede habilitar la canalización front-end para que los sitios existentes utilicen temas del sitio para personalizar el sitio más rápidamente.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: a5661b6b75180dd77eb794eb5d215fd2e1d5eed0
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 39%

---

# Activación de la canalización front-end {#enable-front-end-pipeline}

Descubra cómo puede habilitar la canalización front-end para que los sitios existentes utilicen temas del sitio para personalizar el sitio más rápidamente.

## Información general {#overview}

La canalización front-end es un mecanismo que puede implementar rápidamente solo el código front-end de sus sitios web en función de [temas de sitio](site-themes.md) y [plantillas de sitio.](site-templates.md)

Esta canalización solo administra el código front-end, lo que hace que el proceso de implementación sea más rápido que las implementaciones de pila completa. AEM Permite a los desarrolladores de front-end personalizar el sitio fácilmente sin necesidad de tener conocimientos de las características de la interfaz de usuario de la aplicación

Los sitios basados en plantillas de sitio pueden utilizar la canalización front-end de forma predeterminada. Este documento describe cómo puede adaptar los sitios existentes para aprovechar la canalización front-end.

>[!TIP]
>
>Si no está familiarizado con la canalización front-end y con cómo implementar sitios rápidamente mediante ella y las plantillas de sitio, consulte [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para obtener una introducción.

AEM Puede configurar el sitio para que cargue temas implementados con la canalización front-end, incluso si el sitio no se creó con plantillas de sitio y temas, colocándolos sobre las bibliotecas de cliente existentes.

## Detalles técnicos {#technical-details}

Al activar la canalización front-end para un sitio, AEM realiza los siguientes cambios en la estructura del sitio.

* Todas las páginas del sitio incluyen un archivo CSS y JS adicional, que se puede modificar mediante la implementación de actualizaciones a través de una canalización front-end de Cloud Manager dedicada.
* Los archivos CSS y JS añadidos inicialmente están vacíos. Sin embargo, puede descargar una carpeta &quot;fuentes temáticas&quot; para configurar la estructura de carpetas necesaria para implementar actualizaciones de código CSS y JS a través de la canalización.
* Solo un desarrollador puede deshacer el cambio eliminando los nodos `SiteConfig` y `HtmlPageItemsConfig` que esta operación crea debajo de `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Esta acción no convierte automáticamente las bibliotecas de cliente existentes del sitio para utilizar la canalización front-end. Mover estos orígenes de la carpeta de biblioteca del cliente a la carpeta de canalización front-end es una tarea que requiere el trabajo manual de un desarrollador de front-end.

## Requisitos  {#requirements}

AEM puede adaptar automáticamente el sitio existente para utilizar la canalización front-end. Para poder realizar este flujo de trabajo, el sitio debe utilizar [v2 o una versión posterior del componente de página de los componentes principales.](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/page)

## Activación de la canalización front-end {#enabling}

{{add-cm-allowlist-frontend-pipeline}}

La activación del sitio se realiza desde la consola Sitios mediante el [carril del sitio](site-rail.md).

1. Inicie sesión en AEM y navegue hasta su sitio a través de **Navegación global** > **Sitios**.
1. Seleccione el sitio en la consola. Seleccione la raíz del sitio y no cualquier página secundaria.
1. Con el sitio seleccionado, abra el [selector de carril](/help/sites-cloud/authoring/basic-handling.md#rail-selector) a la izquierda y elija **Sitio**.
1. En el carril del **sitio**, haga clic en el botón **Habilitar canalización front-end**.

   ![Habilitación de la canalización front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM le solicita que confirme con una descripción general de los cambios realizados. Confirme y su sitio estará adaptado.

Ahora, el sitio está listo para usar la canalización front-end. Para obtener más información sobre la canalización front-end y la administración del tema del sitio, consulte lo siguiente:

* [Uso del carril del sitio para administrar el tema del sitio](site-rail.md)
* [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md): este recorrido de documentación le ofrece una visión general de principio a fin del proceso de implementación rápida de un sitio mediante la canalización front-end y la herramienta de creación rápida del sitio.
* [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end): este documento describe la canalización front-end en el contexto de las canalizaciones full-stack y de nivel web.

## Canalización front-end y dominios personalizados {#custom-domains}

Como se describe en la sección [Detalles técnicos](#technical-details), al activar la característica de canalización front-end para un sitio se crean `SiteConfig` y `HtmlPageItemsConfig` nodos por debajo de `/conf/<site-name>/sling:configs`.

Si desea usar la función de dominios personalizados [Cloud Manager](/help/implementing/cloud-manager/custom-domain-names/introduction.md) para su sitio junto con la canalización front-end, se deben agregar propiedades adicionales a estos nodos.

1. Establezca la propiedad `customFrontendPrefix` en `SiteConfig` para el sitio.
1. Esto actualiza el valor `prefixPath` de `HtmlPageItemsConfig` con el dominio personalizado.

Las páginas del sitio hacen referencia a artefactos de temas de la dirección URL actualizada.
