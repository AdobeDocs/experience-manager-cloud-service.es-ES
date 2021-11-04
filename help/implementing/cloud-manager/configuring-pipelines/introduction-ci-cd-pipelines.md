---
title: Canalizaciones CI-CD
description: Siga esta página para obtener más información sobre las canalizaciones de CI-CD de Cloud Manager
index: true
source-git-commit: 471924b2edd5e0bccd7c1eb9d6dd36ad2bd89f88
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# Canalizaciones de CI-CD de Cloud Manager {#intro-cicd}

## Introducción {#introduction}

Una canalización de CD/CI en Cloud Manager se puede activar mediante algún tipo de evento, como una solicitud de extracción de un repositorio de código fuente, es decir, un cambio de código o algún tipo de programación regular para coincidir con una cadencia de versión.

>[!NOTE]
>Para configurar la canalización, debe:
>* definir el déclencheur que iniciará la canalización
>* definir los parámetros que controlan la implementación de producción
>* configurar los parámetros de prueba de rendimiento


En Cloud Manager, hay dos tipos de canalizaciones:

* [Canalización de producción](#prod-pipeline)
* [Canalización que no es de producción](#non-prod-pipeline)

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)


## Canalización de producción {#prod-pipeline}

Las canalizaciones de producción son una canalización creada a propósito que incluye una serie de pasos organizados para llevar el código fuente hasta la producción. Los pasos incluyen la creación, empaquetado, prueba, validación e implementación en todo el entorno de ensayo primero. Huelga decir que una canalización de producción solo se puede añadir una vez que se crea un conjunto de entornos de producción y de fase.

Consulte [Configuración de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para obtener más información.


## Canalización que no es de producción {#non-prod-pipeline}

Una canalización que no es de producción tiene como objetivo ejecutar análisis de calidad de código o implementar código fuente en un entorno de desarrollo.

Consulte [Configuración de una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para obtener más información.

## Explicación de las canalizaciones de CI-CD en Cloud Manager {#understand-pipelines}

La siguiente tabla resume todas las canalizaciones de Cloud Manager junto con su uso.

| Tipo de canalización | Implementación o calidad de código | Código fuente | Cuándo se utiliza | ¿Cuándo o por qué debería usar? |
|--- |--- |--- |---|---|
| Producción o no producción | Implementación | Front-End | Tiempos de implementación rápidos.<br>Se pueden configurar y ejecutar varias canalizaciones front-end simultáneamente por cada entorno.<br>La compilación de canalización de front-end extrae la compilación a un almacenamiento. Cuando se sirve una página html, puede hacer referencia a archivos estáticos del código de front-end que serán servidos por la CDN utilizando este almacenamiento como origen. | Implementar exclusivamente código front-end que contenga una o más aplicaciones de interfaz de usuario del lado del cliente. El código front-end es cualquier código que sirve como archivo estático. Es independiente del código de interfaz de usuario que AEM. Incluye temas de sitios, SPA definidas por el cliente, SPA de luciérnagas y otras soluciones.<br>Debe estar en AEM versión 2021.10.5933.20211012T154732Z |
| Producción o no producción | Implementación | Pila completa | Cuando todavía no se han adoptado las tuberías del front-end.<br>En los casos en los que el código de front-end debe implementarse exactamente al mismo tiempo que el código de AEM Server. | Para implementar AEM código de servidor (contenido inmutable, código Java, configuraciones OSGi, configuración HTTPD/dispatcher, repositorio, contenido mutable, fuentes), que contenga una o más aplicaciones de servidor AEM al mismo tiempo. |
| No producción | Calidad de código | Front-End | Para que Cloud Manager evalúe. el éxito de la compilación y la calidad del código sin realizar una implementación.<br>Se pueden configurar y ejecutar varias canalizaciones. | Ejecute análisis de calidad del código en el código front-end. |
| No producción | Calidad de código | Pila completa | Para que Cloud Manager evalúe. el éxito de la compilación y la calidad del código sin realizar una implementación.<br>Se pueden configurar y ejecutar varias canalizaciones. | Ejecute el análisis de calidad del código en el código de pila completo. |


El diagrama siguiente ilustra las configuraciones de canalización de Cloud Manager con el repositorio front-end tradicional o la configuración de repositorios front-end independiente:

![](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Canalizaciones principales de Cloud Manager {#front-end}

Las canalizaciones front-end ayudan a sus equipos a optimizar su proceso de diseño y desarrollo, al habilitar canalizaciones front-end aceleradas para la implementación de código front-end. Esta canalización diferenciada implementa JavaScript y CSS en la capa de distribución de AEM como tema, lo que da como resultado una nueva versión del tema a la que se puede hacer referencia desde páginas enviadas desde el tiempo de ejecución de AEM. El código front-end es cualquier código que sirve como archivo estático. Es independiente del código de interfaz de usuario que AEM. Incluye temas de sitios, SPA definidas por el cliente, SPA de luciérnagas y otras soluciones.

>[!IMPORTANT]
>Debe estar en AEM versión `2021.10.5933.20211012T154732Z ` para aprovechar las canalizaciones front-end.

>[!NOTE]
>Un usuario que ha iniciado sesión como rol Administrador de implementación puede crear y ejecutar varias canalizaciones front-end simultáneamente. Sin embargo, hay un límite máximo de 300 canalizaciones por programa (en todos los tipos).

Pueden ser del tipo Calidad del código front-end o canalizaciones de implementación front-end.

### Antes de configurar canalizaciones front-end {#before-start}

Antes de empezar a configurar las canalizaciones del front-end, consulte [AEM Recorrido de creación rápida de sitios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) para obtener un flujo de trabajo completo mediante la herramienta de creación rápida AEM sitios, que es muy fácil de usar. Este sitio de documentación le ayudará a optimizar el desarrollo front-end de su sitio AEM y a personalizar rápidamente su sitio sin AEM conocimiento back-end.

### Configuración de una canalización front-end {#configure-front-end}

Para aprender a configurar la canalización front-end, consulte:

* [Adición de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adición de una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

## Canalizaciones de pila completa {#full-stack-pipeline}

La canalización de pila completa ofrece al usuario la opción de implementar la configuración del back-end, front-end y HTTPD/dispatcher al mismo tiempo.  Implementa código y contenido en el tiempo de ejecución de AEM, incluido código front-end (JavaScript/CSS) empaquetado como bibliotecas de cliente AEM. Puede implementar la configuración de nivel web si no se ha configurado una canalización de nivel web. Esto representa la canalización &#39;uber&#39;, a la vez que ofrece a los usuarios las opciones de implementar exclusivamente su código front-end o configuración de Dispatcher a través de la canalización Front-End y la canalización de configuración de nivel web, respectivamente.
Pueden ser del tipo Pila completa - Calidad del código o Pila completa - Implementación .

Se aplicarán las siguientes restricciones:

1. Un usuario debe iniciar sesión como administrador de implementación para configurar o ejecutar canalizaciones.

1. En cualquier momento, solo puede haber una canalización de pila completa por entorno.

1. El usuario puede configurar la canalización de pila completa para que un entorno ignore o no la configuración de Dispatcher. Si la canalización de configuración de nivel web correspondiente para el entorno no existe.

1. La canalización de pila completa para un entorno ignorará la configuración de Dispatcher si existe la canalización de configuración de nivel web correspondiente para el entorno.


### Configuración de una canalización de pila completa {#configure-full-stack}

Para aprender a configurar la canalización de pila completa, consulte:

* [Adición de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adición de una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)