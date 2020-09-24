---
title: Experiencia unificada para herramientas de refactorización de código
description: Experiencia unificada para herramientas de refactorización de código
translation-type: tm+mt
source-git-commit: 5d2b14c827603297a59cba7180fc1a68de0c841a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---


# Experiencia unificada para herramientas de refactorización de código {#unified-experience}

Hemos desarrollado herramientas para automatizar algunas de las tareas de refactorización de código necesarias para ser compatibles con AEM como Cloud Service. Para reducir la complejidad asociada con la instalación y configuración de diferentes herramientas de refactorización de código, hemos desarrollado un complemento para unificar las herramientas que funcionan en código y repositorios.

## Benefits {#benefits}

El complemento Experiencia unificada ofrece las siguientes ventajas:

* Unifica las herramientas que trabajan en el código fuente en una `node.js` aplicación expuesta como `aio-cli ` complemento para proporcionar una experiencia de usuario coherente al usuario.

* Proporciona la capacidad de ejecutar todas las herramientas mediante un único comando, al tiempo que proporciona la flexibilidad necesaria para ejecutar herramientas específicas según sea necesario.

* Proporciona extensibilidad para simplificar la adición de nuevas herramientas, manteniendo la coherencia de la experiencia.

## Explicación del complemento {#understanding-plugin}

El `aio-cli-plugin-aem-cloud-service-migration` complemento consta de dos partes principales:

* **Interfaz de usuario**

   * `aio-cli` comandos para ejecutar una o más herramientas de refactorización de código (mediante la encadenado de las herramientas que se van a ejecutar secuencialmente).
   * `config.yaml` que incorpora los parámetros de entrada necesarios.

* **Grupo de herramientas de refactorización de código subyacente**

   Las herramientas de refactorización de código ejecutan sus funciones mediante:

   * Escanear la sección correspondiente del código del cliente y manipular el código (basado en la implementación de código para mejores prácticas) para producir el resultado que luego se puede validar e implementar.

   * Producción de un informe de resumen para registrar las operaciones realizadas durante la ejecución.

## Disponibilidad {#availability}

Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-Migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para conocer el uso y cómo puede contribuir a este código de complemento que es de código abierto en GitHub.

>[!NOTE]
>Actualmente, el complemento está integrado con AEM Dispatcher Converter y el Modernizador de repositorio.
