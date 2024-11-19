---
title: Ejecución de su propio servicio de editor universal
description: Descubra cómo puede ejecutar su propio servicio de editor universal para el desarrollo local o como parte de su propia infraestructura.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ccdb43c31e3ba1365a514bff696c9ec11dbbc21e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 2%

---


# Ejecución de su propio servicio de editor universal {#local-ue-service}

Descubra cómo puede ejecutar su propio servicio de editor universal para el desarrollo local o como parte de su propia infraestructura.

## Información general {#overview}

El servicio de editor universal es lo que une al editor universal y al sistema backend. Para poder desarrollar localmente para el editor universal, debe ejecutar una copia local del servicio de editor universal. Esto se debe a que:

* El servicio de edición universal oficial de Adobe AEM está alojado a nivel global, y su instancia de local tendría que estar expuesta a Internet.
* AEM Al desarrollar con un SDK de local, no se puede acceder al servicio de editor universal de Adobe desde Internet.
* AEM Si la instancia de la tiene restricciones de IP y el servicio de editor universal de Adobe no está en un intervalo de IP definido, puede alojarlo usted mismo.

## Casos de uso {#use-cases}

Su propia copia del servicio de editor universal resulta útil si desea:

* AEM Desarrollar localmente en la para su uso con el editor universal.
* Ejecute su propio servicio de editor universal como parte de su propia infraestructura, independientemente del servicio de editor universal de Adobe.

Se admiten ambos casos de uso. AEM En este documento se explica cómo ejecutar en HTTPS junto con una copia local del servicio de editor universal (Universal Editor Service).

Si desea ejecutar su propio servicio de editor universal como parte de su propia infraestructura, debe seguir los mismos pasos que en el ejemplo de desarrollo local.

## AEM Configuración de la ejecución de la en HTTPS {#aem-https}

Dentro de un marco externo protegido con HTTPS, no se puede cargar un marco HTTP no seguro. AEM El servicio de editor universal se ejecuta en HTTPS y, por lo tanto, el servicio de editor universal o cualquier otra página remota también deben ejecutarse en HTTPS.

AEM Para ello, debe configurar la ejecución de la en HTTPS. Para fines de desarrollo, puede utilizar un certificado autofirmado.

AEM [Consulte este documento](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=es) sobre cómo configurar la ejecución de la aplicación en HTTPS, incluido un certificado firmado automáticamente que pueda utilizar.

## Instalación del servicio de editor universal {#install-ue-service}

AEM El servicio de editor universal no es una copia completa del editor universal, sino solo un subconjunto de sus funciones para garantizar que las llamadas desde su entorno de trabajo local no se enruten a través de Internet, sino desde un punto final definido que usted controle.

Se requiere la versión 20](https://nodejs.org/en/download/releases) de [NodeJS para ejecutar una copia local del servicio de editor universal.

El servicio de editor universal está disponible a través de la distribución de software. Consulte la [documentación de distribución de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=es) para obtener detalles sobre cómo acceder a ella.

Guarde el archivo `universal-editor-service.cjs` de Distribución de software en el entorno de desarrollo local.

## Crear un certificado para ejecutar el servicio de editor universal con HTTPS {#ue-https}

El servicio de editor universal también requiere un certificado para ejecutarse en HTTPS en el entorno de desarrollo.

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
>Si está ejecutando la versión 130 o posterior de Chrome, debe habilitar el envío de encabezados CORS para el [acceso a la red privada](https://wicg.github.io/private-network-access/#private-network-request) mediante la opción `UES_CORS_PRIVATE_NETWORK`.


La siguiente tabla detalla estos y los valores adicionales disponibles.

| Valor | Opcional | Predeterminado | Descripción |
|---|---|---|---|
| `UES_PORT` | Sí | `8080` | Puerto en el que se ejecuta el servidor |
| `UES_PRIVATE_KEY` | Sí | Ninguno | Ruta a la clave privada del servidor HTTPS |
| `UES_CERT` | Sí | Ninguno | Ruta al archivo de certificación para el servidor HTTPS |
| `UES_TLS_REJECT_UNAUTHORIZED` | Sí | `true` | Rechazar conexiones TLS no autorizadas |
| `UES_DISABLE_IMS_VALIDATION` | Sí | `false` | Deshabilitar validación de IMS |
| `UES_ENDPOINT_MAPPING` | Sí | Vacío | Asignación de los extremos para reescrituras internas<br>Ejemplo: `UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>Resultado: el servicio de editor universal se conectará a `http://10.0.0.1:4502` en lugar de la conexión proporcionada `https://your-public-facing-author-domain.net` |
| `UES_LOG_LEVEL` | Sí | `info` | Nivel de registro del servidor. Los valores posibles son `silly`, `trace`, `debug`, `verbose`, `info`, `log`, `warn`, `error` y `fatal` |
| `UES_SPLUNK_HEC_URL` | Sí | Ninguno | URL de HEC al extremo de Splunk |
| `UES_SPLUNK_TOKEN` | Sí | Ninguno | Token de Splunk |
| `UES_SPLUNK_INDEX` | Sí | Ninguno | Índice para escribir registros en |
| `UES_SPLUNK_SOURCE` | Sí | `universal-editor-service` | Nombre del origen en los registros de splunk |
| `UES_CORS_PRIVATE_NETWORK` | Sí | `false` | Habilitar el envío de encabezados CORS para permitir [red privada.](https://wicg.github.io/private-network-access/#private-network-request) necesario para los usuarios de Chrome versión 130+ |

>[!NOTE]
>
>Antes de la versión [2024.08.13](/help/release-notes/universal-editor/current.md) del Editor universal, se requerían las siguientes variables en el archivo `.env`. Estos valores serán compatibles hasta el 1 de octubre de 2024 para la compatibilidad con versiones anteriores.
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

Asegúrese de que el servicio inicia HTTPS Server y no HTTP Server.

## Uso del servicio de editor universal local en lugar del servicio global {#using-local-ue}

El editor universal sabe qué servicio de editor universal utilizar para editar una página en función de cómo se instrumenta la página. Esto se realiza mediante metaetiquetas en la página cargada en el editor universal.

Para editar una página con el servicio de editor universal local, se debe configurar la siguiente etiqueta meta:

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

Una vez configurado, debería ver que cada llamada de actualización de contenido se dirige a `https://localhost:8000` en lugar del servicio de editor universal predeterminado.

>[!NOTE]
>
>Si se intenta obtener acceso directamente a `https://localhost:8000`, se producirá un error de `404`. Este es el comportamiento esperado.
>
>Para probar el acceso al servicio de editor universal local, use `https://localhost:8000/corslib/LATEST`. Consulte la [siguiente sección](#editing) para obtener más información.

>[!TIP]
>
>AEM Para obtener más información sobre cómo se instrumentan las páginas para utilizar el servicio de editor universal global, consulte el documento [Introducción al editor universal en la documentación de {100000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000000000000000000000](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Edición de una página con el servicio de editor universal local {#editing}

Con el servicio de editor universal [ejecutándose localmente](#running-ue) y la página de contenido [instrumentada para usar el servicio local](#using-loca-ue), ahora puede iniciar el editor.

1. Abra el explorador a `https://localhost:8000/ping`.
1. Indique a su explorador que acepte [su certificado firmado automáticamente.](#ue-https)
1. Una vez que el certificado autofirmado sea de confianza, puede editar la página mediante el servicio de editor universal local.

