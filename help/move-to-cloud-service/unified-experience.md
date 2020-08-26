---
title: Experiencia unificada para herramientas de refactorización de código
description: Experiencia unificada para herramientas de refactorización de código
translation-type: tm+mt
source-git-commit: c00b10b4d564e05099740b9ff991624db4f37a3d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Experiencia unificada para herramientas de refactorización de código {#unified-experience}

Múltiples herramientas con diferentes puntos de interacción para los clientes crean una experiencia desconectada y aumentan la complejidad de utilizar las herramientas, ya que cada una de ellas tiene diferentes requisitos de ejecución en términos de instalación, configuración y ejecución.

## Benefits {#benefits}

Las herramientas de refactorización Experiencia unificada para código invocan y ejecutan todas las herramientas de refactorización de código que funcionan en el código fuente desde el mismo lugar.

Las herramientas de refactorización de experiencias unificadas para código, junto con los repositorios complementarios, permiten:

* Unifique todas las herramientas que trabajan en la migración del código fuente en una `node.js` aplicación expuesta `aio-cli plugin` para proporcionar al usuario una experiencia de usuario coherente.

* Provisión para realizar la migración general a través de un único comando, a la vez que proporciona flexibilidad para ejecutar una herramienta en particular según sea necesario.

* Simplifique la adición futura de nuevas herramientas, como la adición de nueva herramienta al complemento, simplemente debería requerir la adición de un nuevo comando para desarrolladores y una simple actualización del complemento para el usuario, de modo que la experiencia se mantenga consistente con una adición de más valor.

### Explicación del diseño de la aplicación

Esta herramienta unifica todas las herramientas de refactorización de código en una aplicación node.js expuesta `aio-cli plugin` para proporcionar al usuario una experiencia de usuario coherente.

El complemento consta de dos partes principales:

* **Interfaz de usuario**

   `aio-cli` comandos para ejecutar una o varias herramientas de migración (mediante la encadenado de las herramientas que se van a ejecutar secuencialmente)`config.yaml` que incorporan los parámetros de entrada necesarios

* **Grupo de herramientas de migración subyacente**

   Las herramientas de migración ejecutan sus funciones mediante:

   * Analizar la sección respectiva del código del cliente y realizar la migración (en base a la implementación de código para mejores prácticas) para producir el resultado que luego se puede validar e implementar.

   * Registro de las operaciones realizadas durante la migración, de forma coherente para generar un informe de resumen.

## Uso del complemento {#using-plugin}

El `aio-cli-plugin-aem-cloud-service-migration` refactor el código del cliente, la estructura del repositorio o las configuraciones en el equipo local del cliente. Esta página captura los requisitos detallados y las decisiones de diseño para la experiencia unificada.
Está disponible como fuente abierta para que la comunidad se extienda a casos de uso personalizados.

## Disponibilidad {#availability}

Puede instalar y utilizar el `aio-cli-plugin-aem-cloud-service-migration` mediante `aio-cli` (actualmente solo integrado con el convertidor de despachantes).

Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-Migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para conocer el uso y cómo puede contribuir con esta herramienta.

El código de complemento se ha abierto en Github.

