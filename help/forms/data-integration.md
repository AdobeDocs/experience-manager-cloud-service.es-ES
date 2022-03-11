---
title: 'Conexión de una base de datos a [!DNL AEM Forms] ¿as a Cloud Service? '
seo-title: AEM Forms Data Integration
description: Puede recuperar y guardar datos en servicios web RESTful, servicios web basados en SOAP y servicios OData desde [!DNL AEM Forms] as a Cloud Service. El servicio proporciona una herramienta dedicada para recuperar, probar, validar y enviar datos a varios tipos de fuentes de datos.
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# Conexión de las fuentes de datos a Cloud Service {#aem-forms-data-integration}

![Integración de datos](do-not-localize/data-integeration.png)

Las infraestructuras empresariales incluyen sistemas back-end o fuentes de datos dispares, como bases de datos, servicios web, servicios REST, servicios OData y soluciones CRM. En conjunto, crean un sistema de información que sirve datos a las aplicaciones empresariales para realizar el trabajo diario. Por otro lado, las aplicaciones capturan datos y los envían de vuelta para actualizar las fuentes de datos.

[!DNL AEM Forms] las aplicaciones como Adaptive Forms y las comunicaciones interactivas requieren la integración con orígenes de datos para recuperar datos de clientes mientras se procesan formularios y se crean comunicaciones interactivas. Hay casos de uso en los que se recuperan datos de fuentes de datos basadas en entradas del usuario en Adaptive Forms. Además, los datos del formulario adaptable enviados se pueden volver a escribir para actualizar las fuentes de datos correspondientes.

Si bien un sistema modular y distribuido tiene sus propias ventajas, el desafío reside en integrar y crear asociaciones de datos entre fuentes de datos. La integración de datos es la clave de una infraestructura empresarial funcional y eficiente con fuentes de datos dispares conectadas a aplicaciones para el intercambio de datos del negocio.

## Información general sobre la integración de datos {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] La integración de datos permite configurar y conectar fuentes de datos dispares con [!DNL AEM Forms]. Proporciona una interfaz de usuario intuitiva para crear un esquema de representación de datos unificado de entidades y servicios empresariales a través de fuentes de datos conectadas. La representación unificada se conoce como modelo de datos de formulario, una extensión del esquema JSON. Las entidades de un Modelo de datos de formulario se denominan objetos del modelo de datos. Un modelo de datos de formulario le permite:

* Acceda a objetos, propiedades y servicios del modelo de datos desde fuentes de datos conectadas.
* Creación de objetos y propiedades personalizadas del modelo de datos
* Cree asociaciones entre objetos de modelo de datos dentro de y entre orígenes de datos.
* Invoque los servicios de objeto del modelo de datos para consultar o escribir datos desde y hacia orígenes de datos.

Una vez creado un modelo de datos de formulario, puede utilizarlo en varios flujos de trabajo de formularios adaptables y de comunicaciones interactivas, como:

* Creación de Forms adaptable y comunicaciones interactivas basadas en el modelo de datos de formulario
* Rellene previamente Forms adaptable y comunicaciones interactivas desde fuentes de datos configuradas
* Invocar servicios u operaciones de fuentes de datos mediante reglas de formulario adaptable
* Escribir datos de formulario adaptable enviados en fuentes de datos

## Introducción a la integración de datos {#get-started-with-data-integration}

El primer paso para implementar la integración de datos es identificar y configurar las fuentes de datos que almacenan información que desea aprovechar en los casos de uso de comunicaciones interactivas y Forms adaptable. A continuación, se crea un Modelo de datos de formulario que utiliza objetos, propiedades y servicios del modelo de datos de uno o varios orígenes de datos. Puede crear Forms adaptable y comunicaciones interactivas basadas en un Modelo de datos de formulario en el que los campos o marcadores de posición de formulario adaptable de las comunicaciones interactivas están enlazados a las propiedades de origen de datos correspondientes.

[!DNL AEM Forms] también permite crear un Modelo de datos de formulario independiente de los orígenes de datos y asociar o enlazar objetos y propiedades del modelo de datos en el Modelo de datos de formulario con el origen de datos más adelante. Elimina las dependencias de los orígenes de datos mientras trabaja en un modelo de datos de formulario.

Revise lo siguiente para comenzar, comprender e implementar la integración de datos.

* [Configuración de fuentes de datos](configure-data-sources.md)
* [Crear modelo de datos de formulario](create-form-data-models.md)
* [Trabajo con el modelo de datos de formulario](work-with-form-data-model.md)
* [Uso del modelo de datos de formulario](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] no admite la base de datos relacional.
