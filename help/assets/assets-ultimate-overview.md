---
title: Assets Ultimate
description: Obtenga más información sobre los aspectos clave de Assets Ultimate, como las ventajas clave, los tipos de usuarios y sus privilegios.
feature: Asset Management
role: User, Admin
exl-id: 3ae96cd2-e0ac-43a5-a0bf-bebb1a028b10
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 100%

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

Assets as a Cloud Service Ultimate le permite realizar varias operaciones clave de administración de recursos digitales, como las siguientes:

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
| **Capacidades** |
| Acceso a los recursos de marca aprobados en el portal de Content Hub | ✓ | ✓ | ✓ | ✓ |
| Crear y editar recursos mediante Adobe Express y Firefly integrados | − | ✓ | ✓ | ✓ |
| Integración de recursos en su organización con aplicaciones de Adobe y que no sean de Adobe | − | ✓ | ✓ | ✓ |
| Acceder a todas las funciones de AEM Assets, como administración de recursos, los metadatos y la gestión y automatización generales | − | − | ✓ | ✓ |
| Administración de permisos del contenido en el entorno de creación de AEM Assets | − | − | − | ✓ |
| **El usuario debe estar en estos perfiles de producto (Admin Console)** |
| AEM > Instancia de entrega > Usuarios limitados de AEM Assets | ✓ | ✓ | ✓ | ✓ |
| AEM > Instancia de autor de producción > Usuarios colaboradores de AEM Assets | − | ✓ | − | − |
| AEM > Instancia de autor de producción > Usuarios avanzados de AEM Assets | − | − | ✓ | − |
| AEM > Instancia de autor de producción > Administradores de AEM | − | − | − | ✓ |
| **Más información** | Consulte [Habilitar Content Hub](/help/assets/enable-assets-ultimate.md##enable-assets-ultimate-new-users) | Consulte [Incorporación de usuarios colaboradores](/help/assets/enable-assets-ultimate.md#onboard-collaborator-users) | Consulte [Incorporación de usuarios avanzados](/help/assets/enable-assets-ultimate.md#onboard-power-users) | - |

Para obtener información sobre cómo empezar a usar Assets Ultimate, consulte [Habilitar AEM Assets Ultimate](/help/assets/enable-assets-ultimate.md). Si los usuarios de AEM Assets existentes tienen dudas sobre cuándo pueden actualizar a Assets Ultimate, póngase en contacto con el representante de su cuenta de Adobe. También puede consultar [Habilitar Assets Ultimate para los clientes existentes](/help/assets/enable-assets-ultimate.md#enable-assets-ultimate-existing-customers) para obtener más información.

AEM Assets también proporcionan un DAM más ligero para los clientes que no tienen requisitos avanzados como, por ejemplo, extensibilidad de la interfaz de usuario, automatización impulsada por API e implementación de código personalizado. Para más información, consulte [AEM Assets Prime](/help/assets/assets-prime.md).
