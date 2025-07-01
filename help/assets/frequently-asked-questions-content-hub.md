---
title: Preguntas frecuentes (FAQ) sobre Content Hub
description: Obtenga respuestas a algunas de las preguntas más frecuentes (FAQ) sobre Content Hub.
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: 31c9e742d8bdf69c12788794670817864c9c027a
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 98%

---

# Preguntas frecuentes sobre Content Hub {#content-hub-frequently-asked-questions}

![Preguntas frecuentes sobre Content Hub](assets/content-hub-faqs.png)

## ¿Qué es Content Hub? {#what-is-content-hub}

Content Hub es una función de Adobe Experience Manager Assets as a Cloud Service.

Content Hub permite a equipos no especializados descubrir fácilmente recursos aprobados relevantes a través de un portal intuitivo y adaptarlos rápidamente a sus necesidades.  Además, Content Hub proporciona un mecanismo de ingesta que permite a esos usuarios autoabastecerse fácilmente a medida que cargan recursos en DAM. Esto satisface directamente la necesidad que tienen las organizaciones de una mayor velocidad de creación de contenido, al tiempo que preserva la uniformidad de la marca y el cumplimiento de las medidas de seguridad adecuadas.

## ¿Por qué no puedo habilitar Content Hub en mi programa o entorno de Cloud Manager? {#cannot-enable-content-hub}

En este momento, Content Hub solo está disponible en programas de producción de AEM Cloud Manager que incluyan una licencia de Assets (Assets Cloud Service, Assets Ultimate, Assets Prime). Al hacer clic en [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) para habilitarlo, se implementa y se asocia con el entorno de producción de creación de AEM en ese programa. Consulte [Implementar Content Hub](/help/assets/deploy-content-hub.md) para ver los detalles y los requisitos previos.

## Si he habilitado Content Hub en mi programa o entorno de producción, ¿puedo deshabilitarlo? {#can-i-disable-content-hub}

Al habilitar Content Hub en un programa de producción, se implementa como parte de la infraestructura de producción. AEM Cloud Manager no permite eliminar ni deshabilitar la infraestructura de producción para minimizar el riesgo de uso de la producción por errores humanos.

Si no desea proporcionar Content Hub a los usuarios una vez implementado, no asigne ningún usuario al perfil de producto de Content Hub en Admin Console. Consulte [Implementar Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) para obtener más información.

## ¿Cómo puedo evaluar Content Hub en mi organización, si solo está disponible para programas de producción o entornos de creación de producción? {#how-can-i-evaluate-content-hub}

Content Hub es una función que Adobe proporciona y mantiene, y no tiene ningún código personalizado que requiera una validación típica mediante desarrollo, ensayo o producción. Además, el acceso a la función para los usuarios está completamente controlado por el administrador, por lo que puede evaluarla sin exponerla a todos los usuarios.

Es posible evaluar Content Hub sin afectar a los usuarios ni al contenido de producción administrado en AEM as a Cloud Service Assets. El procedimiento de evaluación podría ser el siguiente:

* [Habilitar Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) en el entorno de producción (programa de Cloud Manager)
* [Añada un usuario administrador de AEM](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) del autor de producción al perfil de producto de Content Hub.
* El administrador de AEM [configura Content Hub](/help/assets/configure-content-hub-ui-options.md)
* El administrador de AEM o un usuario de AEM en el autor de producción de AEM [aprueba una serie de recursos para Content Hub](/help/assets/approve-assets-content-hub.md); si no desea modificar ningún contenido de producción en DAM, puede crear una carpeta de evaluación independiente en la instancia de autor de AEM y cargar/etiquetar o copiar en ella algunos recursos de DAM.
* El administrador de Admin Console añade [algunos usuarios seleccionados](/help/assets/deploy-content-hub.md#onboard-content-hub-users) al perfil de producto de Content Hub para que puedan iniciar la evaluación.
* Una vez finalizada la evaluación, los usuarios de AEM en la instancia de autor pueden eliminar la aprobación de los recursos de prueba, aprobar los recursos de producción para Content Hub y, a continuación, el administrador de Admin Console puede añadir a todos los usuarios que necesiten acceder a Content Hub y al contenido aprobado. Enhorabuena, Content Hub ya está activo.

Hay un programa de acceso rápido a Content Hub en los programas de zona protegida y sus entornos de producción de creación. Para más información, consulte [Introducción a los programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Para obtener más información sobre el programa de acceso anticipado, póngase en contacto con el equipo de cuentas de Adobe.

Content Hub aún no está disponible en entornos que no sean de producción (ensayo y desarrollo). La disponibilidad prevista en los entornos de ensayo/desarrollo de Assets Ultimate es marzo de 2025.

## ¿Por qué no veo ningún recurso después de iniciar sesión en Content Hub? {#no-assets-in-content-hub}

Los recursos marcados como aprobados en Assets as a Cloud Service están disponibles automáticamente en Content Hub. Si no puede ver ningún recurso después de iniciar sesión en Content Hub, apruebe los recursos mediante el entorno de creación de AEM as a Cloud Service para que estén disponibles en Content Hub. Para obtener más información, consulte [Aprobar recursos para Content Hub](/help/assets/approve-assets-content-hub.md).

## ¿Por qué no veo los recursos que subo directamente utilizando Content Hub o que importo desde cuentas de Dropbox o OneDrive mediante Content Hub? {#no-assets-uploaded-from-content-hub}

La visualización de los recursos cargados mediante Content Hub depende de si ha habilitado la opción [Aprobación automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) disponible en la interfaz de usuario de configuración:

* Si la opción **Aprobación automática** está habilitada, los recursos que cargue mediante Content Hub estarán disponibles automáticamente.

* Si la opción **Aprobación automática** está deshabilitada, los recursos que cargue mediante Content Hub no se mostrarán automáticamente. Los recursos están disponibles en la carpeta `hydrated-assets` de su entorno de Assets as a Cloud Service. Vaya a la carpeta y [edite en lotes](/help/assets/approve-assets-content-hub.md) el estado de esos recursos a `Approved` para que se muestren en Content Hub.

## ¿Cómo encontrar rápidamente recursos cargados con Content Hub en el entorno de AEM as a Cloud Service? {#find-uploaded-assets-on-aem-cloud}

Para encontrar rápidamente recursos cargados con Content Hub en el entorno de AEM as a Cloud Service, haga lo siguiente:

1. Vaya hasta la carpeta `hydrated-assets`. 

1. Haga clic en **[!UICONTROL Filtros]** y establezca **[!UICONTROL No hay estado]** en el campo **[!UICONTROL Estado del recurso]**.

1. Ordene recursos usando el campo **[!UICONTROL Fecha de modificación]**.

## ¿Por qué no veo la opción Editar mediante Adobe Express en mi tarjeta de recursos para poder versionar recursos y crear nuevas variaciones? {#edit-using-express-not-available}

Para ver la opción **Editar mediante Adobe Express** en la tarjeta de recursos, debe tener derechos de Adobe Express Enterprise (consulte los [planes](https://www.adobe.com/express/pricing)) además de privilegios de [usuarios de Content Hub con derechos para versionar recursos en nuevas variaciones](#onboard-content-hub-users-add-assets).

Hay algunas configuraciones sobre cómo se asignan los usuarios a [!DNL Content Hub] y [!DNL Adobe Express]:

1. La organización tiene la licencia de [Assets Ultimate](/help/assets/assets-ultimate-overview.md) o [Assets Prime](/help/assets/assets-prime.md), y al usuario se le asigna uno de los perfiles de Experience Manager en Admin Console que incluyen derechos de Adobe Express (colaborador o usuario avanzado). La integración funciona sin ninguna configuración adicional.

1. [!DNL Adobe Express] se implementa en la misma [!DNL Adobe Admin Console] que [!DNL Experience Manager Assets] con [!DNL Content Hub]. La integración funciona sin ninguna configuración adicional.

1. [!DNL Adobe Express] se implementado en una [!DNL Adobe Admin Console] diferente a [!DNL Experience Manager Assets] con [!DNL Content Hub]. En este caso, el administrador de [!DNL Assets] puede configurar la integración (consulte la [documentación](/help/assets/connect-assets-with-creative-cloud.md)) para que funcione.

   >[!NOTE]
   >
   >El usuario asignado a los perfiles de producto Express y Assets en dos Admin Consoles necesita tener la misma dirección de correo electrónico y usar una cuenta de empresa **Enterprise o School**, y no la cuenta **Personal**. La configuración ideal es tener ambas Admin Consoles configuradas como **Federated ID** con una relación de confianza configurada entre ellas, de modo que el usuario tenga una experiencia de inicio de sesión único sin problemas. Algunos de los planes Express (por ejemplo, Equipos Express) no admiten el inicio de sesión único/Federated ID.

Además de las autorizaciones de producto adecuadas, la integración de Adobe Express en Content Hub requiere que el usuario asignado tenga al menos permisos [!UICONTROL Puede editar] en el entorno de creación de Assets que alimenta Content Hub, en al menos la jerarquía de carpetas **[!UICONTROL # /content/dam/hydroloaded-assets/]**, en la que los usuarios de Content Hub pueden guardar el contenido que han creado mediante Express. Consulte [Administración de permisos](/help/security/touch-ui-principal-view.md) en la vista de administración (IU táctil) o la [administración de permisos simplificada en la vista de recursos](https://experienceleague.adobe.com/es/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

## ¿Puedo configurar Content Hub para que las directrices de marca de mi organización se muestren como un vínculo en la página de inicio? {#content-hub-setup-brand-guidelines}

Puede añadir vínculos personalizados como pestañas independientes además de las pestañas estándar Todos los recursos, Colecciones e Información en la página de inicio de Content Hub. Para obtener información sobre cómo configurarlos, consulte [Vínculos personalizados](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## ¿Hay algún plan de migración de los clientes existentes de Brand Portal a Content Hub? {#migration-brand-portal}

Adobe proporciona asistencia para la migración del Brand Portal a Content Hub que puede solicitar creando un vale de asistencia de Adobe.

## ¿Por qué no puedo ver la opción de ajustes/configuración del producto en Content Hub? {#ui-configuration-option-missing}

Para acceder a la [interfaz de usuario de configuración](/help/assets/configure-content-hub-ui-options.md), debes ser [administrador de Content Hub](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator). Si se le asigna el perfil de producto de administradores de AEM en la instancia de creación de producción en Adobe Admin Console y sigue sin poder ver la opción de configuración, asegúrese de que no se haya cambiado el nombre del perfil de producto de administradores de AEM. Consulte [Perfiles de equipo y producto de AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) para obtener más información.
