---
title: Desarrollo de sitios con la canalización front-end
description: La canalización front-end mejora la independencia del desarrollador y acelera el proceso de desarrollo. Este artículo describe las consideraciones clave del proceso de compilación del front-end para garantizar un rendimiento y una eficiencia óptimos.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 3%

---


# Desarrollo de sitios con canalización front-end {#developing-site-with-front-end-pipeline}

{{traditional-aem}}

La [canalización front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) ofrece a los desarrolladores de front-end una mayor independencia y acelera significativamente el desarrollo. Este artículo explica cómo funciona el proceso y destaca las consideraciones clave para ayudarle a sacar el máximo partido a él.

>[!TIP]
>
>Si todavía no está familiarizado con el uso de la canalización front-end y sus ventajas, consulte la guía [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md). Proporciona un ejemplo de cómo implementar un nuevo sitio rápidamente y personalizar su tema independientemente del desarrollo del back-end.

## Comprender la configuración de la canalización front-end y el proceso de compilación en AEM Cloud Manager {#front-end-build-contract}

Similar al [entorno de compilación de pila completa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md), la canalización front-end tiene su propio entorno. Los desarrolladores tienen cierta flexibilidad con esta canalización, siempre que sigan el contrato de versión del front-end.

La canalización front-end requiere que el proyecto front-end `Node.js` use la directiva de script `build` para generar la compilación que implementa. Este requisito existe porque Cloud Manager usa el comando `npm run build` para generar el proyecto implementable para la compilación del front-end.

El contenido resultante de la carpeta `dist` es lo que Cloud Manager implementa en última instancia, ofreciéndolos como archivos estáticos. Estos archivos están alojados externamente en AEM, pero están disponibles mediante una dirección URL `/content/...` en el entorno implementado.

## Versiones de Node.js compatibles {#node-versions}

El entorno de compilación del front-end es compatible con las siguientes `Node.js` versiones:

* 23
* 22
* 20
* 18
* 16
* 14 (valor predeterminado)
* 12

Puede usar la `NODE_VERSION` [variable de entorno](/help/implementing/cloud-manager/environment-variables.md) para establecer la versión deseada.

## Prácticas recomendadas para nombrar y administrar canalizaciones front-end en AEM {#single-source-of-truth}

Una práctica recomendada para las implementaciones de AEM es mantener una única fuente fiable y clara. Cloud Manager está diseñado para reforzar este principio. Sin embargo, como la canalización front-end permite desacoplar partes del código, es esencial una configuración adecuada. Para evitar conflictos, asegúrese de que varias canalizaciones front-end no se implementen en el mismo sitio dentro del mismo entorno.

Por este motivo, y especialmente cuando se crean varias canalizaciones front-end, Adobe recomienda mantener una convención de nombres sistemática. Puede utilizar las siguientes recomendaciones:

* El nombre del módulo front-end, definido por la propiedad `name` del archivo `package.json`, debe contener el nombre del sitio al que se aplica. Por ejemplo, para un sitio ubicado en `/content/wknd`, el nombre del módulo front-end sería algo así como `wknd-theme`.
* Cuando un módulo front-end comparte el mismo repositorio de Git con otros módulos, el nombre de su carpeta debe ser igual o contener el mismo nombre que el módulo front-end. Por ejemplo, si el módulo front-end se llama `wknd-theme`, el nombre de la carpeta adjunta sería algo así como `wknd-theme-sources`.
* El nombre de la canalización front-end de Cloud Manager también debe contener el nombre del módulo front-end y también agregar el entorno al que se implementa (producción o desarrollo). Por ejemplo, para el módulo front-end denominado `wknd-theme`, la canalización podría tener el nombre `wknd-theme-prod`.

Esta convención evita los siguientes errores de implementación:

* Aplicación de un módulo front-end al sitio incorrecto.
* Creación de varios módulos front-end que apliquen el mismo sitio, que se sobrescribirían entre sí.
* Crear varias canalizaciones front-end para los mismos orígenes, lo que podría provocar condiciones de carrera, sin garantizar el orden de las implementaciones.

## Coordinación del desarrollo front-end y back-end para lograr estabilidad en AEM {#separation-of-concerns}

Una práctica recomendada clave para cualquier separación de intereses es diseñar y administrar el contrato cuidadosamente para definir los límites entre ellos. En la canalización front-end, este contrato es la salida HTML y JSON procesada por el sitio. Mantener la estabilidad de esta salida garantiza que la canalización front-end ofrezca el máximo valor, lo que permite que el equipo front-end trabaje de forma independiente.

Actualmente no hay ninguna capacidad integrada para ejecutar la canalización de pila completa sincrónicamente con las canalizaciones front-end. Por lo tanto, al separar el desarrollo front-end de la canalización de pila completa, es crucial administrar el contrato con cuidado que define sus límites. Este contrato suele consistir en el HTML, JSON o ambos procesados por Experience Manager. Cualquier cambio en este contrato debe coordinarse cuidadosamente entre los equipos que administran las diferentes canalizaciones para garantizar una transición sin problemas y una secuencia adecuada de las actualizaciones.

Por lo general, se recomiendan los siguientes pasos al realizar cambios en la salida de HTML o JSON, especialmente cuando ambas áreas se ven afectadas.

1. El equipo back-end configura primero un entorno de desarrollo con la nueva salida HTML o JSON.
   1. A través de la canalización de pila completa, implementan el código necesario para procesar la nueva salida de HTML o JSON, o ambas, que se desee.
   1. Si es a un entorno al que el equipo front-end no tenía acceso anteriormente, se deben realizar los siguientes pasos.
      1. URL: el equipo front-end debe conocer la URL de ese entorno de desarrollo.
      1. ACL: el equipo front-end debe tener un usuario local de AEM con algo similar a los derechos de &quot;Colaboradores&quot;.
      1. Git: el equipo front-end debe tener una ubicación Git independiente para el módulo front-end que se dirija específicamente a ese entorno de desarrollo.

         Una práctica habitual es crear una rama `dev` para administrar los cambios realizados en el entorno de desarrollo. Esta práctica permite una combinación más sencilla en la rama `main`, que se utiliza para la implementación en el entorno de producción.

      1. Canalización: el equipo front-end debe tener una canalización front-end que se implemente en el entorno de desarrollo. Esa canalización implementaría el módulo front-end que normalmente se encuentra en la rama `dev`, como se describe en el punto anterior.
1. A continuación, el equipo front-end hace que el código CSS y JS funcione tanto con la salida antigua como con la nueva.
   1. Como de costumbre, para desarrollar localmente, haga lo siguiente:
      1. El comando `npx aem-site-theme-builder proxy` inicia un servidor proxy que recupera contenido de un entorno de AEM. Reemplaza los archivos CSS y JS del módulo front-end con esos archivos de la carpeta local `dist`.
      1. La configuración de la variable `AEM_URL` en el archivo `.env` oculto le permite controlar desde qué entorno de AEM consume el servidor proxy local el contenido.
      1. Por lo tanto, cambiar el valor de `AEM_URL` le permite cambiar entre los entornos de producción y desarrollo para ajustar CSS y JS de modo que se ajuste a ambos entornos.
      1. Debe trabajar con el entorno de desarrollo que procesa el nuevo resultado y con el entorno de producción que procesa el resultado antiguo.
   1. El trabajo front-end se completa cuando el módulo front-end actualizado funciona para ambos entornos y se implementa en ambos.
1. A continuación, el equipo back-end puede actualizar el entorno de producción implementando el código que procesa la nueva salida de HTML o JSON, o ambas cosas, a través de la canalización de pila completa.
1. El equipo front-end puede limpiar su CSS y JS, eliminar los elementos necesarios solo para la salida antigua e implementar la actualización final en producción mediante la canalización front-end.

## Recursos adicionales {#additional-resources}

* Descubra cómo se pueden utilizar los temas del sitio de AEM para personalizar el estilo y el diseño del sitio.

  Ver [temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md).

* Adobe proporciona un Generador de temas del sitio de AEM como un conjunto de scripts para la creación de nuevos temas del sitio.

  Ver [Generador de temas del sitio de AEM](https://github.com/adobe/aem-site-theme-builder)



