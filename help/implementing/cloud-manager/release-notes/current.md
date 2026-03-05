---
title: Notas de la versión 2026.3.0 de Cloud Manager
description: Obtenga información sobre la versión 2026.3.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: eb3e826e27e14b8b1da534440f11d43e973130ec
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 23%

---

# Notas de la versión 2026.3.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Obtenga información sobre la versión 2026.3.0 de Cloud Manager en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2026.3.0 en AEM as a Cloud Service es el viernes, 05 de marzo de 2026.

La próxima versión planificada es para el viernes, 02 de abril de 2026.


## Novedades: Cloud Manager (en inglés) {#cloud-manager-whats-new}

* **Cloud Manager ahora admite la opción** Borrar **para las importaciones de** Copia de contenido ****

  Cuando se habilita **Borrar**, Cloud Manager elimina el contenido existente en el destino antes de iniciar la importación, por lo que puede empezar desde una pizarra limpia y evitar conflictos con el contenido preexistente. Si deja **Borrar** deshabilitado, Cloud Manager importa el nuevo contenido sobre el contenido de destino existente. Aparece un mensaje de confirmación antes de que comience el borrado y Cloud Manager registra la acción de borrado y los detalles de importación para rastrear.

  Ver también [Copiar contenido](/help/implementing/developing/tools/content-copy.md#copy-content).

* **Compatibilidad con la extensibilidad de la IU en AEM Experience Hub**
Ya está habilitada la compatibilidad con las extensiones de IU en [AEM Experience Hub](https://experience.adobe.com/experiencemanager), lo que permite a los desarrolladores ampliar la interfaz con funcionalidad y widgets personalizados creados con Adobe App Builder.

  Para obtener más información, consulta [AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/).

* **Mayor estabilidad, rendimiento y confiabilidad**

  Esta versión incluye actualizaciones de optimización y mantenimiento que mejoraron la estabilidad, el rendimiento y la fiabilidad de Cloud Manager.


## Programas Beta {#private-beta-program}

Participe en los programas Beta de Cloud Manager para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general.

>[!IMPORTANT]
>
>Las versiones de Beta pueden contener defectos y se proporcionan &quot;TAL CUAL&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o admitir de otro modo (mediante los Servicios de soporte de Adobe o de otro modo) las versiones beta. Adobe recomienda a los clientes tener cuidado y no depender del funcionamiento o el rendimiento correctos de las versiones beta, ni de la documentación o los materiales adjuntos. Las funciones y las API de la versión beta están sujetas a cambios sin previo aviso. Por lo tanto, cualquier uso de las versiones beta es totalmente bajo el propio riesgo del cliente.

Ver también [programas de AEM Beta](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

Actualmente están disponibles las siguientes oportunidades:
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Servidor MCP de Cloud Manager para IDE con tecnología IA{#mcp-server-for-cm}

Ahora puede probar un servidor MCP (Model Context Protocol) que expone las API públicas de Cloud Manager como herramientas para IDE habilitados para IA (como Cursor). Después de conectarlo, puede utilizar mensajes conversacionales para enumerar y administrar programas, canalizaciones, entornos y repositorios, lo que le ayuda a moverse más rápido sin salir del editor.

Consulte la documentación [Usar MCP con AEM as a Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

Consulte el tutorial [Servidor MCP de Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-server/cloud-manager#).

¿Le interesa la versión Beta? Envíe un correo electrónico a [GRP-AEM-CM-MCP-FEEDBACK@adobe.com](mailto:GRP-AEM-CM-MCP-FEEDBACK@adobe.com) con su identificador de organización de Adobe y el identificador de programa.


<!--
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

### Compilaciones más rápidas con almacenamiento en caché de módulos {#quick-build-cm-pipelines}

Un nuevo modelo de compilación solo compila los módulos modificados (en lugar de todo el repositorio) mediante el almacenamiento en caché a nivel de módulo para acortar los tiempos de compilación. Se aplica a las canalizaciones de calidad de código, de pila completa y de solo ensayo.

![Editar canalización que no sea de producción en el cuadro de diálogo que muestra las dos opciones de Estrategia de compilación que son Versión completa y Versión inteligente](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*Editar canalización que no sea de producción en el cuadro de diálogo que muestra las dos opciones de estrategia de compilación, compilación completa y compilación inteligente.*

En el cuadro de diálogo **Agregar o editar canalización**, en la ficha **Código Source**, una nueva sección de **Estrategia de compilación** le permite elegir una de las siguientes opciones de compilación:

* **Compilación completa**: genera todos los módulos del repositorio en cada ejecución.
* **Compilación inteligente**: genera solo módulos que han cambiado desde la última confirmación, lo que acorta el tiempo de compilación general.

Usted controla qué canalizaciones utilizan **Smart Build**. Durante la versión beta, esta opción solo aparece para las canalizaciones **Calidad del código** y **Implementación de desarrolladores**.

¿Le interesa? Envíe un correo electrónico a [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) con su identificador de organización de Adobe y el identificador de programa.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

## Correcciones de errores {#bug-fixes}

* Se ha resuelto un problema en el cual la API de puntos de restauración podía devolver un error 500 al recuperar los puntos de restauración. El punto de conexión ahora gestiona correctamente los valores nulos, lo que garantiza respuestas coherentes y fiables. (CMGR-72963)
* Cloud Manager ahora acepta direcciones URL del repositorio de GitHub con o sin el sufijo `.git`, lo que alinea el comportamiento de la API con la interfaz de usuario y hace que la incorporación al repositorio sea más flexible. (CMGR-73296)
* La validación de nombres de perfil de producto ahora no distingue entre mayúsculas y minúsculas, lo que evita errores al crear perfiles con nombres que solo difieren en el uso de mayúsculas y minúsculas. (CMGR-74075)
* Ahora puede realizar varias operaciones de restauración desde la misma ejecución de la canalización, lo que permite realizar restauraciones secuenciales para entornos como Ensayo y Producción sin necesidad de ejecutar una nueva canalización. (CMGR-73538)


<!-- ## Known issues {#known-issues} -->

