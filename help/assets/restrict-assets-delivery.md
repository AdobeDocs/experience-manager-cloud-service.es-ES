---
title: Restringir la entrega de recursos con Dynamic Media con las funciones de OpenAPI
description: Obtenga información sobre cómo restringir la entrega de recursos con las funciones de OpenAPI.
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 6e9fa8301fba9cab1a185bf2d81917e45acfe3a3
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 0%

---

# Restringir la entrega de recursos con Dynamic Media con las funciones de OpenAPI {#restrict-access-to-assets}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

La administración central de recursos en Experience Manager permite al administrador de DAM o a los administradores de marcas administrar el acceso a los recursos disponibles a través de Dynamic Media con funciones OpenAPI. Pueden restringir la entrega de recursos aprobados (a un recurso individual) a [Usuarios o grupos de Adobe Identity Management System (IMS)](https://helpx.adobe.com/in/enterprise/using/users.html#user-mgt-strategy) seleccionados configurando ciertos metadatos en los recursos de su servicio de AEM as a Cloud Service Author.

Una vez que un recurso está restringido a través de Dynamic Media con OpenAPI, solo se concede acceso a los usuarios (Adobe IMS integrado) autorizados para acceder a dicho recurso. Para acceder al recurso, el usuario debe aprovechar las capacidades de [Search](search-assets-api.md) y [Delivery](deliver-assets-apis.md) de Dynamic Media con OpenAPI.

![Acceso restringido a los recursos](/help/assets/assets/restricted-access.png)

En Experience Manager Assets, la entrega restringida a través de IMS implica dos etapas clave:

* Creación
* Entrega

## Creación {#authoring}

### Envío restringido mediante un token de portador de IMS {#restrict-delivery-ims-token}

Puede restringir la entrega de recursos dentro de [!DNL Experience Manager] en función de las identidades de usuario y grupo de IMS

>[!NOTE]
>
> Actualmente, esta capacidad no es de autoservicio. Para restringir la entrega de recursos para los usuarios [Users](https://helpx.adobe.com/in/enterprise/using/manage-directory-users.html) y [Groups](https://helpx.adobe.com/in/enterprise/using/user-groups.html) de IMS, póngase en contacto con el equipo de soporte Enterprise para obtener instrucciones sobre cómo recuperar la información necesaria para restringir el acceso desde el portal [Adobe Admin Console](https://adminconsole.adobe.com/) y cómo configurar el acceso en el servicio de AEM as a Cloud Service Author.

### Restringir la entrega de recursos mediante Fecha y hora de activación y desactivación {#restrict-delivery-assets-date-time}

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



## Entrega de activos restringidos {#delivery-restricted-assets}

La entrega de recursos restringidos se basa en la autorización correcta para acceder a los recursos. AEM AEM La autorización se realiza a través de [tokens de portador de IMS](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/IMS/) (aplicación para solicitudes iniciadas desde [Selector de recursos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)) o una cookie segura (si tiene proveedores de identidad personalizados configurados en sus servicios de Publish/Vista previa de la y ha configurado la creación y la inclusión de cookies en las páginas).

### AEM Envío de solicitudes de autor de recursos o selector de recursos de {#delivery-aem-author-asset-selector}

AEM AEM Para habilitar la entrega de recursos restringidos en caso de que la solicitud se envíe desde servicio de creación o el Selector de recursos, es esencial un token de portador de IMS válido.\
En los servicios de creación de AEM Cloud Service, así como en el Selector de recursos, el token de portador de IMS se genera automáticamente y se utiliza para las solicitudes después de un inicio de sesión correcto.

>[!NOTE]
>
>AEM Para obtener más información sobre cómo habilitar la autenticación IMS en integraciones basadas en el Selector de recursos, póngase en contacto con el Soporte técnico para empresas

1. Para las experiencias no basadas en el Selector de recursos, AEM as a Cloud Service y Dynamic Media con capacidades OpenAPI admiten actualmente integraciones de API del lado del servidor y pueden generar tokens de IMS Bearer.
   * Siga las instrucciones [aquí](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow) para realizar integraciones de API de servicio a servidor que puedan recuperar los tokens de IMS Bearer mediante [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)
   * Durante un tiempo limitado, se puede generar acceso de desarrollador local (no pensado para casos de uso de producción), tokens de IMS al portador de corta duración para el usuario autenticado en [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console) siguiendo las instrucciones [aquí](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)

1. Al realizar solicitudes de API [Search](search-assets-api.md) y [Delivery](deliver-assets-apis.md), agregue el token de IMS Bearer obtenido al encabezado **[!UICONTROL Authorization]** de la solicitud HTTP (asegúrese de que su valor tenga el prefijo **[!UICONTROL Bearer]**).

1. Para validar la restricción de acceso, inicia una solicitud de API de entrega con y sin el encabezado **[!UICONTROL Authorization]**.
   * La respuesta generará un código de estado de error `404` en los casos en los que no haya un token de portador de IMS o el token de portador de IMS proporcionado no pertenezca al usuario al que se concedió acceso al recurso (ya sea directamente o mediante la pertenencia a un grupo).
   * La respuesta arrojará un código de estado de éxito `200` con el contenido binario del recurso si el token del portador de IMS es uno de los usuarios o grupos a los que se les concedió acceso al recurso.

### Envío de proveedores de identidad personalizados en el servicio Publish {#delivery-custom-identity-provider}

AEM Sites, AEM Assets y Dynamic Media AEM con licencias OpenAPI se pueden usar juntos, y la entrega restringida de recursos se puede configurar en sitios web que se entreguen a través de servicios de Publish o Vista previa de la vista previa de la vista previa de los recursos.
Si los servicios Publish y Preview de AEM Sites están configurados para usar un [proveedor de identidad personalizado (IdP)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), el grupo que debe tener acceso a los recursos protegidos en se puede incluir en el atributo `groupMembership` durante el proceso de configuración.\
Cuando un usuario de un sitio web inicia sesión en un proveedor de identidad personalizado y accede al sitio web alojado en el servicio Publish/Preview, se lee el atributo `groupMembership` y se crea una cookie segura que se entrega en el sitio web tras la autenticación correcta. Esta cookie segura se incluye en todas las solicitudes posteriores para enviar el contenido del sitio web al agente de usuario.

AEM Cuando se solicita un recurso protegido en una página, los niveles de Publish y Vista previa de la extraen el material de autorización de la cookie segura y validan el acceso. Si hay una coincidencia, se muestra el recurso.

>[!NOTE]
>
> En el [ticket de asistencia para activar Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities), mencione la entrega restringida en el caso de uso. El departamento de ingeniería de Adobes le ayudará con las aclaraciones necesarias o configurará el proceso para las entregas restringidas.