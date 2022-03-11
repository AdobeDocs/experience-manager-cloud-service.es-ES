---
title: Canalizaciones CI/CD
description: Obtenga información sobre las canalizaciones de CD/CI de Cloud Manager y cómo se pueden utilizar para implementar su código de forma eficiente.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 1%

---

# Canalizaciones de CD/CI de Cloud Manager {#intro-cicd}

Obtenga información sobre las canalizaciones de CD/CI de Cloud Manager y cómo se pueden utilizar para implementar su código de forma eficiente.

## Introducción {#introduction}

Una canalización de CI/CD en Cloud Manager es un mecanismo para crear código desde un repositorio de origen e implementarlo en un entorno. Una canalización se puede activar mediante un evento, como una solicitud de extracción de un repositorio de código fuente (es decir, un cambio de código), o en una programación regular para que coincida con una cadencia de lanzamiento.

Para configurar una canalización, debe:

* Defina el déclencheur que iniciará la canalización.
* Defina los parámetros que controlan la implementación de producción.
* Configure los parámetros de prueba de rendimiento.

Cloud Manager ofrece dos tipos de canalizaciones:

* [Canalizaciones de producción](#prod-pipeline)
* [Canalizaciones que no son de producción](#non-prod-pipeline)

![Tipos de tuberías](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Canalizaciones de producción {#prod-pipeline}

Una canalización de producción es una canalización diseñada específicamente que incluye una serie de pasos organizados para implementar código fuente para uso de producción. Los pasos incluyen la creación, el empaquetado, la prueba, la validación y la implementación en todos los entornos de ensayo. Por lo tanto, una canalización de producción solo se puede añadir una vez que se crea un conjunto de entornos de producción y ensayo.

>[!TIP]
>
>Consulte el documento [Configuración de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para obtener más información.

## Canalización que no es de producción {#non-prod-pipeline}

Una canalización que no es de producción sirve principalmente para ejecutar análisis de calidad del código o para implementar código fuente en un entorno de desarrollo.

>[!TIP]
>
>Consulte el documento [Configuración de una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para obtener más información.

## Fuentes de código {#code-sources}

Además de la producción y la no producción, las canalizaciones pueden diferenciarse por el tipo de código que implementen.

* **[Canalizaciones de pila completa](#full-stack-pipeline)** : implemente simultáneamente compilaciones de código back-end y front-end que contengan una o más aplicaciones de servidor AEM junto con configuraciones de HTTPD/Dispatcher
* **[Canalizaciones front-end](#front-end)** : implemente compilaciones de código front-end que contengan una o más aplicaciones de interfaz de usuario del lado del cliente.
* **[Canalizaciones de configuración de nivel web](#web-tier-config-pipelines)** : implementa las configuraciones de HTTPD/Dispatcher

Estos se describen en detalle más adelante en este documento.

### Explicación de las canalizaciones de CI-CD en Cloud Manager {#understand-pipelines}

La siguiente tabla resume todas las canalizaciones disponibles en Cloud Manager y sus usos.

| Tipo de canalización | Implementación o calidad de código | Código fuente | Función | Notas |
|--- |--- |--- |---|---|
| Producción o no producción | Implementación | Pila completa | Implementa simultáneamente compilaciones de código de back-end y front-end junto con configuraciones de HTTPD/Dispatcher | Cuando el código front-end debe implementarse simultáneamente con AEM código de servidor.<br>Cuando todavía no se han adoptado canalizaciones front-end o canalizaciones de configuración de nivel web. |
| Producción o no producción | Implementación | Front-End | Implementa la compilación de código front-end que contiene una o más aplicaciones de interfaz de usuario del lado del cliente | Admite múltiples canalizaciones front-end simultáneas<br>Mucho más rápido que las implementaciones de pila completa |
| Producción o no producción | Implementación | Configuración de nivel web | Implementa configuraciones de HTTPD/Dispatcher | Implementaciones en minutos |
| No producción | Calidad de código | Pila completa | Ejecuta análisis de calidad del código en código de pila completa sin una implementación | Admite varias canalizaciones |
| No producción | Calidad de código | Front-End | Ejecuta análisis de calidad del código en el código front-end sin una implementación | Admite varias canalizaciones |
| No producción | Calidad de código | Configuración de nivel web | Ejecuta análisis de calidad del código en configuraciones de Dispatcher sin una implementación | Admite varias canalizaciones |

El diagrama siguiente ilustra las configuraciones de canalización de Cloud Manager con repositorios front-end tradicionales, únicos o independientes.

![Configuraciones de canalización de Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Canalizaciones de pila completa {#full-stack-pipeline}

Las canalizaciones de pila completa implementan configuraciones de código back-end, código front-end y nivel web para AEM tiempo de ejecución al mismo tiempo.

* Código back-end: contenido inmutable como código Java, configuraciones OSGi, informes, así como contenido mutable
* Código front-end: recursos de la interfaz de usuario de la aplicación como JavaScript, CSS, fuentes
* Configuración de nivel web: configuraciones de HTTPD/Dispatcher

La canalización de pila completa representa una canalización &#39;uber&#39;, lo que hace todo a la vez que ofrece a los usuarios las opciones de implementar exclusivamente sus configuraciones de código front-end o Dispatcher a través de la canalización front-end y las canalizaciones de configuración de nivel web respectivamente.

Código front-end del paquete de canalizaciones de pila completa (JavaScript/CSS) como [AEM bibliotecas de cliente.](/help/implementing/developing/introduction/clientlibs.md)

Las canalizaciones de pila completa pueden implementar configuraciones de nivel web si [canalización de configuración de capa web](#web-tier-config-pipelines) no está configurado.

Se aplican las restricciones siguientes.

* Un usuario debe registrarse con el **Administrador de implementación** para configurar o ejecutar canalizaciones.
* En cualquier momento, solo puede haber una canalización de pila completa por entorno.

Además, tenga en cuenta cómo se comportará la canalización de pila completa si elige introducir una [canalización de configuración del nivel web.](#web-tier-config-pipelines)

* La canalización de pila completa para un entorno ignorará la configuración de Dispatcher si existe la canalización de configuración de nivel web correspondiente.
* Si la canalización de configuración del nivel web correspondiente para el entorno no existe, el usuario puede configurar la canalización de pila completa incluir o ignorar la configuración de Dispatcher.

Las canalizaciones de pila completa pueden ser canalizaciones de calidad de código o implementación.

## Canalizaciones front-end {#front-end}

El código front-end es cualquier código que sirve como archivos estáticos. Es independiente del código de la interfaz de usuario que AEM y puede incluir temas del sitio, SPA definidos por el cliente, SPA de Firefly y otras soluciones.

Las canalizaciones front-end ayudan a sus equipos a optimizar su proceso de diseño y desarrollo al permitir la implementación acelerada del código front-end asincrónico del desarrollo back-end. Esta canalización dedicada implementa JavaScript y CSS en la capa de distribución de AEM como tema, lo que da como resultado una nueva versión del tema a la que se puede hacer referencia desde páginas enviadas por AEM.

>[!IMPORTANT]
>
>Debe estar en AEM versión `2021.10.5933.20211012T154732Z ` o superior con AEM Sites habilitado para aprovechar las canalizaciones front-end.

>[!NOTE]
>
>Un usuario con la variable **Administrador de implementación** puede crear y ejecutar varias canalizaciones front-end simultáneamente.
>
>Sin embargo, hay un límite máximo de 300 canalizaciones por programa (en todos los tipos). Pueden ser de calidad de código front-end o canalizaciones de implementación front-end.

Las canalizaciones front-end pueden ser canalizaciones de calidad de código o implementación.

### Antes de configurar canalizaciones front-end {#before-start}

Antes de configurar las canalizaciones front-end, revise la [AEM Recorrido de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) para obtener una guía completa a través de la herramienta de creación rápida de sitios de AEM fácil de usar. Este recorrido le ayudará a optimizar su desarrollo front-end y le permitirá personalizar rápidamente su sitio sin conocimientos de AEM back-end.

### Configuración de una canalización front-end {#configure-front-end}

Para aprender a configurar canalizaciones front-end, consulte los siguientes documentos.

* [Adición de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adición de una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Desarrollo de sitios con la canalización front-end {#developing-with-front-end-pipeline}

Con las canalizaciones front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo se puede acelerar.

Consulte el documento [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber cómo funciona este proceso, así como algunas consideraciones que deben tenerse en cuenta para aprovechar al máximo este proceso.

### Configuración de canalizaciones de pila completa {#configure-full-stack}

Para aprender a configurar canalizaciones de pila completa, consulte los siguientes documentos.

* [Adición de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adición de una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Canalizaciones de configuración de nivel web {#web-tier-config-pipelines}

Las canalizaciones de configuración de nivel web permiten la implementación exclusiva de la configuración de HTTPD/Dispatcher en el tiempo de ejecución de AEM desacoplándola de otros cambios de código. Es una canalización optimizada que proporciona a los usuarios que solo desean implementar los cambios de configuración de Dispatcher, un medio acelerado para hacerlo en solo unos minutos.

>[!TIP]
>
>Con las canalizaciones de configuración de capa web, puede elegir entre almacenar la configuración web en la misma ubicación de origen que para la canalización de pila completa o en una ubicación diferente, según la estructura que se adapte mejor a su proyecto.

Se aplican las restricciones siguientes.

* Debe estar en AEM versión `2021.12.6151.20211217T120950Z` o más reciente para aprovechar las canalizaciones de configuración de nivel web.
* Debe [inclusión en el modo flexible de las herramientas de Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para aprovechar las canalizaciones de configuración de nivel web.
* Un usuario debe registrarse con el **Administrador de implementación** para configurar o ejecutar canalizaciones.
* En cualquier momento, solo puede haber una canalización de configuración de nivel web por entorno.
* El usuario no puede configurar una canalización de configuración de nivel web cuando se está ejecutando su canalización de pila completa correspondiente.
* La estructura del nivel web debe adherirse a la estructura de modo flexible, tal como se define en el documento [Dispatcher en la nube.](/help/implementing/dispatcher/disp-overview.md#validation-debug)

Además, tenga en cuenta cómo se usa la variable [canalización de pila completa](#full-stack-pipeline) se comportarán al introducir una canalización de niveles web.

* Si no se ha configurado una canalización de configuración de nivel web para un entorno, el usuario puede realizar una selección al configurar su canalización de pila completa correspondiente para incluir o ignorar la configuración de Dispatcher durante la ejecución y la implementación.
* Una vez que se ha configurado una canalización de configuración de nivel web para un entorno, su canalización de pila completa correspondiente (si existe) ignorará la configuración de Dispatcher durante la ejecución y la implementación.
* Una vez que se elimine una canalización de configuración de nivel web, su canalización de pila completa correspondiente se restablecerá para implementar las configuraciones de Dispatcher durante su ejecución.

Las canalizaciones de configuración de nivel web pueden ser del tipo calidad del código o implementación.

### Configuración de canalizaciones de configuración de nivel web {#configure-web-tier-config-pipelines}

Para aprender a configurar las canalizaciones de configuración de nivel web, consulte los siguientes documentos.

* [Adición de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adición de una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
