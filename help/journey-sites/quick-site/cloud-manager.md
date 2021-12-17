---
title: Comprender Cloud Manager y el flujo de trabajo de creación rápida de sitios
description: Obtenga información sobre Cloud Manager y cómo vincula el nuevo proceso de creación rápida de sitios.
source-git-commit: 5e1a89743c5ac36635a139ada690849507813c30
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 1%

---


# Comprender Cloud Manager y el flujo de trabajo de creación rápida de sitios {#understand-cloud-manager}

Obtenga información sobre Cloud Manager y cómo vincula el nuevo proceso de creación rápida de sitios.

>[!TIP]
>
>Si su función es exclusivamente desarrollo front-end, puede saltar al artículo [Recuperar información de acceso al repositorio de Git](retrieve-access.md) en este recorrido.
>
>Si es administrador de AEM, administrador de Cloud Manager, es responsable de las tareas de desarrollo del front-end y de administrador, o simplemente desea comprender el proceso de extremo a extremo en AEM para el desarrollo del front-end, siga leyendo el documento actual y continúe con este recorrido.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo funciona la AEM herramienta de creación rápida de sitios y le ofrece una visión general del flujo de extremo a extremo. Después de leer, debe:

* Comprender cómo AEM Sites y Cloud Manager trabajan juntos para facilitar el desarrollo del front-end
* Vea cómo el paso de personalización del front-end está completamente disociado del AEM y no requiere conocimientos AEM.

Este documento se centra en comprender estas partes fundamentales de la solución de creación rápida de sitios antes de pasar al siguiente paso del recorrido en el que se inicia la configuración.

Aunque se recomienda continuar con este recorrido paso a paso, si ya comprende que AEM Sites y Cloud Manager trabajan juntos y desean comenzar directamente con la configuración, puede [vaya al siguiente paso del recorrido.](create-site.md)

## Función responsable {#responsible-role}

Esta parte del recorrido se aplica tanto al administrador de AEM como al administrador de Cloud Manager.

## Requisitos y requisitos previos {#requirements-prerequisites}

Antes de empezar a crear y personalizar sitios, debe cumplir varios requisitos con la herramienta de creación rápida de sitios.

Dado que este recorrido está diseñado para desarrolladores de front-end, administradores y combinaciones de todas las funciones, los requisitos para ambos se enumeran aquí.

Es importante comprender que para el desarrollador del front-end no es necesario tener acceso AEM ni conocimientos.

### Conocimiento {#knowledge}

| Conocimiento | Función |
|---|---|
| Comprensión de las herramientas y los procesos estándar del desarrollo front-end | Desarrollador front-end |
| Conocimientos básicos sobre cómo crear y administrar sitios en AEM | Administrador de AEM |
| Conocimientos básicos de Cloud Manager | Administrador de Cloud Manager |

Para el desarrollador de front-end, no se necesita ningún conocimiento AEM.

### Herramientas {#tools}

| Herramienta | Función |
|---|---|
| Entorno de desarrollo front-end preferido | Desarrollador front-end |
| npm | Desarrollador front-end |
| webpack | Desarrollador front-end |
| Acceso a Cloud Manager | Administrador de Cloud Manager |
| Ser miembro de **Propietario empresarial** función en Cloud Manager | Administrador de Cloud Manager |
| Ser administrador de sistemas en Cloud Manager | Administrador de Cloud Manager |
| Acceso al Admin Console | Administrador de Cloud Manager |
| Sea miembro de **Administrador de implementación** función en Cloud Manager | Administrador de Cloud Manager |
| Sea miembro de **Administrador de implementación** función en Cloud Manager | Desarrollador front-end |

Para el desarrollador front-end, no es necesario utilizar AEM.

>[!TIP]
>
>Si no está familiarizado con las funciones y la administración de funciones de Cloud Manager, consulte el documento Permisos basados en roles en la [Recursos adicionales](#additional-resources) para obtener más información.

## Cloud Manager {#cloud-manager}

Cloud Manager es un componente esencial de AEM as a Cloud Service y sirve como punto de entrada único para la plataforma.

Para dar compatibilidad a los clientes con configuraciones de desarrollo empresarial, AEM as a Cloud Service se integra completamente con Cloud Manager y sus canalizaciones de CD/CI creadas específicamente. La herramienta de creación rápida de sitios amplía estas funciones para admitir canalizaciones de desarrollo front-end dedicadas.

A los efectos del presente recorrido, no es necesario tener una comprensión completa de Cloud Manager. En un nivel superior, Cloud Manager consta de varios niveles de estructura.

![Estructura de Cloud Manager](assets/cloud-manager-structure.png)

* **INQUILINO** - Cada cliente está aprovisionado con un inquilino. **WKND Viajes y Aventuras** puede ser inquilino.
* **PROGRAMAS** - Cada inquilino tiene uno o más programas. La variable **WKND Viajes y Aventuras** el inquilino puede tener un **Vida nocturna WKND** y **Proyectos de la tarde de WKND** programa.
* **ENTORNOS** - Cada programa tiene múltiples entornos, como producción para contenido en directo, y ensayo y desarrollo para fines de desarrollo. **Vida nocturna WKND** y **Proyectos de la tarde de WKND** los programas tendrían entornos de desarrollo, fase y producción.
* **REPOSITORIO** - Los entornos tienen repositorios Git donde se mantiene el código de la aplicación y del front-end.
* **HERRAMIENTAS Y FLUJOS DE TRABAJO** : Las canalizaciones administran la implementación de código desde los repositorios a los entornos.

## Flujo de desarrollo del front-end para la creación rápida de sitios {#flow}

El flujo general es sencillo e intuitivo, aunque aún no tenga una amplia experiencia con Cloud Manager.

1. El administrador de AEM inicia sesión en un entorno de AEM y crea un nuevo sitio con una plantilla de sitio.
1. El administrador de Cloud Manager crea una canalización de front-end en Cloud Manager. La canalización organiza la implementación de código desde un repositorio de Git a un entorno AEM.
1. El administrador de AEM exporta el tema del sitio desde la instancia AEM del programa y lo proporciona al desarrollador de front-end.
1. El administrador de Cloud Manager concede al desarrollador del front-end acceso al repositorio de Git de AEM donde se pueden realizar personalizaciones.
1. El desarrollador de front-end recupera las credenciales de acceso para acceder a Git y a la canalización.
1. El desarrollador front-end personaliza el tema, lo prueba con contenido real del sitio mediante un proxy y luego confirma los cambios en el repositorio de Git.
1. El desarrollador de front-end ejecuta la canalización para implementar las personalizaciones de temas en el entorno de producción del programa.

![Flujo de creación rápida del sitio](assets/qsc-flow.png)

La principal ventaja de utilizar la herramienta de creación rápida de sitios es que el desarrollador de front-end es el único responsable de la personalización real. El desarrollador de front-end no tiene interacción con AEM o necesita tener conocimientos de AEM.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de creación rápida AEM sitio, debe:

* Comprender cómo AEM Sites y Cloud Manager trabajan juntos para facilitar el desarrollo del front-end
* Vea cómo el paso de personalización del front-end está completamente disociado del AEM y no requiere conocimientos AEM.

Aproveche este conocimiento y continúe con su recorrido de Creación Rápida AEM Sitio revisando el documento [Crear sitio a partir de una plantilla,](create-site.md) donde aprenderá a crear rápidamente un nuevo sitio AEM con una plantilla.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de creación rápida del sitio revisando el documento [Crear sitio a partir de una plantilla,](create-site.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido.

* [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) : Si desea obtener más información sobre las funciones de Cloud Manager, puede consultar directamente los documentos técnicos detallados.
* [Permisos basados en roles](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) : Cloud Manager tiene funciones preconfiguradas con los permisos adecuados. Consulte este documento para obtener detalles sobre estas funciones y cómo administrarlas.
* [npm](https://www.npmjs.com) - AEM temas utilizados para construir sitios rápidamente se basan en npm.
* [webpack](https://webpack.js.org) - AEM temas utilizados para construir sitios rápidamente dependen del webpack.
