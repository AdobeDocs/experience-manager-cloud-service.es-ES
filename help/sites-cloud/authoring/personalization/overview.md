---
title: Personalización y segmentación de contenido
description: Descubra cómo puede crear contenido personalizado y con objetivo con AEM
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 89%

---


# Personalización y segmentación de contenido {#personalization-and-content-targeting}

La personalización del contenido web que proporciona a los clientes significa adaptar esas experiencias a sus intereses y necesidades. Puede hacerlo en función de la información que tenga sobre ellos, por ejemplo, resúmenes de compras, edad, sexo y geografía, entre otros.

Con Adobe Experience Manager as a Cloud Service AEM () puede crear una selección de contenido y especificar qué audiencias (grupos de usuarios finales) ven cada experiencia individual. Esto significa que está segmentando las experiencias personalizadas a audiencias específicas.

Cuando el lector esté en línea, el motor de segmentación revisará la información disponible sobre el usuario final y la comparará con las definiciones de las experiencias. A continuación, el motor *“decidirá”* qué experiencia personalizada se debe mostrar.

AEM proporciona un marco de herramientas para:

* Crear contenido con objetivo, adecuado para una amplia gama de audiencias, según la información de cliente disponible.
* Definir las reglas utilizadas para determinar la información de usuario conocida con respecto a la definición de una audiencia.
* Configurar las páginas para presentar experiencias personalizadas segmentadas, para procesar el contenido específico aplicable al usuario final actual.

AEM En la siguiente descripción general se presentan algunos de los términos utilizados para la personalización en el as a Cloud Service de la, seguidos de un orden de acción recomendado.

## Experiencia {#experience}

Una experiencia es el contenido que desea mostrar a los usuarios finales.

## Experiencia personalizada {#personalized-experience}

Una experiencia personalizada es una experiencia que se muestra a una audiencia limitada. Usted define la audiencia y el contenido solo se muestra cuando la información conocida sobre el usuario final actual corresponde con esa definición de la audiencia.

Al crear páginas, puede definir varias experiencias, y cada experiencia se destina a una o más audiencias. Si no se especifica ninguna audiencia, entonces se muestra la experiencia predeterminada.

### Oferta {#offer}

Una oferta es una experiencia personalizada que, a menudo, está disponible durante un período de tiempo limitado.

Por ejemplo, una página de un sitio web de ejemplo puede utilizar ofertas para la imagen de teaser que aparece en la parte superior de la página. Una persona mayor de 30 años y una persona menor de 30 años pueden ver diferentes ofertas como teaser de experiencias.

## Audiencia {#audience}

Una audiencia es un grupo de usuarios finales al que desea dirigirse con contenido personalizado. Cuando un visitante abre una página web, la lógica de página determina la audiencia a la que pertenece en función de la información conocida. En función de esa evaluación, AEM muestra el contenido que ha creado para esa audiencia.

Las audiencias se basan en segmentos de marketing. Se crean en AEM o en Adobe Target; puede crear audiencias de Adobe Target directamente en AEM usando la consola Audiencias.

### Segmento {#segment}

En AEM ContextHub, una audiencia se define como un segmento basado en reglas (condiciones). A continuación, se determinan para procesar el contenido requerido.

## Actividad {#activity}

Una actividad:

* define la asignación de una audiencia específica (segmento) con una experiencia específica
* define el periodo de tiempo durante el que se aplica la segmentación
* identifica el [motor de segmentación](#targeting-engine) que utilizan las páginas

La actividad puede ser una actividad de personalización o una actividad de prueba A/B (en el caso del flujo de trabajo de personalización de Adobe Target y AEM).

Por ejemplo, una actividad puede definir las experiencias para dos audiencias independientes: mujeres mayores de 30 años y mujeres menores de 30 años. Una página del sitio web puede mostrar diferentes productos para cada audiencia.

U, otro ejemplo, el catálogo de productos puede incluir teasers que destaquen los productos de temporada. Así que una actividad de deportes de verano podría definir las audiencias a las que se dirigen los teasers durante los meses de verano.

Utilice la [consola Actividades](/help/sites-cloud/authoring/personalization/activities.md) para crear y administrar las actividades de sus [marcas](#brand). También puede crear actividades a medida que crea su [contenido segmentado](/help/sites-cloud/authoring/personalization/targeted-content.md) con el [Modo de segmentación](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### Marca {#brand}

Una marca contiene una selección de actividades y áreas de marketing.

Cuando crea una marca mediante la consola Actividades, esta también aparece en la consola Ofertas.

### Área {#area}

Un área es una subdivisión de una marca.

## Modo de segmentación {#targeting-mode}

Al crear, este es el modo de edición que se utiliza para activar y configurar los componentes de personalización.

Puede [Crear contenido segmentado](/help/sites-cloud/authoring/personalization/targeted-content.md) utilizando el modo de segmentación de AEM. En el modo segmentación y el componente de Target se proporcionan las herramientas necesarias para crear contenido para las experiencias de las actividades de marketing.

## Fragmento de experiencias {#experience-fragments}

Un conjunto agrupado de componentes que constituyen una experiencia.

[Fragmentos de experiencias](/help/sites-cloud/authoring/fragments/content-fragments.md#personalization-experience-fragment) están formadas por contenido e información (estilo, etc.) para crear una experiencia; se pueden utilizar directamente al crear páginas. Pueden considerarse como un subconjunto de una página AEM. Permiten a los autores de contenido reutilizar contenido en varios canales, incluyendo las páginas de Sites y sistemas de terceros.

Para un ejemplo de personalización, se puede combinar un título, una imagen, una descripción y un botón de llamada a la acción para formar una experiencia de teaser. El uso de fragmentos de experiencias es una parte fundamental del uso de la personalización de Adobe Target.

## Motor de segmentación {#targeting-engine}

El motor de segmentación es el mecanismo que determina la lógica para el contenido segmentado. Las [actividades](/help/sites-cloud/authoring/personalization/activities.md) se configuran para utilizar uno de estos dos motores de segmentación disponibles: AEM y Adobe Target.

El motor de segmentación es la plataforma o el mecanismo que decide qué sistema de personalización utilizar.

Actualmente, AEM puede utilizar:

* [AEM ContextHub](#aem-contexthub) (AEM estándar)
* el motor de personalización de [Adobe Target](#adobe-target)

>[!CAUTION]
>
>Una sola página de AEM no puede utilizar ambos motores al mismo tiempo.
>
>Puede usar ambos motores en páginas separadas dentro del mismo sitio.

### AEM ContextHub {#aem-contexthub}

AEM proporciona el motor de segmentación integrado de [ContextHub](/help/implementing/developing/personalization/contexthub.md) que procesa las solicitudes de páginas y determina el contenido que se debe mostrar. Al utilizar el motor de segmentación de AEM, el uso se limita a los segmentos que se crean en AEM para definir las audiencias de las experiencias.

### Adobe Target {#adobe-target}

El motor de segmentación de [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) provoca que la información recopilada de las visitas a la página sean rastreadas en Adobe Target.

* Al utilizar este motor de segmentación, se usan los segmentos importados de Adobe Target para definir los públicos para las experiencias.
* Las actividades que utilizan el motor de Adobe Target se [sincronizan con Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Puede utilizar este motor cuando se haya [integrado con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

## Configuración del contenido personalizado {#how-to-setup-personalized-content}

Existen varios pasos y definiciones necesarias para entregar el contenido personalizado:

1. Configure el motor de segmentación de las siguientes maneras:

   1. Configurando [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)
   1. Integrándolo con [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)

1. Configure las audiencias.

   1. En función del motor de segmentación, defina la [Audiencia objetivo](https://experienceleague.adobe.com/docs/target/using/audiences/target.html?lang=es) o el [Segmento de ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md) junto con las reglas.

1. Cree su [Marca y actividades](/help/sites-cloud/authoring/personalization/activities.md).

1. Cree la selección de experiencias que desea mostrar a las diferentes audiencias.

1. Personalice estas experiencias [segmentándolas](/help/sites-cloud/authoring/personalization/targeted-content.md) para las audiencias específicas (segmentos).