---
title: Autenticación del editor universal
description: Obtenga información sobre cómo se autentica el editor universal.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Autenticación del editor universal {#authentication}

Obtenga información sobre cómo se autentica el editor universal.

## Opciones {#options}

El editor universal utiliza la autenticación del sistema Identity Management de Adobe (IMS), que se proporciona a través del shell unificado.

Todas las aplicaciones o páginas remotas son responsables de la autenticación en los sistemas backend necesarios. El servicio Editor universal necesita esta autenticación en sistemas backend para realizar operaciones CRUD, ya que es un servicio independiente.

## Flujo estándar {#standard-flow}

Esta es la solución para AEM as a Cloud Service y AMS que utilizan IMS para utilizar el editor universal.

Para utilizar el editor universal, el usuario debe iniciar sesión en el shell unificado que se autentica con IMS. El token IMS proporcionado se almacena en el almacén de sesiones de los usuarios.

Cada vez que un usuario realiza una operación CRUD, se envía una llamada al servicio Editor universal con el token de portador de IMS en el encabezado HTTP. A continuación, el servicio Editor universal utiliza el token al portador para autenticar la solicitud en el sistema back-end de AEM para ejecutar operaciones en el nombre del usuario.

![Flujo de autenticación estándar](assets/standard-flow.png)

## Recursos adicionales {#additional-resources}

Para obtener más información sobre el Editor universal, consulte estos documentos.

* [Introducción al Editor universal](introduction.md) : Descubra cómo el Editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Creación de contenido con el editor universal](authoring.md) : Aprenda lo fácil e intuitivo que es para los autores de contenido crear contenido con el Editor universal.
* [Publicación de contenido con el Editor universal](publishing.md) : Descubra cómo el Editor visual universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
* [Introducción al Editor universal en AEM](getting-started.md) : Obtenga información sobre cómo acceder al Editor universal y cómo instrumentar la primera aplicación de AEM para utilizarla.
* [Arquitectura de editor universal](architecture.md) - Obtenga información sobre la arquitectura del Editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md) : Obtenga información sobre los atributos y tipos de datos que requiere el Editor universal.
