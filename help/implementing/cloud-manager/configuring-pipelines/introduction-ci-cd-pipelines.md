---
title: Introducción a las canalizaciones de CI/CD
description: Obtenga información sobre las canalizaciones de CI/CD de Cloud Manager y cómo se pueden utilizar para implementar su código de forma eficaz.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 32%

---


# Canalizaciones de CI/CD de Cloud Manager {#intro-cicd}

Obtenga información sobre las canalizaciones CI/CD (integración continua/entrega continua) de Cloud Manager y cómo se pueden utilizar para implementar su código de forma eficaz.

## Introducción a las canalizaciones de CI/CD {#introduction}

Una canalización de CI/CD en Cloud Manager es un mecanismo para crear código desde un repositorio de origen e implementarlo en un entorno. Un evento almacena en déclencheur una canalización, como una solicitud de extracción de un repositorio de código fuente como Git (es decir, un cambio de código). O bien, se puede activar en una programación regular para que coincida con una cadencia de lanzamiento.

Para configurar una canalización, debe hacer lo siguiente:

* Defina el déclencheur que inicia la canalización.
* Defina los parámetros que controlan la implementación de producción.
* Configurar los parámetros de prueba de rendimiento.

Cloud Manager ofrece dos tipos de canalizaciones:

* [Canalizaciones de producción](#prod-pipeline)
* [Canalizaciones que no sean de producción](#non-prod-pipeline)

![Tipos de canalizaciones](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Canalizaciones de producción {#prod-pipeline}

Una canalización de producción es una canalización diseñada específicamente que incluye una serie de pasos organizados para implementar código fuente para el uso de producción. Los pasos incluyen la generación, el empaquetado, la prueba, la validación y la implementación en todos los entornos de ensayo. Por lo tanto, una canalización de producción solo se puede agregar una vez que se crea un conjunto de entornos de producción y ensayo.

>[!TIP]
>
>Consulte [Configurar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

## Canalizaciones que no sean de producción {#non-prod-pipeline}

Una canalización que no es de producción sirve principalmente para ejecutar análisis de calidad del código o para implementar código fuente en un entorno de desarrollo.

>[!TIP]
>
>Consulte [Configurar una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

## Fuentes de código {#code-sources}

Las canalizaciones también pueden variar según el tipo de código que implementan, además de los entornos de producción y de no producción.

* **[Canalizaciones de pila completa](#full-stack-pipeline)**: Implementan simultáneamente generaciones de código back-end y front-end que contienen una o más aplicaciones de servidor de AEM junto con configuraciones de HTTPD/Dispatcher.
* **[Canalizaciones de configuración](#config-deployment-pipeline)**: puede implementar rápidamente configuraciones para características como reenvío de registros y tareas de mantenimiento relacionadas con la depuración. También incluye varias configuraciones de CDN (red de distribución de contenido), como reglas de filtro de tráfico, incluidas las reglas de Firewall de aplicaciones web (WAF). Además, puede administrar transformaciones de solicitud y respuesta, selectores de origen, redirecciones del lado del cliente, páginas de error, claves CDN, claves API de depuración y autenticación básica. Consulte [Usar canalizaciones de configuración](/help/operations/config-pipeline.md) para obtener más información.
* **[Canalizaciones front-end](#front-end)**: Implementan compilaciones de código front-end que contienen una o más aplicaciones de interfaz de usuario del lado del cliente.
* **[Canalizaciones de configuración de nivel web](#web-tier-config-pipelines)**: Implementa configuraciones de HTTPD/Dispatcher.

Estos tipos de canalización se describen en detalle más adelante en este documento.

### Comprender las canalizaciones de CI-CD en Cloud Manager {#understand-pipelines}

La siguiente tabla resume las canalizaciones disponibles en Cloud Manager y sus usos.

| Tipo de canalización | Implementación o calidad del código | código Source | Función | Notas |
| --- | --- | --- | --- | ---|
| Producción o no producción | Implementación | De pila completa | Implementa simultáneamente generaciones de código de back-end y front-end junto con configuraciones de HTTPD/Dispatcher | Se utiliza cuando el código front-end debe implementarse simultáneamente con el código de servidor de AEM. Se utiliza cuando aún no se han adoptado las canalizaciones front-end o las canalizaciones de configuración de nivel web. |
| Producción o no producción | Implementación | Front-end | Implementa la generación de código front-end que contiene una o más aplicaciones de interfaz de usuario del lado del cliente | Admite varias canalizaciones front-end simultáneas<br>Mucho más rápido que las implementaciones full-stack. |
| Producción o no producción | Implementación | Configuración del nivel web | Implementa configuraciones de HTTPD/Dispatcher | Implementa en minutos |
| Producción o no producción | Implementación | Configuración | Implementa la configuración [para una serie de características](/help/operations/config-pipeline.md) relacionadas con la red de distribución de contenido (CDN), el reenvío de registros y la depuración de tareas de mantenimiento | Implementa en minutos |
| No producción | Calidad de código | Pila completa | Ejecuta el análisis de calidad del código en código de pila completa sin una implementación | Admite varias canalizaciones |
| No producción | Calidad de código | Front-end | Ejecuta análisis de calidad del código en el código front-end sin una implementación | Admite varias canalizaciones |
| No producción | Calidad de código | Configuración del nivel web | Ejecuta análisis de calidad del código en configuraciones de Dispatcher sin una implementación | Admite varias canalizaciones |

El siguiente diagrama ilustra las configuraciones de canalización de Cloud Manager con repositorios front-end tradicionales, únicos o independientes.

![Configuraciones de canalización de Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Canalizaciones de pila completa {#full-stack-pipeline}

Las canalizaciones de pila completa implementan configuraciones de código back-end, código front-end y nivel web para el tiempo de ejecución de AEM al mismo tiempo.

* Código back-end: contenido inmutable como código Java, configuraciones OSGi, informes y contenido mutable
* Código front-end: recursos de la interfaz de usuario de la aplicación como JavaScript, CSS, fuentes
* Configuración de nivel web: configuraciones de HTTPD/Dispatcher

La canalización de pila completa representa una canalización &quot;uber&quot;. Gestiona todo de forma simultánea, a la vez que permite a los usuarios implementar sus configuraciones de código front-end o Dispatcher por separado. Esta implementación se realiza a través de la canalización front-end y las canalizaciones de configuración de nivel web, respectivamente.

Código front-end del paquete de canalizaciones de pila completa (JavaScript/CSS) como [bibliotecas del cliente de AEM](/help/implementing/developing/introduction/clientlibs.md).

Las canalizaciones de pila completa pueden implementar configuraciones de nivel web si la [canalización de configuración de capa web](#web-tier-config-pipelines) no está configurada.

Se aplican las siguientes restricciones.

* Un usuario debe registrarse con la función de **Administrador de implementación** para configurar o ejecutar canalizaciones.
* En cualquier momento, solo puede haber una canalización de pila completa por entorno.

Además, tenga en cuenta cómo se comporta la canalización de pila completa si elige introducir una [canalización de configuración de nivel web](#web-tier-config-pipelines).

* La canalización de pila completa para un entorno ignora la configuración de Dispatcher si existe la canalización de configuración de nivel web correspondiente.
* Si la canalización de configuración del nivel web correspondiente para el entorno no existe, el usuario puede configurar la canalización de pila completa para incluir o ignorar la configuración de Dispatcher.

Las canalizaciones de pila completa pueden ser canalizaciones de calidad del código o implementación.

### Configuración de canalizaciones de pila completa {#configure-full-stack}

Consulte [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code).
Consulte [Agregar una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

## Configuración de canalizaciones {#config-deployment-pipeline}

Mediante una canalización de configuración, puede implementar rápidamente la configuración para el reenvío de registros, las tareas de mantenimiento relacionadas con la depuración y varias configuraciones de CDN, incluidas las reglas de filtro de tráfico (como las reglas de WAF (cortafuegos de aplicaciones web)). Además, puede administrar transformaciones de solicitud y respuesta, selectores de origen, redirecciones del lado del cliente, páginas de error, claves CDN administradas por el cliente, claves API de depuración y autenticación básica.

Consulte [Usar canalizaciones de configuración](/help/operations/config-pipeline.md) para obtener una lista completa de las funciones admitidas y para aprender a administrar las configuraciones en el repositorio de modo que se implementen correctamente.

>[!NOTE]
>
>Las canalizaciones de configuración de Edge Delivery no tienen entornos de desarrollo, ensayo y producción independientes. En AEM as a Cloud Service, los cambios se mueven a través de los niveles de desarrollo, fase y producción. Por el contrario, una canalización de configuración de Edge Delivery aplica su configuración directamente a todos los dominios de Edge Delivery Sites registrados en Cloud Manager. Para obtener más información, consulte [Agregar una canalización de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).


### Configurar canalizaciones de configuración {#configure-config-deployment}

Consulte [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment).
Consulte [Agregar una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment).

## Canalizaciones front-end {#front-end}

El código front-end es cualquier código que sirve como archivos estáticos. Es independiente del código de la IU que sirve AEM y puede incluir temas del sitio, SPA definidos por el cliente, SPA y otras soluciones.

Las canalizaciones front-end ayudan a sus equipos a optimizar su proceso de diseño y desarrollo al permitir la implementación acelerada del código front-end, asincrónica del desarrollo back-end. Esta canalización dedicada implementa JavaScript y CSS en la capa de distribución de AEM como tema, lo que da como resultado una nueva versión del tema, a la que se puede hacer referencia desde páginas que ofrece AEM.

>[!NOTE]
>
>Un usuario con el rol de **Administrador de implementación** puede crear y ejecutar varias canalizaciones front-end simultáneamente.
>
>Sin embargo, hay un límite máximo de 300 canalizaciones por programa (en todos los tipos).

Las canalizaciones front-end pueden ser de calidad del código o implementación.

### Antes de configurar canalizaciones front-end {#before-start}

Antes de configurar las canalizaciones front-end, revise el [Recorrido de creación de sitios rápidos de AEM](/help/journey-sites/quick-site/overview.md) para obtener una guía completa a través de la herramienta de creación de sitios rápidos de AEM fácil de usar. Este recorrido le ayuda a optimizar su desarrollo front-end y le permite personalizar su sitio rápidamente sin conocimientos del back-end de AEM.

### Configuración de una canalización front-end {#configure-front-end}

Consulte [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline).
Consulte [Agregar una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline).

### Desarrollo de sitios con canalización front-end {#developing-with-front-end-pipeline}

Con las canalizaciones front-end, se da más independencia a los desarrolladores de front-end y el proceso de desarrollo se puede acelerar.

Consulte [Desarrollo de sitios con canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber cómo funciona este proceso, así como algunas consideraciones que deben tenerse en cuenta para aprovechar al máximo este proceso.

## Canalizaciones de configuración de nivel web {#web-tier-config-pipelines}

Las canalizaciones de configuración de nivel web permiten la implementación exclusiva de la configuración de HTTPD/Dispatcher en el tiempo de ejecución de AEM, desacoplándola de otros cambios de código. Es una canalización optimizada que proporciona a los usuarios que solo desean implementar los cambios de configuración de Dispatcher, un medio acelerado para hacerlo en solo unos minutos.

>[!TIP]
>
>Las canalizaciones de configuración de nivel web le permiten almacenar su configuración web en la misma ubicación de origen o en una diferente como canalización de pila completa, según lo que mejor se adapte a la estructura de su proyecto.

Se aplican las siguientes restricciones.

* Estar en la versión de AEM `2021.12.6151.20211217T120950Z` o posterior para utilizar canalizaciones de configuración de nivel web.
* [Opte por el modo flexible de las herramientas de Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para usar canalizaciones de configuración de nivel web.
* El usuario debe registrarse con la función de **Administrador de implementación** para configurar o ejecutar canalizaciones.
* En cualquier momento, solo puede haber una canalización de configuración de nivel web por entorno.
* El usuario no puede configurar una canalización de configuración de nivel web cuando se está ejecutando su canalización de pila completa correspondiente.
* La estructura del nivel web debe adherirse a la estructura de modo flexible, tal como se define en el documento [Dispatcher en la nube](/help/implementing/dispatcher/disp-overview.md#validation-debug).

Además, tenga en cuenta cómo se comporta la [canalización de pila completa](#full-stack-pipeline) al introducir una canalización de nivel web.

* Si no se configura una canalización de configuración de nivel web para un entorno, el usuario puede elegir incluir o ignorar la configuración de Dispatcher al configurar la canalización de pila completa. Esta selección se realiza durante la ejecución y la implementación.
* Una vez que una canalización de configuración de nivel web está configurada para un entorno, su canalización de pila completa correspondiente (si existe) ignora la configuración de Dispatcher durante la ejecución y la implementación.
* Una vez que se elimina una canalización de configuración de nivel web, su canalización de pila completa correspondiente se restablece para implementar las configuraciones de Dispatcher durante su ejecución.

Las canalizaciones de configuración de nivel web pueden ser del tipo `Code quality` o `Deployment`.

### Configuración de canalizaciones de nivel web {#configure-web-tier}

Consulte [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment).
Consulte [Agregar una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment).

## Vídeo con información general sobre los tipos de canalización {#video}

Para obtener una descripción general rápida de los tipos de canalización, vea el siguiente vídeo (2 minutos, 26 segundos).

>[!VIDEO](https://video.tv.adobe.com/v/342363)
