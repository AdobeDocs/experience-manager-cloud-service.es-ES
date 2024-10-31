---
title: Preguntas más frecuentes (FAQ) de Content Hub
description: Obtenga respuestas a algunas de las preguntas más frecuentes (FAQ) de Content Hub.
source-git-commit: 3b8a80e346fe63450f9b57733c67de2e4b52b2b8
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 1%

---

# Preguntas frecuentes sobre Content Hub {#content-hub-frequently-asked-questions}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Pregunta frecuente de Content Hub](assets/content-hub-faqs.png)

## ¿Qué es Content Hub? {#what-is-content-hub}

Content Hub es una función de Adobe Experience Manager Assets as a Cloud Service.

Content Hub permite a equipos más amplios descubrir fácilmente recursos relevantes y aprobados a través de un portal intuitivo y adaptarlos rápidamente a sus necesidades.  Además, Content Hub proporciona un mecanismo de ingesta que permite a esos usuarios autoabastecerse fácilmente a medida que cargan recursos en DAM. Esto satisface directamente la necesidad que tienen las organizaciones de una mayor velocidad de creación de contenido, al tiempo que preserva la coherencia de la marca y el cumplimiento de las salvaguardias adecuadas.

## ¿Por qué no puedo habilitar Content Hub en mi programa o entorno de Cloud Manager? {#cannot-enable-content-hub}

En este momento, Content Hub solo está disponible en programas de producción de AEM Cloud Manager, que incluyen una licencia de Assets. Al hacer clic en [Content Hub AEM](/help/assets/deploy-content-hub.md#enable-content-hub) para habilitarlo, se implementa y se asocia con el entorno de producción de autor de los de ese programa. Consulte [Implementar Content Hub](/help/assets/deploy-content-hub.md) para obtener detalles y requisitos previos.

Hay un programa de acceso anticipado a Content Hub en programas de zona protegida/entornos de producción de creación. Para obtener más información, consulte [Introducción a los programas de espacio aislado](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Para obtener más información sobre el programa de acceso anticipado, póngase en contacto con el equipo de la cuenta de Adobe.

Content Hub no está disponible para entornos que no sean de producción (fase, desarrollo, etc.) en esta fase.

## Si he habilitado Content Hub en mi programa o entorno de producción, ¿puedo deshabilitarlo? {#can-i-disable-content-hub}

Al habilitar Content Hub en un programa de producción, se implementa como parte de la infraestructura de producción. AEM Cloud Manager no permite eliminar ni deshabilitar la infraestructura de producción para minimizar el riesgo de que los errores humanos utilicen la producción.

Si no desea proporcionar Content Hub a los usuarios una vez implementado, no asigne ningún usuario al perfil de producto de Content Hub en Admin Console. Consulte [Implementar Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) para obtener más información.

## ¿Cómo puedo evaluar Content Hub en mi organización, ya que solo está disponible para programas de producción/entornos de creación de producción? {#how-can-i-evaluate-content-hub}

Content Hub es una función que Adobe proporciona y mantiene y no tiene ningún código personalizado que requiera una validación típica mediante desarrollo, fase o producción. Además, el acceso a la función para los usuarios está completamente controlado por el administrador, por lo que puede evaluarla sin exponerla a todos los usuarios.

Es posible evaluar Content Hub sin afectar a los usuarios ni al contenido de producción administrado en AEM as a Cloud Service Assets. Un procedimiento de evaluación podría tener este aspecto:

* [Habilitar Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) en el entorno de producción (programa Cloud Manager)
* AEM [Agregue un usuario administrador de la](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) del autor de la producción al perfil de producto de Content Hub.
* AEM El administrador de [configura Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM AEM AEM El administrador de la aplicación o un usuario de la aplicación en la creación de producción [aprueba un número de recursos para Content Hub AEM](/help/assets/approve-assets-content-hub.md); si no desea cambiar ningún contenido de producción en DAM, puede crear una carpeta de evaluación independiente en la instancia de autor de la aplicación y cargar/etiquetar o copiar algunos recursos de DAM en ella.
* El administrador de Admin Console agrega [algunos usuarios seleccionados](/help/assets/deploy-content-hub.md#onboard-content-hub-users) al perfil de producto de Content Hub para que puedan iniciar la evaluación.
* AEM Una vez finalizada la evaluación, los usuarios de la instancia de autor pueden quitar la aprobación de los recursos de prueba, aprobar los recursos de producción para Content Hub y, a continuación, el Admin Console puede agregar todos los usuarios que necesiten acceso a Content Hub y contenido aprobado. Enhorabuena, su Content Hub ya está activo.

Adobe también ofrece un programa de acceso anticipado a Content Hub en entornos de ensayo. Consulte la pregunta [¿Por qué no puedo habilitar Content Hub en mi programa o entorno de Cloud Manager?](#cannot-enable-content-hub) para obtener detalles.

## ¿Por qué no veo ningún recurso después de iniciar sesión en Content Hub? {#no-assets-in-content-hub}

Los recursos marcados como aprobados en Assets as a Cloud Service están disponibles automáticamente en Content Hub. Si no puede ver ningún recurso después de iniciar sesión en Content Hub, apruebe los recursos mediante el entorno de creación de AEM as a Cloud Service para que estén disponibles en Content Hub. Para obtener más información, consulte [Aprobar recursos para Content Hub](/help/assets/approve-assets-content-hub.md).

## ¿Por qué no veo mis recursos que subo directamente mediante Content Hub o los importo desde cuentas de Dropbox o OneDrive mediante Content Hub? {#no-assets-uploaded-from-content-hub}

La visualización de los recursos cargados mediante Content Hub depende de si ha habilitado la opción [Aprobación automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) disponible en la interfaz de usuario de Configuración:

* Si la opción **Aprobación automática** está habilitada, los recursos que cargue mediante Content Hub estarán disponibles automáticamente.

* Si la opción **Aprobación automática** está deshabilitada, los recursos que cargue mediante Content Hub no se mostrarán automáticamente. Los recursos están disponibles en la carpeta `hydrated-assets` de su entorno as a Cloud Service de Assets. Vaya a la carpeta y [edite en lotes](/help/assets/approve-assets-content-hub.md) el estado de esos recursos a `Approved` para que esos recursos se muestren en Content Hub.

## ¿Cómo encontrar rápidamente recursos cargados con Content Hub en el entorno de AEM as a Cloud Service? {#find-uploaded-assets-on-aem-cloud}

Para encontrar rápidamente recursos cargados con Content Hub en el entorno de AEM as a Cloud Service, haga lo siguiente:

1. Navegando a la carpeta `hydrated-assets`.

1. Haciendo clic en **[!UICONTROL Filtros]** y configurando **[!UICONTROL No hay estado]** en el campo **[!UICONTROL Estado del recurso]**.

1. Ordenando recursos usando el campo **[!UICONTROL Fecha de modificación]**.

## ¿Por qué no veo la opción Editar usando el Adobe Express en mi tarjeta de recursos para poder remezclar recursos y crear nuevas variaciones? {#edit-using-express-not-available}

Para ver la opción de edición mediante Adobe Express en la tarjeta de recursos, debe tener derechos de Adobe Express además de privilegios para [usuarios de Content Hub con derechos para remezclar recursos a nuevas variaciones](#onboard-content-hub-users-add-assets). El Adobe Express debe implementarse en la misma organización de Admin Console de Adobe en la que está implementado Adobe Experience Manager.

## ¿Puedo configurar Content Hub para que las directrices de marca de mi organización se muestren como un vínculo en la página principal? {#content-hub-setup-brand-guidelines}

Puede agregar vínculos personalizados como pestañas independientes además de las pestañas estándar Todos los Assets, Colecciones e Información en la página principal de Content Hub. Para obtener información sobre cómo configurarlo, consulte [Vínculos personalizados](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## ¿Hay algún plan para migrar a Content Hub a los clientes de Brand Portal existentes? {#migration-brand-portal}

Adobe proporciona compatibilidad de migración de Brand Portal a Content Hub que puede utilizar creando un vale de soporte de Adobe.

## ¿Por qué no puedo ver la opción Configuración/configuración del producto en Content Hub? {#ui-configuration-option-missing}

Para acceder a la [interfaz de usuario de configuración](/help/assets/configure-content-hub-ui-options.md), debes ser [administrador de Content Hub](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator). AEM Si se le asigna el perfil de producto Administradores de en la instancia de creación de producción de Adobe Admin Console AEM y sigue sin poder ver la opción de configuración, asegúrese de que no se haya cambiado el nombre del perfil de producto Administradores de la aplicación de producción. Consulte [Perfiles de equipo y producto de AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) para obtener más información.


