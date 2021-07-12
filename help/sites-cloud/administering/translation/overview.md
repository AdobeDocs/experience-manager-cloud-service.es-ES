---
title: Traducción de contenido para sitios multilingües
description: Obtenga información general sobre cómo traducir contenido para sitios multilingües.
feature: Copiar idioma
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# Traducción de contenido para sitios multilingües {#translating-content-for-multilingual-sites}

Automatice la traducción del contenido de la página y los recursos para crear y mantener sitios web multilingües. Para automatizar los flujos de trabajo de traducción, se integran los proveedores de servicios de traducción con AEM y se crean proyectos para traducir contenido a varios idiomas. AEM admite flujos de trabajo de traducción automática y humana.

* **Traducción humana:** el contenido se envía a su proveedor de traducción y lo traducen traductores profesionales. Cuando se completa, el contenido traducido se devuelve e importa en AEM. Cuando el proveedor de traducción está integrado con AEM, el contenido se envía automáticamente entre AEM y el proveedor de traducción.
* **Traducción automática:** El servicio de traducción automática traduce inmediatamente su contenido.

La traducción de contenido implica los siguientes pasos:

1. [Conecte AEM con su ](integration-framework.md#connecting-to-a-translation-service-provider) proveedor de servicios de traducción y  [cree configuraciones](integration-framework.md) del marco de integración de traducción.
1. [Asocie las páginas del ](integration-framework.md#configuring-pages-for-translation) maestro de idioma con el servicio de traducción y las configuraciones del marco.
1. [Identifique el tipo de ](rules.md) contenido que desea traducir.
1. [Prepare el contenido para la ](preparation.md) traducción creando el maestro de idioma y las páginas raíz de las copias de idioma.
1. [Cree ](managing-projects.md) proyectos de traducción para recopilar el contenido que desea traducir y preparar el proceso de traducción.
1. Utilice los proyectos de traducción para [administrar el proceso de traducción de contenido](managing-projects.md).

Si el proveedor de servicios de traducción no proporciona un conector para la integración con AEM, AEM admite la extracción manual y la reinserción del contenido de traducción en formato XML.

>[!NOTE]
>
>El usuario debe ser miembro del grupo `project-administrators` para utilizar las funciones de copia de idioma.

## Prácticas recomendadas   {#best-practices}

La página [Prácticas recomendadas de traducción](best-practices.md) contiene información importante sobre la implementación.
