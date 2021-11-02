---
title: Canalizaciones CI-CD
description: Canalizaciones CI-CD
index: false
source-git-commit: 76cff84003576cf23eb1d23674ce6eaf082bbbb1
workflow-type: tm+mt
source-wordcount: '700'
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

## Canalización de producción {#prod-pipeline}

Las canalizaciones de producción son una canalización creada a propósito que incluye una serie de pasos organizados para llevar el código fuente hasta la producción. Los pasos incluyen la creación, empaquetado, prueba, validación e implementación en todo el entorno de ensayo primero. Huelga decir que una canalización de producción solo se puede añadir una vez que se crea un conjunto de entornos de producción y de fase.

Consulte Configuración de canalización de producción para obtener más información.


## Canalización que no es de producción {#non-prod-pipeline}

Una canalización que no es de producción tiene como objetivo ejecutar análisis de calidad de código o implementar código fuente en un entorno de desarrollo.

Consulte las canalizaciones de no producción y solo calidad de código para obtener más información.

## Explicación de las canalizaciones de CI-CD en Cloud Manager {#understand-pipelines}

La siguiente tabla categoriza las canalizaciones en Cloud Manager junto con su uso.

| Tipo de canalización | Implementación o calidad de código | Código fuente | Cuándo se utiliza | ¿Cuándo o por qué debería usar? |
|--- |--- |--- |---|---|---|
| Producción o no producción | Implementación | Front-End | Para implementar el código front-end. El código front-end es cualquier código que sirve como archivo estático. Es independiente del código de interfaz de usuario que AEM. Incluye temas de sitios, SPA definidas por el cliente, SPA de luciérnagas y otras soluciones. Debe estar en AEM versión. | Tiempos de implementación rápidos.<br> Se pueden configurar y ejecutar varias canalizaciones front-end simultáneamente por cada entorno. |
|  | Implementación | Pila completa | Para implementar la configuración del back-end, front-end y HTTPD/dispatcher al mismo tiempo. Nota: Se aplican algunas restricciones. | Cuando aún no se han adoptado las canalizaciones de configuración de front-end o de nivel web. |
|  | Implementación | Configuración de nivel web | Implementar exclusivamente la configuración de HTTPD/Dispatcher en cuestión de minutos.  Esta canalización optimizada proporciona a los usuarios que solo desean implementar los cambios de configuración de Dispatcher, un medio acelerado para hacerlo. Nota: Debe estar en AEM versión [version] | Tiempos de implementación rápidos. |



## Canalizaciones principales de Cloud Manager {#front-end}

Las canalizaciones front-end ayudan a sus equipos a optimizar su proceso de diseño y desarrollo, al habilitar canalizaciones front-end aceleradas para la implementación de código front-end. Esta canalización diferenciada implementa JavaScript y CSS en la capa de distribución de AEM como tema, lo que da como resultado una nueva versión del tema a la que se puede hacer referencia desde páginas enviadas desde el tiempo de ejecución de AEM. El código front-end es cualquier código que sirve como archivo estático. Es independiente del código de interfaz de usuario que AEM. Incluye temas de sitios, SPA definidas por el cliente, SPA de luciérnagas y otras soluciones.

>[!NOTE]
>Un usuario que ha iniciado sesión como rol Administrador de implementación puede crear y ejecutar varias canalizaciones front-end simultáneamente. Sin embargo, hay un límite máximo de 300 canalizaciones por programa (en todos los tipos).

Existen dos tipos de canalizaciones front-end:

* Calidad del código del front-end
* Implementación del front-end

## Canalizaciones de pila completa {#full-stack-pipeline}

La canalización de pila completa ofrece al usuario la opción de implementar la configuración del back-end, front-end y HTTPD/dispatcher al mismo tiempo.  Implementa código y contenido en el tiempo de ejecución de AEM, incluido código front-end (JavaScript/CSS) empaquetado como bibliotecas de cliente AEM. Puede implementar la configuración de nivel web si no se ha configurado una canalización de nivel web. Esto representa la canalización &#39;uber&#39;, a la vez que ofrece a los usuarios las opciones de implementar exclusivamente su código front-end o configuración de Dispatcher a través de la canalización Front-End y la canalización de configuración de nivel web, respectivamente.


Se aplicarán las siguientes restricciones:

1. Un usuario debe iniciar sesión como administrador de implementación para configurar o ejecutar canalizaciones.

1. En cualquier momento, solo puede haber una canalización de pila completa por entorno.

1. El usuario puede configurar la canalización de pila completa para que un entorno ignore o no la configuración de Dispatcher. Si la canalización de configuración de nivel web correspondiente para el entorno no existe.

1. La canalización de pila completa para un entorno ignorará la configuración de Dispatcher si existe la canalización de configuración de nivel web correspondiente para el entorno.

Existen dos tipos de canalizaciones de pila completa:

* Canalización de calidad de código de pila completa
* Canalización de implementación de pila completa

