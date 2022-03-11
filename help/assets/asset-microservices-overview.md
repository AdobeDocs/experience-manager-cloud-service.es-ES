---
title: Procesamiento de recursos mediante microservicios de recursos
description: Procese sus recursos digitales mediante microservicios de procesamiento de recursos escalables y nativos de la nube.
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Release Information,Asset Processing
role: Architect,Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 2%

---

# Información general sobre la ingesta y el procesamiento de recursos con los microservicios de recursos {#asset-microservices-overview}

Adobe Experience Manager as a [!DNL Cloud Service] proporciona un método nativo de la nube para aprovechar las aplicaciones y capacidades de Experience Manager. Uno de los elementos clave de esta nueva arquitectura es la ingesta y el procesamiento de recursos, con tecnología de microservicios de recursos. Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios de nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Las ventajas clave de los microservicios de recursos nativos de la nube son:

* Scalable architecture that allows for seamless processing for resource-intensive operations.
* Efficient indexing and text extractions that does not impact the performance of your Experience Manager environments.
* Minimice la necesidad de flujos de trabajo para gestionar el procesamiento de recursos en el entorno de Experience Manager. This frees up resources, minimizes load on Experience Manager, and provides scalability.
* Mejora de la flexibilidad del procesamiento de recursos. Los problemas potenciales al gestionar archivos atípicos, como archivos dañados o archivos extremadamente grandes, ya no afectan al rendimiento de la implementación.
* Configuración simplificada del procesamiento de recursos para los administradores.
* Assets processing setup is managed and maintained by Adobe to provide best known configuration for handling renditions, metadata, and text extraction for various file types
* Los servicios nativos de procesamiento de archivos de Adobe se utilizan cuando corresponde, lo que proporciona una salida de alta fidelidad y [manejo eficiente de los formatos propietarios de Adobe](file-format-support.md).
* Capacidad para configurar el flujo de trabajo posterior al procesamiento para agregar acciones e integraciones específicas del usuario.

Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como [!DNL ImageMagick] y la transcodificación FFmpeg) y simplifican las configuraciones, al tiempo que proporcionan funcionalidad básica para los formatos de archivo comunes de forma predeterminada.

## Arquitectura de alto nivel {#asset-microservices-architecture}

Un diagrama de arquitectura de alto nivel representa los elementos clave de la ingesta y el procesamiento de recursos y el flujo de recursos a través del sistema.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Ingesta y procesamiento de recursos con microservicios de recursos](assets/asset-microservices-overview.png "Ingesta y procesamiento de recursos con microservicios de recursos")

Los pasos clave de la ingesta y el procesamiento mediante los microservicios de recursos son:

* Los clientes, como los navegadores web o Adobe Asset Link, envían una solicitud de carga a [!DNL Experience Manager] y empiece a cargar el binario directamente en el almacenamiento binario en la nube.
* Cuando se completa la carga binaria directa, el cliente notifica [!DNL Experience Manager].
* [!DNL Experience Manager] envía una solicitud de procesamiento a los microservicios de recursos. El contenido de la solicitud depende de la configuración de perfiles de procesamiento de [!DNL Experience Manager] que especifique, qué representaciones desea generar.
* El back-end de los microservicios de recursos recibe la solicitud y la envía a uno o varios microservicios en función de la solicitud. Cada microservicio accede al binario original directamente desde el almacén de nube binario.
* Los resultados del procesamiento, como las representaciones, se almacenan en el almacenamiento en la nube binaria.
* Se notifica al Experience Manager de que el procesamiento se ha completado junto con punteros directos a los binarios generados (representaciones). Las representaciones generadas están disponibles en [!DNL Experience Manager] para el recurso cargado.

Este es el flujo básico de consumo y procesamiento de recursos. Si está configurado, el Experience Manager también puede iniciar un modelo de flujo de trabajo personalizado para realizar el posprocesamiento del recurso. For example, execute customized steps that are specific to your environment, such as fetch information from an enterprise system and add to asset properties.

The ingestion and processing flow are key concepts of the asset microservices architecture for Experience Manager.

* **Direct binary access**: Assets are transported (and uploaded) to the Cloud Binary Store once configured for Experience Manager environments, and then [!DNL Experience Manager], asset microservices, and finally clients get direct access to them to carry out their work. Esto minimiza la carga en redes y la duplicación de binarios almacenados
* **Procesamiento externo**: El procesamiento de los recursos se realiza fuera de [!DNL Experience Manager] y guarda sus recursos (CPU, memoria) para proporcionar funcionalidades clave de Digital Asset Management (DAM) y admitir el trabajo interactivo con el sistema para los usuarios finales

## Asset upload with direct binary access {#asset-upload-with-direct-binary-access}

Experience Manager clients, which are a part of product offering, all support upload with direct binary access by default. Estas incluyen la carga mediante la interfaz web, el vínculo de recursos de Adobe y [!DNL Experience Manager] aplicación de escritorio.

Puede utilizar herramientas de carga personalizadas que funcionen directamente con [!DNL Experience Manager] API HTTP. Puede utilizar estas API directamente o utilizar y ampliar los siguientes proyectos de código abierto que implementan el protocolo de carga:

* [Biblioteca de carga de código abierto](https://github.com/adobe/aem-upload)
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem)

Para obtener más información, consulte [cargar recursos](add-assets.md).

## Agregar procesamiento posterior de recursos personalizado {#add-custom-asset-post-processing}

Aunque la mayoría de los clientes deben obtener todos los servicios de procesamiento de recursos que necesitan los microservicios de recursos configurables, es posible que algunos necesiten un procesamiento de recursos adicional. Esto es especialmente cierto si los recursos deben procesarse en función de la información proveniente de otros sistemas a través de integraciones. En casos como este, se pueden utilizar flujos de trabajo personalizados posteriores al procesamiento.

Post-processing workflows are regular [!DNL Experience Manager] workflow models, created and managed in [!DNL Experience Manager] Workflow editor. Los clientes pueden configurar los flujos de trabajo para realizar pasos de procesamiento adicionales en un recurso, incluido el uso de los pasos de flujo de trabajo predeterminados disponibles y los flujos de trabajo personalizados.

Adobe Experience Manager can be configured to automatically trigger the post-processing workflows after asset processing completes.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [Introducción a los microservicios de recursos](asset-microservices-configure-and-use.md)
>* [Formatos de archivo compatibles](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)
>* Aplicación de escritorio de [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Apache Oak documentation on direct binary access](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

