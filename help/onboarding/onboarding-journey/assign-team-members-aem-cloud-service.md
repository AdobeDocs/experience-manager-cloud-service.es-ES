---
title: 'Asignación de miembros del equipo a AEM como perfiles de producto del Cloud Service '
description: Siga esta página para obtener información sobre cómo asignar integrantes del equipo a AEM como perfiles de producto del Cloud Service
hide: true
hidefromtoc: true
index: false
source-git-commit: 8b30fc9494e152aa742cf17c02f982f5c9479473
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 2%

---


# Asignación a AEM como perfiles de producto de Cloud Service {#assign-team-members-cloud-service}

## Objetivo {#objective}

Este documento le ayuda a comprender los pasos que debe seguir el administrador del sistema para asignar los integrantes del equipo a AEM como perfiles de producto Cloud Service y por qué es crucial permitir que los autores de AEM inicien su recorrido con AEM.

Después de leer esta sección debe:

* Comprenda por qué y cómo se asignan los miembros de su equipo a AEM como perfiles de producto de Cloud Service
* Obtenga información sobre cómo agregar integrantes del equipo a AEM perfil de producto de usuario
* Obtenga información sobre cómo agregar integrantes del equipo al perfil de producto de AEM administradores


## Introducción {#introduction}

Para obtener acceso a AEM como usuarios Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto, &quot;AEM usuarios&quot; o &quot;AEM administradores&quot;. Los integrantes del equipo deben tener permisos para la instancia de AEM, ya que los permisos para administrar Cloud Manager no serán suficientes. Más información.

>[!NOTE]
>Todos los usuarios asignados a AEM perfil de producto Usuario por el administrador del sistema tendrán acceso (solo lectura) a Cloud Manager.

## Requisitos previos {#prerequisites}

* Explicación de AEM como perfiles de producto de Cloud Service
* Familiarícese con el Admin Console
* Los perfiles de producto de Cloud Manager se han asignado a los miembros de su equipo según corresponda, y se han configurado los recursos de la nube
* Detalles sobre el miembro del equipo: El administrador del sistema debe tener los nombres y las direcciones de correo electrónico, así como las funciones y responsabilidades de los integrantes del equipo que necesitan tener acceso a AEM como Cloud Service. Con el fin de incorporarlo, le recomendamos que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido. Puede continuar con el resto de la incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede escalar a un mayor número de usuarios más adelante.


1. Iniciar sesión en el Admin Console
(Igual que antes)

1. Revisión de AEM como perfiles de producto del Cloud Service
Desde el Admin Console puede ver la lista de perfiles de Cloud Manager. Para ello:

1. Una vez que haya iniciado sesión en Adobe Admin Console, seleccione Adobe Experience Manager as a Cloud Service en la tarjeta Productos y servicios :

1. Desplácese y seleccione la instancia (instancia de autor del entorno de desarrollo) como se muestra en la imagen siguiente.



   Ahora podrá ver la lista de AEM como perfiles de producto de Cloud Service que será necesario asignar a un usuario en función de su función. Para obtener más información sobre estos elementos, vaya a AEM como Cloud Service de perfiles de producto.




## Agregar integrantes del equipo a AEM perfil de usuario o administrador AEM producto {#add-team-members}

Para obtener acceso a la instancia de AEMaaCS, los usuarios deben pertenecer a uno de los dos perfiles de producto &quot;AEM usuarios&quot; o &quot;AEM administradores&quot;.

>[!NOTE]
>Se le deben conceder permisos para la instancia, los permisos para administrar Cloud Manager no serán suficientes. Más información.

Los pasos siguientes deben ser seguidos por el administrador del sistema que también esté en la función Propietario empresarial .

1. En Cloud Manager, vaya a Cloud Manager y seleccione el botón Administrar acceso en el contexto del entorno de interés, como se muestra a continuación:

1. Una vez que haga clic en Administrar acceso, una nueva PESTAÑA lo desplaza al Admin Console desde donde tiene acceso a la instancia de autor del entorno. Seleccione &quot;AEM administradores&quot; o &quot;AEM usuarios&quot; en función de los permisos que se deban otorgar a esta persona. Obtenga más información sobre AEM como Cloud Service de perfiles de producto.

1. Seleccione Agregar usuario como se muestra a continuación y envíe los detalles necesarios para completar la adición del miembro del equipo:


1. Estos pasos se repetirán para todos los entornos, incluidos Desarrollo, Fase y Producción, si tiene disponible la información de los integrantes del equipo que necesitan tener acceso.

   El usuario que ha agregado ahora tendrá acceso al AEM como Cloud Service Author services!


## Siguientes pasos {#whats-next}

Los usuarios que asignó a perfiles de producto de AEMaaCS ya están listos para aprender a acceder a Author y familiarizarse con la creación de páginas en AEM como Cloud Service. Más información.

## Recursos adicionales {#additional-resources}

Configuración del acceso a AEM (vídeo de introducción)
Guía rápida para la creación de páginas
