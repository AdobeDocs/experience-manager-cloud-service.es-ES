---
title: Notas de la versión 2023.10.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.10.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 81a6cbd2-7101-429b-8572-2650c5bea963
source-git-commit: b323fbe3a09de220c61c9b409d8754e43fe0a8d3
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 98%

---

# Notas de la versión 2023.10.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.10.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2023.10.0) de [!DNL Cloud Service] es el 26 de octubre de 2023. La próxima versión de la funcionalidad (2023.11.0) está planificada para el 30 de noviembre de 2023.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de octubre de 2023 para ver un resumen de las funcionalidades añadidas en la versión 2023.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones {#assets-features}

**Complemento de AEM Assets para Adobe Express**: Experience Manager Assets ahora proporciona un complemento para el Adobe Express. El complemento le permite acceder directamente a los recursos almacenados en Experience Manager Assets desde la interfaz de usuario de Adobe Express. Puede colocar contenido administrado en AEM Assets en el lienzo Express y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets. El complemento ofrece las siguientes ventajas clave:

* Mayor reutilización del contenido editando y guardando nuevos recursos en AEM

* Se ha reducido el tiempo y esfuerzo generales para crear nuevos recursos o crear nuevas versiones de los recursos existentes

  ![Incluir recursos del complemento Recursos](/help/assets/assets/aem-assets-add-on-include-assets.png)

### Nuevas funcionalidades de la vista Recursos {#assets-view-features}

* **Importación masiva de recursos desde la fuente de datos de OneDrive**: los administradores ahora tienen la posibilidad de [importar un gran número de recursos de OneDrive a AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). La lista actualizada de las fuentes de datos admitidas para la importación masiva incluye Azure, AWS, Google Cloud, Dropbox y OneDrive.

  ![asignar formulario de metadatos a una carpeta](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **Compatibilidad de derechos entre organizaciones para bibliotecas**: Experience Manager Assets ahora le permite configurar el acceso a las Bibliotecas Creative Cloud en una organización IMS diferente. Permite un acceso más sencillo a los flujos de trabajo entre productos más recientes entre Creative Cloud y Experience Manager, y reduce el tiempo y el esfuerzo de los creativos.

### Nuevas funciones disponibles en [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [compatibilidad con subtítulos múltiples y pistas de audio múltiple para vídeos en Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): ahora se pueden añadir fácilmente varios subtítulos y varias pistas de audio a un vídeo principal. Esta posibilidad significa que los vídeos son accesibles para todo el público global. Puede personalizar un solo vídeo principal publicado para un público global en varios idiomas y seguir las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

  ![Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.](/help/release-notes/assets/msma-aem-cs.png)*Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de [!DNL Experience Manager Forms] {#forms-features}

* **[Propiedades personalizadas para formulario adaptables](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**: puede asociar atributos personalizados (pares de clave y valor) con una plantilla de formulario o un componente de formularios adaptables para permitir que los desarrolladores de formularios proporcionen comportamientos de formulario dinámicos que se adapten en función de los valores de estos atributos personalizados. Por ejemplo, los desarrolladores pueden crear diferentes representaciones de un componente de formularios sin encabezado en plataformas móviles, de escritorio o web, en función de los valores de los atributos personalizados, lo que mejora significativamente la experiencia del usuario en una amplia gama de dispositivos.

* **Temas y plantillas**: comience el proceso de creación de formularios con nuestras nuevas temáticas y plantillas, diseñadas para capacitar tanto a profesionales experimentados como a autores de nuevos formularios. Creadas a la perfección con los componentes principales de formularios adaptables, estas temáticas y plantillas meticulosamente seleccionadas le permiten empezar a crear formularios rápidamente para los casos de uso más comunes.

  ![Plantillas listas para usar](/help/forms/assets/form-templates-ootb.png)


### Programa para primeros usuarios {#forms-early-adopter}

* **[Proteja sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa de protección fortificada no solo protege los datos valiosos de miradas no autorizadas, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos PDF de Adobe que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

  Puede escribir a `aem-forms-early-adopter-program@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta posibilidad.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Reglas de filtro de tráfico, incluidas reglas WAF {#traffic-filter-rules-waf}

[Filtrado de tráfico en la red de distribución de contenido (CDN) administrada por Adobe](/help/security/traffic-filter-rules-including-waf.md) declarando reglas que coincidan con el tráfico del sitio web por propiedades, incluidas la dirección url, la dirección IP y el agente de usuario, o estableciendo límites de velocidad de tráfico personalizado para protegerse de los ataques DoS. Los clientes también pueden otorgar licencias a un conjunto de reglas avanzadas de cortafuegos de aplicaciones web (WAF) para obtener una protección adicional contra amenazas sofisticadas de sitios web.

Le animamos a familiarizarse con las reglas de filtro de tráfico mediante [un tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html?lang=es). Le guiará a través de la configuración de una nueva canalización de configuración de Cloud Manager, la declaración de reglas en un archivo de configuración y el análisis de registros CDN para tráfico malicioso.

Las reglas de filtro de tráfico ya están disponibles en los entornos de desarrollo, con un despliegue gradual en los entornos de fase y producción en noviembre. Puede solicitar acceso anticipado a la fase y la producción enviando un correo electrónico a **aemcs-waf-adopter@adobe.com**.

Las reglas avanzadas de filtro de tráfico WAF se pueden adquirir bajo licencia a finales de este año a través de las ofertas de Seguridad mejorada o Protección WAF-DDoS.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
