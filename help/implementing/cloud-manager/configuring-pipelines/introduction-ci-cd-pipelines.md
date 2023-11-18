---
title: Canalizaciones de CI/CD
description: Obtenga información sobre las canalizaciones de CI/CD de Cloud Manager y cómo se pueden utilizar para implementar su código de forma eficiente.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 90%

---


# Canalizaciones de CI/CD de Cloud Manager {#intro-cicd}

Obtenga información sobre las canalizaciones de CI/CD de Cloud Manager y cómo se pueden utilizar para implementar su código de forma eficiente.

## Introducción {#introduction}

Una canalización de CI/CD en Cloud Manager es un mecanismo para crear código desde un repositorio de origen e implementarlo en un entorno. Una canalización se puede activar mediante un evento, como una solicitud de extracción de un repositorio de código fuente (es decir, un cambio de código), o en una programación regular para que coincida con una cadencia de lanzamiento.

Para configurar una canalización, debe hacer lo siguiente:

* Definir el activador que iniciará la canalización.
* Definir los parámetros que controlan la implementación de producción.
* Configurar los parámetros de prueba de rendimiento.

Cloud Manager ofrece dos tipos de canalizaciones:

* [Canalizaciones de producción](#prod-pipeline)
* [Canalizaciones que no son de producción](#non-prod-pipeline)

![Tipos de canalizaciones](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Canalizaciones de producción {#prod-pipeline}

Una canalización de producción es una canalización diseñada específicamente que incluye una serie de pasos organizados para implementar código fuente para el uso de producción. Los pasos incluyen la generación, el empaquetado, la prueba, la validación y la implementación en todos los entornos de ensayo. Por lo tanto, una canalización de producción solo se puede agregar una vez que se crea un conjunto de entornos de producción y ensayo.

>[!TIP]
>
>Consulte [Configuración de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para obtener más información.

## Canalización que no es de producción {#non-prod-pipeline}

Una canalización que no es de producción sirve principalmente para ejecutar análisis de calidad del código o para implementar código fuente en un entorno de desarrollo.

>[!TIP]
>
>Consulte [Configuración de una canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para obtener más información.

## Fuentes de código {#code-sources}

Además de la producción y la no producción, las canalizaciones pueden diferenciarse por el tipo de código que implementan.

* **[Canalizaciones de pila completa](#full-stack-pipeline)**: Implementan simultáneamente generaciones de código back-end y front-end que contienen una o más aplicaciones de servidor de AEM junto con configuraciones de HTTPD/Dispatcher
* **[Configurar canalizaciones](#config-deployment-pipeline)** - Configurar e implementar reglas de filtro de tráfico, incluidas las reglas WAF, en cuestión de minutos
* **[Canalizaciones front-end](#front-end)**: Implementan generaciones de código front-end que contienen una o más aplicaciones de interfaz de usuario del lado del cliente.
* **[Canalizaciones de configuración de nivel web](#web-tier-config-pipelines)**: Implementan las configuraciones de HTTPD/Dispatcher

Estas se describen en detalle más adelante en este documento.

### Explicación de las canalizaciones de CI-CD en Cloud Manager {#understand-pipelines}

La siguiente tabla resume las canalizaciones disponibles en Cloud Manager y sus usos.

| Tipo de canalización | Implementación o calidad del código | Código fuente | Función | Notas |
|--- |--- |--- |---|---|
| Producción o no producción | Implementación | De pila completa | Implementa simultáneamente generaciones de código de back-end y front-end junto con configuraciones de HTTPD/Dispatcher | Cuando el código front-end debe implementarse simultáneamente con el código de servidor de AEM.<br>Cuando todavía no se han adoptado canalizaciones front-end o canalizaciones de configuración de nivel web. |
| Producción o no producción | Implementación | Front-End | Implementa la generación de código front-end que contiene una o más aplicaciones de interfaz de usuario del lado del cliente | Admite varias canalizaciones front-end simultáneas<br>Mucho más rápido que las implementaciones de pila completa |
| Producción o no producción | Implementación | Configuración de nivel web | Implementa configuraciones de HTTPD/Dispatcher | Implementa en minutos |
| Producción o no producción | Implementación | Configuración | Implementa reglas de filtrado de tráfico | Implementa en minutos |
| No producción | Calidad del código | De pila completa | Ejecuta el análisis de calidad del código en código de pila completa sin una implementación | Admite varias canalizaciones |
| No producción | Calidad del código | Front-End | Ejecuta análisis de calidad del código en el código front-end sin una implementación | Admite varias canalizaciones |
| No producción | Calidad del código | Configuración de nivel web | Ejecuta análisis de calidad del código en configuraciones de Dispatcher sin una implementación | Admite varias canalizaciones |
| No producción | Calidad del código | Configuración | Implementa reglas de filtrado de tráfico |  |

El siguiente diagrama ilustra las configuraciones de canalización de Cloud Manager con repositorios front-end tradicionales, únicos o independientes.

![Configuraciones de canalización de Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Canalizaciones de pila completa {#full-stack-pipeline}

Las canalizaciones de pila completa implementan configuraciones de código back-end, código front-end y nivel web para el tiempo de ejecución de AEM al mismo tiempo.

* Código back-end: contenido inmutable como código Java, configuraciones OSGi, informes y contenido mutable
* Código front-end: recursos de la interfaz de usuario de la aplicación como JavaScript, CSS, fuentes
* Configuración de nivel web: configuraciones de HTTPD/Dispatcher

La canalización de pila completa representa una canalización “uber”, que hace todo a la vez, ofrece a los usuarios las opciones de implementar exclusivamente sus configuraciones de código front-end o Dispatcher a través de la canalización front-end y las canalizaciones de configuración de nivel web respectivamente.

Código front-end del paquete de canalizaciones de pila completa (JavaScript/CSS) como [bibliotecas del cliente de AEM](/help/implementing/developing/introduction/clientlibs.md).

Las canalizaciones de pila completa pueden implementar configuraciones de nivel web si la [canalización de configuración de capa web](#web-tier-config-pipelines) no está configurada.

Se aplican las siguientes restricciones.

* Un usuario debe registrarse con la función de **Administrador de implementación** para configurar o ejecutar canalizaciones.
* En cualquier momento, solo puede haber una canalización de pila completa por entorno.

Además, tenga en cuenta cómo se comporta la canalización de pila completa si elige introducir una [canalización de configuración del nivel web.](#web-tier-config-pipelines)

* La canalización de pila completa para un entorno ignorará la configuración de Dispatcher si existe la canalización de configuración de nivel web correspondiente.
* Si la canalización de configuración del nivel web correspondiente para el entorno no existe, el usuario puede configurar la canalización de pila completa incluir o ignorar la configuración de Dispatcher.

Las canalizaciones de pila completa pueden ser canalizaciones de calidad del código o implementación.

### Configurar canalizaciones de pila completa {#configure-full-stack}

Para aprender a configurar canalizaciones de pila completa, consulte los siguientes documentos:

* [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)
* [Agregar una canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)

## Configurar canalizaciones {#config-deployment-pipeline}

Con una canalización de configuración, puede configurar e implementar reglas de filtro de tráfico, incluidas las reglas WAF, en cuestión de minutos.

Consulte [Reglas de filtro de tráfico, incluidas las reglas WAF](/help/security/traffic-filter-rules-including-waf.md) para obtener información sobre cómo administrar las configuraciones en el repositorio de modo que se implementen correctamente.

### Configuración de canalizaciones de configuración {#configure-config-deployment}

Para obtener información sobre cómo configurar canalizaciones de configuración, consulte los siguientes documentos:

* [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)
* [Agregar una canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)

## Canalizaciones front-end {#front-end}

El código front-end es cualquier código que sirve como archivos estáticos. Es independiente del código de la IU que sirve AEM y puede incluir temas del sitio, SPA definidos por el cliente, SPA y otras soluciones.

Las canalizaciones front-end ayudan a sus equipos a optimizar su proceso de diseño y desarrollo al permitir la implementación acelerada del código front-end asincrónico del desarrollo back-end. Esta canalización dedicada implementa JavaScript y CSS en la capa de distribución de AEM como tema, lo que da como resultado una nueva versión del tema a la que se puede hacer referencia desde páginas que proporciona AEM.

>[!NOTE]
>
>Un usuario con el rol de **Administrador de implementación** puede crear y ejecutar varias canalizaciones front-end simultáneamente.
>
>Sin embargo, hay un límite máximo de 300 canalizaciones por programa (en todos los tipos).

Las canalizaciones front-end pueden ser de calidad del código o implementación.

### Antes de configurar canalizaciones front-end {#before-start}

Antes de configurar las canalizaciones front-end, revise el [Recorrido de creación de sitios rápidos de AEM](/help/journey-sites/quick-site/overview.md) para obtener una guía completa a través de la herramienta de creación de sitios rápidos de AEM fácil de usar. Este recorrido le ayudará a optimizar su desarrollo front-end y le permitirá personalizar rápidamente su sitio sin conocimientos del back-end de AEM.

### Configurar una canalización front-end {#configure-front-end}

Para obtener información sobre cómo configurar canalizaciones front-end, consulte lo siguiente:

* [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Agregar una canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Desarrollo de Sites con la canalización front-end {#developing-with-front-end-pipeline}

Con las canalizaciones front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo se puede acelerar.

Consulte el documento [Desarrollar Sites con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber cómo funciona este proceso, así como algunas consideraciones que deben tenerse en cuenta para aprovechar al máximo este proceso.

## Canalizaciones de configuración de nivel web {#web-tier-config-pipelines}

Las canalizaciones de configuración de nivel web permiten la implementación exclusiva de la configuración de HTTPD/Dispatcher en el tiempo de ejecución de AEM al desacoplarla de otros cambios de código. Es una canalización optimizada que proporciona a los usuarios que solo desean implementar los cambios de configuración de Dispatcher, un medio acelerado para hacerlo en solo unos minutos.

>[!TIP]
>
>Con las canalizaciones de configuración de capa web, puede elegir entre almacenar la configuración web en la misma ubicación de origen que para la canalización de pila completa o en una ubicación diferente, según la estructura que se adapte mejor a su proyecto.

Se aplican las siguientes restricciones.

* Debe estar en la versión de AEM `2021.12.6151.20211217T120950Z` o más reciente para utilizar las canalizaciones de configuración de nivel web.
* Debe [adherirse al modo flexible de las herramientas de Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para utilizar las canalizaciones de configuración de nivel web.
* El usuario debe registrarse con la función de **Administrador de implementación** para configurar o ejecutar canalizaciones.
* En cualquier momento, solo puede haber una canalización de configuración de nivel web por entorno.
* El usuario no puede configurar una canalización de configuración de nivel web cuando se ejecuta su canalización de pila completa correspondiente.
* La estructura del nivel web debe adherirse a la estructura de modo flexible, tal como se define en el documento [Dispatcher en la nube](/help/implementing/dispatcher/disp-overview.md#validation-debug).

Además, tenga en cuenta cómo se comporta la [canalización de pila completa](#full-stack-pipeline) al introducir una canalización de nivel web.

* Si no se ha configurado una canalización de configuración de nivel web para un entorno, el usuario puede realizar una selección al configurar su canalización de pila completa correspondiente para incluir o ignorar la configuración de Dispatcher durante la ejecución y la implementación.
* Una vez que se ha configurado una canalización de configuración de nivel web para un entorno, su canalización de pila completa correspondiente (si existe) ignorará la configuración de Dispatcher durante la ejecución y la implementación.
* Una vez que se elimina una canalización de configuración de nivel web, su canalización de pila completa correspondiente se restablece para implementar las configuraciones de Dispatcher durante su ejecución.

Las canalizaciones de configuración de nivel web pueden ser del tipo calidad del código o implementación.

### Configuración de canalizaciones de nivel web {#configure-web-tier}

Para aprender a configurar canalizaciones de nivel web, consulte los siguientes documentos:

* [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)
* [Agregar una canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)

## Vídeo introductorio de los tipos de canalización {#video}

Para obtener una descripción general rápida de los tipos de canalización, vea este breve vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/342363)
