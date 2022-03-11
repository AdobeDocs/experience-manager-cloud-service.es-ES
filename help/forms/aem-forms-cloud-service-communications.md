---
title: AEM Forms as a Cloud Service - Comunicaciones
description: Combine datos automáticamente con plantillas XDP y PDF o genere resultados en los formatos PCL, ZPL y PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 6b546f551957212614e8b7a383c38797cc21fba1
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# Uso del procesamiento sincrónico {#sync-processing-introduction}

Communications allows you to create, assemble, and deliver brand-oriented and personalized communications such as business correspondences, documents, statements, claim processing letters, benefit notices, claim processing letters, monthly bills, and welcome kits. You can use Communications APIs to combine a template (XFA or PDF) with customer data to generate documents in PDF, PS, PCL, DPL, IPL, and ZPL formats.

Imagine un escenario en el que tiene una o más plantillas y varios registros de datos XML para cada plantilla. Puede utilizar las API de comunicaciones para generar un documento de impresión para cada registro. <!-- You can also combine the records into a single document. --> The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.


Las comunicaciones proporcionan API para la generación de documentos bajo demanda y programados. You can use synchronous APIs for on-demand and batch APIs (asynchronous APIs) for scheduled document generation:

* Las API sincrónicas son adecuadas para casos de uso de generación de documentos bajo demanda, baja latencia y de registro único. Estas API son más adecuadas para casos de uso basados en acciones del usuario. Por ejemplo, la generación de un documento después de que un usuario rellene un formulario.

* Las API por lotes (API asíncronas) son adecuadas para casos de uso programados de alto rendimiento y de generación de documentos. These APIs generate documents in batches. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito y extractos de beneficios generados cada mes.

## Usar operaciones sincrónicas {#batch-operations}

A synchronous operation is a process of generating documents in a linear manner. Admite dos tipos de autenticación:

* **Autenticación básica**: La autenticación básica es un esquema de autenticación simple integrado en el protocolo HTTP. The client sends HTTP requests with the Authorization header that contains the word Basic followed by a space and a base64-encoded string username:password. Por ejemplo, para autorizar como administrador/administrador, el cliente envía Basic [nombre de usuario de la cadena codificada base64]: [contraseña de cadena codificada base64].

* **Autenticación basada en tokens:** La autenticación basada en tokens utiliza un token de acceso (token de autenticación del portador) para que las solicitudes al Experience Manager resulten as a Cloud Service. AEM Forms as a Cloud Service proporciona API para recuperar de forma segura el token de acceso. Para recuperar y utilizar el token para autenticar una solicitud:

   1. [Retrieve Experience Manager as a Cloud Service credentials from the Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Instalar las credenciales as a Cloud Service del Experience Manager en su entorno](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Servidor de aplicaciones, Servidor web u otros servidores no AEM) configurados para enviar solicitudes al servicio en la nube (realizar llamadas).
   1. [Genere un token JWT y lo intercambie con las API IMS de Adobe por un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Run the Experience Manager API with the access token as a Bearer Authentication token.
   1. [Establezca los permisos adecuados para el usuario de cuenta técnica en el entorno del Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe recomienda utilizar la autenticación basada en token en un entorno de producción.

### Requisitos previos {#pre-requisites}

To use Synchronous APIs, the following is required:

* PDF or XDP templates
* [Datos que se van a combinar con plantillas](#form-data)
* Usuarios con privilegios de administrador de Experience Manager
* Cargar plantillas y otros recursos a la instancia de Cloud Service de Experience Manager Forms

#### Cargar plantillas y otros recursos a la instancia de Experience Manager

Una organización suele tener varias plantillas. For example, one template each for credit card statements, benefits statements, and claim applications. Cargue todas estas plantillas XDP y PDF en la instancia de Experience Manager. To upload a template:

1. Abra la instancia de Experience Manager.
1. Vaya a Forms > Forms y documentos
1. Click Create > Folder and create a folder. Abra la carpeta.
1. Haga clic en Crear > Cargar archivo y cargue las plantillas.

### Usar API sincrónica para generar documentos

Separate APIs are available to:

* Generates a PDF Document from a template and merge data to it.
* Genere un documento PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) desde un archivo XDP o documento PDF.

La variable [Documentación de referencia de API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/Communications-Services) proporciona información detallada sobre todos los parámetros, métodos de autenticación y diversos servicios proporcionados por las API. La documentación de referencia de la API también está disponible en formato .yaml . Puede descargar el .yaml para [API sincrónicas](assets/sync.yaml) y cárguelo en postman para comprobar la funcionalidad de las API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Solo los miembros del grupo de usuarios de formularios pueden acceder a las API de comunicaciones.

