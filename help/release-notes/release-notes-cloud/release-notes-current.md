---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 6e834244f3de7e615df12b137f2ae90a11e64ad0
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 19%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] la versión de la función actual (2023.10.0) es el 26 de octubre de 2023. La próxima versión de la funcionalidad (2023.11.0) está planificada para el 30 de noviembre de 2023.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de octubre de 2023 para ver un resumen de las funcionalidades añadidas en la versión 2023.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones {#assets-features}

**Complemento de AEM Assets para Adobe Express**: Experience Manager Assets ahora proporciona un [complemento para Adobe Express](/help/assets/addon-adobe-express.md). El complemento le permite acceder directamente a los recursos almacenados en Experience Manager Assets desde la interfaz de usuario de Adobe Express. Puede colocar contenido administrado en AEM Assets en el lienzo Express y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets. El complemento ofrece las siguientes ventajas clave:

* AEM Mayor reutilización del contenido mediante la edición y el guardado de nuevos recursos en el espacio de trabajo de

* Se ha reducido el tiempo y esfuerzo generales para crear nuevos recursos o crear nuevas versiones de los existentes

  ![Incluir recursos del complemento Recursos](/help/assets/assets/aem-assets-add-on-include-assets.png)

### Nuevas funciones de la vista Recursos {#assets-view-features}

* **Importación masiva de recursos desde la fuente de datos de OneDrive**: Los administradores ahora tienen la capacidad de [importar un gran número de recursos de OneDrive a AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). La lista actualizada de las fuentes de datos admitidas para la importación masiva incluye Azure, AWS, Google Cloud, Dropbox y OneDrive.

  ![asignar formulario de metadatos a una carpeta](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **Compatibilidad de derechos entre organizaciones para bibliotecas**: Experience Manager Assets ahora le permite configurar el acceso a las bibliotecas de Creative Cloud en una organización IMS diferente. Permite un acceso más sencillo a los flujos de trabajo entre productos más recientes entre Creative Cloud y Experience Manager, y reduce el tiempo y el esfuerzo de los creativos.

### Funciones previas al lanzamiento disponibles en [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Compatibilidad con subtítulos múltiples y pistas de audio múltiple para vídeos en Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): ahora se pueden añadir fácilmente varios subtítulos y varias pistas de audio a un vídeo principal. Esta capacidad significa que los vídeos son accesibles para toda la audiencia global. Puede personalizar un solo vídeo principal publicado a una audiencia global en varios idiomas y adherirse a las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

  ![Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.](/help/release-notes/assets/msma-aem-cs.png)*Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de [!DNL Experience Manager Forms] {#forms-features}

* **Propiedades personalizadas para Forms adaptable**: puede asociar atributos personalizados (pares clave-valor) con una plantilla de formulario o un componente de formularios adaptables para permitir a los desarrolladores de formularios proporcionar comportamientos de formulario dinámicos que se adapten en función de los valores de estos atributos personalizados. Por ejemplo, los desarrolladores pueden crear diferentes representaciones de un componente Forms sin encabezado en plataformas móviles, de escritorio o web, en función de los valores de los atributos personalizados, lo que mejora significativamente la experiencia del usuario en una amplia gama de dispositivos.

* **Temas y plantillas**: Inicie el proceso de creación de formularios con nuestras nuevas temáticas y plantillas, diseñadas para potenciar tanto a profesionales experimentados como a autores de nuevos formularios. Creadas sin problemas con los componentes principales de Forms adaptables, estas temáticas y plantillas cuidadosamente depuradas le permiten empezar a crear formularios rápidamente para los casos de uso más comunes.

  ![Plantillas listas para usar](/help/forms/assets/form-templates-ootb.png)

### Funciones previas al lanzamiento disponibles en [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* **Enviar Forms a la lista de SharePoint de Microsoft**: AEM Forms proporciona una integración OOTB para enviar datos de formulario directamente a SharePoint List, lo que le permite aprovechar las capacidades de Listas de SharePoint.

  >[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

### Programa de adopción temprana {#forms-early-adopter}

* **[Protect sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa reforzada de protección no solo protege los datos valiosos de los ojos no autorizados, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos de Adobe PDF que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

  Puede escribir a `aem-forms-early-adopter-program@adobe.com` desde su id de correo electrónico oficial para unirse al programa de usuarios que lo adoptaron por primera vez y solicitar acceso a esta capacidad.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Reglas de filtro de tráfico, incluido WAF {#traffic-filter-rules-waf}

[Filtrado de tráfico en la CDN administrada por Adobe](/help/security/traffic-filter-rules-including-waf.md) declarando reglas que coincidan con el tráfico del sitio web por propiedades, incluidas la dirección url, la dirección IP y el agente de usuario, o estableciendo límites de tasa de tráfico personalizados para protegerse contra ataques DoS. Los clientes también pueden otorgar licencias a un conjunto de reglas avanzadas de cortafuegos de aplicaciones web (WAF) para obtener una protección adicional contra amenazas sofisticadas de sitios web.

Le recomendamos que se familiarice con las reglas de filtro de tráfico con [prueba de un tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html)! Le guiará a través de la configuración de una nueva canalización de configuración de Cloud Manager, la declaración de reglas en un archivo de configuración y el análisis de registros de CDN para tráfico malicioso.

Las reglas de filtro de tráfico ya están disponibles en los entornos de desarrollo, con un despliegue gradual a los entornos de ensayo y producción en noviembre. Puede solicitar acceso anticipado en la fase y producción enviando un correo electrónico a **aemcs-waf-adopter@adobe.com**.

Las reglas avanzadas de filtro de tráfico WAF se pueden licenciar a finales de este año a través de las ofertas de Seguridad mejorada o Protección WAF-DDoS.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
