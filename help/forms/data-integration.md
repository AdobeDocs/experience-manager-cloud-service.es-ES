---
title: Conexión de una base de datos a  [!DNL AEM Forms]  as a Cloud Service
description: Recupere y guarde datos en servicios web RESTful, servicios web basados en SOAP y servicios OData desde un formulario adaptable o un flujo de trabajo de AEM.
feature: Adaptive Forms, Form Data Model
role: Admin, User
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 81%

---

# Conexión de AEM Forms a una base de datos {#aem-forms-data-integration}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/data-integration.html?lang=es) |
| AEM as a Cloud Service | Este artículo |



![Integración de datos](do-not-localize/data-integeration.png)

Las infraestructuras empresariales incluyen diferentes sistemas back-end o fuentes de datos, como bases de datos, servicios web, servicios REST, servicios OData y soluciones CRM. En conjunto, crean un sistema de información que sirve datos a las aplicaciones empresariales para realizar el trabajo diario. Por otro lado, las aplicaciones capturan datos y los envían de vuelta para actualizar las fuentes de datos.

Al conectar un formulario adaptable a una base de datos, se requiere la integración con fuentes de datos para recuperar los datos de los clientes mientras se procesan los formularios. Hay casos de uso en los que se recuperan datos de fuentes de datos basadas en entradas de usuarios de formularios adaptables. Además, cuando se envía un formulario adaptable a una base de datos, los datos del formulario adaptable enviados se pueden escribir de forma diferida para actualizar las fuentes de datos correspondientes.

Si bien un sistema modular y distribuido tiene sus propias ventajas, el desafío consiste en integrar y crear asociaciones de datos entre fuentes de datos. La integración de datos es la clave de una infraestructura empresarial funcional y eficiente con diferentes fuentes de datos conectadas a aplicaciones para intercambiar datos del negocio.

## Información general sobre la integración de datos {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

La integración de datos de [!DNL AEM Forms] permite configurar y conectar diferentes fuentes de datos con [!DNL AEM Forms]. Proporciona una interfaz de usuario intuitiva para crear un esquema de representación de datos unificado de entidades y servicios empresariales a través de fuentes de datos conectadas. La representación unificada se conoce como modelo de datos de formulario (FDM), una extensión del esquema JSON. Las entidades de un modelo de datos de formulario (FDM) se denominan objetos de modelo de datos. Un modelo de datos de formulario (FDM) le permite hacer lo siguiente:

* acceder a los servicios, las propiedades y los objetos de modelo de datos desde las fuentes de datos conectadas;
* crear propiedades y objetos de modelo de datos personalizados;
* crear asociaciones entre objetos de modelo de datos dentro de las fuentes de datos y entre ellas;
* invocar los servicios de los objetos de modelo de datos para consultar o escribir datos desde y hacia fuentes de datos.

Una vez creado un modelo de datos de formulario (FDM), puede utilizarlo para lo siguiente:

* Crear formularios adaptables basados en un modelo de datos de formulario (FDM)
* Rellenar previamente los formularios adaptables desde fuentes de datos configuradas
* invocar servicios u operaciones de fuentes de datos mediante las reglas de los formularios adaptables;
* escribir los datos de los formularios adaptables enviados en fuentes de datos.

## Aplicabilidad y casos de uso

### Seguro

## ¿Se puede utilizar AEM Forms para aplicaciones de pólizas de seguro?

Sí. AEM Forms se puede utilizar para crear formularios de solicitud de seguros digitales que recopilen información del solicitante, validen entradas e integren sistemas de suscripción back-end.

## ¿AEM Forms admite flujos de trabajo de suscripción?

Sí, con flujos de trabajo e integraciones. AEM Forms admite procesos impulsados por flujos de trabajo e integraciones back-end que permiten que los datos de la aplicación fluyan a los sistemas de suscripción y toma de decisiones.

## ¿Se puede integrar AEM Forms con los sistemas principales de seguros?

Sí. AEM Forms admite la integración mediante las API de REST y SOAP, lo que le permite conectarse con sistemas de administración de políticas, sistemas de administración de reclamaciones y CRM.

## ¿AEM Forms puede escribir datos de formulario en sistemas de seguros?

Sí. AEM Forms admite la reescritura de datos en sistemas back-end como parte del envío de formularios y la ejecución del flujo de trabajo.

## Introducción a la integración de datos {#get-started-with-data-integration}

El primer paso para implementar la integración de datos para enviar el formulario adaptable a una base de datos es identificar y configurar las fuentes de datos que almacenan la información que desea utilizar en Formularios adaptables. A continuación, se crea un modelo de datos de formulario que utiliza los servicios, las propiedades y los objetos de modelo de datos de una o varias fuentes de datos. Puede crear formularios adaptables basados en un modelo de datos de formulario en el que los campos de los formularios adaptables están enlazados a las propiedades de sus respectivas fuentes de datos.

[!DNL AEM Forms] también permite crear un modelo de datos de formulario (FDM) independiente de las fuentes de datos y asociar o enlazar propiedades y objetos de modelo de datos en el modelo de datos de formulario (FDM) con la fuente de datos más adelante. Esto elimina la dependencia de las fuentes de datos mientras trabaja en un modelo de datos de formulario (FDM).

Revise la siguiente información para iniciar, entender e implementar la integración de datos:

* [Configuración de las fuentes de datos](configure-data-sources.md)
* [Crear modelo de datos de formulario (FDM)](create-form-data-models.md)
* [Trabajar con el modelo de datos de formulario (FDM)](work-with-form-data-model.md)
* [Uso del modelo de datos de formulario (FDM)](using-form-data-model.md)

<!--

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] does not support relational database.

-->