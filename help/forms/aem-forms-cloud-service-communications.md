---
title: AEM Forms as a Cloud Service - Comunicaciones
description: Combine datos automáticamente con plantillas XDP y PDF o genere salidas en formato PCL, ZPL y PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 07b9118b8cfc27bc9e2bfa134fbb57c7ae2728ad
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 99%

---


# Usar el procesamiento sincrónico {#sync-processing-introduction}

Las comunicaciones le permiten crear, montar y entregar comunicaciones personalizadas y orientadas a la marca, como correspondencia comercial, documentos, declaraciones, cartas de procesamiento de reclamaciones, avisos de beneficios, facturas mensuales y kits de bienvenida. Puede utilizar las API de Comunicaciones para combinar una plantilla (XFA o PDF) con datos de clientes para generar documentos en los formatos PDF, PS, PCL, DPL, IPL y ZPL.

Imagine un escenario en el que tiene una o más plantillas y varios registros de datos XML en cada plantilla. Puede utilizar las API de Comunicaciones para generar un documento de impresión para cada registro. <!-- You can also combine the records into a single document. --> El resultado es un documento PDF no interactivo. Un documento PDF no interactivo no permite a los usuarios introducir datos en los campos.


Las comunicaciones ofrecen API para la generación de documentos bajo demanda y planificados. Puede utilizar API sincrónicas para la generación bajo demanda y API por lotes (API asincrónicas) para la generación planificada de documentos:

* Las API sincrónicas son adecuadas para casos de uso de generación de documentos bajo demanda, con baja latencia y de registro único. Estas API son más adecuadas para casos de uso basados en las acciones del usuario. Por ejemplo, generar un documento después de que un usuario rellene un formulario.

* Las API por lotes (API asíncronas) son adecuadas para casos de uso planificados de alto rendimiento y de generación de múltiples documentos. Estas API generan documentos por lotes. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito y declaraciones de beneficios generados cada mes.

## Usar operaciones sincrónicas {#batch-operations}

Una operación sincrónica es un proceso de generación de documentos de forma lineal. Hay API independientes disponibles para las siguientes tareas:

* Generar un documento PDF a partir de una plantilla y combina los datos con ella;
* Generar un documento PostScript (PS), Printer Command Language (PCL) o Zebra Printing Language (ZPL) a partir de un archivo XDP o un documento PDF.
* Montar los documentos PDF
* Desmontar los documentos PDF
* Convertir un documento en un documento compatible con el estándar PDF/A
* Validar un documento compatible con el estándar PDF/A.


### Autenticar una llamada de API

Las operaciones sincrónicas admiten dos tipos de autenticación:

* **Autenticación básica**: la autenticación básica es un esquema de autenticación simple integrado en el protocolo HTTP. El cliente envía peticiones HTTP con el encabezado Autorización que contiene la palabra “Basic” seguida de un espacio y un nombre de usuario:contraseña de cadena codificados en Base64. Por ejemplo, para autorizar como administrador/administrador, el cliente envía Basic [nombre de usuario de cadena codificado en Base64]: [contraseña de cadena codificada en Base64].

* **Autenticación basada en tokens:** la autenticación basada en tokens utiliza un token de acceso (token de autenticación del portador) para realizar solicitudes a Experience Manager as a Cloud Service. AEM Forms as a Cloud Service proporciona API para recuperar de forma segura el token de acceso. Para recuperar y utilizar el token para autenticar una solicitud:

   1. [Recupere las credenciales de Experience Manager as a Cloud Service desde la consola de desarrollador](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es).
   1. [Instale las credenciales de Experience Manager as a Cloud Service en su entorno](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Servidor de aplicaciones, servidor web u otros servidores no AEM) configurados para enviar solicitudes (realizar llamadas) al servicio en la nube.
   1. [Genere un token JWT e intercámbielo con las API de IMS de Adobe por un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Ejecute la API de Experience Manager con el token de acceso como token de autenticación del portador.
   1. [Establezca los permisos adecuados para el usuario de la cuenta técnica en el entorno de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es#configuraci%C3%B3n-del-acceso-en-aem).

   >[!NOTE]
   >
   >Adobe recomienda utilizar la autenticación basada en token en un entorno de producción.


### (Solo para las API de generación de documentos) Configuración de recursos y permisos

Para utilizar API sincrónicas, se requiere lo siguiente:

* Plantillas PDF o XDP
* [Datos que se deben combinar con las plantillas](#form-data)
* Usuarios con privilegios de administrador en Experience Manager
* Cargue plantillas y otros recursos a su instancia de Experience Manager Forms Cloud Service

### (Solo para las API de generación de documentos) Cargar plantillas y otros recursos en la instancia de Experience Manager

Una organización suele tener varias plantillas. Por ejemplo, una plantilla para los extractos de tarjetas de crédito, las declaraciones de beneficios y las solicitudes de reclamación. Cargue todas estas plantillas XDP y PDF en su instancia de Experience Manager. Para cargar una plantilla:

1. Abra su instancia de Experience Manager.
1. Vaya a Formularios > Formularios y documentos
1. Haga clic en Crear > Carpeta y cree una carpeta. Abra la carpeta.
1. Haga clic en Crear > Cargar archivo y cargue las plantillas.


### Invocar una API

La [documentación de referencia de la API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) ofrece información detallada sobre todos los parámetros, métodos de autenticación y diversos servicios que ofrecen las API. La documentación de referencia de la API también proporciona un archivo de definición de API en formato .yaml. Puede descargar el archivo .yaml y cargarlo en Postman para comprobar la funcionalidad de las API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Solo los miembros del grupo de usuarios de Forms pueden acceder a las API de Comunicaciones.
