---
title: Notas de la versión de Cloud Manager 2026.6.0
description: Obtenga información acerca de la versión de Cloud Manager 2026.6.0 en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 61101046e4383acb534b04f467bef1b0313c4ef5
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 4%

---

# Notas de la versión de Cloud Manager 2026.6.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- 
https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release 
-->

Obtenga información acerca de la versión de Cloud Manager 2026.6.0 en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2026.6.0 en AEM as a Cloud Service es el jueves, 4 de junio de 2026.

La próxima versión planificada es el jueves, 9 de julio de 2026.


## Novedades: Cloud Manager (en inglés) {#cloud-manager-whats-new}

* **Autoservicio de claves administradas por el cliente (CMK)**
Los clientes ahora pueden configurar las claves administradas por el cliente directamente desde Cloud Manager, sin necesidad de que intervenga la asistencia de Adobe. Hay una nueva opción CMK disponible durante la creación del programa, en la configuración de edición del programa y en la página Detalles del entorno.

  El estado de CMK se muestra en las tarjetas de Mis programas y en el panel de licencias, lo que proporciona a los administradores una visibilidad clara de la configuración de cifrado en todos los entornos. Este método simplifica los flujos de trabajo de conformidad para las organizaciones que requieren control sobre sus propias claves de cifrado.

  ![Tarjeta de Mis programas que muestra un icono de clave administrada por el cliente](/help/implementing/cloud-manager/release-notes/assets/cmk-status-on-program-card.png)
  *Tarjeta de Mis programas*


  ![Cuadro de diálogo Configurar para producción que muestra la ficha Seguridad con la opción Claves administradas por el cliente seleccionada](/help/implementing/cloud-manager/release-notes/assets/cmk-security-tab-in-set-up-for-production-dlg.png)
  *Claves administradas por el cliente seleccionadas en la ficha Seguridad del cuadro de diálogo Configurar para producción*

  ![Mostrando el número de claves gestionadas por el cliente disponibles en el tablero de licencias](/help/implementing/cloud-manager/release-notes/assets/cmk-license-dashboard.png)
  *Mostrando el número de claves gestionadas por el cliente disponibles en el tablero de licencias*

* **Límite de variable de entorno aumentado a 400**
Cloud Manager ahora admite hasta 400 variables de entorno por entorno, el doble del límite anterior de 200.

  Las variables de canalización siguen restringidas a 200. La interfaz de usuario aplica el límite correcto por contexto e impide que se agreguen elementos más allá del umbral permitido.

  Este cambio es compatible con clientes con configuraciones de implementación más complejas que requieren un mayor número de configuraciones específicas del entorno.

<!--CMGR-76755 · CMGR-76753 -->


## Programas Beta {#private-beta-program}

Para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general, puede participar en los programas beta de Cloud Manager.

>[!IMPORTANT]
>
>Las versiones de Beta contienen defectos y se proporcionan &quot;TAL CUAL&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o admitir de otro modo las versiones beta. Los clientes utilizan las versiones beta por su cuenta y riesgo, y no deben confiar en el funcionamiento o el rendimiento correctos de las versiones beta ni en la documentación o los materiales adjuntos. Las funciones y las API de la versión beta están sujetas a cambios sin previo aviso. Cualquier uso de las versiones beta corre por cuenta y riesgo del cliente.

Ver también [programas de AEM Beta](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

Actualmente están disponibles las siguientes oportunidades del programa beta:

### Edge Delivery Services con AEM Authoring y configuración flexible del nivel de publicación {#eds-with-aem-authoring}

Cloud Manager presenta dos funciones diseñadas para admitir arquitecturas de envío modernas.

* **Edge Delivery Services con AEM Authoring**
Ahora puede enviar sitios mediante Edge Delivery Services sin dejar de crear contenido en el modo de autor de AEM. Según las preferencias del flujo de trabajo, puede elegir entre los siguientes métodos de creación:

   * Creación basada en documentos
   * Creación basada en AEM

Para obtener más información, consulte [Crear un sitio de Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site).

* **Configuración flexible del nivel de publicación**

Cloud Manager ahora le permite configurar si se requiere un nivel de publicación para su programa. Esta flexibilidad le permite configurar entornos que se adapten mejor a la arquitectura de entrega elegida.

Para obtener más información, consulte [Nivel de publicación flexible (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).

Para unirte a Beta, envía un correo electrónico a [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) con tu ID de organización de Adobe y tu ID de programa.

### Compilaciones más rápidas con almacenamiento en caché de módulos {#quick-build-cm-pipelines}

Un nuevo modelo de compilación compila solo los módulos modificados (en lugar de todo el repositorio) mediante el almacenamiento en caché de nivel de módulo para reducir los tiempos de compilación. Se aplica a las canalizaciones de producción. Usted controla qué canalizaciones de producción utilizan **Smart Build**.

Para obtener más información, consulte lo siguiente:

* [Usando Smart Build en una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build).
* [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

Para unirte a Beta, envía un correo electrónico a [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) con tu ID de organización de Adobe y tu ID de programa.

<!-- 
OLD
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

<!-- 
OLD
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.
-->



## Correcciones de errores {#bug-fixes}

* **Entorno bloqueado en la actualización sin una operación activa**
Ahora se resuelve un problema en el que los entornos se quedan permanentemente atascados en un estado de actualización, incluso cuando no se ejecuta ninguna canalización o cambio de configuración en curso. Los entornos afectados ahora se pueden administrar con normalidad sin requerir la intervención manual del soporte de Adobe. (CMGR-77133)
* **Redes avanzadas: se eliminó una regla de reenvío de puerto incorrecta en los puertos de origen duplicados**
Cuando dos reglas de reenvío de puertos en Redes avanzadas comparten el mismo puerto de origen (portOrig), al eliminar una regla se elimina incorrectamente la otra. Ahora Cloud Manager identifica correctamente y elimina solo la regla deseada. (CMGR-77019)

<!-- There are no significant bug fixes in the June 2026 Cloud Manager release. -->

<!-- ## Known issues {#known-issues} -->

