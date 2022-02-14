---
title: Habilitar canalización front-end
description: Descubra cómo puede habilitar la canalización de front-end para sitios existentes a fin de aprovechar los temas del sitio para personalizar más rápidamente el sitio.
feature: Administering
role: Admin
source-git-commit: dc7e89c601bb02c78f65ca58eff34c15092b5561
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Habilitar canalización front-end {#enable-front-end-pipeline}

Descubra cómo puede habilitar la canalización de front-end para sitios existentes a fin de aprovechar los temas del sitio para personalizar más rápidamente el sitio.

## Información general {#overview}

La canalización front-end es un mecanismo que puede implementar rápidamente solo el código front-end de sus sitios web en función de [temas del sitio](site-themes.md) y [plantillas de sitio.](site-templates.md)

En lugar de implementar la pila completa, solo el código front-end se gestiona mediante esta canalización, lo que hace que el proceso sea más rápido y permite a los desarrolladores de front-end personalizar su sitio de forma fácil y rápida sin tener conocimiento de AEM.

Los sitios basados en plantillas de sitio pueden aprovechar la canalización de front-end de forma predeterminada. Este documento describe cómo puede adaptar los sitios existentes para aprovechar la canalización de front-end.

>[!TIP]
>
>Si no está familiarizado con la canalización del front-end y con cómo implementar rápidamente sitios mediante ella y las plantillas de sitio, revise la [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para una introducción.

Si no ha creado el sitio existente en función de las plantillas y los temas del sitio, AEM configurar el sitio para cargar los temas que se implementan con la canalización de front-end sobre las bibliotecas de cliente existentes.

## Requisitos {#requirements}

AEM adaptar automáticamente el sitio existente para utilizar la canalización front-end. Para poder hacerlo, el sitio debe utilizar [v2 o posterior del componente de página de los componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## Activación de la canalización front-end {#enabling}

La activación del sitio se realiza desde la consola Sitios .

1. Inicie sesión en AEM y navegue hasta su sitio a través de **Navegación global** > **Sitios**.
1. Seleccione el sitio en la consola. Debe seleccionar la raíz del sitio y no cualquier página secundaria.
1. Con el sitio seleccionado, abra el [selector de raíl](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) a la izquierda y elija **Sitio**.
1. En el **Sitio** carril , haga clic en el botón . **Habilitar canalización front-end**.

   ![Habilitar canalización front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM le solicita que confirme con una descripción general de los cambios que se realizarán. Confirme y su sitio está adaptado.

Ahora su sitio está listo para usar la canalización front-end. Para obtener más información sobre la canalización front-end, consulte:

* [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) : Este recorrido de documentación le ofrece una visión general de principio a fin del proceso de implementación rápida de un sitio mediante la canalización front-end y la herramienta de creación rápida del sitio.
* [Canalizaciones CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) : Este documento describe la canalización front-end en el contexto de las canalizaciones de pila completa y de nivel web.
