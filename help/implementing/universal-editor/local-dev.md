---
title: AEM Desarrollo local con el editor universal de la aplicación
description: AEM Descubra cómo el Editor universal admite la edición en instancias de locales con fines de desarrollo.
source-git-commit: bf09c31baf209f5315e35f47c0d79c2b4365d3d3
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# AEM Desarrollo local con el editor universal de la aplicación {#local-dev-ue}

AEM Descubra cómo el Editor universal admite la edición en instancias de locales con fines de desarrollo.

AEM AEM En este documento se explica cómo ejecutar el código en HTTPS junto con una copia local del servicio de editor universal para que pueda desarrollar de forma local el código de tiempo en el editor universal. Se explica cómo ejecutar el código de tiempo en HTTPS junto con una copia local del servicio de editor universal para que pueda desarrollar de forma local el código de tiempo en el que se utiliza el editor universal.

## AEM Configuración de la ejecución de la en HTTPS {#aem-https}

Dentro de un marco externo protegido con HTTPS no se puede cargar un marco HTTP no seguro. AEM El servicio de editor universal se ejecuta en HTTPS y, por lo tanto, el servicio de editor universal o cualquier otra página remota también deben ejecutarse en HTTPS.

AEM Para ello, debe configurar la ejecución de la en HTTPS. Para fines de desarrollo, puede utilizar un certificado autofirmado.

AEM Consulte este documento sobre cómo configurar la ejecución de un servicio en HTTPS, incluido un certificado firmado automáticamente que pueda utilizar.

## Instalación del servicio de editor universal {#install-ue-service}

El servicio de editor universal es lo que une al editor universal y al sistema backend. AEM Dado que el servicio de editor universal oficial está alojado a nivel global, la instancia de la instancia local de la tendría que estar expuesta a Internet. Para evitarlo, puede ejecutar una copia local del servicio de editor universal.

[Versión 16 de NodeJS](https://nodejs.org/en/download/releases) es necesario para ejecutar una copia local del servicio de editor universal

AEM El servicio de edición universal lo distribuye directamente el departamento de ingeniería de la. VIP póngase en contacto con su contacto de ingeniería en el programa de trabajo de la unidad de control para obtener una copia local del mismo.

El departamento de ingeniería le proporcionará un `universal-editor-service.cjs` archivo. Guarde esto en su entorno de desarrollo local.

## Crear un certificado para ejecutar el servicio de editor universal con HTTPS {#ue-https}

El servicio de editor universal también requiere un certificado para ejecutarse en HTTPS en el entorno de desarrollo.

Ejecute el siguiente comando.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

El comando genera un `key.pem` y una `certificate.pem` archivo. Guarde estos archivos en la misma ruta que su `universal-editor-service.cjs` archivo.

## Configuración del servicio de editor universal {#setting-up-service}

Se deben configurar varias variables de entorno en NodeJS para ejecutar el servicio de editor universal localmente.

En la misma ruta que su `universal-editor-service.cjs`, `key.pem` y `certificate.pem` archivos, crear un `.env` con el siguiente contenido.

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

La variable tiene los siguientes significados:

* `EXPRESS_PORT`: define en qué puerto escucha el servicio de editor universal
* `EXPRESS_PRIVATE`: apunta a su [clave privada creada anteriormente,](#ue-https) `key.pem`
* `EXPRESS_CERT`: apunta a su [certificado creado anteriormente,](#ue-https) `certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`: acepta certificados firmados automáticamente

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

```
<meta name="urn:adobe:aem:editor:endpoint" content="https://localhost:8000">
```

Una vez configurado, debería ver cada llamada de actualización de contenido y dirigirse a `https://localhost:8000` en lugar del servicio de editor universal predeterminado.

>[!TIP]
>
>Para obtener más información sobre cómo se instrumentan las páginas para utilizar el servicio de editor universal global, consulte el documento [AEM Introducción al editor universal en el entorno de trabajo de la aplicación de](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Edición de una página con el servicio de editor universal local {#editing}

Con el [Servicio de editor universal que se ejecuta localmente](#running-ue) y su [página de contenido instrumentada para utilizar el servicio local,](#using-loca-ue) ahora puede iniciar el editor.

1. Abra el explorador para `https://localhost:8000/`.
1. Dirija su navegador para que acepte [su certificado autofirmado.](#ue-https)
1. Una vez que el certificado autofirmado sea de confianza, puede editar la página mediante el servicio de editor universal local.
