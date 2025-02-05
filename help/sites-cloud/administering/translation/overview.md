---
title: Traducción de contenido para sitios multilingües
description: Obtenga información general sobre cómo traducir contenido para sitios multilingües.
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 82%

---

# Traducción de contenido para sitios multilingües {#translating-content-for-multilingual-sites}

Automatice la traducción del contenido de la página y los activos para crear y mantener sitios web multilingües. Para automatizar los flujos de trabajo de traducción, se integran los proveedores de servicios de traducción con AEM y se crean proyectos para traducir contenido a varios idiomas. AEM admite flujos de trabajo de traducción automática y humana.

* **Traducción humana:** el contenido se envía a su proveedor de traducción y lo traducen traductores profesionales. Cuando se completa, el contenido traducido se devuelve e importa en AEM. Cuando el proveedor de traducción está integrado con AEM, el contenido se envía automáticamente a AEM y al proveedor de traducción.
* **Traducción automática:** el servicio de traducción automática traduce inmediatamente su contenido.

>[!TIP]
>
>Si no tiene experiencia en la traducción de contenido, consulte el [Recorrido de traducción de sitios](/help/journey-sites/translation/overview.md), que es una ruta guiada a través de la traducción del contenido de AEM Sites AEM AEM mediante herramientas de traducción potentes que se utilizan para traducir contenido. Es ideal para aquellos que no tienen experiencia en traducción o en traducción de sitios.

La traducción de contenido implica los siguientes pasos:

1. [Conectar AEM con su proveedor de servicios de traducción](integration-framework.md#connecting-to-a-translation-service-provider) y [crear configuraciones del marco de trabajo de integración de traducción](integration-framework.md).
1. [Asociar las páginas del maestro de idioma](integration-framework.md#configuring-pages-for-translation) con el servicio de traducción y las configuraciones del marco de trabajo.
1. [Identificar el tipo de contenido](rules.md) para traducir.
1. [Preparar el contenido para su traducción](preparation.md) creando el maestro de idioma y las páginas raíz de las copias de idioma.
1. [Crear proyectos de traducción](managing-projects.md) para recopilar el contenido que se va a traducir y para preparar el proceso de traducción.
1. Utilice los proyectos de traducción para [administrar el proceso de traducción de contenido](managing-projects.md).

Si el proveedor de servicios de traducción no proporciona un conector para la integración con AEM, este admite la extracción manual y la reinserción del contenido de traducción en formato XML.

>[!NOTE]
>
>El usuario debe ser miembro del grupo `project-administrators` para utilizar las características de copia de idioma.

## Prácticas recomendadas   {#best-practices}

La página [Prácticas recomendadas de traducción](best-practices.md) contiene información importante sobre la implementación.
