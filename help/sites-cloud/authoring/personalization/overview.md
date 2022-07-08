---
title: Personalización y targeting de contenido
description: Descubra cómo AEM puede crear contenido personalizado
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '518'
ht-degree: 100%

---

# Personalización y targeting de contenido {#personalization}

## Personalización y targeting de contenido {#personalization-and-content-targeting}

AEM ofrece un marco de herramientas para crear contenido dirigido y presentar experiencias personalizadas.

## Modo Targeting {#targeting-mode}

[Contenido orientado por el autor mediante el modo de Orientación de AEM. ](/help/sites-cloud/authoring/personalization/targeted-content.md) En el modo Targeting y el componente de Target se proporcionan las herramientas necesarias para crear contenido para las experiencias de las actividades de marketing.

## Actividades {#activities}

Las actividades definen y organizan los esfuerzos de marketing. Las actividades constan de las audiencias a las que desea dirigirse y el período de tiempo durante el que se aplica el targeting.

Por ejemplo, el catálogo de productos puede incluir teasers que destacan los productos de temporada. La actividad de deportes de verano define los segmentos de marketing a los que se dirigen los teasers durante los meses de verano.

Las actividades también identifican el [motor de targeting](#targeting-engine) que usan las páginas.

Utilice la [consola Actividades](/help/sites-cloud/authoring/personalization/activities.md) para crear y administrar las actividades de sus marcas. También puede crear actividades a medida que [crea contenido de destino](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Experiencias {#experiences}

Para cada actividad, se definen una o más experiencias que identifican las audiencias a las que se va a dirigir. AEM permite controlar el contenido de que consta cada experiencia.

Las audiencias se basan en segmentos de marketing que se crean en AEM o Adobe Target. Cuando un visitante abre una página web, la lógica de la página determina la audiencia a la que pertenece y muestra el contenido que ha creado para dicha audiencia.

Por ejemplo, una actividad define las experiencias para dos audiencias independientes: mujeres mayores de 30 años y mujeres menores de 30 años. La página para mujeres de un sitio web puede mostrar diferentes productos para cada experiencia.

Se definen experiencias para una actividad. Puede utilizar [consola Actividades](/help/sites-cloud/authoring/personalization/activities.md#adding-editing-an-activity-using-the-activities-console) o el [modo Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode) para añadir experiencias a una actividad.

## Ofertas {#offers}

Una oferta es el contenido que aparece en una ubicación de una página para una experiencia. Utilice ofertas diferentes para distintas experiencias con el fin de maximizar la eficacia del contenido para las audiencias.

Por ejemplo, la página para mujeres de un sitio web de ejemplo puede utilizar ofertas para la imagen de teaser que aparece en la parte superior de la página. Se utiliza una oferta diferente como teaser para la experiencia de mujeres mayores de 30 años y la experiencia de muyeres menores de 30 años.

Utilice la [consola Ofertas](/help/sites-cloud/authoring/personalization/offers.md) para crear ofertas que se pueden usar en varias experiencias. Cree ofertas de un solo uso o añada ofertas de una biblioteca de ofertas al [crear el contenido de destino](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Motor de targeting {#targeting-engine}

El motor de targeting es el mecanismo que lleva a cabo la lógica para el contenido de destino. Las [actividades](/help/sites-cloud/authoring/personalization/activities.md) se configuran para utilizar uno de estos dos motores de targeting disponibles: AEM y Adobe Target.

### AEM {#aem}

AEM proporciona un motor de targeting integrado que procesa solicitudes de páginas y determina el contenido que se debe mostrar. Al utilizar el motor de targeting de AEM, el uso se limita a los segmentos que se crean en AEM para definir las audiencias de las experiencias.

### Adobe Target {#adobe-target}

El motor de targeting de Adobe Target provoca el seguimiento en Adobe Target de la información obtenida de las visitas a una página.

* Al utilizar este motor de targeting, usa los segmentos que importe de Adobe Target para definir audiencias para las experiencias.
* Las actividades que usan el motor de targeting de Adobe Target [se sincronizan con Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Puede utilizar este motor cuando se haya integrado con Adobe Target. <!--You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).-->
