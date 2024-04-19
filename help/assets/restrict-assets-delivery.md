---
title: Restringir la entrega de recursos en Experience Manager
description: Obtenga información sobre cómo restringir la entrega de recursos en [!DNL Experience Manager].
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Restringir el acceso a los recursos en [!DNL Experience Manager] {#restrict-access-to-assets}

La administración central de recursos en Experience Manager permite al administrador de DAM o a los administradores de marcas administrar el acceso a los recursos. AEM Pueden restringir el acceso configurando funciones para los recursos aprobados en el lado de la creación, específicamente en la instancia de autor as a Cloud Service.

Usuarios [búsqueda](search-assets-api.md) o utilizando [URL de envío](deliver-assets-apis.md) puede obtener acceso a los recursos restringidos tras pasar correctamente el proceso de autorización.

![Acceso restringido a los recursos](/help/assets/assets/restricted-access.png)

## Envío restringido mediante un token de IMS {#restrict-delivery-ims-token}

En Experience Manager, la entrega restringida a través de IMS implica dos etapas clave:

* Creación
* Entrega

### Creación {#authoring}

Para restringir la entrega de recursos, las funciones deben configurarse para los recursos dentro de la variable [!DNL Experience Manager] o [!DNL Experience Manager Assets]. Para configurar roles en [!DNL Experience Manager], siga estos pasos:

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
   >Para la nueva vista Recursos, solo puede dar acceso hasta el nivel de carpeta y exclusivamente a grupos en lugar de a usuarios individuales. Más información sobre [administración de permisos en Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

### Entrega de activos restringidos {#delivery-restricted-assets}

La entrega de recursos restringidos se basa en la autorización correcta para acceder a los recursos. AEM La autorización se basa en un token de IMS si la solicitud se envía desde una instancia de autor o un Selector de recursos de la aplicación o se basa en una cookie especial si tiene proveedores de identidad personalizados configurados en la instancia de publicación o vista previa.

#### AEM Entrega para el autor de la o el selector de recursos {#delivery-aem-author-asset-selector}

AEM Para habilitar la entrega de recursos restringidos en caso de que la solicitud se envíe desde instancia de autor o el Selector de recursos, es esencial un token de IMS válido. Siga estos pasos:

1. [Generación de un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * AEM Inicie sesión en la consola de desarrollo de su entorno as a Cloud Service de.

   * Vaya a **[!UICONTROL Entorno]** > **[!UICONTROL Integraciones]** > **[!UICONTROL Token local]** > **[!UICONTROL Obtener token de desarrollo local]** > **[!UICONTROL Copiar valor de accessToken]**. Más información sobre [cómo acceder al token y aspectos relacionados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integre el token de acceso obtenido en **[!UICONTROL Autorización]** , asegurándose de que su valor lleva el prefijo **[!UICONTROL Portador]**.

1. Valide la funcionalidad del token de acceso iniciando una solicitud. Debe generar un error 404 en los casos en los que no haya ningún token de acceso IMS o el token de acceso proporcionado carezca de los mismos principales o grupos que los agregados en los metadatos del recurso.

#### Envío para proveedores de identidad personalizados {#delivery-custom-identity-provider}

En el caso de un proveedor de identidad personalizado configurado en la instancia de publicación o vista previa, puede mencionar el grupo que debe tener acceso a los recursos protegidos dentro de `groupMembership` durante el proceso de configuración. Al iniciar sesión en el proveedor de identidad personalizado mediante [Integración de SAML](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), el `groupMembership` AEM El atributo se lee y se utiliza para construir una cookie, que se envía en todas las solicitudes de autenticación, de forma similar a un token de IMS en caso de una solicitud del autor del recurso o de un selector de recursos de los que se puede obtener acceso.

AEM Cuando un recurso protegido está disponible en una página y se realiza una solicitud a la dirección URL de entrega para procesar el recurso, comprueba los roles presentes en la cookie o el token de IMS y lo compara con el `dam:roles property` se aplican durante la creación del recurso. Si hay una coincidencia, se muestra el recurso.
