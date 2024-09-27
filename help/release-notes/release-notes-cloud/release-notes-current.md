---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 2d5fa0b15456ad9838fa236a2b5c79d41a9af7fe
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

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

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.9.0) fue el viernes, 26 de septiembre de 2024. La próxima versión con funcionalidades (2024.10.0) se planificó para el viernes, 31 de octubre de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!--  ## Release Video {#release-video}

Have a look at the September 2024 Release Overview video for a summary of the features added in the 2024.9.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función de Experience Manager Sites {#new-feature-sites}

#### Administración de traducción {#translation-management}

AEM déclencheur Los flujos de trabajo de traducción y las acciones de API ahora incluyen eventos para proporcionar información sobre los cambios de estado del trabajo de traducción. Los usuarios pueden suscribirse a estos eventos a través de Adobe Developer Console. AEM Consulte [aquí](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/) para obtener más información sobre la API de administración de traducciones de.

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Función de acceso rápido en Dynamic Media {#dm-early-access}

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función está diseñada para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos en tiempo real. La IA analiza la pista de audio del vídeo para transcribir la voz y crear subtítulos, que se pueden editar para mejorar la precisión o la personalización. Estos subtítulos ayudan a cumplir con los requisitos de accesibilidad y mejorar la participación en vídeo de los públicos que dependen de la compatibilidad con vídeo basado en texto o la prefieren.

Para obtener acceso anticipado a la compatibilidad con subtítulos generados por IA en su cuenta de Dynamic Media, [cree y envíe un caso de asistencia al cliente de Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Nuevas funciones del Selector de recursos {#asset-selector-new-features}

El Selector de recursos ahora admite la exploración de Colecciones para encontrar el recurso deseado.
![Colecciones de selectores de recursos](/help/assets/assets/collections-rail-modal-view.png)

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
* Problema con el multicampo de productos de carrusel para arrastrar y soltar.
* Problema con el campo múltiple de categoría de carrusel para arrastrar y soltar.
* Al hacer clic no funciona para los menús de la página de información sobre la categoría y la página del editor de productos.
* El número de pedido no está visible en la página de confirmación de pedido.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Edge Side Includes (ESI) para cargar contenido dinámico {#esi}

La CDN administrada por Adobe es ahora compatible con [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL más altos, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL menores). Esta función se implementará gradualmente.

### Autenticación básica en CDN {#basicauth-cdn}

Proteja determinados recursos de contenido mostrando un cuadro de diálogo de autenticación básica que requiera un nombre de usuario y una contraseña. Esta función se dirige principalmente a casos de uso de autenticación ligera, como el de las partes interesadas empresariales que revisan el contenido, en lugar de servir como solución completa para los derechos de acceso de usuarios finales. La lista de nombre de usuario y contraseñas se administra mediante un archivo de configuración en Git que se implementa mediante la canalización de configuración, con una referencia a variables de entorno de Cloud Manager de tipo secreto. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

### Redirecciones del lado del cliente {#client-side-redirects}

Declare [redirecciones de explorador](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) en un archivo de configuración de Git que se implementan y evalúan en la red de distribución de contenido (CDN). Esto puede resultar útil para escenarios como la eliminación de páginas, el cambio de estructura del sitio y la optimización de los motores de búsqueda.

### AEM Nuevo Developer Console (Beta público) {#aem-developer-console-beta}

AEM Pruebe un [Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) rediseñado, que ofrece una experiencia más interactiva para depurar código en entornos de la nube.

AEM Cualquiera puede acceder a la versión beta pública si hace clic en el botón *Nueva consola disponible* del Developer Console de la versión actual de la aplicación de la. El Adobe agradece los comentarios, que puede enviar por correo electrónico a **<aemcs-new-devconsole-ui-beta@adobe.com>**.

AEM ![Pantalla de paquetes OSGi en la pantalla de los paquetes OSGi en el Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### Los usuarios empresariales pueden declarar redirecciones fuera de Git (programa para primeros usuarios) {#apache-rewritemaps-early-adopter}

AEM De forma similar a la versión 6.5, Apache/dispatcher incorpora mapas de reescritura colocados en una ubicación específica en el repositorio de publicación y los carga sin requerir la ejecución de una canalización de nivel web. Este método permite a los usuarios empresariales declarar redirecciones mediante una hoja de cálculo o una interfaz de usuario, como el administrador de mapas de redirección de ACS Commons o una aplicación personalizada. Únase al programa de usuarios que lo adoptaron por correo electrónico **<aemcs-cdn-config-adopter@adobe.com>**.

### Canalización de configuración para RDE (programa de adopción anticipada) {#config-pipeline-rdes-early-adopter}

La [Canalización de configuración](/help/operations/config-pipeline.md) se usa para implementar configuraciones de archivo yaml, incluidas las opciones de CDN (reglas de filtro de tráfico, transformaciones de solicitud/respuesta, etc.). Únase al programa pionero enviando por correo electrónico a **<aemcs-cdn-config-adopter@adobe.com>** para implementar estas mismas configuraciones en RDE (entornos de desarrollo rápido), que utilizan una CLI.

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
