---
title: Traducción y administrador de varios sitios
description: Aprenda a reutilizar el contenido en su proyecto y a administrar sitios web multilingües en AEM.
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# Traducción y administrador de varios sitios {#msm-and-translation}

Las herramientas de traducción y administrador de varios sitios integradas de Adobe Experience Manager simplifican la localización del contenido.

* Multi Site Manager (MSM) y sus funciones de Live Copy le permiten utilizar el mismo contenido del sitio en varias ubicaciones, a la vez que permiten variaciones:
   * [Reutilización del contenido: administrador de varios sitios y Live Copy](msm/overview.md)
* La traducción permite automatizar la traducción del contenido de la página para crear y mantener sitios web multilingües:
   * [Traducción de contenido para sitios multilingües](translation/overview.md)

Estas dos funciones se pueden combinar para satisfacer las necesidades de los sitios web que sean [multinacionales y multilingües](#multinational-and-multilingual-sites).

>[!TIP]
>
>Si es nuevo en traducir contenido, consulte nuestro [Recorrido de traducción de sitios,](/help/journey-sites/translation/overview.md) que es la ruta guiada a través de la traducción del contenido de AEM Sites mediante las poderosas herramientas de traducción de AEM, ideal para aquellos que no tengan experiencia de traducción o AEM.

## Sitios multinacionales y multilingües {#multinational-and-multilingual-sites}

Puede crear contenido de forma eficaz para sitios multinacionales y multilingües mediante el uso combinado del administrador de varios sitios y el flujo de trabajo de traducción.

Normalmente, se crea una ubicación maestra en un idioma y para un país específico y, a continuación, se utiliza ese contenido como base para los demás sitios, utilizando la traducción donde sea necesario.

1. [](translation/overview.md) Traduzca el sitio principal a diferentes idiomas.
1. Utilice [Multi Site Manager](msm/overview.md) para:
   1. Reutilice el contenido del sitio maestro y sus traducciones para crear sitios para otros países y culturas.
   1. Cuando sea necesario, desasocie elementos de Live Copies para añadir detalles de localización.

>[!TIP]
>
>Limite el uso de Multi Site Manager al contenido en un idioma.
>
>Por ejemplo, use el maestro inglés para crear la versión en inglés de las páginas para EE. UU., Canadá, Reino Unido, etc. y utilice el patrón francés para crear la versión en francés de las páginas para Francia, Suiza, Canadá, etc.

El diagrama siguiente ilustra cómo se cruzan los conceptos principales (pero no muestra todos los niveles/elementos implicados):

![Información general sobre la localización](assets/localization-overview.png)

En este, y comparable, escenarios MSM no administra las diferentes versiones de idioma como tales.

* [](msm/overview.md) MSM administra la implementación de contenido traducido de un modelo (es decir, un maestro global) a Live Copies (es decir, los sitios locales), dentro de los límites de un idioma.
* Las capacidades de integración de [translation](translation/overview.md) de AEM, junto con los servicios de administración de traducciones de terceros, administran los idiomas y traducen el contenido a estos diferentes idiomas.

Para casos de uso más avanzados, también se pueden usar MSM entre maestros de idioma.

>[!TIP]
>
>Para todos los casos de uso, se recomienda leer las siguientes prácticas recomendadas:
>
>* [Prácticas recomendadas para MSM](msm/best-practices.md)
>* [Prácticas recomendadas para la traducción](translation/best-practices.md)

