---
title: AEM como equipo Cloud Service y perfiles de producto
description: Siga esta página para obtener más información sobre AEM como equipo Cloud Service y perfiles de producto.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 56ca8e80081e62ceb3f5fc2bf9c32aa3bcee12c6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# AEM como equipo Cloud Service y perfiles de producto {#product-profiles}

## Perfiles de producto {#profiles}

Al conceder a un usuario acceso a una solución de Adobe específica, no necesariamente desea proporcionarles acceso completo. Los perfiles de producto permiten que cada solución tenga su propio conjunto de permisos de usuario. Están disponibles y son accesibles a través de [Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md).

Obtenga más información sobre [AEM as a Cloud Service product profiles](#aem-product-profiles) y [Cloud Manager product profiles](#cloud-manager-product-profiles) para comprender cómo funcionan de forma conjunta mientras su equipo está configurado.

## Perfiles de producto de AEM as a Cloud Service {#aem-product-profiles}

AEM como Cloud Service es la oferta nativa de la nube que ofrece AEM como servicio. Ofrece AEM de forma nativa en la nube, con nuevos atributos como siempre activados, siempre actuales, siempre seguros y siempre a escala. Al mismo tiempo, conserva la principal propuesta de valor que AEM proporciona como plataforma personalizable a los clientes y permite que los equipos de clasificación empresarial se integren en sus procedimientos de desarrollo y envío. Consulte [Introducción a Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en) para obtener más información sobre AEM como Cloud Service.

Los integrantes del equipo de AEM como Cloud Service se añadirán y asignarán a uno o más de los siguientes perfiles de producto a través del Admin Console durante la incorporación.

* **AEM administradores**: Un administrador de AEM se suele asignar a desarrolladores, en particular a desarrolladores que necesitan tener acceso, por ejemplo, a los entornos de desarrollo. El perfil de producto de los administradores de AEM se utilizará para otorgar privilegios de administrador en la instancia de AEM asociada.

* **AEM usuarios**: AEM Los usuarios son los usuarios de su organización que utilizan AEM como Cloud Service como parte del acuerdo con Adobe. Estos miembros deberán acceder a AEM para realizar sus tareas. El perfil de producto AEM Usuarios suele asignarse a un autor de contenido AEM que crea y revisa el contenido (puede ser de varios tipos; por ejemplo: páginas, recursos, publicaciones, etc.) antes de publicarse en el sitio web. El perfil de producto AEM Usuarios que se muestra a continuación se asigna a estos miembros.

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >Todos los usuarios asignados a un perfil de producto AEM as a Cloud Service tienen acceso (solo lectura) a Cloud Manager.

## Perfiles de producto de Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager tiene perfiles de producto preconfigurados o, más simplemente, permisos basados en funciones. El administrador del sistema es el responsable de configurar el equipo de Cloud Manager asignando el a estos perfiles de producto, y debe familiarizarse con estos perfiles de producto y a qué miembro del equipo debe asignarlos.
>[!NOTE]
>Consulte [Permisos basados en funciones en Cloud Manager](/help/onboarding/learn-concepts/cloud-manager-introduction.md##role-based-permissions) para obtener más información.

Cada uno de los perfiles de producto tiene permisos específicos asociados a él. Por ejemplo, si tiene la función de:

* **Propietario empresarial**, tiene permiso para agregar un nuevo programa o editar un programa, agregar o actualizar un entorno, agregar, editar o eliminar la canalización y ejecutar cualquier canalización, e implementar código en AEM entorno o calidad de código.

* **Administrador de implementación**, tiene permiso para agregar o actualizar un entorno, ejecutar cualquier canalización e implementar código en AEM entorno o calidad del código.

* **Desarrollador**, tiene permiso para generar un token de acceso personal para acceder a Git.

* **Administrador de programas**, tiene permiso para programar canalizaciones, anular puertas de calidad de tres niveles y proporcionar aprobación de producción.

Se puede asignar un usuario a varios perfiles de producto. Por ejemplo, si asigna las funciones Propietario empresarial y Administrador de implementación a un usuario, obtendrá la combinación o suma de estos permisos.

Su equipo de Cloud Manager incluirá al menos:

* Un propietario, que suele ser también el administrador del sistema, y debe ser la primera persona en iniciar sesión y acceder a Cloud Manager
* Un administrador de implementación
* Un desarrollador

   >[!NOTE]
   >Para que se le conceda acceso a AEM como Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto: `AEM Users` o `AEM Administrators`. Debe tener permisos para la instancia, los permisos para administrar el Cloud Manager asociado no serán suficientes.
