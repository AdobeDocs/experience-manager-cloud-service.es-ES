---
title: Trabajo de creación de contenido
description: Descubra qué es el trabajo de creación de contenido de Brand Experience Agent y qué puede hacer por usted.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
source-git-commit: 2e3b10f7886f8bc5757d2144875ec0b441de7bb5
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 1%

---


# Trabajo de creación de contenido {#content-create}

El trabajo de creación de contenido es parte de [Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md) que crea nuevas páginas de marca usando lenguaje natural, información de marketing y una plantilla de AEM. El trabajo acelera la producción de páginas para Adobe Experience Manager (AEM) as a Cloud Service y Edge Delivery Services.

<!-- see Limitations too and update when appropriate -->

>[!NOTE]
>
>El trabajo de creación de contenido está actualmente en disponibilidad limitada. Si desea participar, envíe una solicitud desde su dirección de correo electrónico oficial a [experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com).

## Información general {#overview}

El trabajo de creación de contenido genera nuevas páginas en la marca utilizando un lenguaje natural, junto con una información de marketing y una plantilla de AEM.

Puede acceder al trabajo de creación de contenido desde:

* [El asistente de IA](#access-ai-assistant)

>[!VIDEO](https://video.tv.adobe.com/v/3488436?learn=on)

Para utilizar el trabajo de creación de contenido:

* Usted [proporciona](#provide-the-prompt-and-brief):

   * Un mensaje en lenguaje natural: que describe qué crear y dónde debería residir la página.

   * Un resumen:

      * El trabajo de creación de contenido utiliza una información de marketing o un documento que describe lo que debe generar el agente. El trabajo acepta una amplia gama de formatos para la presentación. Los informes efectivos a menudo especifican objetivos, audiencia, temas, recuento de palabras objetivo y palabras clave.

* A continuación, [envía](#submit) el mensaje y el informe
* A continuación, especifique una [plantilla de AEM](#select-a-template): que define el diseño requerido
* El trabajo proporcionará un [plan para que usted lo revise](#review-the-plan)
* Puede [continuar con la generación](#proceed-with-generation) y [perfeccionar la creación si es necesario](#further-refinement-in-authoring)

El agente alinea la generación con la plantilla y puede añadir o quitar secciones para que coincidan con el resumen; por ejemplo, cuando necesita un recuento de palabras más alto o más bajo.

>[!NOTE]
>
>Esta página usa un ejemplo para crear una nueva página basada en un informe adjunto en `https://frescopa.coffee/sustainability/coffee-bean-types`

## Acceso: asistente de IA {#access-ai-assistant}

Puede acceder al trabajo en AEM mediante el asistente de IA.

Abra el [Asistente de IA](/help/implementing/cloud-manager/ai-assistant-in-aem.md) desde la barra de herramientas superior derecha de [`experience.adobe.com`](https://experience.adobe.com).

## Proporcione la información rápida y breve {#provide-the-prompt-and-brief}

En el asistente de IA debe hacer lo siguiente:

1. Utilice un lenguaje natural para describir lo que desea hacer e identificar dónde se ubicará la página, mediante una ruta o dirección URL dentro del sitio web. Por ejemplo, crear una nueva página basada en su informe:

   * `create a new page based on the attached at https://frescopa.coffee/sustainability/coffee-bean-types`

     ![Trabajo de creación de contenido - agregar un aviso](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-create-page.png)

1. Cargue las instrucciones relevantes para su solicitud. Para cargar el informe:

   1. Seleccione **+** en la parte inferior izquierda del asistente de IA y elija **Adjuntar archivos**:

      ![Trabajo de creación de contenido - cargar un informe](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-load-brief.png)

   1. Añada el archivo breve. Las instrucciones cargadas se mostrarán en la parte superior derecha del cuadro de diálogo de solicitud:

      ![Trabajo de creación de contenido - resumen cargado](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-loaded-brief.png)

1. Cuando esté listo, envíe el mensaje y la información utilizando el icono azul de envío (punta de flecha azul).

## Seleccionar una plantilla {#select-a-template}

A continuación, el agente solicitará que especifique una plantilla. La plantilla proporciona al agente la estructura y el diseño de la página. La generación se ajusta a ese diseño. El agente puede agregar y quitar secciones según sea necesario, en función del resumen; por ejemplo, para cumplir un recuento de palabras diferente.

![Trabajo de creación de contenido - especifique la plantilla](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-select-template.png)

## Revisión del plan {#review-the-plan}

A continuación, el agente presenta un plan para los cambios que realizará, según sus entradas y su análisis de la información. Puede ajustar el plan o continuar con el plan e iniciar la generación.

>[!NOTE]
>
> Si usas [Governance Agent](/help/ai-in-aem/agents/governance/overview.md), la generación puede seguir las pautas de tu marca.

![Trabajo de creación de contenido: revise el plan](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-review-plan.png)

## Continúe con la generación {#proceed-with-generation}

Cuando termina la generación, el agente proporciona dos vínculos:

* un vínculo **preview**
* un vínculo **edit**
   * Use el vínculo de edición para [abrir la página en una superficie de creación de AEM](#further-refinement-in-authoring) para refinarla más.

![Trabajo de creación de contenido - continuar con la generación](/help/ai-in-aem/agents/brand-experience/experience-production/assets/create-content-example-proceed-generation.png)

## Mejoras adicionales en la creación {#further-refinement-in-authoring}

Después de editar la página en AEM, se abrirá en su entorno de creación; por ejemplo, el [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) o el [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md).

En el [Editor universal](#universal-editor-edit-text-with-the-assistant), el asistente de IA tiene en cuenta el contexto *: puede seleccionar elementos en el lienzo y trabajar en ellos con el asistente.*

### Editor universal: editar texto con el asistente {#universal-editor-edit-text-with-the-assistant}

Para perfeccionar la copia del Ayudante durante la creación:

1. Seleccione el elemento en el [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md).
1. Abra el Ayudante de IA en la esquina superior derecha, introduzca el mensaje y realice el envío.

Ejemplos de peticiones de datos:

* `Update to Explore the World of Coffee`
* `Update to be more engaging for the 30-40 year old age demographic and avid coffee drinker`

Seleccione **Aplicar cambios** (o equivalente) para que las actualizaciones aparezcan en la página.

## Activación {#activation}

Puede explorar los agentes de AEM a través de [Playground](https://www.aem.live/developer/aem-playground), o conectarse con su CSM o TAM para discutir el acceso a través del SKU de Agentic.

## Limitaciones {#limitations}

Tenga en cuenta las siguientes limitaciones:

* La capacidad está en disponibilidad limitada y requiere la incorporación manual para la participación. Si desea participar, envíe una solicitud desde su dirección de correo electrónico oficial a [experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com).

## Recursos adicionales {#additional-resources}

Los siguientes recursos pueden resultar útiles a medida que continúa explorando Experience Production Agent:

* También puede usar el [Libro de trabajo de Experience Production Agent](https://www.adobe.com/go/aem-epa-workbook_es) para obtener instrucciones prácticas y guiadas.
