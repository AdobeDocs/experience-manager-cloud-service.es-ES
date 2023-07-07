---
title: Autenticación del editor universal
description: Obtenga información sobre cómo se autentica el editor universal.
exl-id: fb86c510-3c41-4511-81b7-1bdf2f5e7dd3
source-git-commit: 0f62245d31074ab7a64d86b97ef3b1a8d7533001
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 89%

---


# Autenticación del editor universal {#authentication}

Obtenga información sobre cómo se autentica el editor universal.

## Opciones {#options}

El editor universal utiliza la autenticación del sistema Identity Management de Adobe (IMS), que se proporciona a través de Unified Shell.

Todas las aplicaciones o páginas remotas son responsables de la autenticación en los sistemas backend necesarios. El servicio del editor universal necesita esta autenticación en sistemas backend para realizar operaciones CRUD, ya que es un servicio independiente.

## Flujo estándar {#standard-flow}

Esta es la solución para AEM as a Cloud Service y AMS que utilizan IMS para utilizar el editor universal.

Para utilizar el editor universal, el usuario debe iniciar sesión en Unified Shell que se autentica con IMS. El token IMS proporcionado se almacena en el almacén de sesiones de los usuarios.

Cada vez que un usuario realiza una operación CRUD, se envía una llamada al servicio del editor universal con el token de portador de IMS en el encabezado HTTP. A continuación, el servicio del editor universal utiliza el token de portador para autenticar la solicitud en el sistema back-end de AEM para ejecutar operaciones en el nombre del usuario.

![Flujo de autenticación estándar](assets/standard-flow.png)

## Recursos adicionales {#additional-resources}

Para obtener más información acerca del editor universal, consulte estos documentos.

* [Introducción al editor universal](introduction.md) - Descubra cómo el editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para que pueda ofrecer experiencias excepcionales, aumentar la velocidad del contenido y proporcionar una experiencia de desarrollador avanzada.
* [Creación de contenido con el editor universal](authoring.md): aprenda lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.
* [Publicación de contenido con el editor universal](publishing.md): descubra cómo el editor visual universal publica contenido y cómo sus aplicaciones pueden gestionar el publicado.
* [Introducción al editor universal en AEM](getting-started.md): obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
* [Arquitectura del editor universal](architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
