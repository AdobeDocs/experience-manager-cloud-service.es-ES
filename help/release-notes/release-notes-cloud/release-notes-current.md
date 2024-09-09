---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 9cc49bf83d278d4064faa1d0157201226a067cb1
workflow-type: ht
source-wordcount: '1142'
ht-degree: 100%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2022 o 2023.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.8.0) fue el 29 de agosto de 2024. La próxima versión con funcionalidades (2024.9.0) se planificó para el 26 de septiembre de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the August 2024 Release Overview video for a summary of the features added in the 2024.8.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función de Experience Manager Sites {#new-feature-sites}

**Creación de AEM para Edge Delivery Services**

Ahora se admite la funcionalidad de [herencia](/help/sites-cloud/authoring/universal-editor/inheritance.md) de los sitios existentes, que incluye:

* [Lanzamientos de AEM](/help/sites-cloud/authoring/launches/overview.md)
* [MSM](/help/sites-cloud/administering/msm/overview.md) a nivel de páginas

Además, ahora se admiten las siguientes funciones de administración de páginas:

* Las [etiquetas AEM](/help/sites-cloud/authoring/sites-console/tags.md) se pueden exportar como [taxonomía](/help/edge/wysiwyg-authoring/taxonomy.md) a Edge Delivery Services.
* Próximamente, habrá [plantillas](/help/edge/wysiwyg-authoring/templates.md) disponibles para Edge Delivery Services.

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#assets-view-new-features}

**Generación actualizada de imágenes de Adobe Firefly**

Assets as a Cloud Service ahora utiliza el último widget de Firefly, que le permite generar imágenes en diferentes estilos mediante Adobe Firefly. Al definir su estilo, composición, dimensiones, etc., mediante el editor de Firefly integrado, puede crear y guardar rápidamente los recursos que necesite directamente en el repositorio de AEM Assets para su uso inmediato.

![Generación de imágenes de Adobe Firefly](/help/assets/assets/bugatti-type-57.png)

**Compatibilidad con archivos PSB**

Assets as a Cloud Service ahora admite documentos grandes de Photoshop (archivos PSB) además de seguir admitiendo los archivos PSD.

### Nuevas mejoras en Content Hub {#content-hub-new-enhancements}

* Mejor gestión de los nombres de archivo largos, fácil expansión del nombre completo a través de la ayuda contextual.
* Se han mejorado las miniaturas para ajustarse mejor a la relación de aspecto del contenido y cubrir un área de contenido más grande.
* Content Hub admite la experiencia de miniaturas personalizadas de AEM.
* Mejoras en la búsqueda de colores.
* Las mejoras en la experiencia de guardar configuraciones.
* Se ha mejorado la página de información de colecciones para reflejar el nombre del creador.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones en la versión preliminar de AEM Forms {#forms-new-prerelease-features}

#### Guardar automáticamente un borrador para los componentes principales basados en formularios adaptables

Los usuarios ahora pueden beneficiarse de una función de guardado automático que, de manera automática, guarda como borrador un formulario parcialmente completado. Pueden volver más tarde para terminar de rellenarlo en el mismo dispositivo o en otro distinto. Esta función mejora las tasas de conversión para las organizaciones al reducir el abandono de formularios, ya que los usuarios no tienen que volver a empezar a rellenar el formulario desde el principio.


### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo. 

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Asistente de IA de AEM Forms

La IA generativa para los formularios adaptables aporta un nuevo nivel de potencia y facilidad a los procesos de desarrollo de formularios. Le permite crear mejores formularios y más rápido que nunca.

![Asistente de IA generativa, formularios adaptables](/help/forms/assets/generative-ai-assistant.png)

Las funciones de IA generativa que se ofrecen son:

* **Asistente de IA para consultas de productos**: obtenga respuestas instantáneas a sus preguntas relacionadas con AEM Forms. El asistente de IA actúa como su propia base de conocimiento personal, proporcionando orientación y recomendaciones reveladoras directamente dentro de la plataforma.

* **Generación de formularios adaptables**: cree sin esfuerzo formularios completos con indicaciones de la IA generativa. Nuestra IA generativa genera automáticamente formularios fáciles de usar que reducen los abandonos y personalizan la experiencia.

* **Generación de paneles para formularios**: genere secciones de formulario adaptadas a las necesidades específicas de recopilación de datos. Por ejemplo, generar secciones para recopilar información de pago, preferencias del cliente o detalles de viaje.

* **Cambio de diseños de formulario**: experimente con diferentes presentaciones y diseños mediante las indicaciones de la IA generativa. Pruebe diferentes diseños, como las vistas del asistente o con pestañas, para encontrar la opción perfecta para su formulario. Utilice las indicaciones de la IA generativa para optimizar los formularios con capacidad de respuesta móvil y crear formularios atractivos visualmente que gusten a los usuarios.

* **Configurar la acción de envío**: utilice las indicaciones de la IA generativa para configurar sin esfuerzo una acción de envío para el formulario. Elija entre una biblioteca de acciones de envío creadas previamente o una lista de acciones de envío personalizadas, creadas e implementadas por su propio equipo de desarrollo.

>[!IMPORTANT]
>
> Si está interesado en unirse al programa de acceso rápido para cualquier innovación, solo tiene que enviar un correo electrónico desde su dirección oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con la lista de funcionalidades que le interesan.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programas para primeros usuarios relacionados con la distribución de contenido {#foundation-early-adopter}

Correo electrónico **<aemcs-cdn-config-adopter@adobe.com>**, indicando cuál de los programas para primeros usuarios que aparecen a continuación le interesa.

#### Autenticación básica en CDN (programa para primeros usuarios) {#basicauth-cdn}

Proteja determinados recursos de contenido mostrando un cuadro de diálogo de autenticación básica que requiera un nombre de usuario y una contraseña. Esta función se dirige principalmente a casos de uso de autenticación ligera, como el de las partes interesadas empresariales que revisan el contenido, en lugar de servir como solución completa para los derechos de acceso de usuarios finales. La lista de nombres de usuario y contraseñas se administra mediante un archivo de configuración en Git que se implementa mediante la canalización de configuración, con una referencia a variables del entorno de Cloud Manager de tipo secreto. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Redirecciones del lado del cliente (programa para primeros usuarios) {#client-side-redirects-early-adopter}

Configure las redirecciones del lado del cliente 301/302 en el control de código fuente e impleméntelas en la CDN. [Más información](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Tenga en cuenta que ya hay diversas otras funciones disponibles relacionadas con la [configuración de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluidas las transformaciones de solicitudes y respuestas, y el enrutamiento del tráfico a sitios fuera de AEM.

#### Los usuarios empresariales pueden declarar redirecciones fuera de Git (programa para primeros usuarios) {#apache-rewritemaps-early-adopter}

De forma similar a la versión AEM 6.5, Apache/Dispatcher introducirá mapas de reescritura colocados en una ubicación específica del repositorio de publicación y los cargará, sin requerir la ejecución de una canalización de niveles web. Este método permite a los usuarios empresariales declarar redirecciones mediante una hoja de cálculo o una interfaz de usuario, como el administrador de mapas de redirección de ACS Commons o una aplicación personalizada. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) para cargar contenido dinámico (programa para primeros usuarios) {#esi-early-adopter}

La CDN administrada por Adobe es ahora compatible con [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL superiores, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL inferiores).<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->


## Guías de [!DNL Experience Manager] {#guides}

Puede encontrar una lista completa de las funciones nuevas y mejoradas de la última versión de Adobe Experience Manager Guides [aquí](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Puede encontrar una lista completa de las versiones del editor universal [aquí](/help/release-notes/universal-editor/current.md).

## Generar variaciones {#generate-variations}

Puede encontrar una lista completa de las versiones de generar variaciones [aquí](/help/generative-ai/release-notes-generate-variations.md).

## Notas de la versión de Experience Cloud {#experience-cloud}

Puede encontrar información sobre las versiones de otras aplicaciones de Experience Cloud [aquí](https://experienceleague.adobe.com/es/docs/release-notes/experience-cloud/current).
