---
title: 'Consideraciones de permisos para contenido sin encabezado '
description: Obtenga información sobre diferentes consideraciones de permisos y ACL para una implementación sin encabezado con Adobe Experience Manager. Comprenda las diferentes personas y los niveles de permisos potenciales necesarios para los entornos Autor y Publicación .
feature: Content Fragments,GraphQL API
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# Consideraciones de permisos para contenido sin encabezado

Con una implementación sin objetivos, hay varias áreas de seguridad y permisos que deben abordarse. Los permisos y las personas se pueden considerar en general en función del entorno AEM **Autor** o **Publicación**. Cada entorno contiene diferentes personalidades y con diferentes necesidades.

## Consideraciones del servicio de creación

El servicio Autor es donde los usuarios internos crean, administran y publican contenido. Los permisos giran en torno a las diferentes personas que administran el contenido.

### Administrar permisos en el nivel de grupo

Como práctica recomendada, los permisos deben establecerse en Grupos en AEM. También conocidos como grupos locales, estos grupos se pueden administrar dentro del entorno de creación de AEM.

La forma más sencilla de administrar la pertenencia a un grupo es utilizar los grupos de Adobe Identity Management System (IMS) y asignar [Grupos de IMS a grupos de AEM locales](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en#managing-permissions-in-aem).

![Flujo de permisos de Admin Console](assets/admin-console-aem-group-permissions.png)

En un nivel superior, el proceso es:

1. Agregar usuarios de IMS a un grupo de usuarios de IMS nuevo o existente mediante la función [Admin Console](https://adminconsole.adobe.com/)
1. Los grupos de IMS se sincronizan con AEM cuando los usuarios inician sesión.
1. Asigne grupos IMS a AEM grupos.
1. Establezca permisos en Grupos AEM.
1. Cuando los usuarios inician sesión en AEM y se autentican mediante IMS, heredan los permisos del grupo de AEM.

>[!TIP]
>
> Encontrará una guía detallada en vídeo sobre la administración de IMS y AEM usuarios y grupos [here](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html).

Para administrar **grupos** en AEM, vaya a **Herramientas** > **Seguridad** > **Grupos**.

Para administrar los permisos de los grupos en AEM, vaya a **Herramientas** > **Seguridad** > **Permisos**.

### Usuarios de DAM

&quot;DAM&quot;, en este contexto, significa Gestión de Activos Digitales. La variable **Usuarios de DAM** es un grupo predeterminado en AEM que puede utilizarse para usuarios &quot;comunes&quot; que administran recursos digitales y fragmentos de contenido. Este grupo proporciona permisos para **ver**, **add**, **actualizar**, **delete** y **publicar** Fragmentos de contenido y todos los demás archivos de AEM Assets.

Si utiliza IMS para la pertenencia a un grupo, agregue los grupos de IMS adecuados como miembros del **Usuarios de DAM** grupo. Los miembros del grupo IMS heredan los permisos del grupo Usuarios de DAM al iniciar sesión en el entorno de AEM.

#### Personalización del grupo de usuarios de DAM

Se recomienda no modificar directamente los permisos de un grupo predeterminado. En su lugar, también puede crear sus propios grupos siguiendo el modelo de **Usuarios de DAM** permisos de grupo y restringir aún más el acceso a diferentes **carpetas** en AEM Assets.

Para obtener permisos más granulares, utilice la variable **Permisos** consola en AEM y actualizar la ruta `/content/dam` a una ruta más específica, es decir, `/content/dam/mycontentfragments`.

Puede ser deseable conceder a este grupo de usuarios permisos para crear y editar fragmentos de contenido, pero no para eliminarlos. Para revisar y asignar permisos de edición, pero no eliminar, consulte [Fragmentos de contenido: Eliminar consideraciones](/help/assets/content-fragments/content-fragments-delete.md).

### Editores de modelos

La capacidad de modificar **Modelos de fragmento de contenido** debe dejarse a los administradores o a un **grupo pequeño** de usuarios con permisos elevados. Modificar el modelo de fragmento de contenido tiene muchos efectos descendentes.

>[!CAUTION]
>
>Las modificaciones en los modelos de fragmento de contenido modifican la API de GraphQL subyacente en la que se basan las aplicaciones sin encabezado.

Si desea crear un grupo que administre los modelos de fragmento de contenido pero no el acceso de administrador completo, puede crear un grupo con las siguientes entradas de control de acceso:

| Ruta | Permiso | Privilegios |
|-----| -------------| ---------|
| `/conf` | **permitir** | `jcr:read` |
| `/conf/<config-name>/settings/dam/cfm` | **permitir** | `rep:write`, `crx:replicate` |

## Permisos del servicio de publicación

El servicio de publicación se considera el entorno &quot;activo&quot; y es normalmente lo que interactúan los consumidores de la API de GraphQL. El contenido, después de editarse y aprobarse en el servicio Autor, se publica en el servicio Publicación. A continuación, la aplicación sin encabezado consume el contenido aprobado del servicio Publicar a través de las API de GraphQL.

De forma predeterminada, el contenido expuesto a través de los extremos de GraphQL del servicio AEM Publish es accesible para todos, incluidos los usuarios no autenticados.

### Permisos de contenido

El contenido expuesto a través de las API de AEM GraphQL se puede restringir mediante [Grupos de usuarios cerrados (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html) se configura en carpetas de recursos, que especifican qué AEM grupos de usuarios (y sus miembros) pueden acceder al contenido de las carpetas de recursos.

Los CUG de recursos funcionan mediante:

* En primer lugar, denegar todo acceso a la carpeta y las subcarpetas
* A continuación, permitir el acceso de lectura a la carpeta y subcarpetas para todos los grupos de usuarios AEM que se enumeran en la lista de CUG

Los CUG se pueden configurar en carpetas de recursos que contengan contenido expuesto a través de las API de GraphQL. El acceso a las carpetas de recursos en AEM Publish debe controlarse mediante grupos de usuarios, en lugar de hacerlo directamente. Cree (o reutilice) un grupo de usuarios AEM que conceda acceso a carpetas de recursos que contengan contenido expuesto por las API de GraphQL.

#### Seleccione el esquema de autenticación{#publish-permissions-users}

La variable [SDK AEM sin encabezado](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) admite dos tipos de autenticación:

* [Autenticación basada en token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) uso de credenciales de servicio enlazadas a una sola cuenta técnica.
* Autenticación básica con usuarios AEM.

### Acceso a la API de GraphQL

Las solicitudes HTTP que proporcionan la variable [credenciales de autenticación adecuadas](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) Los extremos de la API de GraphQL del servicio AEM Publish incluyen el contenido que las credenciales están autorizadas a leer y el contenido accesible de forma anónima. Otros consumidores de la API de GraphQL no pueden leer el contenido de las carpetas protegidas con CUG.

