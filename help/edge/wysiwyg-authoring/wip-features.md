---
title: Funciones de sitios de trabajo en curso para Edge Delivery Services
description: Descubra qué funciones de AEM Sites y casos de uso son un trabajo en curso y descubra soluciones alternativas al utilizar Edge Delivery Services.
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: 92da26452438f2b56cdec1aecc76587d4982f00e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Funciones de sitios de trabajo en curso para Edge Delivery Services {#wip-sites-features}

Descubra qué funciones de AEM Sites y casos de uso son un trabajo en curso y descubra soluciones alternativas al utilizar Edge Delivery Services.

>[!TIP]
>
>El trabajo en curso no significa el final del camino. Si necesita una función o un caso de uso enumerados como trabajo en curso en este documento, póngase en contacto con el representante del Adobe. Usted y Adobe pueden trabajar juntos para comprender sus necesidades particulares y encontrar soluciones alternativas.

## Funciones de trabajo en curso {#wip-features}

Al utilizar Edge Delivery Services con AEM Sites, la mayoría de las funciones de Sites están disponibles. Por ejemplo, casi cualquier acción disponible en la [consola Sites](/help/sites-cloud/authoring/sites-console/introduction.md) es aplicable a los Edge Delivery Services.

Sin embargo, algunas funciones son un trabajo en curso (WIP). Las funciones de trabajo en curso son funciones de la consola Sitios que aún no están disponibles para los Edge Delivery Services con AEM Sites o que solo están disponibles parcialmente. Por este motivo, las funciones de WIP pueden presentarse de forma diferente a sus equivalentes de Sites o puede haber soluciones alternativas para el caso de uso.

La siguiente lista presenta estas funciones de WIP y soluciones alternativas. Si el proyecto requiere una función de trabajo en curso, revise las alternativas sugeridas a continuación y póngase en contacto con el Adobe para trabajar juntos y comprender su caso de uso.

| Función Sitios | Estado en Edge | Notas | Documentación de Edge |
|---|---|---|---|
| [Herencia de página](/help/sites-cloud/administering/msm-and-translation.md) | Disponible |  | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Herencia de componentes](/help/sites-cloud/administering/msm-and-translation.md) | Disponible parcialmente | Los componentes heredan el contenido, pero la herencia solo se puede revertir en el nivel de página | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Copia de idioma](/help/sites-cloud/administering/translation/overview.md) | Disponible parcialmente | Los componentes heredan el contenido, pero la herencia solo se puede revertir en el nivel de página | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Administración de varios sitios](/help/sites-cloud/administering/msm/overview.md) | Disponible parcialmente | Los componentes heredan el contenido, pero la herencia solo se puede revertir en el nivel de página | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md) | Disponible parcialmente | Los componentes heredan el contenido, pero la herencia solo se puede revertir en el nivel de página | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Plantillas de página](/help/sites-cloud/authoring/page-editor/templates.md) | Disponible parcialmente | Las páginas creadas a partir de plantillas son copias independientes de la plantilla original. | [Uso de plantillas de página con el editor universal](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Centro de contexto y destino](/help/sites-cloud/authoring/personalization/overview.md) | No disponible |  |  |
| [Deformación de tiempo](/help/sites-cloud/authoring/launches/preview.md) | No disponible |  |  |
| [Contenido asociado](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | No disponible |  |  |
| [Fragmentos de experiencias](/help/sites-cloud/authoring/fragments/experience-fragments.md) | Alternativa | Creación de una página y uso de un componente de fragmento |  |

## Casos de uso de trabajo en curso {#wip-use-cases}

Dado que los Edge Delivery Services se basan en una pila de tecnología completamente nueva y moderna, los siguientes casos de uso de AEM Sites aún no están completamente cubiertos y son un trabajo en curso. Si su proyecto requiere un caso de uso de WIP, póngase en contacto con Adobe para trabajar juntos y comprender las necesidades del proyecto.

| Caso de uso de sitios | Detalles |
|---|---|
| Lógica del lado del servidor para procesar páginas | AEM Uso del tiempo de ejecución de la como servidor de aplicaciones |
| Páginas dinámicas | SSI o cualquier técnica de inclusión dinámica |
| Administración de usuarios | AEM Uso de como IdP |
| Autenticación | AEM Uso de para contenido seguro |
| Permiso de contenido | AEM como extranet segura |
