---
title: Guía rápida de WCAG 2.1
seo-title: Guía rápida de WCAG 2.1
translation-type: tm+mt
source-git-commit: 11f0509334ebe4456612789fd415a3099687dc64

---


# Guía rápida de WCAG 2.1{#quick-guide-to-wcag}

Adobe Experience Manager (AEM) como servicio de nube se ha desarrollado para maximizar el cumplimiento de las directrices de accesibilidad del contenido web.

Las Directrices de Accesibilidad al Contenido [Web versión 2.1 (WCAG)](https://www.w3.org/TR/WCAG/) son un conjunto de directrices internacionalmente reconocidas elaboradas por el [World Wide Web Consortium (W3C)](https://www.w3.org/) en el marco de su Iniciativa de Accesibilidad a la [Web (WAI)](https://www.w3.org/WAI/).

WCAG 2.1 consiste en un conjunto de directrices tecnológicas independientes y criterios de éxito para ayudar a crear contenido web accesible para, y utilizable por, personas con discapacidades. Brindan asesoramiento a autores, diseñadores y desarrolladores de contenido web para garantizar que los recursos que producen sean lo más accesibles posible para el mayor número de personas posible, independientemente de cualquier discapacidad que tengan; por ejemplo, deficiencias visuales, pérdida auditiva, dificultades de aprendizaje, limitaciones relacionadas con la edad, entre otras.

Por ejemplo, describir una imagen (o cualquier otro contenido no textual) mediante el uso del `alt` atributo en HTML beneficia en gran medida a las personas ciegas o con visión parcial. La descripción textual del `alt` atributo puede convertirse en salida de voz o transmitirse a pantallas de braille actualizables electrónicas.

Además, WCAG 2.1 puede dar lugar a ventajas para otros beneficiarios, incluidas las personas que pueden considerarse *con discapacidades* de situación. Las personas que, debido a circunstancias como la tecnología de navegación, la velocidad de conexión de red o el entorno de navegación, pueden experimentar barreras similares a las personas con discapacidad.

Con Adobe Experience Manager, los autores de contenido y/o los propietarios de sitios web pueden crear contenido web que cumpla los criterios de éxito relevantes de WCAG 2.1 de nivel A y de nivel AA.

Por lo tanto, comprender los objetivos de WCAG 2.1 y cómo se estructuran las directrices es una parte importante para comprender la accesibilidad web y cómo las directrices pueden ayudar a crear contenido web accesible.

La intención de WCAG 2.1 es proporcionar directrices que:

* Son **tecnológicamente agnósticos:**
En otras palabras, las directrices que pueden aplicarse a una amplia gama de formatos de contenido web, no solo a HTML. Por lo tanto, WCAG 2.1 puede cubrir el contenido generado por PDF, Flash, JavaScript y otras tecnologías web actuales y futuras, o proporcionado por ellas. <!-- This aims to address a recognized weakness of WCAG 1.0, in that it was focused on HTML at the expense of other web content formats. -->

* Son **comprobables:**
Cada directriz está redactada de manera que pueda probarse objetivamente para garantizar que un grupo de expertos en accesibilidad esté generalmente de acuerdo en que se ha cumplido la directriz. Uno de los problemas de las directrices de accesibilidad es que, si bien algunos pueden ser técnicamente probables, otros requieren juicio humano para determinar si la directriz se ha cumplido o no con éxito. <!-- WCAG 2.1 has been written with the aim of reducing the subjectivity that was present in some of the WCAG 1.0 guidelines and checkpoints. -->

* Apoyar la implementación contextual y **priorizada:**
   <!-- As with WCAG 1.0, --> WCAG 2.1 guidelines are given priorities, relating to the likely impact of not following a guideline on a particular group of users with disabilities. This allows authors to make an informed decision on the most important guidelines for their particular situation. In addition, the concept of *accessibility supported* is introduced. This allows authors to make decisions on how best to use web technologies that may not have full accessibility support, or may require users to have specific assistive technologies and/or browsers in order to benefit from accessibility features.

Estos objetivos han influido significativamente en la estructura de WCAG 2.1.

>[!NOTE]
>
>No es posible crear un sitio web que atienda a cada discapacidad o tipo de persona posible. El propósito de WCAG 2.1 es ayudar a los autores de la Web a crear sitios que sean, en la medida de lo posible, accesibles dentro de ciertas condiciones y dentro de la razón.

<!--
>[!NOTE]
>
>If you are familiar with WCAG 1.0, you will notice some changes in WCAG 2.1. These relate to scope, organization and aim.
-->

## Estructura {#structure}

WCAG 2.1 se estructura de manera que introduce conceptos de creación de contenido web accesible de manera progresiva y detallada. Esto puede dar la impresión de que WCAG 2.1 es un conjunto muy complejo de documentos interrelacionados, pero el objetivo es (progresivamente) proporcionar información más detallada a medida que los autores la necesitan, en lugar de proporcionarla en un documento muy grande.

WCAG 2.1 consta de cuatro principios fundamentales para el diseño accesible, a veces mencionados por el acrónimo **POUR**. Estos son:

1. **Perceptible**: ¿Puede un usuario percibir el contenido web en cuestión?
1. **Operable**: ¿Puede un usuario navegar, introducir datos o interactuar de otro modo con el contenido web?
1. **Comprensible**: ¿Puede un usuario procesar y comprender el contenido web que se le presenta?
1. **Sólido**: ¿Está disponible el contenido web de la forma prevista en una amplia gama de entornos de navegación, incluidos los entornos de navegación antiguos y emergentes?

Para más detalles:
* Cada **principio** consiste en una o más **directrices**.

* Las guías están redactadas como instrucciones, que son positivas (haga esto...) o negativas (no lo haga...).
* Las directrices se numeran de 1.1 a 4.1, cuando el primer número corresponde al principio principal.
* Cada directriz consta de uno o más criterios **de**&#x200B;éxito.
* Los criterios de éxito se escriben como afirmaciones, que son `True` o `False` para una página web determinada.
* Los criterios de éxito pueden incluir una u otra opción, o pueden incluir excepciones; situaciones en las que no es necesario cumplir los criterios de éxito.
* Los criterios de éxito se numeran según la directriz y el principio principales, de 1.1.1 a 4.1.1. También tienen un nombre corto que resume la intención del criterio, para facilitar la referencia. Por ejemplo, el criterio de éxito 1.1.1 es una alternativa no textual.
* Los criterios de éxito incluyen una lista de **las técnicas** relacionadas (que se describen más adelante).

## Recursos de apoyo {#supporting-resources}

Además de los componentes básicos del Grupo de Acción Mundial 2.1 de los Principios, Directrices y Criterios de Éxito, hay una serie de documentos de apoyo. Algunos de ellos proporcionan consejos específicos sobre cómo cumplir con los aspectos de las directrices, otros son referencias más generales que ayudan a los autores web, diseñadores y desarrolladores de todas las capacidades a comprender y utilizar WCAG 2.1 con la mayor eficacia posible.

Si bien WCAG 2.1 es un documento estable y no cambiará, la mayoría de estos recursos de apoyo son documentos dinámicos; cambiarán y crecerán con el tiempo, a medida que surjan nuevas tecnologías, y se encuentran nuevos ejemplos de cómo se puede lograr la accesibilidad web.

### Recursos WCAG 2.1 {#wcag-resources}

Esta lista no pretende ser exhaustiva, sino que presenta una introducción a los recursos disponibles:
* [Esquema de todos los documentos relacionados con el Grupo de Trabajo sobre el Cambio Climático](https://www.w3.org/WAI/standards-guidelines/wcag/)
* [Resumen de los diferentes documentos](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)
* [Directrices de accesibilidad del contenido web (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
* [Novedades en WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/)
* [Guía de referencia rápida para conocer WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Preguntas más frecuentes sobre WCAG 2](https://www.w3.org/WAI/standards-guidelines/wcag/faq/)


### Novedades de WCAG 2.1 {#what-is-new}

[Novedades de WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/) proporciona información valiosa sobre el delta entre WCAG y 2.0 y WCAG 2.1.

[WCAG 2.0 y 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/#versions) aclara además la situación de su relación.

### Técnicas para WCAG 2.1 {#techniques-for-wcag}

Las técnicas para WCAG 2.1 están disponibles en la página [Técnicas para WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/) .

**Las técnicas** forman el nivel por debajo de los criterios de éxito en la jerarquía de WCAG 2.1. La WAI los considera informativos, no normativos. En otras palabras, no es necesario seguir una técnica específica para que un recurso se ajuste a WCAG 2.1.

Dado que las técnicas son mucho más específicas que los criterios de éxito, suelen referirse a una tecnología o tipo de contenido determinado (por ejemplo, HTML o vídeo) o a una situación (por ejemplo, comercio electrónico o aplicación de aprendizaje electrónico). Puede considerar las técnicas como ejemplos comprobados de cómo se pueden cumplir las directrices específicas y los criterios de éxito, por lo que son útiles para los autores y desarrolladores que trabajan en contextos concretos.

Se puede acceder a las técnicas:

* Mediante recopilación (las técnicas pueden ser generales o estar relacionadas con una tecnología o un formato específicos, como HTML, CSS o Secuencias de comandos del lado del cliente), o
* A partir de criterios de éxito relacionados. Las técnicas se pueden aplicar a más de un criterio de éxito.

Cada técnica tiene un número único, que se relaciona con su colección. Por ejemplo, una de las técnicas de ARIA es la *Técnica ARIA2: Identificación de los campos obligatorios con la propiedad*&quot;requerido&quot;.

Las técnicas pueden ser suficientes, aconsejables o fallidas:

* Una técnica *suficiente* es la que, si se sigue, será suficiente para cumplir un criterio de éxito determinado.
* Una técnica *consultiva* es una que, de seguirse, tendrá un efecto positivo en la accesibilidad, pero puede que no sea suficiente por sí sola para garantizar que se cumple un criterio de éxito determinado.
* Un *error* es una técnica que describe un ejemplo específico de dónde no se cumplirían los criterios de éxito.

Los detalles de las técnicas incluyen una descripción, aplicabilidad, ejemplos, recursos para obtener más información y detalles sobre cómo los autores pueden probar la aplicación exitosa de la técnica.

La lista de las técnicas no está completa y la WAI está actualizando constantemente la lista con nuevos ejemplos, que reflejan los avances en la tecnología de la Web, los enfoques de diseño y los resultados de las investigaciones. Así que vale la pena revisar regularmente la lista de las técnicas para nuevas adiciones.

### Explicación de WCAG 2.1 {#understanding-wcag}

Esto se refiere a una serie de documentos, que proporcionan consejos para ayudar a los lectores a apreciar el propósito de directrices específicas y criterios de éxito. Puede [descargar una introducción, además de vínculos a información](https://www.w3.org/WAI/WCAG21/Understanding/)más detallada.

Cada directriz individual y criterio de éxito también tiene su propia página de &quot;Comprensión&quot;, que proporciona información sobre:

* El propósito de la directriz;
* Criterios específicos de éxito;
* Las técnicas de asesoramiento, que ayudan a cumplir los requisitos de la directriz, pero que no entran dentro de ningún criterio de éxito específico.

La página de &quot;comprensión&quot; individual de cada criterio de éxito proporciona información sobre:

* La intención del criterio de éxito;
* Ejemplos generales de cómo se puede cumplir el criterio de éxito;
* Recursos relacionados (no W3C) sobre cómo cumplir el criterio de éxito;
* Técnicas y errores: ejemplos específicos y detallados de cómo se puede cumplir el criterio de éxito (se describen con más detalle a continuación)
* Términos clave: glosario de términos importantes para comprender el criterio de éxito.

Encontrará un ejemplo en: [Entender los criterios de éxito 1.1.1 (&quot;Contenido no textual&quot;)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content).

### Cumplir con WCAG 2.1 {#how-to-meet-wcag}

La sección &quot;Cómo reunirse&quot; está disponible en la página [Cumplir con WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/) . En esta sección se ofrece una presentación alternativa del WCAG, que permite perfeccionar el contenido de las directrices para adaptarlo a los intereses o circunstancias del lector. Los lectores pueden filtrar las técnicas de criterios de éxito que deseen aplicar a la vista especificando tecnologías de contenido web específicas, como hojas de estilo en cascada o secuencias de comandos, o especificando un nivel de prioridad determinado.

Sin filtrar, este recurso proporciona todos los criterios de éxito agrupados por guía. Para cada criterio de éxito, se proporciona lo siguiente:

* Texto del criterio de éxito;
* Un vínculo al documento de &quot;entendimiento&quot; correspondiente;
* Una lista de las técnicas correspondientes que se vinculan a los detalles de cada técnica;
* Una lista de las técnicas de asesoramiento conexas, en relación con los detalles de cada técnica (si existe);
* Una lista de errores relacionados, que se vincula a los detalles de cada error.
