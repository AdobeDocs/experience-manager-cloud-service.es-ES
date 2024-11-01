---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: d98aa9d206486022d465ca19c8888088562d56c3
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 63%

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

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2024.10.0) de [!DNL Cloud Service] es el viernes, 31 de octubre de 2024. La próxima versión de la funcionalidad (2024.11.0) está planificada para el viernes, 21 de noviembre de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the October 2024 Release Overview video for a summary of the features added in the 2024.10.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Eventos de página modernizada**

Los siguientes eventos de página de AEM Sites ya están disponibles como eventos consumibles externos basados en AEM as a Cloud Service Eventing Platform. Los eventos se pueden procesar mediante un Adobe I/O para interactuar con procesos externos.
* Página publicada
* Página sin publicar
* Página eliminada

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.

AEM **REST OpenAPI para la entrega de fragmentos de contenido**

AEM La API abierta de [REST para la entrega de fragmentos de contenido](/help/headless/aem-rest-openapi-content-fragment-delivery.md), ya está disponible para AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Función de acceso rápido en Dynamic Media {#dm-early-access}

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función está diseñada para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos en tiempo real. La IA analiza la pista de audio del vídeo para transcribir la voz y crear subtítulos, que se pueden editar para mejorar la precisión o la personalización. Estos subtítulos ayudan a cumplir con los requisitos de accesibilidad y mejorar la participación en vídeo de los públicos que dependen de la compatibilidad con vídeo basado en texto o la prefieren.

Para obtener acceso anticipado a la compatibilidad con subtítulos generados por IA en su cuenta de Dynamic Media, [cree y envíe un caso de asistencia al cliente de Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Nuevas funcionalidades de la vista Recursos {#assets-view-new-features}

**Informes programados**

Ahora los informes se pueden generar automáticamente en la vista de Assets con una programación recurrente o en una fecha futura, lo que reduce el esfuerzo por descubrir perspectivas basadas en datos.

![Informes programados-](/help/assets/assets/scheduled-reports-tab.png)

### Nuevas funciones en Content Hub {#content-hub-new-features}

**Administración de derechos digitales para recursos con licencia**

Las organizaciones ahora pueden aumentar el cumplimiento de las licencias y minimizar el riesgo de compartir recursos con términos de licencia aprovechando DRM para los recursos con licencia para los usuarios de Content Hub, lo que requiere que estos revisen y acepten los términos de licencia antes de poder iniciar la descarga de los recursos con licencia.

![descargar-múltiples-licencias](/help/assets/assets/download-multiple-license.png)

**Configuración de metadatos de tarjeta de recursos**

Content Hub ahora le permite configurar los campos de metadatos clave que necesita mostrar en la tarjeta de recursos hasta un máximo de 6 campos.

![metadatos de clave en la tarjeta de recursos](/help/assets/assets/asset-card-key-metadata.png)

**Configurar la visibilidad y la descarga de recursos caducados**

Los administradores ahora pueden controlar si necesitan que los activos caducados estén visibles en Content Hub. Si los activos caducados están visibles, también se puede definir si los usuarios pueden descargarlos.

![Activos caducados en Content Hub](/help/assets/assets/expired-assets-content-hub.png)

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

* **Generación de formularios adaptables**: cree sin esfuerzo formularios completos con indicaciones de la IA generativa. La IA generativa de Adobe genera automáticamente formularios fáciles de usar que reducen los abandonos y personalizan la experiencia.

* **Generación de paneles para formularios**: genere secciones de formulario adaptadas a las necesidades específicas de recopilación de datos. Por ejemplo, generar secciones para recopilar información de pago, preferencias del cliente o detalles de viaje.

* **Cambio de diseños de formulario**: experimente con diferentes presentaciones y diseños mediante las indicaciones de la IA generativa. Pruebe diferentes diseños, como las vistas del asistente o con pestañas, para encontrar la opción perfecta para su formulario. Utilice las indicaciones de la IA generativa para optimizar los formularios con capacidad de respuesta móvil y crear formularios atractivos visualmente que gusten a los usuarios.

* **Configurar la acción de envío**: utilice las indicaciones de la IA generativa para configurar sin esfuerzo una acción de envío para el formulario. Elija entre una biblioteca de acciones de envío creadas previamente o acciones de envío personalizadas, creadas e implementadas por el equipo de desarrollo.

>[!IMPORTANT]
>
> ¿Le interesa unirse al programa de acceso rápido para disponer de cualquier innovación de los formularios? Envíe un correo electrónico desde su dirección de correo electrónico oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con la lista de capacidades que le interesan.

## Complemento CIF {#cloud-services-cif}

### Corrección de errores {#bug-fixes-cif}

* CIF Se han corregido las pruebas de interfaz de usuario para que funcionen correctamente con los componentes principales de.
* Se ha resuelto un problema con el formato de URL de categoría que no funcionaba como se esperaba en la instancia de nube.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Reenvío de registros de autoservicio con opción de red avanzada {#log-forwarding}

AEM Aunque los registros de (incluidos los de Apache/Dispatcher) y CDN se pueden descargar desde Cloud Manager, muchas organizaciones consideran beneficioso transmitir esos registros a un destino de registro preferido. AEM Ahora admite [reenvío de registro](/help/implementing/developing/introduction/log-forwarding.md) a Azure Blob Storage, Datadog, HTTPS, Elasticsearch (y OpenSearch) y Splunk. AEM De forma opcional, los registros se pueden reenviar a través de configuraciones de red avanzadas, como el uso de una dirección IP dedicada.

Los usuarios configuran esta característica en forma de autoservicio e implementan usando la [Canalización de configuración](/help/operations/config-pipeline.md).

### Redirecciones de URL sin canalizaciones para usuarios empresariales {#pipeline-free-redirects}

Las redirecciones del lado del explorador son útiles cuando una página web se ha eliminado o se ha movido, u otros escenarios. AEM Con [Redirecciones de URL sin canalizaciones](/help/implementing/dispatcher/pipeline-free-url-redirects.md), puede colocar un archivo de mapa de reescritura de Apache en una ubicación de publicación de la, donde se carga automáticamente, sin necesidad de enviar el archivo al control de código fuente ni iniciar una canalización de Cloud Manager.

Las opciones para publicar el archivo de reescritura incluyen cargarlo como un recurso, usar el Administrador de mapas de reescritura de ACS Commons o interactuar con una interfaz de usuario personalizada.

### Configurar canalización para RDE {#config-pipeline-rdes}

Los entornos de desarrollo rápido son una potente herramienta para implementar y probar rápidamente el código y la configuración en un entorno de nube. Los RDE ahora admiten la [sincronización de archivos YAML de configuración](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline), incluida la configuración de CDN, como las reglas de filtro de tráfico y las transformaciones de solicitud/respuesta, así como el reenvío de registros y otras opciones de configuración. [Consulte la lista completa](/help/operations/config-pipeline.md) de opciones de configuración admitidas para obtener más información.

### Nuevos perfiles de producto {#new-product-profiles}

AEM Cuando se crea un nuevo entorno de, los perfiles de producto aparecen automáticamente en Adobe Admin Console, lo que permite a los administradores asignar acceso a las soluciones y funciones con licencia.

Los nuevos entornos ahora incluyen un conjunto actualizado de perfiles de producto, lo que los hace compatibles con las funciones futuras, incluida la generación de credenciales de API en Adobe Developer Console. Los entornos existentes podrán actualizar sus perfiles de producto en una versión futura. [Más información](/help/onboarding/aem-cs-team-product-profiles.md).

### Nuevo AEM Developer Console (Beta pública) {#aem-developer-console-beta}

Pruebe la [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) rediseñada, que ofrece una experiencia más interactiva para depurar código en entornos de la nube.

Cualquiera puede acceder a la versión beta pública haciendo clic en el botón *Nueva consola disponible* en la versión actual de AEM Developer Console. Adobe agradece los comentarios, que puede enviar por correo electrónico a **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Pantalla de paquetes OSGi en AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

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
