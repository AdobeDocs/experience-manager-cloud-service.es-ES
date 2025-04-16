---
title: Notas de la versión 2024.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2024.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 75ecd154-112a-4468-9962-de50bb1f4cd0
source-git-commit: 1481983bde41bda51e725930bae492aa599b6c93
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 91%

---

# Notas de la versión 2024.9.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2024.9.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2022 o 2023.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.9.0) fue el 26 de septiembre de 2024. La próxima versión con funcionalidades (2024.10.0) se planificó para el 31 de octubre de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de septiembre de 2024 para ver un resumen de las funciones añadidas en la versión 2024.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función de Experience Manager Sites {#new-feature-sites}

#### Administración de traducciones {#translation-management}

Los flujos de trabajo de traducción de AEM y las acciones de API ahora activan ciertos eventos para proporcionar datos sobre los cambios de estado de los trabajos de traducción. Los usuarios pueden suscribirse a estos eventos a través de Adobe Developer Console. Consulte [aquí](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/) más información sobre la API de administración de traducciones de AEM.

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Función de acceso rápido en Dynamic Media {#dm-early-access}

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función está diseñada para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos en tiempo real. La IA analiza la pista de audio del vídeo para transcribir la voz y crear subtítulos, que se pueden editar para mejorar la precisión o la personalización. Estos subtítulos ayudan a cumplir con los requisitos de accesibilidad y mejorar la participación en vídeo de los públicos que dependen de la compatibilidad con vídeo basado en texto o la prefieren.

Para obtener acceso anticipado a la compatibilidad con subtítulos generados por IA en su cuenta de Dynamic Media, [cree y envíe un caso de asistencia al cliente de Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Nuevas funciones en el selector de recursos {#asset-selector-new-features}

El selector de recursos ahora admite la exploración de las colecciones para encontrar el recurso deseado.
![Colecciones del selector de recursos](/help/assets/assets/collections-rail-modal-view.png)

### Nuevas funciones en Content Hub {#content-hub-new-features}

Los administradores ahora pueden controlar si necesitan que los activos caducados estén visibles en Content Hub. Si los activos caducados están visibles, también se puede definir si los usuarios pueden descargarlos.

![Activos caducados en Content Hub](/help/assets/assets/view-download-expired-assets.png)

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

### Mejoras {#improvements-fixes-cif}

* Hacer personalizable el límite de categorías.

### Corrección de errores {#bug-fixes-cif}

* Los campos de Commerce no se integran correctamente con el editor de esquemas de metadatos de Assets.
* Problema con campos múltiples de productos del carrusel para arrastrar y soltar.
* Problema con campos múltiples de categorías del carrusel para arrastrar y soltar.
* Al hacer clic no funciona para los menús de la información de página en la página del editor de categorías y productos.
* El número de pedido no está visible en la página de confirmación de pedido.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Edge Side Includes (ESI) para cargar contenido dinámico {#esi}

La CDN administrada por Adobe es ahora compatible con [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL más altos, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL menores). Esta función se implementará gradualmente.

### Autenticación básica en CDN {#basicauth-cdn}

Proteja determinados recursos de contenido mostrando un cuadro de diálogo de autenticación básica que requiera un nombre de usuario y una contraseña. Esta función se dirige principalmente a casos de uso de autenticación ligera, como el de las partes interesadas empresariales que revisan el contenido, en lugar de servir como solución completa para los derechos de acceso de usuarios finales. La lista de nombre de usuario y contraseñas se administra mediante un archivo de configuración en Git que se implementa mediante la canalización de configuración, con una referencia a variables de entorno de Cloud Manager de tipo secreto. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

### Redirecciones del lado del servidor {#server-side-redirects}

Declare [redirecciones de explorador](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) en un archivo de configuración Git que se implementan y evalúan en la CDN. Esto puede resultar útil para escenarios como eliminar páginas, cambiar la estructura del sitio y optimizar la SEO.

### Nuevo AEM Developer Console (Beta pública) {#aem-developer-console-beta}

Pruebe la [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) rediseñada, que ofrece una experiencia más interactiva para depurar código en entornos de la nube.

Cualquiera puede acceder a la versión beta pública haciendo clic en el botón *Nueva consola disponible* en la versión actual de AEM Developer Console. Adobe agradece los comentarios, que puede enviar por correo electrónico a **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Pantalla de paquetes OSGi en AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### Los usuarios empresariales pueden declarar redirecciones fuera de Git (programa para primeros usuarios) {#apache-rewritemaps-early-adopter}

De forma similar a la versión AEM 6.5, Apache/Dispatcher introducirá mapas de reescritura colocados en una ubicación específica del repositorio de publicación y los cargará sin requerir la ejecución de una canalización de niveles web. Este método permite a los usuarios empresariales declarar redirecciones mediante una hoja de cálculo o una interfaz de usuario, como el administrador de mapas de redirección de ACS Commons o una aplicación personalizada. Únase al programa para primeros usuarios enviando un correo electrónico a **<aemcs-cdn-config-adopter@adobe.com>**.

### Canalización de configuración para RDE (programa para primeros usuarios) {#config-pipeline-rdes-early-adopter}

La [Canalización de configuración](/help/operations/config-pipeline.md) se usa para implementar configuraciones de archivo yaml, incluidas las opciones de CDN (reglas de filtro de tráfico, transformaciones de solicitud/respuesta, etc.). Únase al programa para primeros usuarios enviando un correo electrónico a **<aemcs-cdn-config-adopter@adobe.com>** y poder implementar estas mismas configuraciones en RDE (entornos de desarrollo rápido), que utilizan CLI.

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
