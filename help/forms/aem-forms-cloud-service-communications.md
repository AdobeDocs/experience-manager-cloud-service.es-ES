---
title: AEM Forms as a Cloud Service - Comunicaciones
description: Combine datos automáticamente con plantillas XDP y PDF o genere resultados en los formatos PCL, ZPL y PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 07b9118b8cfc27bc9e2bfa134fbb57c7ae2728ad
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 1%

---


# Uso del procesamiento sincrónico {#sync-processing-introduction}

Las comunicaciones le permiten crear, ensamblar y entregar comunicaciones personalizadas y orientadas a la marca, como correspondencia comercial, documentos, declaraciones, cartas de procesamiento de reclamaciones, avisos de beneficios, cartas de procesamiento de reclamaciones, facturas mensuales y kits de bienvenida. Puede utilizar las API de comunicaciones para combinar una plantilla (XFA o PDF) con datos de clientes para generar documentos en los formatos PDF, PS, PCL, DPL, IPL y ZPL.

Imagine un escenario en el que tiene una o más plantillas y varios registros de datos XML para cada plantilla. Puede utilizar las API de comunicaciones para generar un documento de impresión para cada registro. <!-- You can also combine the records into a single document. --> El resultado es un documento PDF no interactivo. Un documento PDF no interactivo no permite a los usuarios introducir datos en sus campos.


Las comunicaciones proporcionan API para la generación de documentos bajo demanda y programados. Puede utilizar API sincrónicas para API bajo demanda y por lotes (API asincrónicas) para la generación programada de documentos:

* Las API sincrónicas son adecuadas para casos de uso de generación de documentos bajo demanda, baja latencia y de registro único. Estas API son más adecuadas para casos de uso basados en acciones del usuario. Por ejemplo, la generación de un documento después de que un usuario rellene un formulario.

* Las API por lotes (API asíncronas) son adecuadas para casos de uso programados de alto rendimiento y de generación de documentos. Estas API generan documentos por lotes. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito y extractos de beneficios generados cada mes.

## Usar operaciones sincrónicas {#batch-operations}

Una operación sincrónica es un proceso de generación de documentos de forma lineal. Hay API independientes disponibles para:

* Genera un documento PDF a partir de una plantilla y combina los datos con ella.
* Genere un documento PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) desde un archivo XDP o documento PDF.
* Montar los documentos PDF
* Desmontar los documentos PDF
* Convertir un documento en documento compatible con el PDF/A
* Validación de un documento compatible con el PDF/A


### Autenticar una llamada de API

Las operaciones sincrónicas admiten dos tipos de autenticación:

* **Autenticación básica**: La autenticación básica es un esquema de autenticación simple integrado en el protocolo HTTP. El cliente envía solicitudes HTTP con el encabezado Autorización que contiene la palabra Básico seguida de un espacio y una cadena codificada base64 username:password. Por ejemplo, para autorizar como administrador/administrador, el cliente envía Basic [nombre de usuario de la cadena codificada base64]: [contraseña de cadena codificada base64].

* **Autenticación basada en tokens:** La autenticación basada en tokens utiliza un token de acceso (token de autenticación del portador) para que las solicitudes al Experience Manager resulten as a Cloud Service. AEM Forms as a Cloud Service proporciona API para recuperar de forma segura el token de acceso. Para recuperar y utilizar el token para autenticar una solicitud:

   1. [Recuperar credenciales as a Cloud Service del Experience Manager desde Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Instalar las credenciales as a Cloud Service del Experience Manager en su entorno](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Servidor de aplicaciones, Servidor web u otros servidores no AEM) configurados para enviar solicitudes al servicio en la nube (realizar llamadas).
   1. [Genere un token JWT y lo intercambie con las API IMS de Adobe por un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Ejecute la API del Experience Manager con el token de acceso como token de autenticación del portador.
   1. [Establezca los permisos adecuados para el usuario de cuenta técnica en el entorno del Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe recomienda utilizar la autenticación basada en token en un entorno de producción.


### (Solo para las API de generación de documentos) Configuración de recursos y permisos

Para utilizar API sincrónicas, se requiere lo siguiente:

* Plantillas PDF o XDP
* [Datos que se van a combinar con plantillas](#form-data)
* Usuarios con privilegios de administrador de Experience Manager
* Cargar plantillas y otros recursos a la instancia de Cloud Service de Experience Manager Forms

### (Solo para las API de generación de documentos) Cargar plantillas y otros recursos a la instancia de Experience Manager

Una organización suele tener varias plantillas. Por ejemplo, una plantilla para los extractos de tarjetas de crédito, los estados de beneficios y las solicitudes de reivindicación. Cargue todas estas plantillas XDP y PDF en la instancia de Experience Manager. Para cargar una plantilla:

1. Abra la instancia de Experience Manager.
1. Vaya a Forms > Forms y documentos
1. Haga clic en Crear > Carpeta y cree una carpeta. Abra la carpeta.
1. Haga clic en Crear > Cargar archivo y cargue las plantillas.


### Invocar una API

La variable [Documentación de referencia de API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) proporciona información detallada sobre todos los parámetros, métodos de autenticación y diversos servicios proporcionados por las API. La documentación de referencia de la API también proporciona un archivo de definición de API en formato .yaml. Puede descargar el archivo .yaml y cargarlo en postman para comprobar la funcionalidad de las API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Solo los miembros del grupo de usuarios de formularios pueden acceder a las API de comunicaciones.
