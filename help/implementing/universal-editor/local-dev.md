---
title: Ejecución de su propio servicio de editor universal
description: Descubra cómo puede ejecutar su propio servicio de editor universal para el desarrollo local o como parte de su propia infraestructura.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Developer
source-git-commit: 0df573a3d869f2718983b4e661a86c769b4d3f1a
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 93%

---


# Ejecución de su propio servicio de editor universal {#local-ue-service}

Descubra cómo puede ejecutar su propio servicio de editor universal para el desarrollo local o como parte de su propia infraestructura.

>[!NOTE]
>
>Los servicios de editor universal local no son necesarios para los proyectos que utilizan la creación de AEM con Edge Delivery Services.

## Información general {#overview}

El servicio de editor universal es lo que une al editor universal y al sistema backend. Para poder desarrollar localmente para el editor universal, debe ejecutar una copia local del servicio de editor universal. Esto se debe a lo siguiente:

* El servicio de editor universal oficial de Adobe está alojado a nivel global, y su instancia local de AEM tendría que estar expuesta a internet.
* Al desarrollar con un SDK de AEM local, no se puede acceder al servicio de editor universal de Adobe desde Internet.
* Si la instancia de AEM tiene restricciones de IP y el servicio de editor universal de Adobe no está en un rango de IP definido, puede alojarla usted mismo.

## Casos de uso {#use-cases}

Tener su propia copia del servicio de editor universal resulta útil si desea hacer lo siguiente:

* Desarrollar localmente en AEM para utilizarlo con el editor universal.
* Ejecutar su propio servicio de editor universal como parte de su propia infraestructura, con independencia del servicio de editor universal de Adobe.

Se admiten ambos casos de uso. En este documento se explica cómo ejecutar AEM en HTTPS junto con una copia local del servicio de editor universal.

Si desea ejecutar su propio servicio de editor universal como parte de su propia infraestructura, debe seguir los mismos pasos que en el ejemplo de desarrollo local.

## Configuración de AEM para que se ejecute en HTTPS {#aem-https}

Dentro de un marco externo protegido con HTTPS, no se puede cargar un marco HTTP no seguro. El servicio de editor universal se ejecuta en HTTPS y, por lo tanto, AEM o cualquier otra página remota también deben ejecutarse en HTTPS.

Para ello, debe configurar AEM para que se ejecute en HTTPS. Para fines de desarrollo, puede utilizar un certificado autofirmado.

[Consulte este documento](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=es) sobre cómo configurar AEM ejecutado en HTTPS, incluido un certificado autofirmado que puede utilizar.

## Instalación del servicio de editor universal {#install-ue-service}

El servicio de editor universal no es una copia completa del editor universal, sino solo un subconjunto de sus funciones para garantizar que las llamadas de su entorno de AEM local no se enruten a través de Internet, sino desde un punto final definido que usted controle.

Se requiere la [versión 20 de NodeJS](https://nodejs.org/en/download/releases) para ejecutar una copia local del servicio de editor universal.

El servicio de editor universal está disponible a través de la distribución de software. Consulte la [documentación de distribución de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=es) para obtener detalles sobre cómo acceder a ella.

Guarde el archivo `universal-editor-service.cjs` de la distribución de software en el entorno de desarrollo local.

## Creación de un certificado para ejecutar el servicio de editor universal con HTTPS {#ue-https}

El servicio de editor universal también requiere un certificado para ejecutarse en HTTPS en su entorno de desarrollo.

Ejecute el siguiente comando.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

El comando genera un archivo `key.pem` y un archivo `certificate.pem`. Guarde estos archivos en la misma ruta que el archivo `universal-editor-service.cjs`.

## Configuración del servicio de editor universal {#setting-up-service}

Se deben configurar varias variables de entorno en NodeJS para ejecutar el servicio de editor universal localmente.

En la misma ruta de acceso que los archivos de `universal-editor-service.cjs`, `key.pem` y `certificate.pem`, cree un archivo de `.env` con el siguiente contenido.

```text
UES_PORT=8000
UES_PRIVATE_KEY=./key.pem
UES_CERT=./certificate.pem
UES_TLS_REJECT_UNAUTHORIZED=false
UES_CORS_PRIVATE_NETWORK=true
```

Estos son los valores mínimos requeridos para el desarrollo local en nuestro ejemplo.

>[!NOTE]
>
>Si está ejecutando la versión 130+ de Chrome, debe habilitar el envío de encabezados CORS para el [acceso a la red privada](https://wicg.github.io/private-network-access/#private-network-request) mediante la opción `UES_CORS_PRIVATE_NETWORK`.


La siguiente tabla detalla estos y los valores adicionales disponibles.

| Valor | Opcional | Predeterminado | Descripción |
|---|---|---|---|
| `UES_PORT` | Sí | `8080` | Puerto en el que se ejecuta el servidor |
| `UES_PRIVATE_KEY` | Sí | Ninguno | Ruta a la clave privada del servidor HTTPS |
| `UES_CERT` | Sí | Ninguno | Ruta al archivo de certificación para el servidor HTTPS |
| `UES_TLS_REJECT_UNAUTHORIZED` | Sí | `true` | Rechazar conexiones TLS no autorizadas |
| `UES_DISABLE_IMS_VALIDATION` | Sí | `false` | Deshabilitar validación de IMS |
| `UES_ENDPOINT_MAPPING` | Sí | Vacío | Asignación de los extremos para reescrituras internas<br>Ejemplo: `UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>Resultado: el servicio de editor universal se conectará a `http://10.0.0.1:4502`, en lugar de la conexión proporcionada `https://your-public-facing-author-domain.net` |
| `UES_LOG_LEVEL` | Sí | `info` | Nivel de registro del servidor. Los valores posibles son `silly`, `trace`, `debug`, `verbose`, `info`, `log`, `warn`, `error` y `fatal` |
| `UES_SPLUNK_HEC_URL` | Sí | Ninguno | URL de HEC al punto final Splunk |
| `UES_SPLUNK_TOKEN` | Sí | Ninguno | Token Splunk |
| `UES_SPLUNK_INDEX` | Sí | Ninguno | Índice para escribir registros en |
| `UES_SPLUNK_SOURCE` | Sí | `universal-editor-service` | Nombre de la fuente en los registros de Splunk |
| `UES_CORS_PRIVATE_NETWORK` | Sí | `false` | Habilitar el envío de encabezados CORS para permitir la [red privada](https://wicg.github.io/private-network-access/#private-network-request). Necesario para usuarios de Chrome versión 130+ |

>[!NOTE]
>
>Antes de la [versión 2024.08.13](/help/release-notes/universal-editor/current.md) del editor universal, se requerían las siguientes variables en el archivo `.env`. Estos valores serán compatibles hasta el 1 de octubre de 2024 para la compatibilidad con versiones anteriores.
>
>`EXPRESS_PORT=8000`
>`EXPRESS_PRIVATE_KEY=./key.pem`
>`EXPRESS_CERT=./certificate.pem`
>`NODE_TLS_REJECT_UNAUTHORIZED=0`

## Ejecución del servicio de editor universal {#running-ue}

Para iniciar el servicio de editor universal, ejecute el siguiente comando:

```text
$ node ./universal-editor-service.cjs
```

Debe enviar lo siguiente al terminal:

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

Asegúrese de que el servicio inicie un servidor HTTPS y no un servidor HTTP.

## Uso del servicio de editor universal local en lugar del servicio global {#using-local-ue}

El editor universal sabe qué servicio de editor universal utilizar para editar una página en función de cómo se instrumenta. Esto se hace mediante metaetiquetas en la página cargada en el editor universal.

Para editar una página con el servicio de editor universal local, se debe configurar la siguiente metaetiqueta:

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

Una vez configurada, debería ver que cada llamada de actualización de contenido se dirige a `https://localhost:8000`, en lugar del servicio de editor universal predeterminado.

>[!NOTE]
>
>Si se intenta obtener acceso directamente a `https://localhost:8000`, se producirá un error `404`. Este es el comportamiento esperado.
>
>Para probar el acceso al servicio de editor universal local, use `https://localhost:8000/corslib/LATEST`. Consulte la [siguiente sección](#editing) para obtener más información.

>[!TIP]
>
>Para obtener más información sobre cómo se instrumentan las páginas para utilizar el servicio de editor universal global, consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Edición de una página con el servicio de editor universal local {#editing}

Con el [servicio de editor universal ejecutándose localmente](#running-ue) y la [página de contenido instrumentada para usar el servicio local](/help/implementing/universal-editor/getting-started.md), ahora puede iniciar el editor.

1. Abra el explorador en `https://localhost:8000/ping`.
1. Indique a su explorador que acepte [su certificado autofirmado](#ue-https).
1. Una vez que el certificado firmado automáticamente es de confianza, la página se carga mediante el servicio de editor universal local.
1. Haga clic en [Inicio de sesión de desarrollador local](/help/sites-cloud/authoring/universal-editor/navigation.md#local-developer-login) en la barra de herramientas y realice la autenticación en su instancia local de AEM.

Ahora puede editar páginas en la instancia de prueba local de AEM mediante el servicio de editor universal local.
