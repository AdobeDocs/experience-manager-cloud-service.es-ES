---
title: Ampliación [!DNL Adobe Experience Manager] as a Cloud Service con el Generador de aplicaciones de Adobe Developer.
description: Ampliación [!DNL Adobe Experience Manager] as a Cloud Service con el Generador de aplicaciones de Adobe Developer.
exl-id: 50d82745-5deb-4bfa-961b-714842403601
source-git-commit: a14ee350b3fdc3ac197b703aa36957d1d1dd7355
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Ampliación [!DNL Adobe Experience Manager] as a Cloud Service con el Generador de aplicaciones de Adobe Developer {#extend-using-app-builder}

## AEM ¿Qué es App Builder para el uso de la as a Cloud Service? {#project-appbuilder}

El nuevo Generador de aplicaciones de Adobe Developer AEM proporciona un marco de trabajo de extensibilidad para que un desarrollador pueda ampliar fácilmente las funcionalidades as a Cloud Service de la.

App Builder proporciona un marco de trabajo de extensibilidad unificado de terceros para integrar y crear experiencias personalizadas que amplíen Adobe Experience Manager. Con este marco de trabajo de extensibilidad completo, basado en la infraestructura de Adobe, los desarrolladores pueden crear microservicios personalizados, ampliar e integrar Adobe Experience Manager en todas las soluciones de Adobe y en el resto de la pila de TI.

App Builder permite a los clientes ampliar fácilmente Adobe Experience Manager en varios casos de uso:

* Extensibilidad de middleware: conecte sistemas externos con aplicaciones de Adobe creando conectores personalizados o aproveche un conjunto de integraciones prediseñadas.
* Extensibilidad de los servicios principales: amplíe las funciones de las aplicaciones principales ampliando el comportamiento predeterminado con funciones personalizadas y lógica empresarial.
* Extensibilidad de la experiencia del usuario: amplíe la experiencia principal para satisfacer los requisitos comerciales o cree propiedades digitales, tiendas y aplicaciones de back-office específicas para el cliente.

App Builder está disponible para clientes y socios empresariales a través de nuestra vista previa para desarrolladores desde el verano de 2020. La disponibilidad general (GA) del Generador de aplicaciones está programada para diciembre de 2021. Damos la bienvenida a los desarrolladores a probar el App Builder a través de nuestro [Programa de prueba](https://adobe.ly/appbuilder-trial).

>[!NOTE]
>
> AEM Para los clientes de 6.5 que desean aprovechar el Generador de aplicaciones, vaya a [Ampliación de Adobe Experience Manager 6.5 con el Generador de aplicaciones de Adobe Developer](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## Arquitectura {#architecture}

En lugar de una solución predeterminada, Adobe Developer App Builder proporciona una plataforma de desarrollo común, coherente y estandarizada para ampliar las soluciones de Adobe AEM Cloud, como las siguientes:

* Consola de Adobe Developer: para el desarrollo personalizado de microservicios y extensiones, permite a los desarrolladores crear y administrar proyectos al mismo tiempo que acceden a todas las herramientas y API que necesitan para crear complementos e integraciones.
* Herramientas para desarrolladores: herramientas de código abierto, SDK y bibliotecas para permitir a los desarrolladores crear fácilmente integraciones y extensiones personalizadas. Utilice React Spectrum (kit de herramientas de IU de Adobe) para tener una IU común para todas las aplicaciones de Adobe.
* Servicios: I/O Runtime para alojar infraestructura en nuestra plataforma sin servidor y eventos de I/O para integraciones basadas en eventos. También proporcionamos soporte listo para usar para almacenar datos y archivos.
* Adobe Experience Cloud: los desarrolladores pueden enviar extensiones e integraciones para que se publiquen dentro de su organización de Experience Cloud. Los administradores del sistema pueden revisar, administrar y aprobar estas extensiones. Una vez publicadas, las extensiones y herramientas personalizadas del Generador de aplicaciones se pueden encontrar junto con otras aplicaciones de Adobe Experience Cloud.

El diagrama siguiente ilustra cómo una aplicación estándar creada en App Builder aprovecha estas funcionalidades:

![Arquitectura](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

Para obtener más información sobre la arquitectura del Generador de aplicaciones, consulte [Descripción general de arquitectura](https://www.adobe.io/app-builder/docs/guides/).

## Introducción al Generador de aplicaciones {#additional-resources}

Para ayudarle a empezar con el Generador de aplicaciones, hemos creado una serie de documentación que le ayudará a empezar:

* [Introducción al Generador de aplicaciones](https://www.adobe.io/app-builder/docs/getting_started/)

## Continuar aprendiendo con la documentación {#appbuilder-documentation}

App Builder proporciona vídeos y documentación para desarrolladores de, incluidas guías y documentación de referencia, para ayudarle a empezar a desarrollar sus propias aplicaciones personalizadas:

* [Documentación del Generador de aplicaciones](https://www.adobe.io/app-builder/docs/overview/)
* [Vídeos del Generador de aplicaciones](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Pruebe una de las aplicaciones de ejemplo {#appbuilder-codesamples}

¿Listo para empezar a desarrollar? Tenemos un montón de aplicaciones de ejemplo para ayudarle a ponerse en marcha rápidamente:

* [App Builder Code Labs en el sitio web de Adobe Developer](https://www.adobe.io/app-builder/docs/resources/)