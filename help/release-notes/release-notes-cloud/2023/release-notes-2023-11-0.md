---
title: Notas de la versión 2023.11.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.11.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 19cff082-80aa-445c-9462-5e319b7fe0e9
feature: Release Information
role: Admin
source-git-commit: 0845447c1c4f47b77debd179f24eac95a0d2c2db
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 41%

---

# Notas de la versión 2023.11.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.11.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2023.11.0) de [!DNL Cloud Service] es el viernes, 30 de noviembre de 2023. La próxima versión de la funcionalidad (2023.12.0) está planificada para el viernes, 14 de diciembre de 2023.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo de información general sobre la versión de noviembre de 2023 para ver un resumen de las funciones añadidas en la versión 2023.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programa para primeros usuarios {#sites-early-adopter}

**[Buscar y reemplazar cadenas en fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**: La consola de fragmentos de contenido proporciona a los usuarios una forma fácil e intuitiva de reemplazar una cadena que aparece en varios fragmentos de contenido a la vez para acelerar la velocidad de contenido.

![Buscar y reemplazar](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

¿Quiere probar la función y compartir sus comentarios? Envíe un correo electrónico a **aemcs-headless-adopter@adobe.com** desde su ID de correo electrónico oficial para obtener más información sobre el programa de usuarios que lo adoptaron por primera vez.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones en la vista de Assets {#assets-view-features}

* **Editor Adobe Express incrustado en AEM Assets**: Los usuarios con acceso a Express ahora tienen herramientas integradas de edición y creación de imágenes de Adobe Express y Adobe Firefly disponibles directamente en los AEM Assets para mejorar la reutilización del contenido y acelerar la velocidad de contenido.

  ![asignar formulario de metadatos a una carpeta](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Informes de uso del almacenamiento en Insights**: Los administradores ahora tienen la capacidad de ver los informes de uso del almacenamiento disponibles como parte de Insights.

  ![uso de almacenamiento en Insights](/help/assets/assets/storage-usage-insights.png)

* **Buscar en la primera configuración de página principal**: Experience Manager Assets ahora le permite configurar la experiencia de página principal para su organización. Si selecciona Buscar primero como página principal, puede configurar la alineación de la barra de búsqueda, la imagen de fondo y el logotipo de su organización.

  ![configuración de Buscar primero](/help/assets/assets/search-first-configuration.png)

### Nuevas funciones del prelanzamiento para la vista de administrador {#admin-view-features-prerelease}

**Vista previa de vídeo**: ahora los AEM Assets generan representaciones de vista previa de todos los formatos de vídeo admitidos de forma predeterminada, sin necesidad de configurar un perfil de procesamiento.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas características de [!DNL Experience Manager Forms] {#forms-features}

* **[Componente de casilla de verificación](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html?lang=es)**: los Forms adaptables basados en componentes principales ahora pueden incluir un componente de casilla de verificación. Permite a los usuarios realizar elecciones binarias, seleccionando o anulando la selección de una opción en particular. Normalmente aparece como un pequeño cuadro en el que se puede hacer clic o pulsar para alternar entre dos estados: activado y desactivado. La casilla de verificación es un elemento de formulario común que se utiliza para presentar una opción sí/no o verdadero/falso.

* **[Componente Términos y condiciones](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html?lang=es)**: el Forms adaptable basado en componentes principales ahora puede incluir un componente Términos y condiciones. Permite a los autores de formularios introducir una sección específica dentro del formulario en la que se presentan a los usuarios los términos, condiciones o acuerdos legales asociados al uso de un servicio, producto o plataforma. Este componente está diseñado para informar a los usuarios sobre las reglas, regulaciones y obligaciones que aceptan enviando el formulario.

  ![Casilla de verificación, Términos y condiciones y componentes de ficha Vertical](/help/forms/assets/forms-components.png)

* **[Componente de pestañas verticales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html?lang=es)**: los Forms adaptables basados en componentes principales ahora pueden organizar el contenido del formulario en una lista vertical de pestañas, lo que proporciona un diseño estructurado y navegable. El uso de pestañas verticales en un formulario puede mejorar la experiencia general del usuario al simplificar la navegación y mejorar la organización del contenido del formulario, especialmente en situaciones en que un formulario contiene varias secciones o información compleja.



### Nuevas funciones en el prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **[Conectar un Forms adaptable con Microsoft® SharePoint List](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: AEM Forms proporciona una integración OOTB para enviar datos de formularios directamente a SharePoint List, lo que le permite aprovechar las capacidades de Listas de SharePoint. Puede configurar Microsoft SharePoint List como fuente de datos para un modelo de datos de formulario y utilizar la acción de envío **Enviar mediante el modelo de datos de formulario** para conectar un formulario adaptable con SharePoint List.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programa para primeros usuarios {#forms-early-adopter}

* **Envío de un formulario adaptable a un escenario de Adobe Workfront Fusion**: Forms as a Cloud Service ofrece opciones listas para usar para conectar fácilmente un formulario adaptable con Adobe Workfront.  Esto simplifica el proceso de envío de un formulario adaptable a un escenario de Adobe Workfront, permitiéndole activar un escenario de Workfront Fusion al enviar un formulario adaptable.

* **Compatibilidad con idiomas de derecha a izquierda**: los formularios adaptables creados en los componentes principales ahora se pueden presentar en un idioma de derecha a izquierda (RTL) como árabe, persa y urdu.  Más de 2000 millones de personas en todo el mundo hablan los idiomas RTL.  El uso de un formulario en idioma RTL le permite ampliar el alcance de sus formularios adaptables para adaptarse a estas diversas audiencias y acceder a los mercados RTL. En ciertas regiones, también es un mandato legal proporcionar formularios en el idioma local.  Al adaptarse a los idiomas locales, no solo abre las puertas a una audiencia más amplia, sino que también garantiza el cumplimiento de las leyes y regulaciones relevantes.

  ![Compatibilidad con idiomas de derecha a izquierda](/help/forms/assets/right-to-left-language-support.png)

* **[Proteja sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa de protección fortificada no solo protege los datos valiosos de miradas no autorizadas, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos PDF de Adobe que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

  Puede escribir a `aem-forms-ea@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta posibilidad.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Ahora Se Puede Otorgar Licencia A Las Reglas De Filtro De Tráfico De WAF {#cdn-waf-license}

Las reglas de filtro de tráfico se publicaron en octubre e incluían una nota en la que se indicaba que la categoría especial de reglas de cortafuegos de aplicaciones web (WAF) estaría disponible a finales de este año para complementar las reglas ya disponibles para los clientes de Sites y Forms. Como actualización, la oferta WAF-DDoS Protection ahora puede obtener una licencia.

Una vez adquirida la licencia, estas reglas avanzadas de WAF se pueden implementar en la CDN mediante la canalización de configuración de Cloud Manager para añadir una capa adicional de protección contra ataques web.

Obtenga información sobre [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md), incluido WAF. Hable con el equipo de su cuenta de AEM sobre la licencia de Protección WAF-DDoS o Seguridad mejorada.

### Programa de adopción temprana de asignación de dominios {#cdn-config-early-adopter}

Además de las [reglas de filtro de tráfico (incluyendo WAF)](/help/security/traffic-filter-rules-including-waf.md) publicadas recientemente, existe la oportunidad de usar la canalización de configuración para declarar e implementar otros tipos de configuración de CDN. Nos encantaría conocer sus casos de uso, incluidos los siguientes:
* Redirecciones del lado del cliente 301/302
* solicitudes de proxy en el perímetro a orígenes arbitrarios
* transformaciones de URL
* configuración o modificación de encabezados de solicitud o respuesta
* páginas de error personalizadas cuando la CDN no puede llegar a AEM
* autenticación por nombre de usuario/contraseña
* cualquier otra configuración de CDN útil

Envíe un correo electrónico a **aemcs-cdn-config-adopter@adobe.com** desde su ID de correo electrónico oficial con sus comentarios.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Problemas conocidos {#known-issues}

* No se puede enviar el Forms adaptable basado en los componentes principales. El problema se produce para Forms adaptable creado con las versiones 2.0.38 - 2.0.60 de los componentes principales.

  Para resolver el problema. Puede pasar a la versión 2.0.62 o posterior de los componentes principales del formulario adaptable. Para establecer una versión de los componentes principales de Forms adaptable para su entorno, establezca las versiones de las dependencias `core.forms.components.version`, `core.forms.components.af.version` y `core.wcm.components.version component`en su repositorio de Forms as a Cloud Service o proyecto basado en el arquetipo de AEM e implemente los cambios en su entorno de Forms as a Cloud Service. Puede encontrar la versión más reciente de las dependencias de los componentes principales de Forms adaptable en [Repositorio de Git de componentes principales de Forms adaptable](https://github.com/adobe/aem-core-forms-components#system-requirements).
