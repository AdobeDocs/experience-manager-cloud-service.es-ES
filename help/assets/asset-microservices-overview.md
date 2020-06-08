---
title: Conozca cómo los microservicios de recursos pueden procesar sus recursos digitales en la nube
description: Procese sus recursos digitales mediante microservicios de procesamiento de recursos escalables y nativos de la nube.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 3%

---


# Visión general de la ingestión y el procesamiento de activos con microservicios de activos {#asset-microservices-overview}

<!--
First half of content at https://git.corp.adobe.com/aklimets/project-nui/blob/master/docs/Project-Nui-Asset-Compute-Service.md is useful for this article.
TBD: Post-GA we will provide detailed information at \help\assets\asset-microservices-configure-and-use.md. However, for GA, all information is added, in short, in this article.
-->

Adobe Experience Manager como servicio de nube proporciona un método nativo de la nube para aprovechar las aplicaciones y capacidades de Experience Manager. Uno de los elementos clave de esta nueva arquitectura es la ingestión y el procesamiento de activos, impulsados por microservicios de activos. Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios en la nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los beneficios clave de los microservicios de recursos nativos de la nube son:

* Arquitectura escalable que permite un procesamiento sin problemas para operaciones con gran cantidad de recursos.
* extracciones de texto e indexación eficaces que no afectan al rendimiento de los entornos de Experience Manager.
* Minimice la necesidad de flujos de trabajo para gestionar el procesamiento de recursos en el entorno de Experience Manager. Esto libera recursos, minimiza la carga en Experience Manager y proporciona escalabilidad.
* Se ha mejorado la resiliencia del procesamiento de recursos. Los posibles problemas al gestionar archivos atípicos, como archivos dañados o archivos extremadamente grandes, ya no afectan al rendimiento de la implementación.
* Configuración simplificada del procesamiento de recursos para los administradores.
* Adobe administra y mantiene la configuración de procesamiento de recursos para proporcionar la configuración más conocida para la gestión de representaciones, metadatos y extracción de texto para distintos tipos de archivos
* Los servicios nativos de procesamiento de archivos de Adobe se utilizan cuando procede, lo que proporciona una salida de alta fidelidad y una gestión [eficaz de los formatos](file-format-support.md)propiedad de Adobe.
* Capacidad de configurar el flujo de trabajo posterior al procesamiento para agregar acciones e integraciones específicas del usuario.

Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como la transcodificación de ImageMagick y FFmpeg) y simplifican las configuraciones, al tiempo que proporcionan una funcionalidad lista para usar para tipos de archivos comunes.

## Arquitectura de alto nivel {#asset-microservices-architecture}

Un diagrama de arquitectura de alto nivel muestra los elementos clave de la ingesta y el procesamiento y flujo de recursos en todo el sistema.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Ingesta y procesamiento de activos con](assets/asset-microservices-overview.png "microservicios de activosToma y procesamiento de activos con microservicios de activos")

Los pasos clave de la ingestión y el procesamiento mediante microservicios de activos son:

* Los clientes, como los exploradores web o Adobe Asset Link, envían una solicitud de carga a Experience Manager y inicio que cargan el binario directamente en el almacenamiento de nube binario.
* Cuando se completa la carga binaria directa, el cliente notifica a Experience Manager.
* Experience Manager envía una solicitud de procesamiento a los microservicios de recursos. El contenido de la solicitud depende de la configuración de perfiles de procesamiento de Experience Manager que especifique, qué representaciones se generarán.
* Assets microservices back-end recibe la solicitud, la envía a uno o varios microservicios en función de la solicitud. Cada microservicio accede al binario original directamente desde el almacén de nube binario.
* Los resultados del procesamiento, como las representaciones, se almacenan en el almacenamiento de nube binaria.
* Se notifica a Experience Manager que el procesamiento se completa junto con punteros directos a los binarios (representaciones) generados. Las representaciones generadas están disponibles en Experience Manager para el recurso cargado.

Este es el flujo básico de procesamiento e ingesta de recursos. Si está configurado, Experience Manager también puede inicio de un modelo de flujo de trabajo personalizado para realizar el posprocesamiento del recurso. Por ejemplo, ejecute pasos personalizados que sean específicos de su entorno, como recuperar información de un sistema empresarial y agregarla a las propiedades del recurso.

La ingestión y el flujo de procesamiento son conceptos clave de la arquitectura de los microservicios de recursos para Experience Manager.

* **Acceso** binario directo: Los recursos se transportan (y se cargan) al almacén binario de la nube una vez configurados para los entornos de Experience Manager y, a continuación, AEM, los microservicios de recursos y, finalmente, los clientes obtienen acceso directo a ellos para realizar su trabajo. Esto minimiza la carga en las redes y la duplicación de binarios almacenados
* **Procesamiento** externo: El procesamiento de los recursos se realiza fuera del entorno AEM y guarda sus recursos (CPU, memoria) para proporcionar funciones clave de la administración de recursos digitales y admitir el trabajo interactivo con el sistema para los usuarios finales

## Carga de recursos con acceso binario directo {#asset-upload-with-direct-binary-access}

Los clientes de Experience Manager, que forman parte de la oferta de productos, admiten la carga con acceso binario directo de forma predeterminada. Estas incluyen la carga mediante la interfaz web, Adobe Asset Link y la aplicación de escritorio de AEM.

Puede utilizar herramientas de carga personalizadas, que funcionan directamente con las API HTTP de AEM. Puede utilizar estas API directamente o utilizar y ampliar los siguientes proyectos de código abierto que implementan el protocolo de carga:

* [Biblioteca de carga de código abierto](https://github.com/adobe/aem-upload)
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem)

Para obtener más información, consulte [Carga de recursos](add-assets.md).

## Añadir postprocesamiento de recursos personalizados {#add-custom-asset-post-processing}

Aunque la mayoría de los clientes deben obtener todos sus requisitos de procesamiento de recursos de los microservicios de recursos configurables, algunos podrían necesitar un procesamiento de recursos adicional. Esto es especialmente cierto si los recursos deben procesarse en base a la información proveniente de otros sistemas a través de integraciones. En casos como este, se pueden utilizar flujos de trabajo de postprocesamiento personalizados.

Los flujos de trabajo posteriores al procesamiento son modelos habituales de flujo de trabajo de AEM, creados y administrados en el editor de flujo de trabajo de AEM. Los clientes pueden configurar los flujos de trabajo para realizar pasos de procesamiento adicionales en un recurso, incluido el uso de los pasos de flujo de trabajo predeterminados y flujos de trabajo personalizados disponibles.

Adobe Experience Manager se puede configurar para que active automáticamente los flujos de trabajo posteriores al procesamiento después de que finalice el procesamiento de recursos.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [Introducción a los microservicios de recursos](asset-microservices-configure-and-use.md)
>* [Formatos de archivo compatibles](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)
>* [Aplicación de escritorio de AEM](https://docs.adobe.com/content/help/es-ES/experience-manager-desktop-app/using/introduction.translate.html)
>* [Documentación de Apache Oak sobre acceso binario directo](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

