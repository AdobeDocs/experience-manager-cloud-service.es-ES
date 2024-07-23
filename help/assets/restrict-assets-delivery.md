---
title: Restringir la entrega de recursos en Experience Manager
description: Obtenga información sobre cómo restringir la entrega de recursos en  [!DNL Experience Manager].
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 16b313a4fb79f915613044d12d29e618209113ec
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Restringir el acceso a los recursos en [!DNL Experience Manager] {#restrict-access-to-assets}

La administración central de recursos en Experience Manager permite al administrador de DAM o a los administradores de marcas administrar el acceso a los recursos. Pueden restringir el acceso configurando funciones para los recursos aprobados en el lado de la creación, específicamente en la instancia de autor de AEM as a Cloud Service.

Los usuarios [que buscan](search-assets-api.md) o que utilizan [URL de envío](deliver-assets-apis.md) pueden obtener acceso a los recursos restringidos tras pasar correctamente el proceso de autorización.

![Acceso restringido a los recursos](/help/assets/assets/restricted-access.png)

## Envío restringido mediante un token de IMS {#restrict-delivery-ims-token}

En Experience Manager Assets, la entrega restringida a través de IMS implica dos etapas clave:

* Creación
* Entrega

### Creación {#authoring}

Puede restringir la entrega de recursos dentro de [!DNL Experience Manager] en función de los roles. Para configurar las funciones, ejecute los siguientes pasos:

1. Vaya a [!DNL Experience Manager] como administrador de DAM.
1. Seleccione el recurso para el que debe configurar la función.
1. Vaya a **[!UICONTROL Propiedades]** > **[!UICONTROL Avanzadas]** y asegúrese de que el campo **[!UICONTROL Roles]** exista en la pestaña [!UICONTROL Metadatos avanzados].

   ![Metadatos de roles](/help/assets/assets/roles_metadata.jpg)
Si el campo no está disponible, siga estos pasos para agregar el campo:

   1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
   1. Seleccione el esquema de metadatos y haga clic en **[!UICONTROL Editar _(e)_]**.
   1. Agregue un campo **[!UICONTROL Texto con varios valores]** desde la sección **[!UICONTROL Generar formulario]** a la derecha de la sección Metadatos del formulario.
   1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
      1. Cambie **[!UICONTROL Etiqueta de campo]** por _Roles_.
      1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/metadata/dam:roles_.

1. Obtenga los grupos de IMS que se agregarán en los metadatos de funciones del recurso. Para recuperar los grupos de IMS, siga estos pasos:
   1. Iniciar sesión a las `https://adminconsole.adobe.com/.`
   1. Vaya a su organización respectiva y navegue hasta **[!UICONTROL Grupos de usuarios]**.
   1. Seleccione el **[!UICONTROL grupo de usuarios]** que necesita agregar y extraiga **[!UICONTROL orgID]** y **[!UICONTROL userGroupID]** de la URL o use su identificador de organización como `{orgID}@AdobeOrg:{usergroupID}`.

1. Agregue el ID de grupo al campo **[!UICONTROL Roles]** de las propiedades del recurso. <br>
Los identificadores de grupo definidos en el campo **[!UICONTROL Roles]** son los únicos usuarios que pueden acceder al recurso. También puede agregar el ID de cliente IMS y el ID de perfil IMS en el campo **[!UICONTROL Roles]**. Por ejemplo, `{orgId}@AdobeOrg:{profileId}`.

   >[!NOTE]
   >
   >Para la nueva vista de Assets, solo puede dar acceso hasta el nivel de carpeta y exclusivamente a grupos en lugar de a usuarios individuales. Más información sobre [administrar permisos en Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### Restringir la entrega de recursos mediante Fecha y hora de activación y desactivación {#restrict-delivery-assets-date-time}

Los autores de DAM también pueden restringir la entrega de recursos definiendo un tiempo de activación o desactivación disponible en las propiedades del recurso.

Si define un Tiempo de activación para la activación de un recurso, se generará una URL de entrega para el recurso en el momento definido. El recurso permanece inactivo antes del tiempo definido. Del mismo modo, si define un Tiempo de inactividad para un recurso, este se desactiva en el momento definido y la URL de entrega del recurso deja de mostrar el recurso.

Ejecute los siguientes pasos para establecer el tiempo de activación y desactivación del recurso:

1. Seleccione el recurso y haga clic en **[!UICONTROL Propiedades]**.

1. En la sección **[!UICONTROL Activación programada (de)]** de la ficha **[!UICONTROL Básico]**, defina el Tiempo de activación o el Tiempo de inactividad según sus necesidades.

Del mismo modo, en la vista de Assets, puede seleccionar el recurso y hacer clic en **[!UICONTROL Detalles]** para ver las propiedades del recurso y definir Tiempo de activación y Tiempo de inactividad.

El campo está disponible en el formulario de metadatos predeterminado. Si el recurso no se basa en el esquema de metadatos predeterminado y los campos Tiempo de activación y Tiempo de inactividad no están disponibles en las propiedades del recurso, ejecute los siguientes pasos en la vista de administración:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
1. Seleccione el esquema de metadatos y haga clic en **[!UICONTROL Editar]**.
1. Agregue un campo **[!UICONTROL Date]** de la sección **[!UICONTROL Generar formulario]** en el lado derecho a la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
   1. Cambie la etiqueta de campo **[!UICONTROL Field]** a **Tiempo de activación** o **Tiempo de inactividad**.
   1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/onTime_ para el campo **A tiempo** y _./jcr:content/offTime_ para el campo **Tiempo de inactividad**.
1. Haga clic en **[!UICONTROL Guardar]**.

Del mismo modo, para la vista de Assets, si el recurso no se basa en el esquema de metadatos predeterminado y los campos Tiempo de activación y Tiempo de inactividad no están disponibles en las propiedades del recurso, ejecute los siguientes pasos:

1. Haga clic en **[!UICONTROL Forms de metadatos]** en la sección **[!UICONTROL Configuración]**.
1. Seleccione el formulario de metadatos y haga clic en **[!UICONTROL Editar]**.
1. Agregue un campo **[!UICONTROL Fecha]** de la sección **[!UICONTROL Componentes]** del panel izquierdo al formulario.
1. Haga clic en el campo recién agregado y cambie la **[!UICONTROL Etiqueta]** a **Tiempo de activación** o **Tiempo de inactividad**.
1. Actualizar la **[!UICONTROL propiedad de metadatos]** a _./jcr:content/onTime_ para el campo **A tiempo** y _./jcr:content/offTime_ para el campo **Tiempo de inactividad**.
1. Haga clic en **[!UICONTROL Guardar]**.



### Entrega de activos restringidos {#delivery-restricted-assets}

La entrega de recursos restringidos se basa en la autorización correcta para acceder a los recursos. AEM La autorización se basa en un token de IMS si la solicitud se envía desde una instancia de autor o un Selector de recursos de la aplicación o se basa en una cookie especial si tiene proveedores de identidad personalizados configurados en la instancia de Publish o de vista previa.

#### AEM Envío de solicitudes de autor de recursos o selector de recursos de {#delivery-aem-author-asset-selector}

AEM Para habilitar la entrega de recursos restringidos en caso de que la solicitud se envíe desde instancia de autor o el Selector de recursos, es esencial un token de IMS válido. Siga estos pasos:

1. [Generar un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Inicie sesión en la consola de desarrollo de su entorno de AEM as a Cloud Service.

   * Vaya a **[!UICONTROL Entorno]** > **[!UICONTROL Integraciones]** > **[!UICONTROL Token local]** > **[!UICONTROL Obtener token de desarrollo local]** > **[!UICONTROL Copiar valor de accessToken]**. Más información sobre [cómo acceder al token y aspectos relacionados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integre el token de acceso obtenido en el encabezado **[!UICONTROL Autorización]**, asegurándose de que su valor tenga el prefijo **[!UICONTROL Portador]**.

1. Valide la funcionalidad del token de acceso iniciando una solicitud. Debe generar un error 404 en los casos en los que no haya ningún token de acceso IMS o el token de acceso proporcionado carezca de los mismos principales o grupos que los agregados en los metadatos del recurso.

#### Envío de proveedores de identidad personalizados en una instancia de Publish {#delivery-custom-identity-provider}

En el caso de un proveedor de identidad personalizado configurado en la instancia de Publish o Vista previa, puede mencionar el grupo que debe tener acceso a los recursos protegidos con el atributo `groupMembership` durante el proceso de configuración. AEM Cuando inicia sesión en el proveedor de identidad personalizado a través de la [integración SAML](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), se lee el atributo `groupMembership` y se usa para construir una cookie, que se envía en todas las solicitudes de autenticación, de forma similar a un token de IMS en caso de una solicitud del autor o del Selector de recursos.

AEM Cuando un recurso protegido está disponible en una página y se realiza una solicitud a la dirección URL de entrega para procesar el recurso, comprueba los roles presentes en la cookie o el token de IMS y lo compara con el `dam:roles property` aplicado durante la creación del recurso, lo que se conoce como &quot;token&quot; de IMS. Si hay una coincidencia, se muestra el recurso.

>[!NOTE]
>
> En el [ticket de asistencia para activar Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities), mencione la entrega restringida en el caso de uso. El departamento de ingeniería de Adobes le ayudará con las aclaraciones necesarias o configurará el proceso para las entregas restringidas.
