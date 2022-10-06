---
title: Conexión de una base de datos a  [!DNL AEM Forms]  as a Cloud Service
seo-title: AEM Forms Data Integration
description: Puede recuperar y guardar datos en servicios web RESTful, servicios web basados en SOAP y servicios OData desde  [!DNL AEM Forms] as a Cloud Service. El servicio proporciona una herramienta dedicada para recuperar, probar, validar y enviar datos a varios tipos de fuentes de datos.
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 100%

---

# Conexión de las fuentes de datos a Cloud Service {#aem-forms-data-integration}

![Integración de datos](do-not-localize/data-integeration.png)

Las infraestructuras empresariales incluyen diferentes sistemas back-end o fuentes de datos, como bases de datos, servicios web, servicios REST, servicios OData y soluciones CRM. En conjunto, crean un sistema de información que sirve datos a las aplicaciones empresariales para realizar el trabajo diario. Por otro lado, las aplicaciones capturan datos y los envían de vuelta para actualizar las fuentes de datos.

Las aplicaciones de [!DNL AEM Forms], como los formularios adaptables y las comunicaciones interactivas, requieren la integración con fuentes de datos para recuperar los datos de los clientes mientras representan los formularios y crean las comunicaciones interactivas. Hay casos de uso en los que se recuperan datos de fuentes de datos basadas en entradas de usuarios de formularios adaptables. Además, los datos de los formularios adaptables enviados se pueden escribir de forma diferida para actualizar las fuentes de datos correspondientes.

Si bien un sistema modular y distribuido tiene sus propias ventajas, el desafío consiste en integrar y crear asociaciones de datos entre fuentes de datos. La integración de datos es la clave de una infraestructura empresarial funcional y eficiente con diferentes fuentes de datos conectadas a aplicaciones para intercambiar datos del negocio.

## Información general sobre la integración de datos {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

La integración de datos de [!DNL AEM Forms] permite configurar y conectar diferentes fuentes de datos con [!DNL AEM Forms]. Proporciona una interfaz de usuario intuitiva para crear un esquema de representación de datos unificado de entidades y servicios empresariales a través de fuentes de datos conectadas. La representación unificada se conoce como modelo de datos de formulario, una extensión del esquema JSON. Las entidades de un modelo de datos de formulario se denominan objetos de modelo de datos. Un modelo de datos de formulario le permite:

* acceder a los objetos, las propiedades y los servicios de modelo de datos desde las fuentes de datos conectadas;
* crear objetos y propiedades personalizadas para el modelo de datos;
* crear asociaciones entre objetos de modelo de datos dentro de las fuentes de datos y entre ellas;
* invocar los servicios de los objetos de modelo de datos para consultar o escribir datos desde y hacia fuentes de datos.

Una vez haya creado un modelo de datos de formulario, podrá utilizarlo en varios flujos de trabajo de formularios adaptables y comunicaciones interactivas, como:

* crear formularios adaptables y comunicaciones interactivas basadas en el modelo de datos de formulario;
* prerrellenar formularios adaptables y comunicaciones interactivas desde las fuentes de datos configuradas;
* invocar servicios u operaciones de fuentes de datos mediante las reglas de los formularios adaptables;
* escribir los datos de los formularios adaptables enviados en fuentes de datos.

## Introducción a la integración de datos {#get-started-with-data-integration}

El primer paso para implementar la integración de datos es identificar y configurar las fuentes de datos que almacenan la información que desea aprovechar en los casos de uso de las comunicaciones interactivas y los formularios adaptable. A continuación, se crea un modelo de datos de formulario que utiliza los objetos, las propiedades y los servicios de modelo de datos de una o varias fuentes de datos. Puede crear formularios adaptables y comunicaciones interactivas basadas en un modelo de datos de formulario en el que los campos de los formularios adaptables o los marcadores de posición de las comunicaciones interactivas están enlazados a las propiedades de sus respectivas fuentes de datos.

[!DNL AEM Forms] también permite crear un modelo de datos de formulario independiente de las fuentes de datos y asociar o enlazar objetos y propiedades de modelo de datos en el modelo de datos de formulario con la fuente de datos más adelante. Esto elimina la dependencia de las fuentes de datos mientras trabaja en un modelo de datos de formulario.

Revise la siguiente información para iniciar, entender e implementar la integración de datos.

* [Configurar fuentes de datos](configure-data-sources.md)
* [Crear modelo de datos de formulario](create-form-data-models.md)
* [Trabajar con el modelo de datos de formulario](work-with-form-data-model.md)
* [Uso del modelo de datos de formulario](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] no es compatible con bases de datos relacionales.
