---
title: Notas de la versión 2024.10.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2024.10.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 7a63f04f-10f0-4879-bd06-4182bb288a9b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 99%

---

# Notas de la versión 2024.10.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2024.10.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2022 o 2023.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2024.10.0) de [!DNL Cloud Service] es el 31 de octubre de 2024. La próxima versión de la funcionalidad (2024.11.0) está planificada para el 21 de noviembre de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de octubre de 2024 para ver un resumen de las funcionalidades añadidas en la versión 2024.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3440501?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Eventos de la página modernizados**

Los siguientes eventos de la página de AEM Sites ya están disponibles como eventos consumibles externos basados en AEM as a Cloud Service Eventing Platform. Los eventos se pueden procesar mediante Adobe I/O para interactuar con los procesos externos.

* Página publicada
* Página sin publicar
* Página eliminada

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.

**AEM REST OpenAPI para la entrega de fragmentos de contenido**

[AEM REST OpenApi para la entrega de fragmentos de contenido](/help/headless/aem-content-fragment-delivery-with-openapi.md), ya está disponible para AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Función de acceso rápido en Dynamic Media {#dm-early-access}

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función está diseñada para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos en tiempo real. La IA analiza la pista de audio del vídeo para transcribir la voz y crear subtítulos, que se pueden editar para mejorar la precisión o la personalización. Estos subtítulos ayudan a cumplir con los requisitos de accesibilidad y mejorar la participación en vídeo de los públicos que dependen de la compatibilidad con vídeo basado en texto o la prefieren.

Para obtener acceso anticipado a la compatibilidad con subtítulos generados por IA en su cuenta de Dynamic Media, [cree y envíe un caso de asistencia al cliente de Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Nuevas funcionalidades de la vista Recursos {#assets-view-new-features}

**Informes programados**

Ahora los informes se pueden generar automáticamente en la vista de Assets con una programación recurrente o en una fecha futura, lo que reduce el esfuerzo por descubrir perspectivas basadas en datos.

![Informes programados:](/help/assets/assets/scheduled-reports-tab.png)

### Nuevas funciones en Content Hub {#content-hub-new-features}

**Digital Rights Management para recursos con licencia**

Las organizaciones ahora pueden aumentar el cumplimiento de las licencias y minimizar el riesgo de compartir recursos con términos y condiciones de la licencia aprovechando DRM para los recursos con licencia para los usuarios de Content Hub, exigiendo a los usuarios que revisen y acepten los términos y condiciones de la licencia para poder iniciar la descarga de los recursos con licencia. Para obtener más información, consulte [Administración de recursos con licencia en Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

![descargar-múltiples-licencias](/help/assets/assets/download-multiple-license.png)

**Configuración de metadatos de la tarjeta de recursos**

Content Hub ahora le permite configurar los campos de metadatos clave que necesita mostrar en la tarjeta de recursos hasta un máximo de 6 campos. Para obtener más información, consulte la sección Tarjeta de recursos en [Configuración de Content Hub](/help/assets/configure-content-hub-ui-options.md#asset-card).

![metadatos clave de la tarjeta de recursos](/help/assets/assets/asset-card-key-metadata.png)

**Configurar la visibilidad y la descarga de los recursos caducados**

Los administradores ahora pueden controlar si necesitan que los activos caducados estén visibles en Content Hub. Si los activos caducados están visibles, también se puede definir si los usuarios pueden descargarlos. Para obtener más información, consulte la sección Activos caducados en [Configuración de Content Hub](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub).

![Activos caducados en Content Hub](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nueva función en AEM Forms {#forms-new-features}

* [Mejorar la experiencia del usuario con botones de navegación en los diseños de panel](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button): ahora puede añadir botones de navegación a los diseños de panel, como Pestañas horizontales, Pestañas verticales, Acordeones o el Asistente. Estos botones mejoran la experiencia del usuario al simplificar las transiciones entre paneles y se centran en el panel seleccionado.

<!--* **Specify Display Styles for Document of Record (DoR) Components**: In an XFA file, you can now specify the display styles for Document of Record components. These styles can later be applied to the corresponding components in Adaptive Forms Editor.-->

### Nuevas funciones en la versión preliminar de AEM Forms {#forms-new-prerelease-features}

* [Guardar automáticamente un borrador para formularios adaptables basados en componentes principales](/help/forms/save-core-component-based-form-as-draft.md): los usuarios ahora pueden beneficiarse de una función de guardado automático que guarda automáticamente un formulario parcialmente completado como borrador. Pueden volver más tarde para terminar de rellenarlo en el mismo dispositivo o en otro distinto. Esta función mejora las tasas de conversión para las organizaciones al reducir el abandono de formularios, ya que los usuarios no tienen que volver a empezar a rellenar el formulario desde el principio.

* [Actualizar los ámbitos de Adobe Sign fácilmente](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms): puede modificar los ámbitos de una configuración de Adobe Sign directamente desde la página Configuraciones de nube de AEM, lo que facilita y agiliza la actualización de las configuraciones existentes.

* [Compatibilidad con funciones asincrónicas para formularios adaptables](/help/forms/using-async-funct-in-rule-editor.md): cuando el formulario adaptable requiera operaciones asincrónicas, como esperar procesos externos o recuperar datos, puede implementar estas operaciones con funciones personalizadas y configurarlas en el Editor de reglas.

### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo.

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Asistente de IA de AEM Forms

[La IA generativa para los formularios adaptables](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features#aem-forms-ai-assistant-gen-ai) aporta un nuevo nivel de potencia y facilidad a sus procesos de desarrollo de formularios. Le permite crear mejores formularios y más rápido que nunca.

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

### Correcciones de errores {#bug-fixes-cif}

* Se han corregido las pruebas de interfaz de usuario para que funcionen correctamente con los componentes principales de CIF.
* Se ha resuelto un problema con el formato de URL de la categoría que no funcionaba tal como se esperaba en la instancia en la nube.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Configuración para controlar los envíos de formularios {#configuration-submissions}

Para controlar los envíos de formularios de Coral o Foundation en ubicaciones específicas, AEM ha introducido una nueva configuración: `com.adobe.granite.ui.components.FormRestrict`. Esta configuración consta de dos campos:

1. **Adición de rutas permitidas**: especifica las rutas en las que se permiten las acciones de formulario.
1. **Restricción de comportamiento**: determina el comportamiento de las rutas restringidas (rutas no incluidas en la lista de permitidos). Puede elegir entre dos opciones:
   * **Emergente** (predeterminado): muestra una notificación emergente.
   * **Impedir**:Blocks envío de formulario.

>[!NOTE]
>
>Esta configuración no es compatible con todos los formularios de Coral o Foundation ubicados en `/apps`, `/libs`, `/mnt/overlay` y `/mnt/override`.

### Reenvío de registros de autoservicio con la opción de redes avanzadas {#log-forwarding}

Aunque los registros de AEM (incluidos Apache/Dispatcher) y CDN se pueden descargar desde Cloud Manager, muchas organizaciones consideran beneficioso transmitir esos registros a un destino de registro preferido. AEM ahora admite un [reenvío de registro](/help/implementing/developing/introduction/log-forwarding.md) a Azure Blob Storage, Datadog, HTTPS, Elasticsearch (y OpenSearch) y Splunk. De forma opcional, los registros de AEM se pueden reenviar a través de configuraciones de red avanzadas, como el uso de una dirección IP dedicada.

Los usuarios configuran esta característica en forma de autoservicio y la implementan usando la [Canalización de configuración](/help/operations/config-pipeline.md).

### Redirecciones de URL sin canalizaciones para usuarios empresariales {#pipeline-free-redirects}

Las redirecciones del lado del explorador son útiles cuando una página web se ha eliminado o se ha movido, o en el caso de otros escenarios. Con las [Redirecciones de URL sin canalizaciones](/help/implementing/dispatcher/pipeline-free-url-redirects.md), puede colocar un archivo de mapa de reescritura de Apache en una ubicación de publicación de AEM, donde se carga automáticamente, sin necesidad de enviar el archivo al control de código fuente ni iniciar una canalización de Cloud Manager.

Las opciones para publicar el archivo de reescritura incluyen cargarlo como un recurso, usar el Administrador de mapas de reescritura de ACS Commons o interactuar con una interfaz de usuario personalizada.

### Configuración de la canalización para RDE {#config-pipeline-rdes}

Los Entornos de desarrollo rápido (RDE) son una potente herramienta para implementar y probar rápidamente el código y la configuración en un entorno en la nube. Los RDE ahora admiten la [sincronización de archivos YAML de configuración](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline), incluida la configuración de CDN, como las reglas de filtro de tráfico y las transformaciones de solicitud/respuesta, así como el reenvío de registros y otras opciones de configuración. [Consulte la lista completa](/help/operations/config-pipeline.md) de opciones de configuración admitidas para obtener más información.

### Nuevos perfiles de producto {#new-product-profiles}

Cuando se crea un nuevo entorno de AEM, los perfiles de producto aparecen automáticamente en Adobe Admin Console, lo que permite a los administradores asignar acceso a las soluciones y funciones con licencia.

Los nuevos entornos ahora incluyen un conjunto actualizado de perfiles de producto, lo que los hace compatibles con futuras funciones, incluida la generación de credenciales de API en Adobe Developer Console. Los entornos existentes podrán actualizar sus perfiles de producto en una versión futura. [Más información](/help/onboarding/aem-cs-team-product-profiles.md).

### Nuevo AEM Developer Console (Beta pública) {#aem-developer-console-beta}

Pruebe la [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) rediseñada, que ofrece una experiencia más interactiva para depurar código en entornos de la nube.

Cualquiera puede acceder a la versión beta pública haciendo clic en el botón *Nueva consola disponible* en la versión actual de AEM Developer Console. Adobe agradece los comentarios, que puede enviar por correo electrónico a **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Pantalla de paquetes OSGi en AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## Guías de [!DNL Experience Manager] {#guides}

Puede encontrar una lista completa de las funciones nuevas y mejoradas de la última versión de Adobe Experience Manager Guides [aquí](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

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
