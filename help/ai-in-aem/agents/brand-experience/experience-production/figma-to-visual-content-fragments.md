---
title: Trabajo de Figma a fragmentos de contenido visual
description: Descubra qué es el trabajo de Figma to Visual Content Fragments de Brand Experience Agent y qué puede hacer por usted.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
source-git-commit: 5413e173ac159015f224845e238779c5dc997ee5
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# Trabajo de Figma a fragmentos de contenido visual {#figma-to-visual-content-fragments-job}

El trabajo de Figma en fragmentos de contenido visuales de [Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md) automatiza el proceso de recreación de diseños Figma en Adobe Experience Manager (AEM) as a Cloud Service.

<!-- CQDOC-23232 - remove when GA -->

>[!NOTE]
>
>El trabajo de Figma a fragmentos de contenido visuales está actualmente en disponibilidad limitada.
>
>Si desea participar, envíe una solicitud desde su dirección de correo electrónico oficial a [experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com).

## Información general {#overview}

Los fragmentos de contenido visual de AEM permiten obtener una vista previa y enviar fragmentos de contenido mediante un diseño visual basado en una [plantilla de HTML](/help/implementing/developing/extending/content-fragments-visualization-templates.md).

Aunque la definición de información de estilo y diseño en plantillas HTML codificadas a mano es totalmente viable, se trata de un proceso muy técnico que suelen realizar los desarrolladores web.

Para optimizar este proceso para [Fragmentos de contenido visual](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md), y dado que los diseños visuales para experiencias modulares a menudo se crean en Figma, también es posible importar directamente diseños de Figma a AEM.

## Requisitos previos {#prerequisites}

Antes de empezar:

* La importación desde Figma requiere autenticación. El usuario de Figma debe crear un token de acceso en Figma y almacenarlo en el servicio de AEM.

  Esto se logra mediante:

   * generación de un token personal en Figma
   * iniciando sesión en Adobe Experience Cloud a las `https://experience.adobe.com`
   * conservando el token en `https://experience.adobe.com/#/aem/figmatocontentfragment`

## Para cargar un diseño {#to-upload-a-design}

El flujo es el siguiente:

1. El diseñador (usuario de Figma) crea el diseño en Figma.
1. El usuario de Figma crea un vínculo compartido con el objeto de diseño en Figma.
1. El usuario de Figma envía el vínculo compartido al usuario de AEM.
1. A partir de un [prompt](#sample-prompts) inicial, el usuario de AEM puede usar el AI Assistant para interactuar con el trabajo de Figma en fragmentos de contenido visuales y volver a crear automáticamente el diseño aprobado en AEM. AEM creará automáticamente los modelos de fragmentos de contenido, los fragmentos de contenido y las plantillas de HTML necesarios.
   * Cuando sea necesario, el agente solicitará más información, como el entorno de AEM que debe utilizar.
   * El proceso de creación agéntica también incluye funcionalidades que permiten reutilizar modelos de contenido o fragmentos existentes cuando ya están disponibles.
1. El agente genera un fragmento de contenido y un modelo de fragmento de contenido para el contenido, así como una plantilla de HTML para el diseño.
   * El agente proporciona un vínculo directo al fragmento desde el que puede acceder al modelo y a la plantilla.

## Indicadores de ejemplo {#sample-prompts}

Los indicadores de ejemplo incluyen:

* Para importar desde Figma:
   * Importar de Figma {*Figma_share_URL*} a AEM
* Para seleccionar el programa AEM de entre las sugerencias del agente:
   * Importar de Figma {*Figma_share_URL*} a {*AEMaaCS_program/environment_link*}

## Recursos adicionales {#additional-resources}

Los siguientes recursos pueden resultar útiles a medida que continúa explorando fragmentos de contenido visual:

* [Fragmentos de contenido visual](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)
* [Fragmentos de contenido visual: plantillas](/help/implementing/developing/extending/content-fragments-visualization-templates.md)
* [Fragmentos de contenido visual: enviar con la dirección URL de publicación](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md)
