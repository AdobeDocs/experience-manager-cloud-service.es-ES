---
title: Restringir la entrega de recursos en Experience Manager
description: Obtenga información sobre cómo restringir la entrega de recursos en [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Restringir el acceso a los recursos en [!DNL Experience Manager] {#restrict-access-to-assets}

La administración central de recursos en Experience Manager permite al administrador de DAM o a los administradores de marcas administrar el acceso a los recursos. Pueden restringir el acceso configurando funciones para los recursos aprobados en el lado de la creación, específicamente en la instancia de autor de AEM as a Cloud Service.

Usuarios [búsqueda](search-assets-api.md) o utilizando [URL de envío](deliver-assets-apis.md) puede obtener acceso a los recursos restringidos tras pasar correctamente el proceso de autorización.

![Acceso restringido a los recursos](/help/assets/assets/restricted-access.png)

## Envío restringido mediante un token de IMS {#restrict-delivery-ims-token}

En Experience Manager, la entrega restringida a través de IMS implica dos etapas clave:

* Creación
* Entrega

### Creación {#authoring}

Puede restringir la entrega de recursos en [!DNL Experience Manager] según las funciones. Para configurar las funciones, ejecute los siguientes pasos:

1. Vaya a la [!DNL Experience Manager] como administrador de DAM.
1. Seleccione el recurso para el que debe configurar la función.
1. Vaya a **[!UICONTROL Propiedades]** > **[!UICONTROL Avanzadas]**, y asegúrese de que las variables **[!UICONTROL Funciones]** el campo existe en [!UICONTROL Metadatos avanzados] pestaña.

   ![Metadatos de roles](/help/assets/assets/roles_metadata.jpg)
Si el campo no está disponible, siga estos pasos para agregar el campo:

   1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
   1. Seleccione el esquema de metadatos y haga clic en **[!UICONTROL Editar _(e)_]**.
   1. Añadir un **[!UICONTROL Texto con varios valores]** del campo **[!UICONTROL Generar formulario]** en el lado derecho a la sección Metadatos del formulario.
   1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en la  **[!UICONTROL Configuración]** panel:
      1. Cambie el **[!UICONTROL Etiqueta de campo]** hasta _Funciones_.
      1. Actualice el **[!UICONTROL Asignar a la propiedad]** hasta _./jcr:content/metadata/dam:roles_.

1. Obtenga los grupos de IMS que se agregarán en los metadatos de funciones del recurso. Para recuperar los grupos de IMS, siga estos pasos:
   1. Inicie sesión en https://adminconsole.adobe.com/.
   1. Vaya a su organización respectiva y navegue hasta **[!UICONTROL Grupos de usuarios]**.
   1. Seleccione el **[!UICONTROL Grupo de usuarios]** debe añadir y extraer el **[!UICONTROL orgID]** y **[!UICONTROL userGroupID]** desde la dirección URL o utilice su ID de organización como `{orgID}@AdobeOrg:{usergroupID}`.

1. Añadir el ID de grupo a **[!UICONTROL Funciones]** del campo Propiedades del recurso. <br>
Los ID de grupo definidos en la variable **[!UICONTROL Funciones]** son los únicos usuarios que pueden acceder al recurso. También puede añadir el ID de cliente de IMS y el ID de perfil de IMS en la **[!UICONTROL Funciones]** field. Por ejemplo, `{orgId}@AdobeOrg:{profileId}`.

   >[!NOTE]
   >
   >Para la nueva vista de Assets, solo puede dar acceso hasta el nivel de carpeta y exclusivamente a grupos en lugar de a usuarios individuales. Más información sobre [administración de permisos en Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### Restringir la entrega de recursos mediante Fecha y hora de activación y desactivación {#restrict-delivery-assets-date-time}

Los autores de DAM también pueden restringir la entrega de recursos definiendo un tiempo de activación o desactivación disponible en las propiedades del recurso.

Si define un Tiempo de activación para la activación de un recurso, se generará una URL de entrega para el recurso en el momento definido. El recurso permanece inactivo antes del tiempo definido. Del mismo modo, si define un Tiempo de inactividad para un recurso, este se desactiva en el momento definido y la URL de entrega del recurso deja de mostrar el recurso.

Ejecute los siguientes pasos para establecer el tiempo de activación y desactivación del recurso:

1. Seleccione el recurso y haga clic en **[!UICONTROL Propiedades]**.

1. En el **[!UICONTROL Activación programada (de)]** de la sección **[!UICONTROL Básico]** , defina el Tiempo de activación o el Tiempo de desactivación según sus necesidades.

Del mismo modo, en la vista de Assets, puede seleccionar el recurso y hacer clic en **[!UICONTROL Detalles]** para ver las propiedades del recurso y definir Tiempo de activación y Tiempo de desactivación.

El campo está disponible en el formulario de metadatos predeterminado. Si el recurso no se basa en el esquema de metadatos predeterminado y los campos Tiempo de activación y Tiempo de inactividad no están disponibles en las propiedades del recurso, ejecute los siguientes pasos en la vista de administración:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
1. Seleccione el esquema de metadatos y haga clic en **[!UICONTROL Editar]**.
1. Añadir un **[!UICONTROL Fecha]** del campo **[!UICONTROL Generar formulario]** en el lado derecho a la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en la  **[!UICONTROL Configuración]** panel:
   1. Cambie el **[!UICONTROL Etiqueta de campo]** hasta **Tiempo de activación** o **Tiempo de inactividad**.
   1. Actualice el **[!UICONTROL Asignar a la propiedad]** hasta _./jcr:content/onTime_ para **Tiempo de activación** field y _./jcr:content/offTime_ para **Tiempo de inactividad** field.
1. Haga clic en **[!UICONTROL Guardar]**.

Del mismo modo, para la vista de Assets, si el recurso no se basa en el esquema de metadatos predeterminado y los campos Tiempo de activación y Tiempo de inactividad no están disponibles en las propiedades del recurso, ejecute los siguientes pasos:

1. Clic **[!UICONTROL Metadatos de Forms]** en el **[!UICONTROL Configuración]** sección.
1. Seleccione el formulario de metadatos y haga clic en **[!UICONTROL Editar]**.
1. Añadir un **[!UICONTROL Fecha]** del campo **[!UICONTROL Componentes]** en el panel izquierdo del formulario.
1. Haga clic en el campo recién añadido y cambie la **[!UICONTROL Etiqueta]** hasta **Tiempo de activación** o **Tiempo de inactividad**.
1. Actualice el **[!UICONTROL Propiedad de metadatos]** hasta _./jcr:content/onTime_ para **Tiempo de activación** field y _./jcr:content/offTime_ para **Tiempo de inactividad** field.
1. Haga clic en **[!UICONTROL Guardar]**.



### Entrega de activos restringidos {#delivery-restricted-assets}

La entrega de recursos restringidos se basa en la autorización correcta para acceder a los recursos. AEM La autorización se basa en un token de IMS si la solicitud se envía desde una instancia de autor o un Selector de recursos de la aplicación o se basa en una cookie especial si tiene proveedores de identidad personalizados configurados en la instancia de Publish o de vista previa.

#### AEM Envío de solicitudes de autor de recursos o selector de recursos de {#delivery-aem-author-asset-selector}

AEM Para habilitar la entrega de recursos restringidos en caso de que la solicitud se envíe desde instancia de autor o el Selector de recursos, es esencial un token de IMS válido. Siga estos pasos:

1. [Generación de un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Inicie sesión en la consola de desarrollo de su entorno de AEM as a Cloud Service.

   * Vaya a **[!UICONTROL Entorno]** > **[!UICONTROL Integraciones]** > **[!UICONTROL Token local]** > **[!UICONTROL Obtener token de desarrollo local]** > **[!UICONTROL Copiar valor de accessToken]**. Más información sobre [cómo acceder al token y aspectos relacionados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integre el token de acceso obtenido en **[!UICONTROL Autorización]** , asegurándose de que su valor lleva el prefijo **[!UICONTROL Portador]**.

1. Valide la funcionalidad del token de acceso iniciando una solicitud. Debe generar un error 404 en los casos en los que no haya ningún token de acceso IMS o el token de acceso proporcionado carezca de los mismos principales o grupos que los agregados en los metadatos del recurso.

#### Envío de proveedores de identidad personalizados en una instancia de Publish {#delivery-custom-identity-provider}

En el caso de un proveedor de identidad personalizado configurado en la instancia de Publish o Vista previa, puede mencionar el grupo que debe tener acceso a los recursos protegidos dentro de `groupMembership` durante el proceso de configuración. Al iniciar sesión en el proveedor de identidad personalizado mediante [Integración de SAML](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), el `groupMembership` AEM El atributo se lee y se utiliza para construir una cookie, que se envía en todas las solicitudes de autenticación, de forma similar a un token de IMS en caso de una solicitud del autor del recurso o de un selector de recursos de los que se puede obtener acceso.

AEM Cuando un recurso protegido está disponible en una página y se realiza una solicitud a la dirección URL de entrega para procesar el recurso, comprueba los roles presentes en la cookie o el token de IMS y lo compara con el `dam:roles property` se aplican durante la creación del recurso. Si hay una coincidencia, se muestra el recurso.

>[!NOTE]
>
> En el [ticket de asistencia para activar Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities), mencione la entrega restringida en el caso de uso. El departamento de ingeniería de Adobes le ayudará con las aclaraciones necesarias o configurará el proceso para las entregas restringidas.
