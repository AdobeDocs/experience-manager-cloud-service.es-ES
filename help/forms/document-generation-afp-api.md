---
title: ¿Cómo se utiliza la API de sincronización de salida AFP?
description: Aprenda a utilizar la API de sincronización de salida AFP para recuperar y sincronizar representaciones de salida.
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, User
exl-id: 5602fc63-ef74-44eb-b3be-61b8f8a2795a
source-git-commit: 33dcc771c8c2deb2e5fcb582de001ce5cfaa9ce4
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 14%

---

# Generar salida AFP mediante la API de AEM Forms

<span class="preview"> Esta es una función previa al lanzamiento y se puede acceder en el [canal previo al lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features). </span>

Presentación de funciones avanzadas (AFP) es un formato de documento de alto rendimiento diseñado principalmente para fines de impresión.\
Esta guía describe todos los pasos y configuraciones necesarios para generar la salida AFP mediante AEM Forms.

<!--
## Prerequisites

To support AFP output generation, the following OSGi bundles must be present and in an **active** state:

* **AFP Core Bundle** – Available in the AFP repository
* **Forms Output Core** – Found in the Forms Output comments package
* **Bedrock Connector** – Provided by the Forms Output API
* **Cloud Ready Implementation** – Available through the Forms installer

>[!NOTE]
>
> * If any bundle is inactive, resolve dependency issues or reinstall manually.
> * To enable AFP generation, the `FT_FORMS-17887` toggle configurations must be set in AEM configuration manager.-->

## API de generación AFP

Genera un archivo AFP (presentación de funciones avanzadas) mediante una plantilla XDP y datos de entrada.

### Autorización

Puede usar **BasicAuth** (credenciales de administrador) para entornos locales o la autorización de **BearerAuth** para instancias de AEM Cloud.

### Solicitud

**Punto final:**
`POST http://<server>:<port>/adobe/forms/document/generate/afp`

### Encabezados

| Clave | Valor |
| --------------- | ------------------------------------------------------ |
| `Content-Type` | `application/pdf` |
| `Authorization` | `(Bearer Access token)` |

### Cuerpo de solicitud

**Tipo de contenido: multipart/form-data**

| Clave | Tipo | Requerido | Descripción |
| ---------- | ---- | -------- | ------------------------------------------------------------------------- |
| `template` | Archivo/Texto | Sí | Archivo XDP utilizado como plantilla para la generación de AFP (por ejemplo, `demo.xdp`) |
| `data` | Archivo/Texto | No | Archivo de datos (XML o JSON) que combinar con la plantilla (por ejemplo, `data.xml`) |
| `options` | Texto | No | Cadena JSON con opciones para controlar la salida de AFP (por ejemplo, resolución, configuración regional) |

**Ejemplo `options` JSON (campo de texto):**

```json
{
  "pdfVersion": "1.7",
  "resolution": 300,
  "locale": "en-US",
  "embedFonts": true,
  "contentRoot": "/usr/tmp"
}
```

### Respuestas

| Código | Descripción |
| ----- | ------------------------------------------------------------------------- |
| `200` | Operación correcta. Devuelve el flujo de documentos AFP. |
| `400` | Solicitud incorrecta. La carga de la solicitud tiene un formato incorrecto o faltan campos obligatorios. |
| `500` | Error interno del servidor. Inténtelo de nuevo más tarde. |

### Comando Curl

```
curl --location 'http://<server>:<port>/adobe/forms/document/generate/afp' \
--header 'Authorization: Bearertoken <base64-encoded-credentials>' \
--form 'template=@"<path-to-template>.xdp"' \
--form 'data=@"<path-to-data-file>.xml"' \
--form 'options=<JSON-options-string>'
```

### Prueba de la API

Puede descargar el archivo .yaml y cargarlo en Postman para comprobar la funcionalidad de las API.

![Imagen de Postman AFP](/help/forms/assets/afp-postman.png)

Puede guardar la respuesta y abrir el archivo guardado en el lector AFP para verlo.

![Buscar documento CI](/help/forms/interactive-communication/assets/introimg.png)
