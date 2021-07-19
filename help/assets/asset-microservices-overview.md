---
title: Procesamiento de recursos mediante microservicios de recursos
description: Procese sus recursos digitales mediante microservicios de procesamiento de recursos escalables y nativos de la nube.
contentOwner: AG
feature: Microservicios de asset compute,Flujo de trabajo,Información de versión,Procesamiento de recursos
role: Architect,Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 2%

---

# Descripción general de la ingesta y el procesamiento de recursos con los microservicios de recursos {#asset-microservices-overview}

Adobe Experience Manager as a [!DNL Cloud Service] proporciona un método nativo de la nube para aprovechar las aplicaciones y capacidades de Experience Manager. Uno de los elementos clave de esta nueva arquitectura es la ingesta y el procesamiento de recursos, con tecnología de microservicios de recursos. Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios de nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Las ventajas clave de los microservicios de recursos nativos de la nube son:

* Arquitectura escalable que permite un procesamiento sin problemas para operaciones que requieren muchos recursos.
* La indexación eficaz y las extracciones de texto que no afectan al rendimiento de los entornos de Experience Manager.
* Minimice la necesidad de flujos de trabajo para gestionar el procesamiento de recursos en el entorno de Experience Manager. Esto libera recursos, minimiza la carga en el Experience Manager y proporciona escalabilidad.
* Mejora de la flexibilidad del procesamiento de recursos. Los problemas potenciales al gestionar archivos atípicos, como archivos dañados o archivos extremadamente grandes, ya no afectan al rendimiento de la implementación.
* Configuración simplificada del procesamiento de recursos para los administradores.
* La configuración del procesamiento de recursos se administra y mantiene en Adobe para proporcionar la configuración más conocida para administrar representaciones, metadatos y extracción de texto para varios tipos de archivo
* Los servicios nativos de procesamiento de archivos de Adobe se utilizan cuando corresponde, proporcionando salida de alta fidelidad y [manejo eficiente de formatos propietarios de Adobe](file-format-support.md).
* Capacidad para configurar el flujo de trabajo posterior al procesamiento para agregar acciones e integraciones específicas del usuario.

Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como la [!DNL ImageMagick] y la transcodificación FFmpeg) y simplifican las configuraciones, al tiempo que proporcionan funcionalidad básica para los formatos de archivo comunes de forma predeterminada.

## Arquitectura de alto nivel {#asset-microservices-architecture}

Un diagrama de arquitectura de alto nivel representa los elementos clave de la ingesta y el procesamiento de recursos y el flujo de recursos a través del sistema.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Ingesta y procesamiento de recursos con ](assets/asset-microservices-overview.png "microservicios de recursosIngesta y procesamiento de recursos con microservicios de recursos")

Los pasos clave de la ingesta y el procesamiento mediante los microservicios de recursos son:

* Los clientes, como los navegadores web o Adobe Asset Link, envían una solicitud de carga a [!DNL Experience Manager] y comienzan a cargar el binario directamente en el almacenamiento binario en la nube.
* Cuando se completa la carga binaria directa, el cliente notifica a [!DNL Experience Manager].
* [!DNL Experience Manager] envía una solicitud de procesamiento a los microservicios de recursos. El contenido de la solicitud depende de la configuración de perfiles de procesamiento de [!DNL Experience Manager] que especifique, qué representaciones generar.
* El back-end de los microservicios de recursos recibe la solicitud y la envía a uno o varios microservicios en función de la solicitud. Cada microservicio accede al binario original directamente desde el almacén de nube binario.
* Los resultados del procesamiento, como las representaciones, se almacenan en el almacenamiento en la nube binaria.
* Se notifica al Experience Manager de que el procesamiento se ha completado junto con punteros directos a los binarios generados (representaciones). Las representaciones generadas están disponibles en [!DNL Experience Manager] para el recurso cargado.

Este es el flujo básico de consumo y procesamiento de recursos. Si está configurado, el Experience Manager también puede iniciar un modelo de flujo de trabajo personalizado para realizar el posprocesamiento del recurso. Por ejemplo, ejecute pasos personalizados específicos de su entorno, como recuperar información de un sistema empresarial y agregarla a propiedades de recursos.

La ingesta y el flujo de procesamiento son conceptos clave de la arquitectura de microservicios de recursos para Experience Manager.

* **Acceso binario directo**: Los recursos se transportan (y se cargan) a la tienda binaria de la nube una vez configurados para entornos de Experience Manager y, a continuación,  [!DNL Experience Manager], los microservicios de recursos y, finalmente, los clientes obtienen acceso directo a ellos para llevar a cabo su trabajo. Esto minimiza la carga en redes y la duplicación de binarios almacenados
* **Procesamiento** externalizado: El procesamiento de los recursos se realiza fuera del  [!DNL Experience Manager] entorno y guarda sus recursos (CPU, memoria) para proporcionar funcionalidades clave de la administración de recursos digitales (DAM) y admitir el trabajo interactivo con el sistema para los usuarios finales

## Carga de recursos con acceso binario directo {#asset-upload-with-direct-binary-access}

Los clientes Experience Manager, que forman parte de la oferta de productos, admiten la carga con acceso binario directo de forma predeterminada. Estas incluyen la carga mediante la interfaz web, el vínculo de recursos de Adobe y la aplicación de escritorio [!DNL Experience Manager].

Puede utilizar herramientas de carga personalizadas que funcionen directamente con [!DNL Experience Manager] API HTTP. Puede utilizar estas API directamente o utilizar y ampliar los siguientes proyectos de código abierto que implementan el protocolo de carga:

* [Biblioteca de carga de código abierto](https://github.com/adobe/aem-upload)
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem)

Para obtener más información, consulte [carga de recursos](add-assets.md).

## Agregar procesamiento posterior de recursos personalizado {#add-custom-asset-post-processing}

Aunque la mayoría de los clientes deben obtener todos los servicios de procesamiento de recursos que necesitan los microservicios de recursos configurables, es posible que algunos necesiten un procesamiento de recursos adicional. Esto es especialmente cierto si los recursos deben procesarse en función de la información proveniente de otros sistemas a través de integraciones. En casos como este, se pueden utilizar flujos de trabajo personalizados posteriores al procesamiento.

Los flujos de trabajo posteriores al procesamiento son modelos de flujo de trabajo [!DNL Experience Manager] normales, creados y administrados en el editor de flujo de trabajo [!DNL Experience Manager]. Los clientes pueden configurar los flujos de trabajo para realizar pasos de procesamiento adicionales en un recurso, incluido el uso de los pasos de flujo de trabajo predeterminados disponibles y los flujos de trabajo personalizados.

Adobe Experience Manager se puede configurar para que déclencheur automáticamente los flujos de trabajo posteriores al procesamiento una vez finalizado el procesamiento de los recursos.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [Introducción a los microservicios de recursos](asset-microservices-configure-and-use.md)
* [Formatos de archivo compatibles](file-format-support.md)
* [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)
* Aplicación de escritorio de [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
* [Documentación de Apache Oak sobre acceso binario directo](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

