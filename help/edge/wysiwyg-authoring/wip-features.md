---
title: Funciones en fase de desarrollo de Sites para Edge Delivery Services
description: Conozca qué funciones y casos de uso de AEM Sites están en fase de desarrollo y descubra soluciones alternativas al utilizar Edge Delivery Services.
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 100%

---

# Funciones en fase de desarrollo de Sites para Edge Delivery Services {#wip-sites-features}

Conozca qué funciones y casos de uso de AEM Sites están en fase de desarrollo y descubra soluciones alternativas al utilizar Edge Delivery Services.

>[!TIP]
>
>Que las funciones estén en fase de desarrollo no significa que sea el final. Si necesita una función o un caso de uso que figure como en fase de desarrollo en este documento, póngase en contacto con su representante de Adobe. Puede trabajar con Adobe para comprender sus necesidades particulares y encontrar soluciones alternativas.

## Funciones en fase de desarrollo {#wip-features}

Al utilizar Edge Delivery Services con AEM Sites, la mayoría de las funciones de Sites están disponibles. Por ejemplo, casi cualquier acción disponible en la [consola de Sites](/help/sites-cloud/authoring/sites-console/introduction.md) es aplicable a Edge Delivery Services.

Sin embargo, algunas funciones están en fase de desarrollo (WIP). Las funciones WIP son funciones de la consola de Sites que aún no están disponibles para Edge Delivery Services con AEM Sites o que solo lo están parcialmente. Por este motivo, las funciones WIP pueden presentarse de forma diferente a sus equivalentes de Sites o puede haber soluciones alternativas para el caso de uso.

La siguiente lista presenta estas funciones WIP y soluciones alternativas. Si su proyecto requiere una función WIP, revise las alternativas sugeridas a continuación y póngase en contacto con Adobe para trabajar juntos y comprender su caso de uso.

| Función de Sites | Estado en Edge | Notas | Documentación de Edge |
|---|---|---|---|
| [Herencia de página](/help/sites-cloud/administering/msm-and-translation.md) | Disponible |  | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Herencia de componentes](/help/sites-cloud/administering/msm-and-translation.md) | Disponible parcialmente | Los componentes heredan el contenido, pero la herencia solo se puede revertir en el nivel de página | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Copia de idioma](/help/sites-cloud/administering/translation/overview.md) | Disponible parcialmente | Los componentes heredan el contenido, pero la herencia solo se puede revertir en el nivel de página | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Administración de varios sitios](/help/sites-cloud/administering/msm/overview.md) | Disponible parcialmente | Los componentes heredan el contenido, pero la herencia solo se puede revertir en el nivel de página | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md) | Disponible parcialmente | Los componentes heredan el contenido, pero la herencia solo se puede revertir en el nivel de página | [Herencia de contenido en el editor universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Plantillas de página](/help/sites-cloud/authoring/page-editor/templates.md) | Disponible parcialmente | Las páginas creadas a partir de plantillas son copias independientes de la plantilla original. | [Uso de plantillas de página con el editor universal](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Centro de contexto y direccionamiento](/help/sites-cloud/authoring/personalization/overview.md) | No disponible |  |  |
| [Deformación de tiempo](/help/sites-cloud/authoring/launches/preview.md) | No disponible |  |  |
| [Contenido asociado](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | No disponible |  |  |
| [Fragmentos de experiencias](/help/sites-cloud/authoring/fragments/experience-fragments.md) | Alternativa | Creación de una página y uso de un componente de fragmento |  |

## Casos de uso en fase de desarrollo {#wip-use-cases}

Dado que Edge Delivery Services se basa en una pila de tecnología completamente nueva y moderna, los siguientes casos de uso de AEM Sites aún no están completamente cubiertos y están en fase de desarrollo. Si su proyecto requiere un caso de uso WIP, póngase en contacto con Adobe para trabajar juntos y comprender las necesidades de su proyecto.

| Caso de uso de Sites | Detalles |
|---|---|
| Lógica del lado del servidor para procesar páginas | Uso del tiempo de ejecución de AEM como servidor de aplicaciones |
| Páginas dinámicas | SSI o cualquier técnica de inclusión dinámica |
| Administración de usuarios | Uso de AEM como IdP |
| Autenticación | Uso de AEM para contenido seguro |
| Permiso de contenido | AEM como extranet segura |
