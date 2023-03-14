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

AEM Hemos desarrollado herramientas para automatizar algunas de las tareas de refactorización de código necesarias para ser compatibles con las versiones as a Cloud Service de los. Para reducir la complejidad asociada con la instalación y configuración de diferentes herramientas de refactorización de código, hemos desarrollado un complemento para unificar las herramientas que funcionan en el código y los repositorios.

## Ventajas {#benefits}

El complemento de experiencia unificada ofrece las siguientes ventajas:

* Unifica las herramientas que funcionan en el código fuente en una sola `node.js` aplicación expuesta como `aio-cli ` para proporcionar una experiencia de usuario coherente al usuario.

* Proporciona la capacidad de ejecutar todas las herramientas mediante un único comando, al mismo tiempo que proporciona la flexibilidad para ejecutar herramientas específicas según sea necesario.

* Proporciona extensibilidad para simplificar la adición de nuevas herramientas, manteniendo al mismo tiempo la experiencia coherente.

## Explicación del complemento {#understanding-plugin}

El `aio-cli-plugin-aem-cloud-service-migration` El complemento consta de dos partes principales:

* **Interfaz de usuario**

   * `aio-cli` comandos para ejecutar una o más herramientas de refactorización de código (mediante el encadenamiento de las herramientas que se van a ejecutar secuencialmente).
   * `config.yaml` que incorpora los parámetros de entrada necesarios.

* **Conjunto de herramientas de refactorización de código subyacente**

   Las herramientas de refactorización de código ejecutan sus funcionalidades mediante:

   * Escanear la sección correspondiente del código del cliente y manipular el código (en función de la implementación del código para obtener las prácticas recomendadas) para generar el resultado que se pueda validar e implementar.

   * Producir un informe de resumen para registrar las operaciones realizadas durante la ejecución.

## Disponibilidad {#availability}

Consulte [Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obtener más información sobre el uso y cómo puede contribuir al código de este complemento de código abierto en GitHub.

>[!NOTE]
>AEM Actualmente, el complemento está integrado con Dispatcher Converter y el Modernizador de repositorios de Dispatcher.
