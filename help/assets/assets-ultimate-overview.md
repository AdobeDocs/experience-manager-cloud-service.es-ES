---
title: Assets Ultimate
description: Obtenga más información sobre los aspectos clave de Assets Ultimate, como las ventajas clave, los tipos de usuarios y sus privilegios.
feature: Asset Management
role: User, Admin
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 3ae96cd2-e0ac-43a5-a0bf-bebb1a028b10
source-git-commit: bcdfc9bb418ab405faa82c55820a6ec6062c2b17
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 41%

---

# [!DNL Assets] as a Cloud Service Ultimate {#assets-ultimate-user-types-privileges}

![Assets as a Cloud Service Ultimate](/help/assets/assets/aem-assets-ultimate-banner.png)

Assets as a Cloud Service Ultimate ofrece funcionalidades avanzadas de DAM. AEM Assets Ultimate está diseñado para administrar cadenas de suministro de contenido complejas, lo que garantiza que cada contenido funcione bien en todos los canales.

## ¿Por qué Assets Ultimate? {#why-ultimate-existing-new-users}

Assets as a Cloud Service Ultimate ofrece varias ventajas clave que ayudan a administrar de forma eficaz las necesidades de recursos de su organización, como las siguientes:

* Mayor flexibilidad con más tipos de usuarios y privilegios asociados con esos tipos de usuarios, como usuarios colaboradores, usuarios avanzados y usuarios limitados.

* Distribución de recursos perfecta con Content Hub.

* Creación y remezcla de contenido con tecnología de IA mediante Adobe Express con Firefly.

* Una experiencia de incorporación o actualización más fluida para los usuarios nuevos y existentes.

## Funcionalidades clave de Assets Ultimate {#capabilities-assets-ultimate}

Assets as a Cloud Service Ultimate incluye las siguientes funciones clave:

* **Servicios de biblioteca y administración de recursos**: herramientas que permiten a los usuarios ingestar, almacenar, catalogar, controlar, administrar y gobernar los recursos digitales de una marca en un repositorio centralizado

* **Búsqueda, descubrimiento y colaboración**: herramientas que permiten a los usuarios examinar, descubrir, colaborar y compartir los recursos que necesitan para crear experiencias de cliente enriquecidas.

* **Seguridad y Rights Management**: herramientas para administrar el acceso, los permisos, los derechos y la seguridad con el fin de garantizar el cumplimiento, la coherencia y la integridad de la marca.

* **Conexiones de Creative Cloud**: herramientas que permiten a los equipos creativos y de marketing colaborar con el acceso simplificado, los comentarios, la revisión y las anotaciones para actualizar o finalizar los recursos digitales.

* **Conexiones de Experience Cloud**: herramientas para admitir el acceso nativo a recursos digitales desde otras aplicaciones y servicios de Experience Cloud.

* **Experiencia del portal de distribución (Content Hub)**: herramientas para ampliar el acceso a los recursos digitales aprobados de una marca a las partes interesadas extendidas para garantizar el uso y la coherencia de marca.

* **Integraciones**: integraciones con otras aplicaciones de Adobe y que no sean de Adobe.

* **Dynamic Media (complemento)**: herramientas para transformar y enviar imágenes, vídeos y otro contenido emergente para experiencias multimedia interactivas enriquecidas para cualquier dispositivo a escala.

* **Personalización**: herramientas para personalizar el acceso de la interfaz de usuario de DAM a las API para un desarrollo posterior.

* **Extensibilidad personalizada**: gran flexibilidad a través de su sólida plataforma API-First, que permite una integración y personalización sin problemas para satisfacer la compleja infraestructura de TI del cliente.

* **Automatización de contenido (complemento)**: herramientas para unificar la administración del trabajo y automatizar los flujos de trabajo de transformación de recursos digitales para la producción de contenido a escala.

Las operaciones que se pueden realizar en Assets as a Cloud Service dependen del tipo de usuario. Consulte [Tipos de usuarios disponibles](#available-user-types) para obtener más información.


## ¿Cuáles son los tipos de usuarios y privilegios disponibles? {#available-user-types}

Assets as a Cloud Service ofrece cuatro tipos de usuarios. Cada tipo de usuario proporciona un conjunto diferente de privilegios. Los tipos de usuario incluyen:

* **Administrador**: el usuario administrador estándar, que configura los otros tres tipos de usuarios de la organización.

* **Usuarios limitados**: los usuarios limitados pueden acceder a los recursos aprobados de su organización y aprovecharlos mediante el portal de Content Hub de AEM Assets.

* **Usuarios colaboradores**: como usuario colaborador, puede:

   * Trabajar con recursos de Experience Manager mediante integraciones de Assets disponibles para su organización en otros productos de Adobe y aplicaciones que no sean de Adobe.

   * Crear y editar recursos mediante Adobe Express y Firefly integrados que aprovechen plantillas diseñadas profesionalmente, kits de marca, recursos de Adobe Stock, etc.

   * Acceder a los recursos aprobados de su organización y aprovecharlos mediante el portal de Content Hub de AEM Assets.

* **Usuarios avanzados**: como usuario avanzado, puede:

   * Acceder a todas las funciones de AEM Assets, incluida la administración de recursos, los metadatos y la gestión y automatización generales de los recursos digitales.

   * Trabajar con recursos de Experience Manager mediante integraciones de Assets disponibles para su organización en otras aplicaciones de Adobe y que no sean de Adobe.

   * Crear y editar recursos mediante Adobe Express y Firefly integrados que aprovechen plantillas diseñadas profesionalmente, kits de marca, recursos de Adobe Stock, etc.

   * Acceder a los recursos aprobados de su organización y aprovecharlos mediante el portal de Content Hub de AEM Assets.

  ![Usuario avanzado de Assets as a Cloud Service](/help/assets/assets/assets-cs-power-users.png)

La siguiente tabla resume los tipos de usuarios de AEM Assets disponibles, los privilegios que tienen y los perfiles de producto necesarios para obtener esos privilegios:


| Función de usuario | Usuarios limitados | Usuarios colaboradores | Usuarios avanzados | Administradores |
|---------------|----------|----------|-------------------------|---|
| **Capacidades** |  |  |  |  |
| Acceso a los recursos de marca aprobados en el portal de Content Hub | ✓ | ✓ | ✓ | ✓ |
| Crear y editar recursos mediante Adobe Express y Firefly integrados | − | ✓ | ✓ | ✓ |
| Integración de recursos en su organización con aplicaciones de Adobe y que no sean de Adobe | − | ✓ | ✓ | ✓ |
| Acceder a todas las funciones de AEM Assets, como administración de recursos, los metadatos y la gestión y automatización generales | − | − | ✓ | ✓ |
| Administración de permisos del contenido en el entorno de creación de AEM Assets | − | − | − | ✓ |
| **El usuario debe estar en estos perfiles de producto (Admin Console)** |  |  |  |  |
| AEM > Instancia de entrega > Usuarios limitados de AEM Assets | ✓ | ✓ | ✓ | ✓ |
| AEM > Instancia de autor de producción > Usuarios colaboradores de AEM Assets | − | ✓ | − | − |
| AEM > Instancia de autor de producción > Usuarios avanzados de AEM Assets | − | − | ✓ | − |
| AEM > Instancia de autor de producción > Administradores de AEM | − | − | − | ✓ |
| **Más información** | Consulte [Habilitar Content Hub](/help/assets/enable-assets-ultimate.md##enable-assets-ultimate-new-users) | Consulte [Incorporación de usuarios colaboradores](/help/assets/enable-assets-ultimate.md#onboard-collaborator-users) | Consulte [Incorporación de usuarios avanzados](/help/assets/enable-assets-ultimate.md#onboard-power-users) | - |

Para obtener información sobre cómo empezar a usar Assets Ultimate, consulte [Habilitar AEM Assets Ultimate](/help/assets/enable-assets-ultimate.md). Si los usuarios de AEM Assets existentes tienen dudas sobre cuándo pueden actualizar a Assets Ultimate, póngase en contacto con el representante de su cuenta de Adobe. También puede consultar [Habilitar Assets Ultimate para los clientes existentes](/help/assets/enable-assets-ultimate.md#enable-assets-ultimate-existing-customers) para obtener más información.

AEM Assets también proporcionan un DAM más ligero para los clientes que no tienen requisitos avanzados como, por ejemplo, extensibilidad de la interfaz de usuario, automatización impulsada por API e implementación de código personalizado. Para más información, consulte [AEM Assets Prime](/help/assets/assets-prime.md).

## Preguntas frecuentes {#frequently-asked-questions-assets-ultimate}

### ¿Qué es Ultimate de AEM Assets y en qué se diferencia de otras ofertas de AEM Assets? {#what-is-assets-ultimate}

AEM Assets Ultimate es la oferta avanzada de administración de activos digitales de Adobe en Adobe Experience Manager as a Cloud Service, diseñada para administrar cadenas de suministro de contenido complejas y garantizar que el contenido funcione bien en todos los canales. Ofrece cuatro tipos distintos de usuarios, usuarios limitados, usuarios colaboradores, usuarios avanzados y administradores, cada uno con un conjunto definido de funciones y asignaciones de perfil de producto. AEM Assets Ultimate también incluye una distribución de Content Hub perfecta, creación de contenido con tecnología de IA a través de Adobe Express y Firefly e integraciones con aplicaciones de Adobe y que no sean de Adobe.

### ¿Qué puede hacer un usuario limitado en AEM Assets Ultimate? {#limited-user-capabilities}

Un usuario limitado de AEM Assets Ultimate puede acceder y utilizar recursos aprobados por la marca de la organización a través del portal Content Hub de AEM Assets. Los usuarios limitados no pueden crear ni editar recursos, administrar metadatos, acceder al entorno de creación de AEM Assets ni integrar recursos con otras aplicaciones. Su acceso tiene como objetivo exclusivo descubrir y aprovechar los recursos aprobados a través de Content Hub, lo que hace que este tipo de usuario sea adecuado para las partes interesadas extendidas que necesitan acceso controlado a los recursos de marca finalizados.

### ¿A qué perfil de producto se debe agregar un usuario limitado en AEM Assets Ultimate? {#limited-user-product-profile}

Un usuario limitado en AEM Assets Ultimate debe añadirse al siguiente perfil de producto en Adobe Admin Console: AEM > Instancia de envío > Usuarios limitados de AEM Assets. Este es el único perfil de producto necesario para los usuarios limitados. Otorga acceso al portal Content Hub de AEM Assets para la detección y el uso aprobados de los recursos. No se requiere ningún perfil de instancia de autor de producción para este tipo de usuario.

### ¿Qué puede hacer un usuario de Collaborator en AEM Assets Ultimate? {#collaborator-user-capabilities}

Un usuario colaborador en AEM Assets Ultimate puede acceder a los recursos aprobados por la marca a través del portal Content Hub de AEM Assets, crear y editar recursos con Adobe Express y Firefly con plantillas y kits de marca diseñados profesionalmente, y trabajar con recursos de Adobe Experience Manager mediante integraciones disponibles en otros productos de Adobe y aplicaciones que no sean de Adobe. Los usuarios de Collaborator no pueden administrar recursos en el nivel DAM, ni controlar los metadatos, ni gestionar permisos en el entorno de creación de AEM Assets; estas funciones están reservadas para los usuarios avanzados y los administradores.

### ¿Qué perfiles de producto se deben añadir a un usuario de Collaborator en AEM Assets Ultimate? {#collaborator-user-product-profiles}

Un usuario colaborador en AEM Assets Ultimate debe añadirse a dos perfiles de producto en Adobe Admin Console: AEM > Instancia de envío > Usuarios limitados de AEM Assets y AEM > Instancia de autor de producción > Usuarios colaboradores de AEM Assets. El perfil Delivery instance concede acceso a Content Hub. El perfil de instancia de autor de producción permite las integraciones de recursos y la creación de contenido con tecnología de Adobe Express y Firefly. Ambos perfiles son necesarios para disfrutar de la experiencia completa de usuario de Collaborator.

### ¿Qué puede hacer un usuario avanzado en AEM Assets Ultimate? {#power-user-capabilities}

Un usuario avanzado en AEM Assets Ultimate tiene acceso a toda la gama de funciones de AEM Assets, incluidas la ingesta de recursos, el almacenamiento, la catalogación, la administración de metadatos, la gobernanza y la automatización en torno a los recursos digitales. Los usuarios avanzados también pueden crear y editar recursos con Adobe Express y Firefly, trabajar con recursos a través de integraciones en aplicaciones de Adobe y que no sean de Adobe y acceder a recursos aprobados por la marca a través del portal de Content Hub para AEM Assets. Los usuarios avanzados no pueden administrar permisos en el entorno de creación de AEM Assets; esta capacidad está reservada para los administradores.

### ¿Qué perfiles de producto se deben añadir a un usuario avanzado en AEM Assets Ultimate? {#power-user-product-profiles}

Un usuario avanzado en AEM Assets Ultimate debe agregarse a dos perfiles de producto en Adobe Admin Console: AEM > Instancia de envío > Usuarios limitados de AEM Assets y AEM > Instancia de autor de producción > Usuarios avanzados de AEM Assets. El perfil Delivery instance concede acceso a Content Hub. El perfil de instancia del autor de producción desbloquea las funciones completas de DAM de los AEM Assets, incluida la administración de recursos, el control de metadatos y los flujos de trabajo de automatización. Ambos perfiles son necesarios para disfrutar de la experiencia completa de usuario avanzado.

### ¿Qué puede hacer un administrador en AEM Assets Ultimate? {#administrator-capabilities}

Un administrador en AEM Assets Ultimate tiene todas las funciones de un usuario avanzado y, además, administra permisos de contenido en el entorno de creación de AEM Assets. Los administradores son responsables de configurar los otros tres tipos de usuarios de la organización: usuarios limitados, usuarios de Collaborator y usuarios avanzados. Esto incluye la asignación de perfiles de producto en Adobe Admin Console, el control de los derechos de acceso y la garantía de que se cuenta con la estructura de privilegios correcta para cada tipo de usuario en toda la organización.

### ¿A qué perfil de productos se debe agregar un administrador en AEM Assets Ultimate? {#administrator-product-profiles}

Un administrador en AEM Assets Ultimate debe añadirse a dos perfiles de producto en Adobe Admin Console: AEM > Instancia de envío > Usuarios limitados de AEM Assets y AEM > Instancia de autor de producción > Administradores de AEM. El perfil Delivery instance concede acceso a Content Hub. El perfil de instancia del autor de producción concede un control administrativo completo, incluida la administración de permisos en el entorno de creación de AEM Assets, y la capacidad de configurar todos los demás tipos de usuarios dentro de la organización.

### ¿Qué tipos de usuarios de AEM Assets Ultimate pueden acceder al portal de Content Hub? {#content-hub-access-user-types}

Los cuatro tipos de usuarios de AEM Assets Ultimate (usuarios limitados, usuarios colaboradores, usuarios avanzados y administradores) pueden acceder al portal Content Hub de AEM Assets para detectar y utilizar recursos aprobados por la marca. El acceso a Content Hub se concede a través del perfil de producto AEM > Instancia de envío > Usuarios limitados de AEM Assets en Adobe Admin Console, que es un perfil requerido para cada tipo de usuario en AEM Assets Ultimate, independientemente de sus funciones adicionales.

### ¿Qué tipos de usuarios de AEM Assets Ultimate pueden crear y editar recursos con Adobe Express y Firefly? {#express-firefly-access-user-types}

Los usuarios colaboradores, los usuarios avanzados y los administradores de AEM Assets Ultimate pueden crear y editar recursos mediante las funciones integradas de Adobe Express y Firefly, incluidas plantillas diseñadas profesionalmente, kits de marca y recursos de Adobe Stock. Los usuarios limitados no tienen acceso a las funciones de creación o edición de recursos; su acceso tiene como objetivo descubrir y utilizar recursos aprobados por la marca solo a través del portal Content Hub para AEM Assets.

### ¿Qué tipos de usuarios de AEM Assets Ultimate pueden integrar recursos con aplicaciones de Adobe y que no sean de Adobe? {#integration-access-user-types}

Los usuarios colaboradores, los usuarios avanzados y los administradores de AEM Assets Ultimate pueden trabajar con recursos de Adobe Experience Manager mediante integraciones disponibles en otros productos de Adobe y aplicaciones que no sean de Adobe. Los usuarios limitados no pueden acceder a las integraciones de recursos: sus capacidades se limitan al acceso al portal de Content Hub para la detección y el uso aprobados de los recursos. El acceso a la integración se habilita a través de los perfiles de producto de la instancia de AEM > Production Author asignados a cada uno de estos tipos de usuarios.

### ¿Qué tipo de usuario en AEM Assets Ultimate tiene funcionalidades completas de administración de DAM, incluido el control de metadatos? {#dam-management-user-types}

Los usuarios avanzados y los administradores de AEM Assets Ultimate tienen acceso a toda la gama de funcionalidades de DAM para AEM Assets, incluidas la ingesta de recursos, el almacenamiento, la catalogación, la administración de metadatos, la gobernanza y la automatización en torno a los recursos digitales. Los usuarios de Collaborator y los usuarios limitados no tienen acceso a la administración a nivel DAM ni a la administración de metadatos. El acceso completo a DAM se habilita a través del perfil de producto AEM > Instancia de autor de producción > Usuarios avanzados de AEM Assets o Administradores de AEM en Adobe Admin Console.

### ¿Qué tipo de usuario de AEM Assets Ultimate puede administrar permisos en el entorno de creación de AEM Assets? {#permission-management-user-type}

Solo los administradores de AEM Assets Ultimate pueden administrar permisos de contenido en el entorno de creación de AEM Assets. Los usuarios avanzados, los usuarios colaboradores y los usuarios limitados no tienen capacidades de administración de permisos. Esta capacidad exclusiva se habilita a través del perfil de producto AEM > Production Author instance > AEM Administrators en Adobe Admin Console. Los administradores también son responsables de configurar y asignar los perfiles de producto correctos a todos los demás tipos de usuarios dentro de la organización.


**Consulte también**

* [Traducir recursos](/help/assets/translate-assets.md)
* [API HTTP de recursos](/help/assets/mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](/help/assets/file-format-support.md)
* [Buscar recursos](/help/assets/search-assets.md)
* [Recursos de red](/help/assets/use-assets-across-connected-assets-instances.md)
* [Informes de recurso](/help/assets/asset-reports.md)
* [Esquemas de metadatos](/help/assets/metadata-schemas.md)
* [Descarga de recursos](/help/assets/download-assets-from-aem.md)
* [Administración de metadatos](/help/assets/manage-metadata.md)
* [Administración de plantillas de Dynamic Media](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [Administrar informes](/help/assets/manage-reports-assets-view.md)
* [Facetas de búsqueda](/help/assets/search-facets.md)
* [Administrar colecciones](/help/assets/manage-collections.md)
* [Importación masiva de metadatos](/help/assets/metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

