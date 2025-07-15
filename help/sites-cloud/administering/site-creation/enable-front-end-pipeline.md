---
title: Activación de la canalización front-end
description: Descubra cómo puede habilitar la canalización front-end para los sitios de creación tradicionales de AEM existentes con envío de publicación para utilizar temas de sitio y personalizar el sitio más rápidamente.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: 6ee55bed8ca09470291e0488321732beed7bab42
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 24%

---


# Activación de la canalización front-end {#enable-front-end-pipeline}

{{traditional-aem}}

Descubra cómo puede habilitar la canalización front-end para los sitios de creación tradicionales de AEM existentes con envío de publicación para utilizar temas de sitio y personalizar el sitio más rápidamente.

## Información general {#overview}

La canalización front-end es un mecanismo para la creación tradicional de proyectos de AEM con [envío de publicación](/help/sites-cloud/authoring/author-publish.md) que puede implementar rápidamente solo el código front-end de sus sitios web en función de [temas del sitio](site-themes.md) y [plantillas de sitio](site-templates.md).

Esta canalización solo administra el código front-end, lo que hace que el proceso de implementación sea más rápido que las implementaciones de pila completa. Permite a los desarrolladores de front-end personalizar el sitio fácilmente sin necesidad de tener conocimientos de AEM.

Los sitios basados en plantillas de sitio pueden utilizar la canalización front-end de forma predeterminada. Este documento describe cómo puede adaptar los sitios existentes para aprovechar la canalización front-end.

>[!TIP]
>
>Si no está familiarizado con la canalización front-end y con cómo implementar sitios rápidamente mediante ella y las plantillas de sitio, consulte [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para obtener una introducción.

AEM puede configurar el sitio para que cargue temas implementados con la canalización front-end, incluso si el sitio no se creó con plantillas de sitio y temas, colocándolos sobre las bibliotecas de cliente existentes.

## Detalles técnicos {#technical-details}

Al activar la canalización front-end para un sitio, AEM realiza los siguientes cambios en la estructura del sitio.

* Todas las páginas del sitio incluyen un archivo CSS y JS adicional, que se puede modificar mediante la implementación de actualizaciones a través de una canalización front-end de Cloud Manager dedicada.
* Los archivos CSS y JS añadidos inicialmente están vacíos. Sin embargo, puede descargar una carpeta &quot;fuentes temáticas&quot; para configurar la estructura de carpetas necesaria para implementar actualizaciones de código CSS y JS a través de la canalización.
* Solo un desarrollador puede deshacer el cambio eliminando los nodos `SiteConfig` y `HtmlPageItemsConfig` que esta operación crea debajo de `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Esta acción no convierte automáticamente las bibliotecas de cliente existentes del sitio para utilizar la canalización front-end. Mover estos orígenes de la carpeta de biblioteca del cliente a la carpeta de canalización front-end es una tarea que requiere el trabajo manual de un desarrollador de front-end.

## Requisitos  {#requirements}

AEM puede adaptar automáticamente el sitio existente para utilizar la canalización front-end. Para poder realizar este flujo de trabajo, el sitio debe usar [v2 o posterior del componente de página de los componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/wcm-components/page).

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

La canalización front-end se puede usar con la característica de dominios personalizados de [Cloud Manager,](/help/implementing/cloud-manager/custom-domain-names/introduction.md), pero tenga en cuenta los siguientes requisitos al usar las dos características juntas.

### Archivos front-end estáticos {#static-files}

Los recursos front-end estáticos implementados mediante la canalización front-end se proporcionan, de forma predeterminada, desde el dominio estático predefinido de Adobe.

Si necesita un dominio personalizado para los recursos front-end, puede instalar un dominio personalizado en el nivel de publicación y configurar Dispatcher para que enrute rutas específicas (como `/static/`) a la ubicación de alojamiento estática de Adobe. Este método requiere la actualización de las [reglas de Dispatcher](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/dispatcher) para reenviar y almacenar en caché correctamente las solicitudes de los recursos estáticos.

Una vez configurados el dominio personalizado y el despachante, puede configurar AEM para que sirva los recursos front-end desde el dominio estático.

### Configuración {#configuration}

Como se describe en la sección [Detalles técnicos](#technical-details), al activar la característica de canalización front-end para un sitio se crean `SiteConfig` y `HtmlPageItemsConfig` nodos por debajo de `/conf/<site-name>/sling:configs`.

Si desea utilizar la función de dominios personalizados de Cloud Manager para su sitio junto con la canalización front-end para los recursos de estado, se deben agregar propiedades adicionales a estos nodos.

1. Establezca la propiedad `customFrontendPrefix` en `SiteConfig` para el sitio.
   1. Navegue hasta `/conf/<site-name>/sling:configs/com.adobe.aem.wcm.site.manager.config.SiteConfig`.
   1. Agregue o actualice la propiedad `customFrontendPrefix = "https://your-custom-domain.com/static/"`.
1. Esto actualiza el valor `prefixPath` de `HtmlPageItemsConfig` con el dominio personalizado.
   1. Navegue hasta `/conf/<site-name>/sling:configs/com.adobe.cq.wcm.core.components.config.HtmlPageItemsConfig`.
   1. Compruebe que `prefixPath` refleje su dominio personalizado como `prefixPath = "https://your-custom-domain.com/static/<hash>/..."`.
   * Este valor también se puede sobrescribir manualmente según sea necesario.
1. Compruebe la configuración.
   1. Después de la implementación, compruebe que las páginas hagan referencia correctamente a los artefactos de temas del dominio personalizado.
   1. Abra las herramientas para desarrolladores del explorador e inspeccione las rutas de archivo `theme.css` y `theme.js` para confirmar que se han cargado desde el dominio correcto.

Las páginas del sitio hacen referencia a artefactos de temas de la dirección URL actualizada. A continuación, el despachante enruta las solicitudes de esos recursos al dominio estático.

## Prácticas recomendadas para desarrolladores de front-end {#best-practices}

Si necesita desarrollar y probar recursos front-end localmente antes de implementarlos a través de la canalización front-end, tenga en cuenta los siguientes enfoques:

* Use el [Modo proxy del generador de temas del sitio](https://github.com/adobe/aem-site-theme-builder?tab=readme-ov-file#proxy) para anular los artefactos de temas localmente y realizar pruebas.
* Proporcione manualmente los archivos de tema de un servidor de desarrollo local y actualice `prefixPath` en `HtmlPageItemsConfig` para que coincida con la dirección del servidor local.
* Asegúrese de que el almacenamiento en caché del explorador esté deshabilitado durante la prueba para ver las actualizaciones en directo.

Para obtener más información sobre el desarrollo del front-end local, consulte la [documentación del Generador de temas del sitio.](https://github.com/adobe/aem-site-theme-builder)
