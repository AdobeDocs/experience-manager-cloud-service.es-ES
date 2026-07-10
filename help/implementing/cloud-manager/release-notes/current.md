---
title: Notas de la versión de Cloud Manager 2026.7.0
description: Obtenga información acerca de la versión de Cloud Manager 2026.7.0 en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: dea8a3df29876df1c97454a97602045eb50121ad
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---

# Notas de la versión de Cloud Manager 2026.7.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Obtenga información acerca de la versión de Cloud Manager 2026.7.0 en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2026.7.0 en AEM as a Cloud Service es el jueves, 9 de julio de 2026.

La próxima versión planificada es el jueves, 6 de agosto de 2026.


## Nuevas funciones: Cloud Manager {#cloud-manager-whats-new}

* **Traer su propio Git (BYOG): autenticación basada en secretos para el clon de Git**

  Ahora puede autenticar solicitudes de clonación de Git en el repositorio [!DNL Bring Your Own Git] mediante el secreto byogit que Cloud Manager genera, además de un token de IMS. Esta funcionalidad permite que [!DNL Edge Delivery Services] clientes usen las mismas credenciales que hélice-admin ya almacena para la sincronización de código. Los flujos de trabajo de clonación autenticados por IMS existentes no se ven afectados.

  Consulte [Autenticar solicitudes de clonación de Git](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md#authenticate-git-clone-requests).

* **Infraestructura de red VPN: enrutamiento BGP y conexiones múltiples**\
  La API de infraestructura de red VPN de redes avanzadas ahora admite el enrutamiento dinámico BGP (Border Gateway Protocol) junto con el enrutamiento estático existente. Los equipos pueden configurar BGP por conexión proporcionando el número de sistema autónomo BGP del lado del cliente y la dirección de intercambio entre pares; Cloud Manager gestiona el aprendizaje de rutas dinámicamente, no se requieren prefijos estáticos.

  También se ha eliminado el límite anterior de una conexión VPN por infraestructura. Ahora se admiten varias conexiones dentro de la misma infraestructura, y las conexiones estáticas y BGP pueden coexistir. Esto proporciona a los equipos de red empresarial más flexibilidad al diseñar topologías de VPN para entornos de AEM Cloud Service.

* **Rendimiento de compilación mejorado con almacenamiento en caché de módulos**
Un nuevo modelo de compilación compila solo los módulos modificados (en lugar de todo el repositorio) mediante el almacenamiento en caché de nivel de módulo para mejorar el rendimiento de la compilación. Se aplica a las canalizaciones de producción. Usted controla qué canalizaciones de producción utilizan **Smart Build**.

  Para obtener más información, consulte lo siguiente:

   * [Acerca del uso de Smart Build en una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build) y [Acerca del uso de Smart Build en una canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build-non-production-pipeline)
   * [Agregar una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code) y [Agregar una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#configuring-non-production-pipelines).

* **Copia de contenido: flujo de reenvío y entre programas**\
  Cloud Manager **Content Copy**, que permite a los equipos copiar contenido entre entornos de AEM sin una implementación, incluye dos funcionalidades disponibles para todos los programas. La compatibilidad entre programas permite copiar contenido en diferentes programas de Cloud Manager, no solo dentro del mismo programa. El Flujo de avance elimina la restricción direccional, lo que permite copiar el contenido de cualquier entorno a cualquier otro, incluso desde entornos más bajos hacia arriba.


## Programas Beta {#private-beta-program}

Para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general, puede participar en los programas beta de Cloud Manager.

>[!IMPORTANT]
>
>Las versiones de Beta contienen defectos y se proporcionan &quot;TAL CUAL&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o admitir de otro modo las versiones beta. Los clientes utilizan las versiones beta por su cuenta y riesgo; no confíe en el funcionamiento ni el rendimiento correctos de las versiones beta ni en la documentación o los materiales adjuntos. Las funciones y las API de la versión beta están sujetas a cambios sin previo aviso. Cualquier uso de las versiones beta corre por cuenta y riesgo del cliente.

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

Para unirte a la versión beta, envía un correo electrónico a [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) con tu identificador de organización de Adobe y tu identificador de programa.

<!-- 
OLD
### Improved build performance with module caching {#quick-build-cm-pipelines}

A new build model compiles only changed modules (rather than the entire repository) using module-level caching to improve build performance. It applies to production pipelines. You control which production pipelines use **Smart Build**.

For more information, see the following:

* [Using Smart Build in a production pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build).
* [Add a production pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

To join the Beta, email [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) with your Adobe Organization ID and Program ID.

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

* Los créditos principales no se liberan cuando ambos entornos de prod-group completan la eliminación suave simultáneamente. Este problema se ha resuelto. Los créditos ahora se liberan correctamente independientemente del orden en que se completen las eliminaciones simultáneas. (CMGR-77845)

* Crédito de Content Hub huérfano después de la eliminación suave del entorno seguido de la eliminación grave. Cloud Manager ahora libera correctamente el crédito de Content Hub cuando el entorno asociado se elimina completamente. (CMGR-77585)

* el comando CLI aio cloudmanager:tail-log se desconecta durante la rotación del registro en lugar de volver a conectarse. El comando ahora se vuelve a conectar automáticamente cuando se detecta una rotación de registro. (CMGR-76557)

* El contenido del cuadro de diálogo de lanzamiento completo no se puede desplazar en Información general del programa. El cuadro de diálogo ahora se desplaza correctamente, lo que garantiza que se pueda acceder a todo el contenido independientemente del tamaño de la pantalla. (CMGR-76405)

* La asignación de dominios personalizados falla en los entornos RDE recién creados. Después de crear un nuevo Entorno de desarrollo rápido (RDE), los clientes encontraron el error &quot;El estado del entorno no es válido para el cambio de configuración del dominio&quot; al intentar agregar una asignación de dominio personalizada inmediatamente después del aprovisionamiento.Ahora, Cloud Manager refleja correctamente el estado listo del entorno antes de intentar cualquier asignación de dominio. (CMGR-75904)

* Al eliminar un certificado DV y volver a crearlo para el mismo dominio, se produce el error &quot;certificado existente&quot;. Cuando los clientes eliminaban un certificado validado por el dominio (DV) y luego intentaban crear uno nuevo para el mismo dominio, Cloud Manager devolvía el error &quot;Hay un certificado existente que cubre todos los dominios&quot;. Como resultado, bloqueó la emisión del nuevo certificado. La eliminación parecía correcta en la interfaz de usuario, pero el certificado no se eliminó completamente internamente, lo que dejó bloqueado el dominio. Este problema ya está resuelto. (CMGR-72784)

<!-- There are no significant bug fixes in the July 2026 Cloud Manager release. -->

<!-- ## Known issues {#known-issues} -->

