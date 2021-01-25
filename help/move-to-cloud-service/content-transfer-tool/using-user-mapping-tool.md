---
title: Uso de la herramienta Asignación de usuarios
description: Uso de la herramienta Asignación de usuarios
translation-type: tm+mt
source-git-commit: 664c278494a5ac88362b994946060ab3baa846d8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Uso de la herramienta de asignación de usuarios {#user-mapping-tool}

## Información general {#overview}

Como parte del recorrido de transición para AEM como Cloud Service, debe mover usuarios y grupos del sistema de AEM existente a AEM como Cloud Service. Esto lo realiza la Herramienta de transferencia de contenido.

Un cambio importante en AEM como Cloud Service es el uso completamente integrado de ID de Adobe para acceder al nivel de autor.  Esto requiere el uso de Adobe Admin Console para administrar usuarios y grupos de usuarios. La información de usuario-perfil está centralizada en el sistema Identity Management de Adobe (IMS), que proporciona el inicio de sesión único en todas las aplicaciones de nube de Adobe. Para obtener más información, consulte Identity Management. Debido a este cambio, los usuarios y grupos existentes deben asignarse a sus ID de IMS para evitar los usuarios y grupos de duplicado en la instancia de creación de Cloud Service.

## Consideraciones importantes {#important-considerations}

Hay algunos casos excepcionales que hay que considerar. Se registrarán los siguientes casos específicos y no se asignará al usuario o grupo en cuestión:

1. Si un usuario no tiene una dirección de correo electrónico en el campo `profile/email` de su nodo jcr.

1. Si no se encuentra un correo electrónico determinado en el sistema IMS para el identificador de organización utilizado (o si el identificador IMS no se puede recuperar por otro motivo).

1. Si el usuario está deshabilitado actualmente, se trata de la misma manera que si no estuviera deshabilitado.  Se asignará y migrará como de costumbre, y permanecerá deshabilitado en la instancia de nube.

## Uso de la herramienta de asignación de usuarios {#using-user-mapping-tool}

La herramienta de asignación de usuarios utiliza una API que le permite buscar usuarios de IMS por correo electrónico y devolver sus ID de IMS. Esta API requiere que el usuario cree un ID de cliente para su organización, un secreto de cliente y un autentificador de Token de acceso/portador.

Siga estos pasos para configurar esta configuración:

1. Vaya a [Consola de programadores de Adobe](https://console.adobe.io) con su Adobe ID.
1. Crear un proyecto nuevo o abrir un proyecto existente
1. Añadir una API
1. Elija la API de administración de usuarios
1. Crear una credencial JWT
1. Generar un par de claves o Cargar una clave pública (rsa no es buena)
1. Genere un token de acceso (o token JWT o token de portador).
1. Guarde toda esta información (ID de cliente, Secreto de cliente, ID de cuenta técnica, Correo electrónico de cuenta técnica, ID de organización, Token de acceso) en un lugar seguro.