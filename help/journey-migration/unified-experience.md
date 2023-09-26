---
title: Experiencia unificada para herramientas de refactorización de código
description: Obtenga información sobre la experiencia unificada para las herramientas de refactorización de código.
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# Experiencia unificada para herramientas de refactorización de código {#unified-experience}

Adobe ha desarrollado herramientas para automatizar algunas de las tareas de refactorización de código necesarias para ser compatibles con Adobe Experience Manager AEM () as a Cloud Service. Para reducir la complejidad asociada con la instalación y configuración de diferentes herramientas de refactorización de código, Adobe ha desarrollado un complemento para unificar las herramientas que funcionan en el código y los repositorios.

## Ventajas {#benefits}

El complemento de experiencia unificada ofrece las siguientes ventajas:

* Unifica las herramientas que funcionan en el código fuente en una sola `node.js` aplicación expuesta como `aio-cli ` para proporcionar una experiencia de usuario coherente al usuario.

* Ejecuta todas las herramientas mediante un único comando, a la vez que proporciona la flexibilidad para ejecutar herramientas específicas según sea necesario.

* Simplifica la adición de nuevas herramientas, a la vez que mantiene la coherencia de la experiencia.

## Explicación del complemento {#understanding-plugin}

El `aio-cli-plugin-aem-cloud-service-migration` El complemento consta de dos partes principales:

* **Interfaz de usuario**

   * `aio-cli` comandos para ejecutar una o más herramientas de refactorización de código (encadenando las herramientas que se van a ejecutar secuencialmente).
   * `config.yaml` que incorpora los parámetros de entrada necesarios.

* **Conjunto de herramientas de refactorización de código subyacente**

  Las herramientas de refactorización de código ejecutan sus funcionalidades mediante:

   * Escanear la sección correspondiente del código del cliente y manipular el código (en función de la implementación del código para obtener las prácticas recomendadas) para generar el resultado que se pueda validar e implementar.

   * Producir un informe de resumen para registrar las operaciones realizadas durante la ejecución.

## Disponibilidad {#availability}

Consulte [Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) donde puede obtener información sobre el uso y cómo puede contribuir al código de este complemento de código abierto en GitHub.

>[!NOTE]
>AEM Actualmente, el complemento está integrado con Dispatcher Converter y el Modernizador de repositorios de Dispatcher.
