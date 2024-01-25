---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: fa106c2e3fec70971e2c54572199e35c24db0aa7
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 38%

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

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.1.0) fue el viernes, 25 de enero de 2024. La próxima versión con funcionalidades (2024.2.0) está planificada para el viernes, 29 de febrero de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Extension Manager en AEM Sites {#sites-extension-manager}

**Explore la nueva [Extension Manager en AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/)** AEM para personalizar la configuración de la mediante la configuración de extensiones de interfaz de usuario.

![Extension Manager en AEM Sites](/help/assets/sites/extension-manager/homepage.png)

El Extension Manager de AEM Sites permite a los desarrolladores y profesionales acceder, administrar y personalizar las extensiones de la interfaz de usuario creadas para mejorar la funcionalidad de AEM Sites.
Con el Extension Manager, puede:

* Habilitar o deshabilitar las extensiones por instancia;
* Configurar parámetros de extensión;
* Previsualizar extensiones y generar un vínculo de vista previa compartible;
* Descubra las funciones de extensibilidad de la IU mediante demostraciones interactivas;
* Acceda a las funciones experimentales de Adobe mediante extensiones de origen.

Estamos buscando activamente comentarios y nuevos casos de uso para las extensiones de interfaz de usuario. Si desea conectarse, envíe un correo electrónico a `uix@adobe.com`.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funciones de prelanzamiento de vista de administrador {#admin-view-prerelease}

**Previsualizar representaciones para todos los tipos de vídeo admitidos**

Experience Manager Assets ahora genera de forma predeterminada representaciones de previsualización de todos los tipos de vídeo admitidos sin requerir una configuración de perfil de procesamiento

### Vista de recursos {#assets-view-features}

**Lista de bloqueados de etiquetas inteligentes**

Ahora, Assets Essentials permite definir una lista de bloqueados compuesta por palabras que no deben añadirse como etiquetas inteligentes a los recursos cuando se cargan en el repositorio. Esta posibilidad le ayuda a mantener el cumplimiento de la marca y reduce el esfuerzo por moderar las etiquetas inteligentes.

![Lista de bloqueados de etiquetas inteligentes](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programa de usuarios pioneros {#forms-early-adopter}

* **[Envío de un formulario adaptable a un escenario de Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service ofrece opciones listas para usar para conectar fácilmente un formulario adaptable con Adobe Workfront. Esto simplifica el proceso de envío de un formulario adaptable a un escenario de Adobe Workfront, lo que le permite almacenar en déclencheur un escenario de Workfront Fusion al enviar un formulario adaptable.

* **[Compatibilidad con idiomas de derecha a izquierda](/help/forms/supporting-new-language-localization-core-components.md)**: Forms adaptable creado en los componentes principales ahora se puede presentar en un idioma de derecha a izquierda (RTL) como árabe, persa y urdu. Más de 2.000 millones de personas en todo el mundo hablan los idiomas RTL. El uso de un formulario en idioma RTL le permite ampliar el alcance de sus formularios adaptables para adaptarse a estas diversas audiencias y seleccionar en los mercados RTL. En ciertas regiones, también es un mandato legal proporcionar formularios en el idioma local. Al adaptarse a los idiomas locales, no solo abre las puertas a una audiencia más amplia, sino que también garantiza el cumplimiento de las leyes y regulaciones relevantes.

  ![Compatibilidad con idiomas de derecha a izquierda](/help/forms/assets/right-to-left-language-support.png)

* **[Protect sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se convierte a un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan acceder. Esta capa reforzada de protección no solo protege los datos valiosos de posibles visitas no autorizadas, sino que también proporciona tranquilidad. Las API de firmas permiten a su organización proteger la seguridad y la privacidad de los documentos PDF de Adobe que distribuye y recibe. Este servicio utiliza firmas digitales y certificaciones para garantizar que solo los destinatarios autorizados puedan modificar los documentos.

  Puede escribir a `aem-forms-early-adopter-program@adobe.com` desde su id de correo electrónico oficial para unirse al programa de usuarios que lo adoptaron por primera vez y solicitar acceso a esta capacidad.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Compatibilidad con Dynatrace {#dynatrace}

AEM Los clientes de Dynatrace pueden monitorizar su uso de la. [Leer cómo](/help/implementing/cloud-manager/dynatrace.md) para solicitar conectividad con su entorno de Dynatrace para monitorizar el rendimiento de las aplicaciones. Tenga en cuenta que New Relic APM, que está disponible para todos los clientes, dejará de recopilar datos si Dynatrace está habilitado.

### Compatibilidad con RDE para código front-end mediante temas de sitio y plantillas de sitio: Programa para usuarios pioneros {#rde-frontend-early-adopter}

[Entornos de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) ahora admite código front-end basado en [temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md) y [plantillas del sitio](/help/sites-cloud/administering/site-creation/site-templates.md), para los primeros usuarios. Con los RDE, esto se hace usando una directiva de línea de comandos, en lugar de una [canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Póngase en contacto con **aemcs-rde-support@adobe.com** para probarlo y proporcionar comentarios.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
