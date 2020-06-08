---
title: Información acerca de la segmentación
description: La segmentación es una consideración clave al crear una campaña
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
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

El contenido se puede dirigir específicamente a las necesidades e intereses del visitante en función de los segmentos que coincidan.

## Uso de la segmentación {#using-segmentation}

Los segmentos se definen en Configurar segmentación. Se utilizan para dirigir el contenido real que visualiza un público objetivo concreto.<!--Segments are defined in [Configuring Segmentation](/help/sites-administering/campaign-segmentation.md). They are used to steer the actual content seen by a specific target audience.-->

## Segmentation Terminology {#segmentation-terminology}

Al analizar la segmentación, se emplea la siguiente terminología:

* **Visitante** - Un visitante es una persona que visita un sitio web. La visita de esa persona se suele iniciar desde una página de referencia y después se mueve a una o varias vistas de página en su propio sitio web. Se puede crear un perfil de comportamiento a partir de la información de la visita de esa persona.
* **Usuario** : un usuario es un visitante que se registra en el sitio web para recibir un perfil de cuenta. Para generar su perfil, proporcionan identificación adicional como, por ejemplo, una dirección de correo electrónico y el género, entre otros datos. La información adicional también se puede recopilar, incluyendo la actividad de la comunidad y los modelos de compra, entre otros datos. En función de la información proporcionada en el perfil, se puede crear un perfil demográfico.
* **Característica** : una característica es una propiedad o característica de un visitante que se puede utilizar para determinar la pertenencia a un segmento específico.
* **Segmento** : un segmento es una colección de visitantes que comparten ciertas características. Los segmentos deben ser distintivos, con un mínimo de superposición con otros segmentos.
* **Características** del comportamiento: las características del comportamiento son aquellas que se relacionan con el comportamiento de un visitante en el sitio web. Entre estas características se incluyen:
   * Interés en el sitio web, incluyendo las páginas y los productos comprados
   * Interés en el sitio web de referencia, incluyendo los términos de búsqueda utilizados o los anuncios en los que se ha hecho clic
   * Interés en otros sitios; se determina con herramientas como Spyjax
   * lealtad al Visitante; duración de la visita, frecuencia de las visitas
* **Características** demográficas: Son características de población seleccionadas, entre ellas:
   * Edad
   * Ingresos
   * Tamaño familiar
   * Estado civil
   * Sexo
   * Lugar de residencia
* **Características** derivadas: Algunas características demográficas son difíciles de determinar sin registrarse, pero se pueden derivar combinando características demográficas y de comportamiento.
   * Por ejemplo, la combinación de la dirección URL de referencia (como característica de comportamiento) con datos demográficos (adquiridos con herramientas como [Google Ad Planner](https://www.google.com/adplanner/)) permite que los propietarios del sitio obtengan características demográficas de los visitantes.
* **Subsegmento** : un segmento se puede subdividir en varios subsegmentos. Esto se lleva a cabo definiendo características adicionales.
* **Página** de teaser: una página de teaser se dirige a una audiencia específica. Incluye contenido reutilizable que se puede emplear en el párrafo de teaser.
* **Campaña** : una campaña es una colección de páginas de teaser y páginas de mercadotecnia de correo electrónico, como newsletters o invitaciones. Normalmente, una campaña se ejecuta durante un período limitado y se reemplaza por otra campaña.
* **Párrafo** de teaser: es un párrafo que extrae contenido de otra página en función de una estrategia de selección. Esta estrategia de selección puede tener en cuenta segmentos y campañas.
* **Lista** : se extrae una lista de un segmento de usuarios registrados. Por ejemplo, la ubicación se utiliza para dirigir los contenidos del párrafo de teaser.
