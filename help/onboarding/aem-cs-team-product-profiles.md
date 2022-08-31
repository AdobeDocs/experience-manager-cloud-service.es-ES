---
title: AEM perfiles as a Cloud Service de equipo y producto
description: Conozca cómo AEM equipo as a Cloud Service y perfiles de producto y conceda y limite el acceso a sus soluciones de Adobe con licencia.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: d54c25791cbb06232ff6e24bb7b8005b366a2144
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# AEM perfiles as a Cloud Service de equipo y producto {#product-profiles}

Conozca cómo AEM equipo as a Cloud Service y perfiles de producto y conceda y limite el acceso a sus soluciones de Adobe con licencia.

## Perfiles de producto {#profiles}

Al conceder a un usuario acceso a una solución de Adobe específica, no necesariamente desea proporcionarles acceso completo. Los perfiles de producto permiten que cada solución tenga su propio conjunto de permisos de usuario. Están disponibles y son accesibles a través de la variable [Admin Console.](/help/journey-onboarding/admin-console.md)

## Perfiles de producto as a Cloud Service de AEM {#aem-product-profiles}

AEM as a Cloud Service es una oferta totalmente nativa de la nube que ofrece AEM como servicio. Ofrece AEM de forma nativa en la nube, con nuevos atributos como siempre activados, siempre actuales, siempre seguros y siempre a escala. Al mismo tiempo, conserva la principal propuesta de valor que AEM proporciona como plataforma personalizable a los clientes y permite que los equipos de clasificación empresarial se integren en sus procedimientos de desarrollo y envío. Consulte [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) para obtener más información sobre AEM as a Cloud Service.

Los integrantes del equipo as a Cloud Service AEM se agregarán y asignarán a uno o más de los siguientes perfiles de producto a través del Admin Console durante la incorporación.

* **Administradores de AEM**: Un administrador de AEM se suele asignar a desarrolladores, en particular a desarrolladores que necesitan tener acceso, por ejemplo, a los entornos de desarrollo. El perfil de producto del administrador de AEM se utilizará para otorgar privilegios de administrador en la instancia de AEM asociada.

* **AEM usuarios**: AEM usuarios son los usuarios de su organización que utilizan AEM as a Cloud Service generalmente para crear contenido. Estos usuarios deberán acceder a AEM para realizar sus tareas. El perfil de producto de los usuarios AEM suele asignarse a un autor de contenido AEM que crea y revisa el contenido. Este contenido puede ser de muchos tipos, como páginas, recursos, publicaciones, etc. El perfil de producto de AEM usuarios que se muestra a continuación se asigna a estos miembros.

![Perfiles de producto](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Todos los usuarios asignados a un perfil de producto as a Cloud Service AEM tienen acceso (solo lectura) a Cloud Manager.

>[!TIP]
>
>Para obtener más información sobre el proceso de incorporación, consulte la [recorrido de incorporación.](/help/journey-onboarding/overview.md)

## Perfiles de producto de Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager tiene perfiles de producto preconfigurados que se pueden considerar como permisos basados en funciones. El administrador del sistema es responsable de configurar el equipo de Cloud Manager asignándolo a estos perfiles de producto.

>[!TIP]
>
>Consulte el documento [Permisos basados en roles en Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) para obtener más información.

Cada uno de los perfiles de producto tiene permisos específicos asociados a ellos.

* **Propietario empresarial** - En esta función, tiene permiso para agregar un nuevo programa o editar un programa, agregar o actualizar un entorno, implementar código en AEM entorno o ejecutar comprobaciones de calidad del código.
* **Administrador de implementación** : En esta función, tiene permiso para agregar o actualizar un entorno, ejecutar cualquier canalización e implementar código en AEM entorno, o ejecutar comprobaciones de calidad del código.
* **Desarrollador** - En esta función, tiene el permiso para generar tokens de acceso personal para acceder a Git.
* **Administrador de programas** - En esta función, tiene permiso para programar canalizaciones, anular las puertas de calidad de 3 niveles y proporcionar la aprobación de producción.

Se puede asignar un usuario a varios perfiles de producto. Por ejemplo, si se asignan ambas **Propietario empresarial** y **Administrar implementación** o a un usuario les da la suma de estos permisos.

Su equipo de Cloud Manager incluirá al menos:

* One **Propietario empresarial**, que suele ser también el administrador del sistema y debe ser la primera persona en iniciar sesión y acceder a Cloud Manager
* One **Administrador de implementación**
* One **Desarrollador**

>[!NOTE]
>
>Para que se le conceda acceso a AEM as a Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto: `AEM Users` o `AEM Administrators`. Los permisos para administrar Cloud Manager no serán suficientes.
