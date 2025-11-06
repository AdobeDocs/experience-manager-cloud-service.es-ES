---
title: Autenticación del editor universal
description: Descubra cómo el editor universal utiliza el sistema de administración de identidades (IMS) de Adobe para la autenticación.
exl-id: fb86c510-3c41-4511-81b7-1bdf2f5e7dd3
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 100%

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

Este diagrama y este artículo describen la autenticación interna del editor universal propiamente dicho.

{{ue-headless-auth}}
