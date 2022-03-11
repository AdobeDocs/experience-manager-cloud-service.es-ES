---
title: Información acerca de la segmentación
description: La segmentación es una consideración clave al crear una campaña
exl-id: 36a9623a-bb19-498a-a0e9-ef80582b1fcf
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 58%

---

# Información acerca de la segmentación {#understanding-segmentation}

La segmentación es una consideración clave al crear una campaña. En la mayoría de los casos, será necesario tener segmentos ya definidos antes de comenzar una campaña.

Los visitantes del sitio tienen diferentes intereses y objetivos cuando acceden al sitio. Comprender estos objetivos y cumplir las expectativas son importantes factores de éxito para el marketing en línea.

La segmentación ayuda a lograr esto, analizando y caracterizando los siguientes aspectos de un visitante:

* Actividad en el sitio web
* Perfil
* Actividad en otros sitios web

A continuación, el contenido se puede dirigir específicamente a las necesidades y los intereses del visitante según los segmentos con los que coincida.

## Uso de la segmentación {#using-segmentation}

Los segmentos se definen en Configurar segmentación. Se utilizan para dirigir el contenido real que visualiza un público objetivo concreto.<!--Segments are defined in [Configuring Segmentation](/help/sites-administering/campaign-segmentation.md). They are used to steer the actual content seen by a specific target audience.-->

## Terminología de segmentación {#segmentation-terminology}

Al analizar la segmentación, se emplea la siguiente terminología:

* **Visitante** - Un visitante es una persona que visita un sitio web. La visita de esa persona se suele iniciar desde una página de referencia y después se mueve a una o varias vistas de página en su propio sitio web. Se puede crear un perfil de comportamiento a partir de la información de la visita de esa persona.
* **Usuario** - Un usuario es un visitante que se registra en el sitio web para recibir un perfil de cuenta. Para generar su perfil, proporcionan identificación adicional como, por ejemplo, una dirección de correo electrónico y el género, entre otros datos. La información adicional también se puede recopilar, incluyendo la actividad de la comunidad y los modelos de compra, entre otros datos. En función de la información proporcionada en el perfil, se puede crear un perfil demográfico.
* **Característica** - Un rasgo es una característica o propiedad de un visitante que se puede usar para determinar la pertenencia a un segmento específico.
* **Segmento** - Un segmento es una colección de visitantes que comparten ciertas características. Los segmentos deben ser distintivos, con un mínimo de superposición con otros segmentos.
* **Características de comportamiento** - Los rasgos de comportamiento son los que se relacionan con el comportamiento de un visitante en el sitio web. Entre estas características se incluyen:
   * Interés en el sitio web, incluyendo las páginas y los productos comprados
   * Interés en el sitio web de referencia, incluyendo los términos de búsqueda utilizados o los anuncios en los que se ha hecho clic
   * Interés en otros sitios; se determina con herramientas como Spyjax
   * Lealtad del visitante; duración de la visita, frecuencia de las visitas
* **Características demográficas** - Son características de población seleccionadas, incluidas:
   * Edad
   * Ingresos
   * Tamaño familiar
   * Estado civil
   * Sexo
   * Lugar de residencia
* **Características derivadas** - Algunas características demográficas son difíciles de determinar sin registro, pero se pueden derivar combinando características demográficas y de comportamiento.
   * Por ejemplo, la combinación de la dirección URL de referencia (como característica de comportamiento) con datos demográficos (adquiridos con herramientas como [Google Ad Planner](https://www.google.com/adplanner/)) permite que los propietarios del sitio obtengan características demográficas de los visitantes.
* **Subsegmento** : un segmento se puede subdividir en varios subsegmentos. Esto se lleva a cabo definiendo características adicionales.
* **Página Teaser** : una página de teaser se dirige a una audiencia específica. Incluye contenido reutilizable que se puede emplear en el párrafo de teaser.
* **Campaign** - Una campaña es una colección de páginas de teaser y páginas de marketing por correo electrónico, como newsletters o invitaciones. Normalmente, una campaña se ejecuta durante un periodo limitado y se reemplaza por otra campaña.
* **Párrafo de teaser** : es un párrafo que extrae contenido de otra página en función de una estrategia de selección. Esta estrategia de selección puede tener en cuenta segmentos y campañas.
* **Lista** - Se extrae una lista de un segmento de usuarios registrados. Por ejemplo, la ubicación se utiliza para dirigir los contenidos del párrafo de teaser.
