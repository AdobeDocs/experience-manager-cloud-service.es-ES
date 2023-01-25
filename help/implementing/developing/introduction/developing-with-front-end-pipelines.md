---
title: Desarrollo de Sites con la canalización front-end
description: Con la canalización de front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo puede ganar una velocidad sustancial. En este documento se describen algunas consideraciones particulares del proceso de compilación del front-end que deben darse.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
source-git-commit: 2afdd0682d1baf39d737ee7a5721657e639739a7
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 1%

---


# Desarrollo de Sites con la canalización front-end {#developing-site-with-front-end-pipeline}

[Con la canalización frontal,](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) se da más independencia a los desarrolladores de front-end y el proceso de desarrollo puede ganar una velocidad sustancial. Este documento describe cómo funciona este proceso junto con algunas consideraciones que hay que tener en cuenta para aprovechar todo el potencial de este proceso.

>[!TIP]
>
>Si todavía no conoce cómo utilizar la canalización front-end y los beneficios que puede reportar, consulte la [Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para ver un ejemplo de cómo implementar rápidamente un nuevo sitio y personalizar su tema completamente independiente del desarrollo del back-end.

## Contrato de compilación del front-end {#front-end-build-contract}

Similar a la variable [entorno de compilación de pila completa,](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) la canalización front-end tiene su propio entorno. Los desarrolladores tienen cierta flexibilidad en esta canalización siempre y cuando se observe el siguiente contrato de construcción front-end.

La canalización front-end requiere que el proyecto front-end Node.js use el `build` directiva script para generar la compilación que implementará la canalización front-end. Es decir, Cloud Manager utiliza el comando `npm run build` para generar el proyecto implementable en el `dist` carpeta.

El contenido de la variable `dist` carpeta es lo que se implementa finalmente en AEM as a Cloud Service desde la canalización de Cloud Manager.

### Versiones de nodo {#node-versions}

De forma predeterminada, la canalización de front-end utiliza el nodo 14, pero también están disponibles los nodos 12 y 16.

Puede usar la variable `CM_CUSTOM_VAR_NODE_VERSION` para establecer la versión deseada.

## Fuente única de la verdad {#single-source-of-truth}

Una buena práctica general es mantener una única fuente de verdad para lo que se ha implementado en AEM. El objetivo de Cloud Manager es hacer que esa única fuente de verdad sea obvia. Sin embargo, como la canalización frontal permite desacoplar la ubicación de las partes del código, algunas responsabilidades adicionales radican en la configuración correcta de las canalizaciones front-end. Se debe tener cuidado de no crear varias canalizaciones front-end que se implementen en el mismo sitio en el mismo entorno.

Por este motivo, y especialmente cuando se crean varias canalizaciones front-end, se recomienda mantener una convención de nomenclatura sistemática como la siguiente:

* El nombre del módulo front-end definido por la variable `name` propiedad de la variable `package.json` debe contener el nombre del sitio al que se aplica. Por ejemplo, para un sitio ubicado en `/content/wknd`, el nombre del módulo front-end sería algo así como `wknd-theme`.
* Cuando un módulo front-end comparte el mismo repositorio de Git con otros módulos, el nombre de su carpeta debe ser igual o contener el mismo nombre del módulo front-end. Por ejemplo, si el módulo front-end tiene el nombre `wknd-theme`, el nombre de la carpeta que la rodea sería algo así `wknd-theme-sources`.
* El nombre de la canalización front-end de Cloud Manager también debe contener el nombre del módulo front-end y también añadir el entorno al que se implementa (producción o desarrollo). Por ejemplo, para el módulo front-end denominado `wknd-theme`, la canalización podría llamarse algo así como `wknd-theme-prod`.

Una convención de este tipo debería evitar de forma eficaz los siguientes errores de implementación:

* Aplicación de un módulo front-end al sitio incorrecto
* Creación de varios módulos front-end que apliquen el mismo sitio, que se sobrescribirían entre sí
* Creación de varias canalizaciones front-end para las mismas fuentes, lo que podría provocar condiciones de carrera, sin garantizar el orden de las implementaciones

## Separación de preocupaciones {#separation-of-concerns}

Otra buena práctica que se aplica a toda separación de preocupaciones es la de poner especial cuidado en la forma en que se diseña y gestiona el contrato que separa las preocupaciones. En el caso de la canalización front-end, el contrato que separa ese código del resto es el HTML y JSON procesados por el sitio. Si ese HTML y JSON permanecen estables, entonces la canalización front-end ofrece su máximo valor al hacer que el equipo front-end sea totalmente independiente.

Actualmente no hay ninguna capacidad específica para ejecutar la canalización de pila completa sincrónicamente con las canalizaciones front-end. Por esta razón, al desvincular el desarrollo front-end de la canalización de toda la pila, se debe tener cuidado adicional en el contrato que separa estas dos áreas de preocupación. Ese contrato suele ser el HTML o JSON que el Experience Manager procesa. Por lo tanto, los cambios en dicho contrato deben planificarse bien entre los equipos que gestionen las diferentes canalizaciones, de modo que acuerden cómo secuenciar los cambios correspondientes.

Por lo general, se recomiendan los siguientes pasos cuando es necesario realizar cambios en el HTML o en la salida JSON que afecten a ambas áreas de preocupación.

1. El equipo back-end configura primero un entorno de desarrollo con el nuevo HTML o la salida JSON.
   1. A través de la canalización de pila completa, implementan el código necesario para procesar el nuevo HTML o la salida JSON que desee.
   1. Si es para un entorno al que el equipo front-end no tenía acceso anteriormente, se deben realizar los siguientes pasos.
      1. URL: El equipo front-end debe conocer la dirección URL de ese entorno de desarrollo.
      1. ACL: El equipo front-end debe tener un usuario AEM local con derechos similares a los de los &quot;colaboradores&quot;.
      1. Git: El equipo front-end debe tener una ubicación Git independiente para el módulo front-end que se dirija específicamente a ese entorno de desarrollo.
         * Una práctica habitual es crear un `dev` para que los cambios realizados para el entorno de desarrollo se puedan volver a fusionar fácilmente en la `main` que se va a implementar en el entorno de producción.
      1. Canalización: El equipo front-end debe tener una canalización front-end que se implemente en el entorno de desarrollo. Esa canalización implementaría el módulo front-end que generalmente se encuentra en la `dev` como se describe en el punto anterior.
1. A continuación, el equipo front-end hace que el código CSS y JS funcionen tanto con la salida antigua como con la nueva.
   1. Como de costumbre, para desarrollarse localmente:
      1. La variable `npx aem-site-theme-builder proxy` ejecutar en el módulo front-end inicia un servidor proxy que solicita el contenido desde un entorno AEM, mientras reemplaza los archivos CSS y JS del módulo front-end por los del servidor local `dist` carpeta.
      1. Configuración de la variable `AEM_URL` en la variable oculta `.env` permite controlar desde qué entorno AEM el servidor proxy local consume el contenido.
      1. Cambio del valor de esto `AEM_URL` por lo tanto, permite cambiar entre los entornos de producción y desarrollo para ajustar CSS y JS de modo que se ajuste a ambos entornos.
      1. Debe trabajar con el entorno de desarrollo que procesa la nueva salida y con el entorno de producción que procesa la salida antigua.
   1. El trabajo front-end se completa cuando el módulo front-end actualizado funciona para ambos entornos y se implementa en ambos.
1. El equipo back-end puede actualizar el entorno de producción implementando el código que procesa el nuevo HTML o la salida JSON a través de la canalización de pila completa.
1. El equipo front-end puede limpiar su CSS y JS y eliminar lo que solo necesitaba la salida antigua, implementando la última actualización en producción a través de la canalización front-end.

## Recursos adicionales {#additional-resources}

* [Temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md) - Aprenda cómo se pueden utilizar AEM temas del sitio para personalizar el estilo y el diseño de su sitio.
* [AEM Generador de temas del sitio](https://github.com/adobe/aem-site-theme-builder) : Adobe proporciona un Generador de temas AEM del sitio como un conjunto de secuencias de comandos para la creación de nuevos temas del sitio.
