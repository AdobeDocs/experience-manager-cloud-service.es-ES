---
title: Plataformas de cliente compatibles
description: Descubra qué exploradores son compatibles para la creación de contenido con Adobe Experience Manager as a Cloud Service y con el acceso a los sitios publicados con AEM.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: d53bfe103ff8e40c8221805a2d66faf3c5cd3823
workflow-type: ht
source-wordcount: '419'
ht-degree: 100%

---

# Plataformas de cliente compatibles {#supported-platforms}

Descubra qué exploradores son compatibles para la creación de contenido con Adobe Experience Manager as a Cloud Service y con el acceso a los sitios publicados con AEM.

>[!TIP]
>
>En este documento se describen las plataformas de cliente compatibles con AEM as a Cloud Service. Para obtener más información sobre el entorno de compilación para desarrollar su proyecto de AEM, consulte el documento [Entorno de compilación.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## Niveles de compatibilidad {#support-levels}

Adobe define los siguientes niveles de compatibilidad con las plataformas cliente de AEM.

| Nivel de soporte | Descripción |
|---|---|
| A: Compatible | Adobe proporciona soporte y mantenimiento completos para esta configuración. Esta configuración está cubierta por el proceso de garantía de calidad de Adobe. |
| R: Compatibilidad restringida | La compatibilidad requiere que se haga una solicitud formal a Adobe para utilizar la configuración en un proyecto. Una vez confirmado por Adobe, este proporciona una compatibilidad completa dentro del programa de compatibilidad restringida. Para obtener más información, póngase en contacto con el Servicio de atención al cliente de Adobe. |
| Z: No compatible | La configuración no es compatible. Adobe no realiza ninguna declaración sobre si la configuración funciona o no, y no la admite. |

## Exploradores compatibles para la creación de contenido {#authoring}

La interfaz de usuario de AEM se ha optimizado para pantallas más grandes que se encuentran en portátiles, equipos de escritorio y dispositivos de tableta (como Apple iPad o Microsoft Surface). El factor de formato de teléfono no es compatible con ningún caso de uso de creación.

La interfaz de usuario de Adobe Experience Manager funciona con las siguientes plataformas de cliente, según el [método de creación.](/help/edge/overview.md#authoring-method)

* [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md)
* [Creación basada en documentos](/help/edge/docs/authoring.md) mediante [Sidekick](/help/edge/docs/sidekick.md)

Todos los exploradores se prueban con el conjunto predeterminado de complementos.

| Explorador | Nivel de compatibilidad del editor universal | Nivel de compatibilidad del editor de páginas | Nivel de compatibilidad de Sidekick |
|---|---|---|---|
| Google Chrome (Evergreen) | A: Compatible | A: Compatible | A: Compatible |
| Microsoft Edge (Evergreen) | A: Compatible | A: Compatible | Z: No compatible |
| Mozilla Firefox (Evergreen) | A: Compatible | A: Compatible | Z: No compatible |
| Última versión de Mozilla Firefox ESR [1] | A: Compatible | A: Compatible | Z: No compatible |
| Safari en macOS (Evergreen) | A: Compatible | A: Compatible | Z: No compatible |
| Safari en iPadOS (Evergreen) | Z: No compatible | A: Compatible | Z: No compatible |

1. Lanzamiento de soporte ampliado de Firefox ([más información en mozilla.org](https://www.mozilla.org/es-ES/firefox/enterprise/))

>[!NOTE]
>
>**Compatibilidad con exploradores con ciclos de lanzamiento rápidos:**
>
>Firefox, Chrome y Edge lanzan actualizaciones con regularidad. Adobe se compromete a mantener el nivel de compatibilidad indicado anteriormente para las próximas versiones de estos exploradores.

## Exploradores compatibles con los sitios web {#websites}

La compatibilidad del explorador con los sitios web procesados por AEM depende de la implementación de las plantillas de página, los bloques, el diseño y la salida de componentes de AEM. Por lo tanto, los desarrolladores que implementan el proyecto tienen el control final de la compatibilidad del sitio.

El [elemento repetitivo del proyecto,](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md#create-github-project) los [componentes principales](/help/implementing/developing/components/overview.md#aem-core-components) y el [sitio de muestra WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) son todos compatibles con todos los exploradores modernos de AEM.
