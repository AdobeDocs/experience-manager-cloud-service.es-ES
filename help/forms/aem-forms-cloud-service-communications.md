---
title: AEM Forms as a Cloud Service - Comunicaciones
description: Combine datos automáticamente con plantillas XDP y PDF o genere salidas en formato PCL, ZPL y PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 46%

---


# Usar el procesamiento sincrónico {#sync-processing-introduction}

Forms as a Cloud Service: las API de comunicaciones le permiten crear, ensamblar y entregar comunicaciones personalizadas y orientadas a la marca, como correspondencia comercial, documentos, declaraciones, cartas de procesamiento de reclamaciones, avisos de beneficios, cartas de procesamiento de reclamaciones, facturas mensuales y kits de bienvenida. Puede utilizar las API de Comunicaciones para combinar una plantilla (XFA o PDF) con datos de clientes para generar documentos en los formatos PDF, PS, PCL, DPL, IPL y ZPL.

Imagine un escenario en el que tiene una o más plantillas y varios registros de datos XML en cada plantilla. Puede utilizar las API de Comunicaciones para generar un documento de impresión para cada registro. <!-- You can also combine the records into a single document. --> El resultado es un documento PDF no interactivo. Un documento PDF no interactivo no permite a los usuarios introducir datos en los campos.

Forms as a Cloud Service: Comunicaciones proporciona API bajo demanda y por lotes (API asincrónicas) para la generación programada de documentos:

* Las API sincrónicas son adecuadas para casos de uso de generación de documentos bajo demanda, con baja latencia y de registro único. Estas API son más adecuadas para casos de uso basados en las acciones del usuario. Por ejemplo, generar un documento después de que un usuario rellene un formulario.

* Las API por lotes (API asíncronas) son adecuadas para casos de uso planificados de alto rendimiento y de generación de múltiples documentos. Estas API generan documentos por lotes. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito y declaraciones de beneficios generados cada mes.

## Usar operaciones sincrónicas {#batch-operations}

Una operación sincrónica es un proceso de generación de documentos de forma lineal. Estas API están clasificadas como API de un solo inquilino y API de varios inquilinos:

### API de un solo inquilino

* API de generación de documentos
* API de manipulación de documentos

### API de varios inquilinos

* API de utilidad de documento

### Autenticar una API de un solo inquilino

Las operaciones de API de un solo inquilino admiten dos tipos de autenticación:

* **Autenticación básica**: la autenticación básica es un esquema de autenticación simple integrado en el protocolo HTTP. El cliente envía peticiones HTTP con el encabezado Autorización que contiene la palabra “Basic” seguida de un espacio y un nombre de usuario:contraseña de cadena codificados en Base64. Por ejemplo, para autorizar como administrador/administrador, el cliente envía Basic [nombre de usuario de cadena codificado en Base64]: [contraseña de cadena codificada en Base64].

* **Autenticación basada en tokens:** la autenticación basada en tokens utiliza un token de acceso (token de autenticación del portador) para realizar solicitudes a Experience Manager as a Cloud Service. AEM Forms as a Cloud Service proporciona API para recuperar de forma segura el token de acceso. Para recuperar y utilizar el token para autenticar una solicitud:

   1. [Recuperar credenciales as a Cloud Service del Experience Manager desde Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es).
   1. [Instalar credenciales as a Cloud Service del Experience Manager en su entorno](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es). (Servidor de aplicaciones, servidor web u otros servidores no AEM) configurados para enviar solicitudes (realizar llamadas) al servicio en la nube.
   1. [Genere un token JWT e intercámbielo con las API de IMS de Adobe por un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es).
   1. Ejecute la API de Experience Manager con el token de acceso como token de autenticación del portador.
   1. [Establezca los permisos adecuados para el usuario de la cuenta técnica en el entorno de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es#configuraci%C3%B3n-del-acceso-en-aem).

   >[!NOTE]
   >
   >Adobe recomienda utilizar la autenticación basada en token en un entorno de producción.

### Autenticar una API de varios inquilinos

#### Encabezados de autenticación

Cada llamada de API HTTP entrante a la API de Cloud Manager debe contener estos tres encabezados:

* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

Los valores que deben enviarse en la variable `x-api-key` y `x-gw-ims-org-id` los encabezados se proporcionan en la pantalla de detalles Credenciales de la [Consola de Adobe Developer](https://developer.adobe.com/console). El valor de la variable `x-api-key` es el ID de cliente y el valor de la variable `x-gw-ims-org-id` es el ID de organización.

#### Configuración de la consola de Adobe Developer para generar un token de acceso

Para configurar las API de autenticación, cree un proyecto en la consola de Adobe Developer y añada las API de comunicación al proyecto en la consola de Adobe Developer. La integración genera la clave de API, el secreto del cliente y la carga útil (JWT):

1. Póngase en contacto con el administrador de la consola de Adobe Developer. Solicite al administrador que añada como desarrollador.
1. Iniciar sesión en `https://developer.adobe.com/console/`. Utilice su cuenta de desarrollador aprovisionada por el administrador para iniciar sesión en Adobe Developer Console.
1. Seleccione su organización en la esquina superior derecha. Si no conoce su organización, póngase en contacto con su administrador.
1. Toque **[!UICONTROL Crear nuevo proyecto]**. Aparece una pantalla para comenzar con el nuevo proyecto. Toque **[!UICONTROL Añadir API]**. Aparece una pantalla con una lista de todas las API habilitadas para su cuenta.
1. Select **[!UICONTROL AEM Forms: comunicaciones]** y toque **[!UICONTROL Siguiente]**. Aparece una pantalla para configurar la API.
1. Select **[!UICONTROL OPCIÓN 1 Generar un par de claves]** y toque **[!UICONTROL Generar par de teclas]**. Crea y descarga el archivo de configuración. El archivo de configuración descargado contiene todos los ajustes de la aplicación, junto con la única copia de la clave privada. Adobe no registra la clave privada, asegúrese de almacenar de forma segura el archivo descargado. Pulse **[!UICONTROL Siguiente]**.
1. Select **[!UICONTROL Integraciones: Cloud Service]** y toque **[!UICONTROL Guardar la API configurada]**. Toque **[!UICONTROL Cuenta de servicio (JWT)]** para ver la clave de API, el secreto del cliente y otra información necesaria para acceder a las API. Se configura para utilizar el token para acceder a las API.

#### Generar y utilizar mediante programación un token de acceso

Para generar mediante programación un token de acceso, genere un token web de JSON (JWT) y cámbielo por el servicio Identity Management de Adobe (IMS) para obtener un token de acceso.

Utilice las claves siguientes, denominadas reclamaciones, para construir el objeto JSON de JWT:

* `exp`: la caducidad solicitada del token de acceso, expresada como un número de segundos desde el 1 de enero de 1970 GMT. Para la mayoría de los casos de uso, este es un valor relativamente pequeño. Por ejemplo, 5 minutos, durante cinco minutos a partir de ahora, este valor debe ser 1670923791.
* `iss` : el ID de organización del proyecto de la consola de Adobe Developer, con el formato org_ident@AdobeOrg.
* `sub` : el ID de cuenta técnica de la integración de la consola de Adobe Developer, con el formato: id@techacct.adobe.com.
* `aud` : el ID de cliente de la integración de la consola de Adobe Developer precedido de `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - se establece en el valor literal `true`

Este objeto JSON debe codificarse y firmarse base64 con la clave privada para el proyecto. Finalmente, el valor codificado se envía en el cuerpo de una solicitud de POST a `https://ims-na1.adobelogin.com/ims/exchange/jwt` junto con el ID de cliente y el Secreto de cliente para el proyecto.

##### Ejemplo

```JSON
    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache
```

#### Compatibilidad de idiomas con JWT

Aunque es posible realizar todo el proceso de generación e intercambio de JWT en código personalizado, es más común utilizar una biblioteca de nivel superior para hacerlo. Algunas de estas bibliotecas se enumeran en la [Documentación de JWT de Adobe I/O](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

### (Solo para las API de generación de documentos) Configuración de recursos y permisos

Para utilizar API sincrónicas, se requiere lo siguiente:

* Usuarios con privilegios de administrador en Experience Manager
* Cargue plantillas y otros recursos a su instancia de Experience Manager Forms Cloud Service

### (Solo para las API de generación de documentos) Cargar plantillas y otros recursos en la instancia de Experience Manager

Una organización suele tener varias plantillas. Por ejemplo, una plantilla para los extractos de tarjetas de crédito, las declaraciones de beneficios y las solicitudes de reclamación. Cargue todas estas plantillas XDP y PDF en su instancia de Experience Manager. Para cargar una plantilla:

1. Abra su instancia de Experience Manager.
1. Vaya a Formularios > Formularios y documentos
1. Haga clic en Crear > Carpeta y cree una carpeta. Abra la carpeta.
1. Haga clic en Crear > Cargar archivo y cargue las plantillas.

### Invocar una API

La [documentación de referencia de la API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) ofrece información detallada sobre todos los parámetros, métodos de autenticación y diversos servicios que ofrecen las API. La documentación de referencia de la API también proporciona un archivo de definición de la API en formato .yaml. Puede descargar el archivo .yaml y cargarlo en [Postman](https://www.postman.com/) para comprobar la funcionalidad de las API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Solo los miembros del grupo de usuarios de Forms pueden acceder a las API de Comunicaciones.
