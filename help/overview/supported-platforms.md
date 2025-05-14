---
title: Plataformas de cliente compatibles
description: Descubra qué exploradores son compatibles con la creación de contenido con Adobe Experience Manager as a Cloud Service y con el acceso a los sitios publicados con AEM.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: e57610e4c5e498ddfdbaa0ba39c9197ecfb5d177
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 15%

---

# Plataformas de cliente compatibles {#supported-platforms}

Descubra qué exploradores son compatibles con la creación de contenido con Adobe Experience Manager as a Cloud Service y con el acceso a los sitios publicados con AEM.

>[!TIP]
>
>Este documento describe las plataformas de cliente compatibles con AEM as a Cloud Service. Para obtener más información sobre el entorno de compilación para desarrollar el proyecto de AEM, consulte el documento [Entorno de compilación.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## Niveles de soporte {#support-levels}

Adobe define los siguientes niveles de compatibilidad con las plataformas cliente de AEM.

| Nivel de soporte | Descripción |
|---|---|
| A: Compatible | Adobe proporciona soporte y mantenimiento completos para esta configuración. Esta configuración está cubierta por el proceso de garantía de calidad de Adobe. |
| R: Compatibilidad restringida | El soporte requiere una solicitud formal a Adobe para utilizar la configuración en un proyecto. Una vez confirmado por Adobe, Adobe proporciona soporte completo dentro del programa de soporte restringido. Para obtener más información, póngase en contacto con el Servicio de atención al cliente de Adobe. |
| Z: No compatible | La configuración no es compatible. Adobe no realiza declaraciones sobre si la configuración funciona o no y no la admite. |

## Exploradores admitidos para la creación de contenido {#authoring}

La interfaz de usuario de AEM está optimizada para pantallas más grandes que se encuentran en portátiles, equipos de escritorio y dispositivos de tableta (como Apple iPad o Microsoft Surface). El factor de forma del teléfono no es compatible con ningún caso de uso de creación.

La interfaz de usuario de Adobe Experience Manager funciona con las siguientes plataformas de cliente, según el [método de creación.](/help/edge/overview.md#authoring-method)

* [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [Editor de página](/help/sites-cloud/authoring/page-editor/introduction.md)
* [Creación basada en documentos](/help/edge/docs/authoring.md) con [Sidekick](/help/edge/docs/sidekick.md)

Todos los exploradores se prueban con el conjunto predeterminado de complementos y complementos.

| Explorador | Nivel de soporte del editor universal | Nivel de compatibilidad del editor de páginas | Nivel de soporte de Sidekick |
|---|---|---|---|
| Google Chrome (evergreen) | A: Compatible | A: Compatible | A: Compatible |
| Microsoft Edge (evergreen) | A: Compatible | A: Compatible | Z: No compatible |
| Mozilla Firefox (evergreen) | A: Compatible | A: Compatible | Z: No compatible |
| Última versión de Mozilla Firefox ESR [1] | A: Compatible | A: Compatible | Z: No compatible |
| Safari en macOS (evergreen) | A: Compatible | A: Compatible | Z: No compatible |
| Safari en iOS (evergreen) [2] | Z: No compatible | A: Compatible | Z: No compatible |

1. Lanzamiento de soporte ampliado de Firefox ([más información en mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/))
1. Compatibilidad solo con Apple iPad

>[!NOTE]
>
>**Compatibilidad con exploradores con ciclos de lanzamiento rápidos:**
>
>Firefox, Chrome y Edge se actualizan periódicamente. Adobe se compromete a mantener el nivel de asistencia mencionado anteriormente para las próximas versiones de estos exploradores.

## Exploradores admitidos para sitios web {#websites}

La compatibilidad del explorador con los sitios web procesados por AEM depende de la implementación de las plantillas de página, los bloques, el diseño y la salida de componentes de AEM. Por lo tanto, los desarrolladores que implementan el proyecto tienen el control final de la compatibilidad del sitio.

Las plantillas de proyecto [AEM,](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md#create-github-project) los [componentes principales](/help/implementing/developing/components/overview.md#aem-core-components) y el sitio de muestra [WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) son todos compatibles con todos los exploradores modernos.
