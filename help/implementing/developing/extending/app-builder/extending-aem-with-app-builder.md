---
title: Ampliando  [!DNL Adobe Experience Manager] as a Cloud Service mediante Adobe Developer App Builder.
description: Ampliando  [!DNL Adobe Experience Manager] as a Cloud Service mediante Adobe Developer App Builder.
exl-id: 50d82745-5deb-4bfa-961b-714842403601
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 00a05b3bdc1a689947c1507847da99b54c94dcac
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Ampliar [!DNL Adobe Experience Manager] as a Cloud Service mediante Adobe Developer App Builder {#extend-using-app-builder}

## Qué es App Builder para AEM as a Cloud Service {#project-appbuilder}

La nueva Adobe Developer App Builder proporciona un marco de trabajo de extensibilidad para que un desarrollador pueda ampliar fácilmente las funcionalidades de AEM as a Cloud Service.

App Builder proporciona un marco de trabajo de extensibilidad unificado de terceros para integrar y crear experiencias personalizadas que amplíen Adobe Experience Manager. Con este marco de trabajo de extensibilidad completo, basado en la infraestructura de Adobe, los desarrolladores pueden crear microservicios personalizados, ampliar e integrar Adobe Experience Manager en todas las soluciones de Adobe y en el resto de la pila de TI.

App Builder permite a los clientes ampliar fácilmente Adobe Experience Manager en varios casos de uso:

* Extensibilidad de middleware: conecte sistemas externos con aplicaciones de Adobe creando conectores personalizados o utilice un conjunto de integraciones prediseñadas.
* Extensibilidad de los servicios principales: amplíe las funciones de las aplicaciones principales ampliando el comportamiento predeterminado con funciones personalizadas y lógica empresarial.
* Extensibilidad de la experiencia del usuario: amplíe la experiencia principal para satisfacer los requisitos comerciales o cree propiedades digitales, tiendas y aplicaciones de back-office específicas para el cliente.

>[!NOTE]
>
> Para los clientes de AEM 6.5 que deseen usar App Builder, consulte [Ampliación de Adobe Experience Manager 6.5 con Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## Arquitectura {#architecture}

En lugar de una solución predeterminada, Adobe Developer App Builder proporciona una plataforma de desarrollo común, coherente y estandarizada para ampliar las soluciones de Adobe Cloud como AEM, que incluye:

* Adobe Developer Console: para el desarrollo de microservicios y extensiones personalizadas, permite a los desarrolladores crear y administrar proyectos mientras acceden a todas las herramientas y API necesarias para poder crear complementos e integraciones.
* Herramientas para desarrolladores: herramientas de código abierto, SDK y bibliotecas para permitir a los desarrolladores crear fácilmente integraciones y extensiones personalizadas. Utilice React Spectrum (Kit de herramientas de IU de Adobe) para tener una interfaz de usuario común para todas las aplicaciones de Adobe.
* Servicios: I/O Runtime para alojar infraestructura en la plataforma sin servidor de Adobe y eventos de I/O para integraciones basadas en eventos. Adobe también es compatible de serie con el almacenamiento de datos y archivos.
* Adobe Experience Cloud: los desarrolladores pueden enviar extensiones e integraciones para que se publiquen dentro de su organización de Experience Cloud. Los administradores del sistema pueden revisar, administrar y aprobar estas extensiones. Una vez publicadas, las extensiones y herramientas personalizadas de App Builder se pueden encontrar junto con otras aplicaciones de Adobe Experience Cloud.

El diagrama siguiente ilustra cómo una aplicación estándar creada en App Builder utiliza estas funcionalidades:

![Arquitectura](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

Para obtener más información acerca de la arquitectura de App Builder, vea [Descripción general de la arquitectura.](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/architecture_overview/architecture-overview)

## Introducción a App Builder {#additional-resources}

Adobe ha creado la siguiente documentación de introducción para que pueda empezar a usar App Builder:

* [Introducción a App Builder](https://developer.adobe.com/app-builder/docs/getting_started/)

## Continuar aprendiendo con la documentación {#appbuilder-documentation}

App Builder proporciona vídeos y documentación para desarrolladores, incluidas guías y documentación de referencia, para ayudarle a empezar a desarrollar sus propias aplicaciones personalizadas:

* [Documentación de App Builder](https://developer.adobe.com/app-builder/docs/overview/)
* [Vídeos de App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Pruebe una de las aplicaciones de ejemplo {#appbuilder-codesamples}

¿Listo para empezar a desarrollar? Adobe tiene muchas aplicaciones de ejemplo para ayudarle a ponerse en marcha rápidamente:

* [App Builder Code Labs en el sitio web de Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/)