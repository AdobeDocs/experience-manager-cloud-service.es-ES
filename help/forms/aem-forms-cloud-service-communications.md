---
title: AEM Forms as a Cloud Service - Comunicaciones
description: Combine datos automáticamente con plantillas XDP y PDF o genere resultados en los formatos PCL, ZPL y PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: c38a34519822449ff2577a9474b1294d5d45d3ae
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---


# Usar las API de comunicaciones as a Cloud Service de AEM Forms: procesamiento sincrónico {#frequently-asked-questions}

**La función Comunicaciones está en versión beta.**

Communications allows you to create, assemble, and deliver brand-oriented and personalized communications such as business correspondences, documents, statements, claim processing letters, benefit notices, claim processing letters, monthly bills, and welcome kits. Puede utilizar las API de comunicaciones para combinar una plantilla (XFA o PDF) con datos de clientes para generar documentos en los formatos PDF, PS, PCL, DPL, IPL y ZPL.

Imagine un escenario en el que tiene una o más plantillas y varios registros de datos XML para cada plantilla. You can use Communications APIs to generate a print document for each record. <!-- You can also combine the records into a single document. --> El resultado es un documento PDF no interactivo. Un documento PDF no interactivo no permite a los usuarios introducir datos en sus campos.


Las comunicaciones proporcionan API para la generación de documentos bajo demanda y programados. Puede utilizar API sincrónicas para API bajo demanda y por lotes (API asincrónicas) para la generación programada de documentos:

* Las API sincrónicas son adecuadas para casos de uso de generación de documentos bajo demanda, baja latencia y de registro único. These APIs are more suitable for user-action based use cases. Por ejemplo, la generación de un documento después de que un usuario rellene un formulario.

* Las API por lotes (API asíncronas) son adecuadas para casos de uso programados de alto rendimiento y de generación de documentos. Estas API generan documentos por lotes. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito y extractos de beneficios generados cada mes.

## Usar operaciones sincrónicas {#batch-operations}

Una operación sincrónica es un proceso de generación de documentos de forma lineal. Admite dos tipos de autenticación:

* **Autenticación básica**: La autenticación básica es un esquema de autenticación simple integrado en el protocolo HTTP. El cliente envía solicitudes HTTP con el encabezado Autorización que contiene la palabra Básico seguida de un espacio y una cadena codificada base64 username:password. Por ejemplo, para autorizar como administrador/administrador, el cliente envía Basic [nombre de usuario de la cadena codificada base64]: [contraseña de cadena codificada base64].

* **Autenticación basada en tokens:** La autenticación basada en tokens utiliza un token de acceso (token de autenticación del portador) para realizar solicitudes AEM as a Cloud Service. AEM Forms as a Cloud Service proporciona API para recuperar de forma segura el token de acceso. Para recuperar y utilizar el token para autenticar una solicitud:

   1. [Recuperar AEM credenciales as a Cloud Service desde Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Install AEM as a Cloud Service credentials on your environment](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Application Server, Web Server, or other non-AEM servers) configured to send requests to (make calls) the cloud service.
   1. [Genere un token JWT y lo intercambie con las API IMS de Adobe por un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Ejecute la API de AEM con el token de acceso como token de autenticación del portador.
   1. [Establezca los permisos adecuados para el usuario de cuenta técnica en el entorno de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe recomienda utilizar la autenticación basada en token en un entorno de producción.

### Requisitos previos {#pre-requisites}

Para utilizar API sincrónicas, se requiere lo siguiente:

* PDF or XDP templates
* [Data to be merged with templates](#form-data)
* Usuarios con privilegios de administrador de Experience Manager
* Upload templates and other assets to your Experience Manager Forms Cloud Service instance

#### Cargar plantillas y otros recursos a la instancia de Experience Manager

Una organización suele tener varias plantillas. Por ejemplo, una plantilla para los extractos de tarjetas de crédito, los estados de beneficios y las solicitudes de reivindicación. Cargue todas estas plantillas XDP y PDF en la instancia de Experience Manager. Para cargar una plantilla:

1. Abra la instancia de Experience Manager.
1. Vaya a Forms > Forms y documentos
1. Haga clic en Crear > Carpeta y cree una carpeta. Abra la carpeta.
1. Haga clic en Crear > Cargar archivo y cargue las plantillas.

### Usar la API sincrónica para generar documentos

Hay API independientes disponibles para:

* Genera un documento PDF a partir de una plantilla y combina los datos con ella.
* Generate a PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) document from an XDP file or PDF document.

The [API reference documentation](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/Communications-Services) provides detailed information about all the parameters, authentication methods, and various services provided by APIs. La documentación de referencia de la API también está disponible en formato .yaml . Puede descargar el .yaml para [API sincrónicas](assets/sync.yaml) y cárguelo en postman para comprobar la funcionalidad de las API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Solo los miembros del grupo de usuarios de formularios pueden acceder a las API de comunicaciones.

