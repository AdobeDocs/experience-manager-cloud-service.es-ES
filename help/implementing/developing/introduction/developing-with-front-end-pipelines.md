---
title: Desarrollo de Sites con la canalización front-end
description: Con la canalización front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo puede ganar velocidad sustancial. Este documento describe algunas consideraciones particulares del proceso de compilación del front-end que deben darse.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 1%

---


# Desarrollo de Sites con la canalización front-end {#developing-site-with-front-end-pipeline}

[Con la canalización front-end,](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) se da más independencia a los desarrolladores de front-end y el proceso de desarrollo puede ganar velocidad sustancial. En este documento se describe cómo funciona este proceso, así como algunas consideraciones que hay que tener en cuenta para aprovechar todo el potencial de este proceso.

>[!TIP]
>
>Si todavía no está familiarizado con cómo utilizar la canalización front-end y las ventajas que puede aportar, consulte la [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para ver un ejemplo de cómo implementar rápidamente un nuevo sitio y personalizar su tema completamente independientemente del desarrollo del back-end.

## Contrato de versión front-end {#front-end-build-contract}

Similar a la [entorno de compilación de pila completa,](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) la canalización front-end tiene su propio entorno. Los desarrolladores tienen cierta flexibilidad al utilizar esta canalización siempre y cuando se observe el siguiente contrato de versión del front-end.

La canalización front-end requiere que el proyecto front-end Node.js utilice el `build` para generar la compilación que implementa. Esto se debe a que Cloud Manager utiliza el comando `npm run build` para generar el proyecto implementable para la compilación del front-end.

El contenido resultante de la `dist` Esta carpeta es lo que implementa Cloud Manager en última instancia, y los sirve como archivos estáticos. AEM Estos archivos están alojados de forma externa a la, pero están disponibles a través de una `/content/...` URL en el entorno implementado.

## Versiones de nodo {#node-versions}

El entorno de compilación del front-end es compatible con las siguientes versiones de Node.js.

* 12
* 14 (predeterminado)
* 16
* 18

Puede usar el complemento `NODE_VERSION` [variable de entorno](/help/implementing/cloud-manager/environment-variables.md) para establecer la versión deseada.

## Fuente única de verdad {#single-source-of-truth}

AEM Una buena práctica general es mantener una única fuente de datos para lo que se implementa en el sistema de informes de la aplicación de la plataforma de datos de la plataforma de datos de la plataforma de datos de la plataforma de datos de la red de. El objetivo de Cloud Manager es hacer obvia esa única fuente de verdad. Sin embargo, como la canalización front-end permite desacoplar la ubicación de partes del código, parte de la responsabilidad adicional reside en la configuración correcta de las canalizaciones front-end. Se debe tener cuidado de no crear varias canalizaciones front-end que se implementen en el mismo sitio en el mismo entorno.

Por este motivo, y especialmente cuando se crean varias canalizaciones front-end, se recomienda mantener una convención de nombres sistemática como la siguiente:

* El nombre del módulo front-end, definido por la variable `name` propiedad del `package.json` debe contener el nombre del sitio al que se aplica. Por ejemplo, para un sitio ubicado en `/content/wknd`, el nombre del módulo front-end sería algo así como `wknd-theme`.
* Cuando un módulo front-end comparte el mismo repositorio de Git con otros módulos, el nombre de su carpeta debe ser igual o contener el mismo nombre que el módulo front-end. Por ejemplo, si el módulo front-end se denomina `wknd-theme`, el nombre de la carpeta adjunta sería algo así como `wknd-theme-sources`.
* El nombre de la canalización front-end de Cloud Manager también debe contener el nombre del módulo front-end y también agregar el entorno al que se implementa (producción o desarrollo). Por ejemplo, para el módulo front-end denominado `wknd-theme`, la canalización podría tener el siguiente nombre `wknd-theme-prod`.

Una convención de este tipo debería evitar de manera eficiente los siguientes errores de implementación:

* Aplicación de un módulo front-end al sitio incorrecto
* Creación de varios módulos front-end que apliquen el mismo sitio, que se sobrescribirían entre sí
* Crear varias canalizaciones front-end para los mismos orígenes, lo que podría provocar condiciones de carrera, sin garantizar el orden de las implementaciones

## Separación de preocupaciones {#separation-of-concerns}

Otra buena práctica que se aplica a toda separación de intereses es poner especial cuidado en la forma en que se concibe y gestiona el contrato que separa los intereses. En el caso de la canalización front-end, el contrato que separa ese código del resto es el HTML y el JSON procesados por el sitio. Si ese HTML y JSON se mantienen estables, la canalización front-end ofrece su valor máximo al hacer que el equipo front-end sea totalmente independiente.

Actualmente no hay ninguna capacidad específica para ejecutar la canalización de pila completa sincrónicamente con las canalizaciones front-end. Por esta razón, al desacoplar el desarrollo front-end de la canalización full-stack, se debe poner un cuidado adicional en el contrato que separa estas dos áreas de preocupación. Ese contrato suele ser el HTML o JSON que Experience Manager procesa. Por lo tanto, los cambios en ese contrato deben estar bien planificados entre los equipos que operan las diferentes canalizaciones para que acuerden cómo secuenciar los cambios correspondientes.

En general, se recomiendan los siguientes pasos cuando es necesario realizar cambios en el HTML o en la salida JSON que afecten a ambas áreas de interés.

1. El equipo back-end configura primero un entorno de desarrollo con el nuevo HTML o salida JSON.
   1. A través de la canalización de pila completa, implementan el código necesario para procesar el nuevo HTML o la salida JSON que se desea.
   1. Si se trata de un entorno al que el equipo front-end no tenía acceso anteriormente, se deben realizar los siguientes pasos.
      1. URL: el equipo front-end debe conocer la URL de ese entorno de desarrollo.
      1. AEM ACL: el equipo front-end debe tener un usuario de la interfaz de usuario local con algo similar a los derechos de &quot;Colaboradores&quot;.
      1. Git: el equipo front-end debe tener una ubicación Git independiente para el módulo front-end que se dirija específicamente a ese entorno de desarrollo.
         * Una práctica habitual es crear un `dev` , para que los cambios realizados en el entorno de desarrollo se puedan volver a fusionar fácilmente con el `main` rama que se va a implementar en el entorno de producción.
      1. Canalización: el equipo front-end debe tener una canalización front-end que se implemente en el entorno de desarrollo. Esa canalización implementaría el módulo front-end que generalmente se encuentra en `dev` rama, tal como se describe en el punto anterior.
1. A continuación, el equipo front-end hace que el código CSS y JS funcione tanto con la salida antigua como con la nueva.
   1. Como de costumbre, para desarrollar localmente:
      1. El `npx aem-site-theme-builder proxy` AEM El comando ejecutado en el módulo front-end inicia un servidor proxy que solicita el contenido de un entorno de, al tiempo que reemplaza los archivos CSS y JS del módulo front-end por los del entorno local `dist` carpeta.
      1. Configuración de la `AEM_URL` en la variable oculta `.env` AEM permite controlar desde qué entorno consume el contenido el servidor proxy local.
      1. Cambiar el valor de esto `AEM_URL` por lo tanto, permite cambiar entre los entornos de producción y desarrollo para ajustar CSS y JS de modo que se adapte a ambos entornos.
      1. Debe trabajar con el entorno de desarrollo que procesa el nuevo resultado y con el entorno de producción que procesa el resultado antiguo.
   1. El trabajo front-end se completa cuando el módulo front-end actualizado funciona para ambos entornos y se implementa en ambos.
1. El equipo back-end puede actualizar el entorno de producción implementando el código que procesa el nuevo HTML o la salida JSON a través de la canalización full-stack.
1. El equipo front-end puede limpiar su CSS y JS y eliminar lo que solo necesitaba la salida antigua, implementando la última actualización en producción a través de la canalización front-end.

## Recursos adicionales {#additional-resources}

* [Temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md) AEM - Aprenda cómo se pueden utilizar los temas del sitio para personalizar el estilo y el diseño del sitio.
* [AEM Generador de temas del sitio](https://github.com/adobe/aem-site-theme-builder) : el Adobe AEM proporciona un Generador de temas del sitio de forma de un conjunto de secuencias de comandos para crear nuevos temas del sitio.
