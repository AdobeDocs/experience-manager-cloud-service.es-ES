---
title: Experiencia unificada para herramientas de refactorización de código
description: Experiencia unificada para herramientas de refactorización de código
translation-type: tm+mt
source-git-commit: c554506aea99518c94666f5d2e6151a3dce3b91e
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---


# Experiencia unificada para herramientas de refactorización de código {#unified-experience}

Las herramientas de refactorización Experiencia unificada para código unifican la experiencia de ejecución de AEM como herramientas de refactorización de código Cloud Service que funcionan en archivos, código y repositorios de distribución.

Esta herramienta reduce la complejidad del uso de herramientas de refactorización de código, y cada una de ellas tiene diferentes requisitos de ejecución en términos de instalación, configuración y ejecución.

## Benefits {#benefits}

Las herramientas de refactorización Experiencia unificada para código invocan y ejecutan todas las herramientas de refactorización de código que funcionan en el código fuente desde el mismo lugar.

Las herramientas de refactorización de experiencias unificadas para código, junto con los repositorios complementarios, permiten:

* Unifique todas las herramientas que trabajan en la migración del código fuente en una `node.js` aplicación expuesta `aio-cli plugin` para proporcionar al usuario una experiencia de usuario coherente.

* Provisión para realizar la migración general a través de un único comando, a la vez que proporciona flexibilidad para ejecutar una herramienta en particular según sea necesario.

* Simplifique la adición futura de nuevas herramientas, como la adición de nueva herramienta al complemento, simplemente debería requerir la adición de un nuevo comando para desarrolladores y una simple actualización del complemento para el usuario, de modo que la experiencia se mantenga consistente con una adición de más valor.

## Explicación del complemento {#understanding-plugin}

El `aio-cli-plugin-aem-cloud-service-migration` refactor el código del cliente, la estructura del repositorio o las configuraciones en el equipo local del cliente. Esta página captura los requisitos detallados y las decisiones de diseño para la experiencia unificada.
Está disponible como fuente abierta para que la comunidad se extienda a casos de uso personalizados.

Esta herramienta unifica todas las herramientas de refactorización de código en una aplicación node.js expuesta `aio-cli plugin` para proporcionar al usuario una experiencia de usuario coherente. El complemento explora la base de código local del cliente y produce AEM como un código compatible con el Cloud Service, configuraciones y paquetes que luego pueden implementarse en entornos de Cloud Service.

El complemento consta de dos partes principales:

* **Interfaz de usuario**

   `aio-cli` comandos para ejecutar una o varias herramientas de migración (mediante la encadenado de las herramientas que se van a ejecutar secuencialmente)`config.yaml` que incorporan los parámetros de entrada necesarios

* **Grupo de herramientas de migración subyacente**

   Las herramientas de migración ejecutan sus funciones mediante:

   * Analizar la sección respectiva del código del cliente y realizar la migración (en base a la implementación de código para mejores prácticas) para producir el resultado que luego se puede validar e implementar.

   * Registro de las operaciones realizadas durante la migración, de forma coherente para generar un informe de resumen.

## Disponibilidad {#availability}

Puede instalar y utilizar el `aio-cli-plugin-aem-cloud-service-migration` mediante `aio-cli`.

>[!NOTE]
>Actualmente, esta herramienta solo está integrada con Dispatcher Converter.

Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-Migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para conocer el uso y cómo puede contribuir con este código de complemento que es de código abierto en GitHub.

