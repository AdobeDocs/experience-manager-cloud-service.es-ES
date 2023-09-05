---
title: Comprensión de la instalación del complemento Demostraciones de referencia
description: Obtenga información sobre Cloud Manager y cómo se utiliza para instalar el complemento.
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '956'
ht-degree: 100%

---

# Comprensión de la instalación del complemento Demostraciones de referencia {#understand-installation}

Obtenga información sobre Cloud Manager y cómo se utiliza para instalar el complemento.

>[!TIP]
>
>Si tiene experiencia con Cloud Manager o desea saltar directamente a la configuración y el uso del complemento, puede pasar a [Creación de un programa y una canalización](create-program.md)
>
>Si desea saber cómo Cloud Manager y AEM trabajan juntos para crear sus entornos de demostración y cómo configurar y utilizar los suyos, siga leyendo el documento actual.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo funciona el proceso de instalación del Complemento de demostraciones de referencia, ilustrando cómo funcionan juntos las diferentes piezas. Después de leer, debería haber logrado lo siguiente:

* Obtenga información básica sobre Cloud Manager.
* Comprenda cómo las canalizaciones ofrecen contenido y configuración a AEM.
* Vea cómo las plantillas pueden crear sitios previamente rellenados con contenido de demostración con solo unos clics.

Este documento se centra en comprender estas partes fundamentales del Complemento de demostraciones de referencia de AEM antes de pasar al siguiente paso del recorrido en el que se inicia la instalación.

Aunque se recomienda pasar por este recorrido paso a paso, si ya tiene experiencia con Cloud Manager o desea ir directamente a la configuración y el uso del complemento, puede pasar a [Creación de un programa y una canalización](create-program.md).

## Función responsable {#responsible-role}

Este recorrido se aplica a un administrador del sistema que sea miembro de la función **Propietario empresarial** en Cloud Manager para su organización.

## Requisitos y requisitos previos {#requirements-prerequisites}

Existen requisitos mínimos para obtener información y comenzar a utilizar el complemento Demostraciones de referencia.

### Conocimiento {#knowledge}

* Conocimientos básicos de Cloud Manager

### Herramientas {#tools}

* Ser miembro de la función **Propietario empresarial** en Cloud Manager para su organización

## Conocimiento de Cloud Manager {#cloud-manager}

Cloud Manager es un componente esencial de AEM as a Cloud Service y sirve como punto de entrada único para la plataforma.

Cloud Manager se utiliza para administrar los recursos de la nube que admiten sus proyectos de AEM, incluidos los entornos y las herramientas necesarias. A los efectos del presente recorrido, no es necesario tener una comprensión completa de Cloud Manager. Sin embargo, debe estar familiarizado con algunos conceptos básicos.

>[!TIP]
>
>Si desea obtener información detallada sobre Cloud Manager, consulte la sección [Recursos adicionales](#additional-resources) para obtener más información.

### Programas {#programs}

Cuando inicia sesión en Cloud Manager, tiene acceso a uno o más **programas**. Un programa se puede definir de muchas maneras diferentes, pero es más fácil pensar en él como asociado con los sitios y experiencias asociados con una identidad de marca.

Si inicia sesión en Cloud Manager representando **WKND Viajes y Aventuras**, puede crear un programa **Vida nocturna WKND** y un programa **Proyectos WKND Backyard**. Ambos programas tendrían entornos AEM para administrar sus sitios asociados.

### Zonas protegidas {#sandboxes}

Los programas pueden ser programas de producción o de zonas protegidas.

* **Un programa de producción** se crea para permitir finalmente el tráfico en directo cuando el programa esté listo para ejecutarse.
* **Un programa de zona protegida** se crea para formación, administración de demostraciones, habilitación, POC, etc. y no está diseñado para tráfico en directo.

Para instalar el complemento Demostraciones de referencia de AEM, cree un programa de zona protegida.

>[!NOTE]
>
>El complemento Demostraciones de referencia de AEM solo está disponible en programas de zona protegida.

## Flujo de instalaciones y uso {#installation-flow}

Ahora que comprende algunos conceptos fundamentales de Cloud Manager, la instalación del complemento Demos de referencia de AEM es conceptualmente sencilla.

1. Inicie sesión en Cloud Manager.
1. Cree un nuevo programa de AEM de zona protegida, con la activación del Complemento Demostraciones de Referencia de AEM como opción para el programa.
1. El contenido y la configuración de la demostración se implementan en el programa. El contenido de la demostración incluye lo siguiente:
   * Plantillas de sitio utilizadas para crear varios AEM Sites con funciones de AEM, previamente rellenadas con ejemplos de prácticas recomendadas.
   * Herramientas de configuración para administrar el contenido de demostración.
1. Inicie sesión en AEM en el nuevo programa de zona protegida, utilice la herramienta de creación rápida de sitios y cree sitios de demostración basados en las plantillas.
1. Utilice las herramientas de configuración para administrar esos sitios y plantillas de demostración, incluso eliminándolos cuando ya no sea necesario.

## Plantillas del sitio de AEM {#site-templates}

Las plantillas de sitio de AEM son paquetes que contienen contenido y estructura predefinidos para un sitio. Las plantillas de sitio se pueden personalizar para satisfacer las necesidades de proyectos específicos, de modo que, cuando los administradores de AEM creen sitios, puedan elegir plantillas que se apliquen a sus casos empresariales.

El complemento Demostraciones de referencia de AEM incluye varias plantillas para diversas necesidades de prueba y demostración. Una vez que haya creado el programa e implementado la canalización para instalar el complemento, puede iniciar sesión en AEM y crear sitios basados en muchas plantillas de demostración

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido del complemento de las demostraciones de referencia de AEM, debe hacer lo siguiente:

* Obtenga información básica sobre Cloud Manager.
* Comprenda cómo las canalizaciones ofrecen contenido y configuración a AEM.
* Vea cómo las plantillas pueden crear sitios previamente rellenados con contenido de demostración con solo unos clics.

Amplíe este conocimiento y continúe con su recorrido de creación rápida de sitios AEM con el documento [Crear un programa y una canalización,](create-program.md) donde aprenderá a configurar un nuevo programa y una canalización para implementar el complemento.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de creación rápida de sitios revisando [Crear un programa y una canalización](create-program.md), los siguientes son algunos recursos opcionales adicionales. Estos recursos profundizan en los conceptos mencionados en este documento. Sin embargo, no son necesarios para continuar el recorrido.

* [Explicación de programas y tipos de programas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/program-types.html?lang=es): empiece aquí para comprender las diferencias entre los programas en directo y los programas de zona protegida.
* [Plantillas de sitio](/help/sites-cloud/administering/site-creation/site-templates.md): si desea obtener más información sobre la estructura de las plantillas de sitio y cómo se utilizan para crear sitios, consulte este documento.
* [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts//cloud-manager-introduction.html?lang=es): si desea obtener más información sobre las funciones de Cloud Manager, puede consultar directamente los documentos técnicos detallados.
