---
title: Pruebas funcionales
description: Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en el proceso de implementación de AEM as a Cloud Service para garantizar la calidad y fiabilidad de su código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 5%

---


# Introducción {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Pruebas funcionales"
>abstract="Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en el proceso de implementación de AEM as a Cloud Service. Las pruebas garantizan la calidad y fiabilidad del código."

Descubra las puertas de calidad disponibles en el [proceso de implementación de AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) y los diversos tipos de pruebas funcionales integradas. Descubra cómo puede contribuir y optimizar su uso en el marco de una estrategia de pruebas completa.

## Acerca de las pruebas funcionales

El diagrama siguiente proporciona información general de alto nivel sobre las canalizaciones disponibles en el contexto de una estrategia general de pruebas y el [proceso de implementación de AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md).

![Puertas de calidad para la implementación de AEM Cloud Service](assets/functional-testing/quality-gates-compact.svg)

## Finalidad de las pruebas funcionales

El propósito de las canalizaciones de implementación de AEM Cloud Service es facilitar implementaciones sólidas y seguras en varias etapas del ciclo de vida de su desarrollo y lanzamiento del producto de AEM. Estas canalizaciones incorporan varias puertas de calidad en diferentes niveles para garantizar la integridad y seguridad de las implementaciones, tanto para los cambios de la aplicación de AEM como para las actualizaciones de productos de AEM.

Adobe proporciona varias puertas de calidad integradas, mientras que otras requieren su intervención para la implementación y configuración. Estas puertas de calidad son versátiles, se aplican en varias etapas del ciclo vital y se integran directamente en la configuración de desarrollo y los procesos de CI/CD.

Las puertas de calidad integradas validan principalmente la funcionalidad del producto AEM en el contexto de la aplicación de AEM. Por el contrario, las puertas de calidad personalizadas que configure están diseñadas para comprobar que las funciones críticas de la aplicación y las interacciones del usuario funcionan según lo previsto. De forma conjunta, estos dos conjuntos de puertas de calidad trabajan juntos para garantizar implementaciones automatizadas sólidas y seguras, tanto para las modificaciones de código como para las actualizaciones de productos de AEM.

Es importante tener en cuenta que estas puertas de calidad no están pensadas para ser un marco de prueba completo para toda la estrategia de prueba. El producto AEM se somete a amplias pruebas antes de entrar en el proceso de implementación del servicio en la nube de AEM. Del mismo modo, la aplicación ya debe ser de alta calidad antes de que llegue a la fase de implementación. Este enfoque garantiza que las puertas de calidad se centren en su objetivo principal de salvaguardar el proceso de despliegue, en lugar de ser un sustituto de un régimen de pruebas completo.

## Puertas de calidad en pruebas

El diagrama siguiente proporciona una vista detallada de las puertas de calidad disponibles y su uso en la estrategia general de pruebas y el [proceso de implementación de AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md).

![Puertas de calidad para la implementación de AEM Cloud Service](assets/functional-testing/quality-gates-overview.svg)

### Puertas de calidad proporcionadas por el cliente

|                               | Pruebas de unidad | Pruebas funcionales <br/> personalizadas | Pruebas de IU <br/> personalizadas | Validaciones del cliente <br/> | Pruebas <br/> manuales |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **Canalización de producción** | Sí<br/>bloqueo<br/> | Sí<br/>bloqueo<br/>tiempo de espera de 60 m | Sí<br/>bloqueo<br/>tiempo de espera de 30 m | No | No |
| **Canalización que no es de producción** | Sí<br/>bloqueo<br/> | Tiempo de espera de inclusión <br/>bloqueo<br/>60m | Tiempo de espera de inclusión <br/>bloqueo<br/>30m | No | No |
| **Validación interna de Adobe** | Sí<br/>bloqueo<br/> | Sí<br/>bloqueo<br/>tiempo de espera de 60 m | Sí<br/>bloqueo<br/>tiempo de espera de 30 m | No | No |
| **CD/CI del cliente** | Sí | Sí | Sí | Sí | Sí |
| **Desarrollador local del cliente** | Sí | Sí | Sí | Sí | Sí |

### Prueba unitaria

Se recomienda proporcionar las pruebas unitarias para la aplicación de AEM, que son la base de cada estrategia de prueba. Están pensados para correr rápido y a menudo y dar una respuesta temprana y rápida. Están totalmente integrados en los flujos de trabajo de los desarrolladores, su propio CD/CI y las canalizaciones de implementación del servicio en la nube de AEM.

Se implementan mediante JUnit y se ejecutan con Maven. Consulte el [módulo principal del tipo de archivo del proyecto de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using#unit-tests) para ver un ejemplo de prueba unitaria de AEM y cómo empezar.

### Calidad de código

Esta puerta de calidad está configurada de forma predeterminada y ejecuta un análisis de código estático en el código de la aplicación AEM.

Consulte [Prueba de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md) y [Reglas de calidad de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md) para obtener más información.

### Pruebas de productos

Las pruebas funcionales del producto son pruebas de integración (TI) HTTP estables para la funcionalidad principal de AEM, incluidas las tareas de creación y replicación. Adobe los proporciona y los mantiene de forma predeterminada. Su objetivo es evitar que se implementen cambios en el código de aplicación personalizado si rompen la funcionalidad principal del producto de AEM.

Utilizan JUnit para la implementación, se ejecutan con Maven y dependen de los [clientes de prueba de AEM](https://github.com/adobe/aem-testing-clients) oficiales. El grupo de pruebas del producto se mantiene como
un [proyecto de código abierto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke), sigue las prácticas recomendadas y puede considerarse un buen punto de partida para la implementación de pruebas.

### Pruebas funcionales personalizadas

Al igual que las pruebas de producto, las pruebas funcionales de cliente son pruebas de integración HTTP (TI) implementadas con JUnit, ejecutadas con Maven y creadas sobre los [clientes de prueba de AEM](https://github.com/adobe/aem-testing-clients) oficiales.

>[!NOTE]
>
>Las pruebas funcionales personalizadas se ejecutan en canalizaciones de producción y de no producción (inclusión) utilizadas para implementaciones de cambios de aplicaciones de AEM y actualizaciones push de productos de AEM. Desempeñan un papel crucial a la hora de garantizar que su aplicación funcione correctamente y mejorar la seguridad de las versiones. Las pruebas funcionales del cliente también se ejecutan en canalizaciones de validación internas previas al lanzamiento para cada cliente, lo que ayuda a proporcionar comentarios tempranos.

Para mantener ejecuciones de canalización eficientes, Adobe recomienda centrarse en las funciones clave y en los flujos de interacción del usuario principal, con el objetivo de un tiempo de ejecución de prueba funcional de unos 15 minutos o menos. Los grupos de pruebas funcionales completos que superen este tiempo deben ejecutarse como parte de las canalizaciones de validación de cliente generales durante el proceso de desarrollo.

Consulte [pruebas de productos de código abierto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) o el módulo [it.tests del arquetipo de AEM Projects](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) para ver ejemplos.

Consulte [Pruebas funcionales de Java](/help/implementing/cloud-manager/java-functional-testing.md) para obtener más información.

### Pruebas de IU personalizadas

Para maximizar el control de riesgos para el desarrollo específico del cliente, Adobe le recomienda capturar las pruebas de interfaz de usuario críticas en AEM as a Cloud Service. Manténgalos limitados, pero centrados en maximizar su impacto en la experiencia del cliente.

Las pruebas se empaquetan en una imagen Docker diseñada para ser lo más volátil posible (con soporte para Cypress, Playwright, Selenium, Java y JavaScript). Siguen las mismas características y propósitos que las pruebas funcionales personalizadas.

>[!NOTE]
>
>Las pruebas de IU personalizadas se ejecutan en canalizaciones de producción y de no producción (inclusión) utilizadas para implementaciones de cambios de aplicaciones de AEM y actualizaciones push de productos de AEM. Son esenciales para garantizar el correcto funcionamiento de su aplicación y mejorar la seguridad de liberación. Las pruebas de interfaz de usuario del cliente también se ejecutan en canalizaciones de validación internas previas al lanzamiento para cada cliente, lo que ayuda a proporcionar comentarios tempranos.
>
>Los contenedores que no son de Selenium deben ejecutar pruebas utilizando un proxy HTTP basado en las variables de entorno de la [Sección de pruebas de interfaz de usuario](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing).

Para mantener la eficacia de la ejecución de las canalizaciones, Adobe recomienda centrarse en las funciones clave y en los flujos de interacción principales del usuario. Los grupos de pruebas de IU completa que superen esta puerta de calidad deben ejecutarse como parte de las canalizaciones generales de validación del cliente. Incorpórelos al proceso de desarrollo del cliente.

Consulte [pruebas de ejemplo de código abierto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) o el módulo [ui.tests del tipo de archivo de AEM Projects](/help/implementing/cloud-manager/ui-testing.md) para ver ejemplos.

Consulte [Pruebas de IU personalizadas](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obtener más información.

### Auditoría de experiencias

La puerta de calidad de auditoría de experiencias está realizando [auditorías de Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) en la página web del cliente.

AEM proporciona esta puerta de calidad de forma predeterminada, pero no bloquea las canalizaciones de implementación. De manera predeterminada, se realiza una auditoría en la página raíz (`/`) de la instancia de publicación. Puede contribuir configurando hasta 25 rutas personalizadas que se tienen en cuenta en las auditorías.

Consulte [Pruebas de auditoría de experiencias](/help/implementing/cloud-manager/reports/report-experience-audit.md) para obtener más información.

### Validaciones de clientes

La puerta de calidad de las validaciones del cliente es un marcador de posición para la estrategia y el esfuerzo de prueba propios del cliente, ejecutados antes de que los cambios de la aplicación del cliente lleguen a las canalizaciones de implementación de la nube de AEM.

Aquí puede elegir las herramientas y los marcos que prefiera. A diferencia de las pruebas de funciones de cliente y las pruebas de IU personalizadas, no hay límites relacionados con AEM as a Cloud Service. Como tal, Adobe recomienda realizar pruebas funcionales y de interfaz de usuario de larga duración aquí.

Aunque puede elegir cualquier herramienta y marco de trabajo, Adobe sugiere alinear las pruebas de integración e interfaz de usuario basadas en HTTP con las herramientas y los marcos utilizados en las puertas de calidad de las pruebas funcionales y de interfaz de usuario personalizadas. Además, Adobe recomienda incorporar [Entornos de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) en su estrategia de pruebas local para imitar de cerca los entornos de nube de AEM.

### Pruebas manuales

La puerta de calidad de prueba manual es un marcador de posición para los clientes que realizan pruebas manuales. Dado que las canalizaciones de nube de AEM no admiten las pruebas manuales, deben incluirse en la estrategia de pruebas local.

Para las pruebas manuales, puede resultar útil integrarse con un entorno de desarrollo de AEM Cloud Service adicional.
