---
title: Ampliación [!DNL Adobe Experience Manager] as a Cloud Service mediante el Generador de aplicaciones para desarrolladores de Adobe.
description: Ampliación [!DNL Adobe Experience Manager] as a Cloud Service mediante el Generador de aplicaciones para desarrolladores de Adobe.
source-git-commit: 528abc0938a71746c2c8b69382c961686cc42634
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Ampliación [!DNL Adobe Experience Manager] as a Cloud Service con el Generador de aplicaciones para desarrolladores de Adobe {#extend-using-app-builder}

## ¿Qué es App Builder para AEM as a Cloud Service? {#project-firefly}

El nuevo Adobe Developer App Builder proporciona un marco de extensibilidad para que un desarrollador pueda ampliar fácilmente AEM funcionalidades as a Cloud Service.

App Builder proporciona un marco de extensibilidad unificado de terceros para integrar y crear experiencias personalizadas que amplíen Adobe Experience Manager. Con este marco de extensibilidad completo, basado en la infraestructura de Adobe, los desarrolladores pueden crear microservicios personalizados, ampliar e integrar Adobe Experience Manager en las soluciones de Adobe y en el resto de la pila de TI.

App Builder permite a los clientes ampliar fácilmente Adobe Experience Manager en varios casos de uso:

* Extensibilidad de Middleware : conecte sistemas externos con aplicaciones de Adobe que generen conectores personalizados o aproveche un conjunto de integraciones prediseñadas.
* Extensibilidad de los servicios principales : amplíe las funcionalidades de las aplicaciones principales ampliando el comportamiento predeterminado con funciones personalizadas y lógica empresarial.
* Extensibilidad de la experiencia del usuario : amplíe la experiencia principal para satisfacer los requisitos comerciales o genere propiedades digitales, tiendas y aplicaciones de back-office específicas del cliente.

App Builder (anteriormente conocido como Project Firefly) está disponible para clientes y socios empresariales a través de nuestra vista previa para desarrolladores desde el verano de 2020. La disponibilidad general (GA) de App Builder está programada para diciembre de 2021. Agradecemos a los desarrolladores probar App Builder a través de nuestra [Programa de prueba](http://adobe.ly/appbuilder-trial).

>[!NOTE]
>
> Para AEM clientes de 6.5 que deseen aprovechar el Creador de aplicaciones, vaya a [Ampliación de Adobe Experience Manager 6.5 mediante Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## Arquitectura {#architecture}

En lugar de una solución lista para usar, Adobe Developer App Builder proporciona una plataforma de desarrollo común, coherente y estandarizada para ampliar las soluciones de Adobe Cloud, como las AEM, que incluye:

* Adobe Developer Console: para el microservicio personalizado y el desarrollo de extensiones, permite a los desarrolladores crear y administrar proyectos al acceder a todas las herramientas y API necesarias para crear complementos e integraciones.
* Herramientas para desarrolladores: herramientas de código abierto, SDK y bibliotecas para que los desarrolladores puedan crear fácilmente extensiones e integraciones personalizadas. Utilice React Spectrum (kit de herramientas de IU de Adobe) para tener una IU común para todas las aplicaciones de Adobe.
* Servicios: I/O Runtime para la infraestructura de alojamiento en nuestra plataforma sin servidor y Eventos de E/S para integraciones basadas en eventos. También proporcionamos soporte para el almacenamiento de datos y archivos.
* Adobe Experience Cloud: los desarrolladores pueden enviar extensiones e integraciones para publicarlas en su organización de Experience Cloud. Los administradores del sistema pueden revisar, administrar y aprobar estas extensiones. Una vez publicadas, las herramientas y extensiones personalizadas de App Builder se encuentran junto con otras aplicaciones de Adobe Experience Cloud.

El diagrama siguiente ilustra cómo una aplicación estándar creada en App Builder aprovecha estas funcionalidades:

![Arquitectura](/help/implementing/developing/extending/assets/firefly-architecture.jpg)

Para obtener más información sobre la arquitectura de App Builder, consulte [Información general sobre la arquitectura](https://www.adobe.io/app-builder/docs/guides/).

## Introducción a App Builder {#additional-resources}

Para ayudarle a empezar con App Builder, hemos creado una serie de documentación para ayudarle a empezar:

* [Introducción a App Builder](https://www.adobe.io/app-builder/docs/getting_started/)

## Continuar aprendiendo con la documentación {#appbuilder-documentation}

App Builder proporciona vídeos y documentación para desarrolladores, incluidas guías, y documentación de referencia para ayudarle a empezar a desarrollar sus propias aplicaciones personalizadas:

* [Documentación de App Builder](https://www.adobe.io/app-builder/docs/overview/)
* [Vídeos de App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Pruebe una de las aplicaciones de ejemplo {#appbuilder-codesamples}

¿Listo para empezar a desarrollarse? Tenemos muchas aplicaciones de muestra para ayudarle a ponerse en marcha rápidamente:

* [Etiquetas de código de App Builder en el sitio web del desarrollador de Adobe](https://www.adobe.io/app-builder/docs/resources/)

## Asistencia {#support}

Para el tipo de solicitud de asistencia al desarrollador, recomendamos a los desarrolladores que utilicen nuestra [Foro de Experience League](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly).
