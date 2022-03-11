---
title: Experiencia unificada para herramientas de refactorización de código
description: Experiencia unificada para herramientas de refactorización de código
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Experiencia unificada para herramientas de refactorización de código {#unified-experience}

Hemos desarrollado herramientas para automatizar algunas de las tareas de refactorización de código necesarias para ser compatibles con AEM as a Cloud Service. Para reducir la complejidad asociada con la instalación y configuración de diferentes herramientas de refactorización de código, hemos desarrollado un complemento para unificar las herramientas que funcionan en código y repositorios.

## Ventajas {#benefits}

El complemento Experiencia unificada ofrece las siguientes ventajas:

* Unifica las herramientas que funcionan en el código fuente en una `node.js` aplicación expuesta como `aio-cli ` para proporcionar al usuario una experiencia de usuario coherente.

* Proporciona la capacidad de ejecutar todas las herramientas a través de un único comando, al tiempo que proporciona la flexibilidad para ejecutar herramientas específicas según sea necesario.

* Proporciona extensibilidad para simplificar la adición de nuevas herramientas y mantener la coherencia de la experiencia.

## Explicación del complemento {#understanding-plugin}

La variable `aio-cli-plugin-aem-cloud-service-migration` el complemento consta de dos partes principales:

* **Interfaz de usuario**

   * `aio-cli` comandos para ejecutar una o más herramientas de refactorización de código (mediante encadenamiento de las herramientas que se van a ejecutar secuencialmente).
   * `config.yaml` que incorpora los parámetros de entrada necesarios.

* **Grupo de herramientas de refactorización de código subyacente**

   Las herramientas de refactorización de código ejecutan sus funcionalidades mediante:

   * Analizar la sección respectiva del código del cliente y manipular el código (en función de la implementación del código para prácticas recomendadas) para producir el resultado que se puede validar e implementar.

   * Creación de un informe de resumen para registrar las operaciones realizadas durante la ejecución.

## Disponibilidad {#availability}

Consulte [Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obtener más información sobre el uso y cómo puede contribuir a este código de complemento de código abierto en GitHub.

>[!NOTE]
>Actualmente, el complemento está integrado con AEM Dispatcher Converter y el Modernizador de repositorio.
