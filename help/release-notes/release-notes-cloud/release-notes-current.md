---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
nudge: please
source-git-commit: f5d4707fdc5a920f11edbd1f1784f1f7cc6d082a
workflow-type: tm+mt
source-wordcount: '4356'
ht-degree: 16%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores, como 2024 o 2025.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como la versión de característica actual de [!DNL Cloud Service] (2026.6.0) es el 25 de junio de 2026. La próxima versión de la funcionalidad (2026.7.0) está planificada para el 30 de julio de 2026.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the May 2026 Release Overview video for a summary of the features added in the 2026.5.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3491490/?quality=12)

-->

## Programas de AEM Beta {#aem-beta-programs}

Los programas beta de Adobe Experience Manager (AEM) son una forma para que los clientes obtengan acceso a las funciones y el código de la versión preliminar, proporcionen comentarios y guíen el futuro de AEM.

>[!IMPORTANT]
>
>Las versiones de Beta pueden contener defectos y se proporcionan &quot;TAL CUAL&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o admitir de otro modo (mediante los Servicios de soporte de Adobe o de otro modo) las versiones beta. Adobe recomienda a los clientes tener cuidado y no depender del funcionamiento o el rendimiento correctos de las versiones beta, ni de la documentación o los materiales adjuntos. Las funciones y las API de la versión beta están sujetas a cambios sin previo aviso. Por lo tanto, cualquier uso de las versiones beta es totalmente bajo el propio riesgo del cliente.

**Ventajas de participar**

El acceso anticipado a las funciones que Adobe está desarrollando permite a los clientes y socios proporcionar comentarios y dar forma al desarrollo de productos. También les ayuda a prepararse para adoptar nuevas capacidades antes de la disponibilidad general.

**Programas beta actuales**

Las siguientes secciones enumeran los programas beta activos.

### Agentes en AEM {#agents-in-aem}

Si desea explorar las nuevas y poderosas capacidades de AEM en producción, administración, optimización, detección y desarrollo, [obtenga información sobre cómo puede obtener acceso a ellas aquí.](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM Foundation (programas de Beta) {#aem-foundation-beta-programs}

Ver [programas beta de AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programas de Beta) {#cloud-manager-beta-programs}

Ver [programas beta de Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

### AEM Assets (programas de Beta) {#aem-assets-beta-programs}

Ver [programas beta de AEM Assets](#assets-beta-program-features).

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Fragmentos de contenido visual {#visual-content-fragments}

AEM ahora admite [Fragmentos de contenido visual](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md), que procesan la salida de fragmentos de contenido como experiencias de HTML con formato mediante plantillas de HTML adjuntas. Esto permite a los autores de contenido obtener una vista previa del contenido estructurado y validarlo en su forma visual final antes de la publicación, así como ofrecer experiencias modulares de forma coherente en todos los canales, incluidos la web, el correo electrónico y Edge Delivery Services. Hay disponible una plantilla genérica integrada para garantizar la calidad básica sin requerir una plantilla personalizada.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Abrir recursos de Photoshop en el editor incrustado de Adobe Express**

Ahora puede abrir archivos Adobe Photoshop (.psd) además de los formatos JPEG y PNG en el editor incrustado de Adobe Express desde la vista de Assets y Content Hub. Esta mejora permite a los equipos creativos y de marketing trabajar con archivos de diseño por niveles sin salir de los AEM Assets, lo que optimiza las actualizaciones de contenido y reduce la necesidad de cambiar entre aplicaciones. La compatibilidad con PSD acelera los flujos de trabajo de creación de contenido, a la vez que preserva la flexibilidad de los recursos de diseño de origen. Los usuarios pueden guardar las creaciones remezcladas resultantes como recursos listos para el canal en AEM.

**Importar recursos de Adobe Illustrator y Adobe InDesign de AEM Assets a Adobe Express**

Adobe Express ahora admite la importación de archivos Adobe Illustrator (.ai) y Adobe InDesign (.indd) de AEM Assets mediante el complemento Assets. Los archivos de Adobe Illustrator se pueden importar en el documento actual o en un nuevo documento Express. Los archivos Adobe InDesign se pueden importar en un nuevo documento Express. Esta capacidad permite a los equipos creativos y de marketing acceder y reutilizar los recursos de diseño aprobados con mayor facilidad, lo que acelera la creación de contenido y ayuda a garantizar experiencias de marca coherentes en todos los canales.

>[!IMPORTANT]
>
>Esta función está disponible como función de disponibilidad limitada. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.

**Mantener linaje de recursos entre Adobe Express y los AEM Assets**

Los AEM Assets ahora conservan la información de linaje de los recursos creados en Adobe Express mediante recursos procedentes de AEM. Esta capacidad registra las relaciones entre los recursos de origen y el contenido resultante y lo almacena como metadatos de recurso en AEM, lo que permite a las organizaciones rastrear cómo se reutilizan los recursos aprobados en los flujos de trabajo creativos.

Al mantener los metadatos de linaje de recursos, los equipos pueden mejorar la gobernanza, el cumplimiento y la transparencia de supply chain de contenido. También ayuda a los especialistas en marketing y a los administradores de contenido a comprender mejor la reutilización de recursos, apoyar las iniciativas de administración de derechos y rastrear el origen de los recursos utilizados en el contenido publicado.

>[!IMPORTANT]
>
>Esta función está disponible como función de disponibilidad limitada. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.

**Integración de AEM con Workfront Planning y GenStudio for Performance Marketing para metadatos de campaña estándar**

Cuando AEM Assets está integrado con [Workfront Planning y GenStudio for Performance Marketing](https://experienceleague.adobe.com/en/docs/workfront/using/adobe-workfront-planning/planning-and-genstudio-integration/planning-and-genstudio-integration-article-index), los campos de metadatos de campaña, incluidos Nombre de campaña, Región, Canal, Persona y Producto, ahora están disponibles en el carril de propiedades de la vista de recursos en una pestaña de solo lectura dedicada de Campaign. Cuando los usuarios de Workfront Planning conectan recursos de AEM a GenStudio con los objetos respectivos de Adobe GenStudio Workspace, se añaden automáticamente valores específicos (por ejemplo, un nombre de campaña específico) a los metadatos del recurso de AEM.

La integración permite a los usuarios descubrir y buscar recursos rápidamente en función de los atributos de la campaña. Esta mejora mejora mejora la capacidad de búsqueda de recursos, optimiza los flujos de trabajo de administración de contenido y ayuda a los equipos a localizar los recursos adecuados para iniciativas de marketing específicas de forma más eficaz.

>[!IMPORTANT]
>
>Esta función está disponible como función de disponibilidad limitada y requiere licencias para Workfront Planning y GenStudio for Performance Marketing. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.


### Nuevas funciones en Dynamic Media con funciones de OpenAPI {#new-features-dynamic-media-openapi}

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Dynamic Media con funciones de OpenAPI utilizan inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función está diseñada para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos en tiempo real. La IA analiza la pista de audio del vídeo para transcribir la voz y crear subtítulos, que se pueden editar para mejorar la precisión o la personalización. Estos subtítulos ayudan a cumplir con los requisitos de accesibilidad y mejorar la participación en vídeo de los públicos que dependen de la compatibilidad con vídeo basado en texto o la prefieren.

>[!IMPORTANT]
>
>Esta función está disponible como función de disponibilidad limitada. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.

**Transcripciones de vídeo incrustadas para mejorar la accesibilidad y la SEO**

El componente Dynamic Media ahora incrusta transcripciones de vídeos para mejorar la accesibilidad de los clientes. Son transcripciones procesadas del lado del servidor (SSR) que aumentan directamente la visibilidad SEO y LLM de los vídeos. También incrusta un VideoObject [ref https://schema.org/VideoObject] compatible que ayuda al motor de búsqueda y a las herramientas LLM a reconocer vídeos en su página.

>[!IMPORTANT]
>
>Esta función está disponible como función de disponibilidad limitada. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.

**Miniaturas personalizadas para vídeos**

Dynamic Media con funciones de OpenAPI ahora le permite cargar miniaturas personalizadas para recursos de vídeo. Al reemplazar las miniaturas generadas automáticamente por imágenes de marca o creadas específicamente, las organizaciones pueden mejorar la presentación del contenido, mejorar la capacidad de detección de recursos y crear una experiencia de visualización más atractiva.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones en AEM Forms

#### Editor de comunicación interactivo

El editor de [comunicaciones interactivas (IC)](/help/forms/interactive-communication/introduction.md) ya está disponible en AEM Forms as a Cloud Service. Es una solución basada en explorador para crear, administrar y entregar correspondencia interactiva basada en datos, como correspondencia comercial, documentos, declaraciones, avisos de beneficios, correos de marketing, facturas y kits de bienvenida.

![Editor de comunicación interactiva](/help/forms/assets/ic-editor.png)

* **Editor basado en la nube**: A diferencia de AEM Forms Desktop Designer, que solo se puede instalar en equipos Windows, el editor de comunicaciones interactivas se ejecuta en cualquier explorador moderno sin necesidad de instalación. Este enfoque basado en la nube elimina los problemas de instalación, proporciona accesibilidad entre plataformas y permite la colaboración desde cualquier ubicación con acceso a Internet. Para obtener más información, consulte [Introducción al editor de CI](/help/forms/interactive-communication/getting-started.md).

* **Componentes y propiedades**: cree comunicaciones con una biblioteca de componentes de arrastrar y soltar: campos de texto, tablas, imágenes, códigos de barras, subformularios y mucho más. Configure el diseño, la tipografía, los márgenes y la apariencia a través del panel Propiedades. Para obtener más información, consulte [Introducción al editor de comunicaciones interactivas](/help/forms/interactive-communication/introduction.md).

* **Enlace de datos**: conecte los componentes a los modelos de datos de formulario (FDM) mediante la asignación visual para obtener resultados personalizados controlados por datos. Para obtener más información, consulte [Enlace de datos en el editor de comunicaciones interactivas](/help/forms/interactive-communication/configure-data-binding.md).

* **Editor de reglas**: cree acciones dinámicas impulsadas por datos directamente en sus documentos mediante una interfaz intuitiva que apunte y haga clic. Defina fácilmente la lógica condicional, automatice los flujos de trabajo y personalice el contenido sin escribir código. Para obtener más información, consulte [Crear reglas en el editor de comunicaciones interactivas](/help/forms/interactive-communication/use-the-rule-editor.md).

* **Plantillas y fragmentos de documento**: cree plantillas reutilizables y bloques de contenido modular (encabezados, pies de página, exenciones de responsabilidad) para mantener la coherencia y la eficacia en varias comunicaciones. Para obtener más información, consulte [Crear una plantilla](/help/forms/interactive-communication/create-interactive-communication-template.md) y [Crear un fragmento](/help/forms/interactive-communication/create-interactive-communication-fragment.md).

* **Bloqueo de plantillas**: bloquea los elementos de contenido y diseño dentro de las plantillas para mantener la integridad de la marca y evitar modificaciones no autorizadas. Para obtener más información, consulte [Bloqueo de plantilla](/help/forms/interactive-communication/enable-template-lock.md).

* **Vista previa de PDF**: obtenga una vista previa de la comunicación interactiva sin datos, archivos JSON locales o modelos de datos para realizar pruebas flexibles basadas en datos. Para obtener más información, consulte [Vista previa de PDF](/help/forms/interactive-communication/generate-pdf-preview.md).

* **Fuentes personalizadas**: incruste fuentes personalizadas o aprobadas por la organización para garantizar un procesamiento de PDF coherente y de marca en todos los dispositivos. Para obtener más información, vea [Agregar fuentes personalizadas](/help/forms/interactive-communication/add-custom-fonts.md).

* **Importar y exportar**: migre y reutilice sin problemas la comunicación interactiva con sus fragmentos y modelos de datos entre entornos. Para obtener más información, consulte [Importar y exportar](/help/forms/interactive-communication/import-and-export-the-interactive-communication.md).

* **Desbordamiento de contenido**: la opción &quot;Permitir saltos de página dentro del contenido&quot; permite diseños fluidos para una edición sin problemas de varias páginas y una mejor administración de texto para documentos complejos. Para obtener más información, consulte [Control de desbordamiento de contenido](/help/forms/interactive-communication/handle-content-overflow.md).

* **Edición de archivos XDP**: edite los archivos XDP en un explorador en lugar de Forms Designer, que solo se ejecuta en el escritorio de Microsoft Windows. Para obtener más información, consulte [Compatibilidad con la edición XDP](/help/forms/interactive-communication/support-xdp-editing.md).

* **IU asociada**: Una interfaz de tiempo de ejecución simplificada para que los asociados de cara al cliente introduzcan datos y generen comunicaciones personalizadas en tiempo real. Invoque la interfaz de usuario de Associate directamente en las instancias de Publish para simplificar la integración y acelerar la implementación en todos los entornos. Para obtener más información, consulte [Información general sobre la interfaz de usuario asociada](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md), [Habilitar y configurar la interfaz de usuario asociada](/help/forms/interactive-communication/enable-configure-associate-ui.md) e [Integrar la interfaz de usuario asociada](/help/forms/interactive-communication/invoke-associate-ui.md).

* **Numeración dinámica de páginas**: muestra automáticamente &quot;Nº de página de ##&quot; en las páginas maestras para una paginación clara y coherente en los documentos de varias páginas. Para obtener más información, consulte [Numeración dinámica de páginas](/help/forms/interactive-communication/implement-dynamic-page-numbering.md).

* **Creación de versiones y comentarios en el editor de comunicaciones interactivas**: el editor de comunicaciones interactivas ahora admite las versiones y los comentarios para que los autores puedan guardar versiones etiquetadas, capturar comentarios del revisor, revertir a estados anteriores y mantener un seguimiento de auditoría en el ciclo de vida del contenido. Para obtener más información, consulte [Creación de versiones y comentarios en el editor de comunicaciones interactivas](/help/forms/interactive-communication/versioning-and-commenting-in-interactive-communication-editor.md).

* **Revisar y anotar una comunicación interactiva**: los revisores ahora pueden realizar anotaciones en las comunicaciones interactivas en una vista de solo lectura dedicada, anclar comentarios a componentes específicos del lienzo y compartir comentarios en un lugar sin editar el diseño. Los autores pueden realizar un seguimiento y resolver anotaciones directamente en el editor. Para obtener más información, vea [Revisar y anotar una comunicación interactiva](/help/forms/interactive-communication/howto/review-and-annotate-interactive-communication.md).

* **Comparar versiones de comunicaciones interactivas**: ahora puede comparar dos versiones guardadas cualquiera de una comunicación interactiva en paralelo como vistas previas de PDF para revisar los cambios de diseño y contenido estático antes de publicarla. Para obtener más información, vea [Comparar versiones de comunicaciones interactivas](/help/forms/interactive-communication/howto/compare-interactive-communication-versions.md).

* **Combinar y dividir celdas de tabla**: el Editor de comunicaciones interactivas ahora admite la combinación de celdas de tabla adyacentes y la división de las celdas combinadas en columnas individuales, lo que permite abarcar encabezados, filas de resumen y diseños de tabla más flexibles. Para obtener más información, vea [Combinar y dividir celdas de tabla](/help/forms/interactive-communication/howto/merge-and-split-table-cells.md).

* **Mover un componente a la página maestra**: ahora puede mover un componente de una página de diseño a la página maestra en una acción para que aparezca de forma coherente en todas las páginas de una comunicación interactiva sin volver a crearla. Para obtener más información, vea [Mover un componente a la página maestra](/help/forms/interactive-communication/howto/move-component-to-master-page.md).

* **Configurar opciones desplegables para la interfaz de usuario asociada**: los campos desplegables de la interfaz de usuario asociada ahora utilizan un modelo de **enlace de opciones**. Los autores configuran **Enlazar a partir de datos** para listas de opciones dinámicas u opciones manuales estáticas, de modo que los asociados vean las opciones correctas y el valor preseleccionado. **Enlace de datos** no es compatible con los campos desplegables. Para obtener más información, consulte [Configurar opciones desplegables para la interfaz de usuario asociada](/help/forms/interactive-communication/associateui/configure-dropdown-options-binding.md).

* **Configurar variables enlazadas y no enlazadas para la interfaz de usuario asociada**: las variables enlazadas y no enlazadas de los componentes **Texto** ahora se pueden configurar para la interfaz de usuario asociada. Los autores eligen si los asociados deben editar todo el bloque de texto en línea en la vista previa del documento o introducir valores para variables individuales en el panel de entrada de datos. Los nombres de variables duplicados propagan los valores en todas las ocurrencias coincidentes en la vista previa. Para obtener más información, vea [Configurar variables enlazadas y no enlazadas para la interfaz de usuario asociada](/help/forms/interactive-communication/associateui/configure-bound-unbound-variables-associate-ui.md).

#### Opciones adicionales de CAPTCHA para la protección de bots

AEM Forms ahora admite dos soluciones CAPTCHA adicionales para proteger Forms adaptable de bots y envíos de correo no deseado, además del reCAPTCHA de Google ya disponible. Esto le proporciona más opciones y flexibilidad para proteger los formularios.

* **Torniquete Cloudflare**: Un CAPTCHA sin fricción que verifica a los usuarios a través de un desafío simple sin requerir interacción explícita, mejorando la experiencia del usuario. Para obtener más información, vea [Usar el torniquete en un formulario adaptable para componentes principales](/help/forms/integrate-adaptive-forms-turnstile-core-components.md) y [Usar el torniquete en un formulario adaptable para componentes de base](/help/forms/integrate-adaptive-forms-turnstile.md).
* **hCaptcha**: Un CAPTCHA centrado en la privacidad que ofrece una alternativa fácil de usar con énfasis en la privacidad de datos, el equilibrio entre la seguridad y la experiencia del usuario. Para obtener más información, consulte [Usar hCaptcha en un formulario adaptable para componentes principales](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md) y [Usar hCaptcha en un formulario adaptable para componentes de base](/help/forms/integrate-adaptive-forms-hcaptcha.md).

### Funciones de usuario pionero

#### Documento de registro para formularios incrustados en AEM Sites

Los autores ahora pueden configurar y generar un documento de registro (PDF de envío) para los componentes principales de Forms adaptable incrustados en páginas de AEM Sites. La configuración del DoR (que incluye la generación automática, las plantillas XDP personalizadas y la personalización de marca) está disponible directamente desde el **contenedor de formulario adaptable** en el editor de páginas de Sites. [Más información](/help/forms/generate-document-of-record-core-components.md#configure-document-of-record-for-forms-embedded-in-aem-sites).

#### Plantillas XDP personalizadas específicas de la configuración regional para el documento de registro

Cuando asocia una plantilla XDP personalizada para el DoR, puede proporcionar versiones específicas de la configuración regional en la misma carpeta mediante la convención `basename.<locale>.xdp` (por ejemplo, `a.xdp` y `a.fr.xdp`). AEM Forms selecciona automáticamente la plantilla que coincide con la configuración regional del formulario al generar la PDF de envío, con reserva a la plantilla predeterminada. [Más información](/help/forms/generate-document-of-record-core-components.md#locale-specific-custom-xdp-templates-for-document-of-record).

#### Caducidad del acuerdo de Adobe Sign

Puede establecer cuánto tiempo deben completar la firma los destinatarios especificando **Caducidad del documento (días)** en la sección **Firma electrónica** de un formulario adaptable. El valor se envía a Adobe Sign como `daysUntilSigningDeadline`. Si se deja vacío, el acuerdo no caduca. [Más información](/help/forms/working-with-adobe-sign.md#set-document-expiration-for-an-adobe-sign-agreement).

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] como [!DNL Cloud Service] nuevas características de base {#foundation-new}

#### Interfaz de IA conversacional para preguntas sobre Cloud Manager {#devagent-cloudmanager}

El Agente de desarrollo se expande para administrar preguntas relacionadas con Cloud Manager a través de [Cloud Manager Job](/help/ai-in-aem/agents/brand-experience/development/development.md#cloud-manager-job). En el asistente de IA, recupere información sobre programas, entornos y canalizaciones (por ejemplo, estado de ejecución). Encuentre rápidamente vínculos a registros de errores, registros de acceso y registros de generación.

#### Mejoras en el trabajo del agente de resolución de problemas de canalización {#devagent-pipeline-troubleshooting}

El [trabajo de solución de problemas de canalización](/help/ai-in-aem/agents/brand-experience/development/development.md#cloud-manager-pipeline-troubleshooting) del agente de desarrollo ayuda a los desarrolladores a diagnosticar y resolver problemas en implementaciones de AEM as a Cloud Service. Las nuevas funciones incluyen:

* Compatibilidad con la canalización de configuración de nivel web: además de admitir canalizaciones de pila completa (implementación y calidad de código), el agente de desarrollo ahora admite la resolución de problemas para la **canalización de configuración de nivel web**

* Widget de inicio de experiencia para canalizaciones con errores: La función de administrador y TI verá un [nuevo widget](/help/ai-in-aem/agents/brand-experience/development/development.md#troubleshoot-from-experience-home) que resaltará los errores de canalización. Un botón en el que se puede hacer clic inicia el trabajo de resolución de problemas de canalización en el asistente de IA.

#### Administre las horas tranquilas y actualice los períodos gratuitos con el asistente de IA {#quiet-hours-ai}

Ahora puede ver, crear y editar [Horas tranquilas y actualizar periodos gratis](/help/ai-in-aem/agents/brand-experience/development/development.md#control-updates-job) directamente a través del Asistente de IA de AEM.La principal ventaja es que se cometen menos errores de programación. A medida que realiza una solicitud, el asistente le guía a través de lo que es posible y marca los límites aplicables, como el límite de tres períodos, el espacio obligatorio de una semana entre períodos y las ventanas de exclusión de mantenimiento planificadas que no se pueden programar. Por lo tanto, en lugar de descubrir una restricción después de una configuración fallida, los propietarios del negocio y los administradores de implementación se dirigen a una programación válida en la misma conversación. Esto protege las ventanas empresariales críticas de las actualizaciones de mantenimiento automáticas, al tiempo que reduce las idas y venidas y la configuración incorrecta.

### [!DNL Experience Manager] como [!DNL Cloud Service] avisos importantes de Foundation {#foundation-notices}

#### Errores enriquecidos de autenticación IMS {#ims-auth-rich-errors}

Para solucionar problemas de integraciones de IMS, `imsauth` ha agregado compatibilidad con *errores enriquecidos*.

En lugar de devolver únicamente un código de estado HTTP, estos errores proporcionan un contexto adicional para ayudar a diagnosticar y resolver los problemas que pueden bloquear la autenticación y el acceso.

#### Degradaciones de API de Java {#java-api-deprecation}

Es fundamental eliminar el uso de API obsoletas.

Desde el **14 de abril de 2026**, las canalizaciones de Cloud Manager que contienen código mediante API dirigidas a la eliminación el 26/2/2026 **fallan durante el paso de calidad del código**. Las implementaciones se bloquearán hasta que se elimine el uso de API obsoleto. *Esto puede impedir que publique actualizaciones con plazos específicos y podría afectar a las operaciones de su empresa.*

A partir del **23 de julio de 2026**, los entornos que sigan usando estas API obsoletas **no recibirán actualizaciones críticas de la versión de Adobe** y no estarán sujetos a los compromisos estándar de Adobe en cuanto a rendimiento y disponibilidad. Como resultado, no recibirá nuevas funciones ni correcciones de errores, la estabilidad y el tiempo de actividad de la aplicación podrían verse afectados negativamente y la exposición al riesgo de seguridad podría aumentar aún más.

Consulte el [artículo sobre obsolescencia](/help/release-notes/deprecated-removed-features.md#aem-apis) para obtener más detalles, pero, para mayor comodidad, estas API se enumeran a continuación:

+++ Expandir para ver las funciones obsoletas de la API de Java

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

#### El servidor MCP local de Dispatcher forma parte de AEM SDK {#local-dispatcher-mcp}

El servidor MCP local de Dispatcher ahora está incluido en **AEM SDK** en el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html), empaquetado dentro del zip de herramientas de AEM Dispatcher. Anteriormente, el servidor MCP local de Dispatcher estaba empaquetado en una lista beta independiente de herramientas de AEM Dispatcher.

El servidor MCP local de Dispatcher permite que las herramientas de IA validen la configuración HTTPD de Dispatcher y Apache, rastreen la administración de solicitudes e inspeccionen el comportamiento de la caché con una instancia de Dispatcher que se ejecuta localmente en Docker.

#### Preparación para Java 25: Cronología de actualización del tiempo de ejecución de AEM Cloud Service

Java 25 es la próxima versión de soporte a largo plazo (LTS) después de Java 21, que ofrece mejoras en rendimiento, productividad de desarrollador y seguridad:

- **Rendimiento**: La reducción del espacio de memoria, la recolección de elementos no utilizados más eficiente y el calentamiento más rápido de JVM benefician las implementaciones nativas de la nube.
- **Productividad del desarrollador**: la inicialización de objetos más limpia, la coincidencia de patrones más expresiva y la administración simplificada de tareas simultáneas reducen las plantillas y mejoran la claridad del código.
- **Seguridad**: se ha modernizado la API de derivación de claves criptográficas para simplificar los flujos de trabajo de seguridad comunes.

Para ayudar a las organizaciones a planificar las pruebas y la validación antes de la actualización necesaria del tiempo de ejecución de Java 25, Adobe proporciona las siguientes fechas objetivo. Cualquier actualización de esta cronología se comunicará mediante las notas de la versión.

| Período de tiempo | Hito |
|---|---|
| **Mediados de octubre de 2026** | AEM Cloud Service SDK admite el tiempo de ejecución de Java 25. El JDK de Java 25 está disponible para su descarga en el portal de distribución de software de Adobe. |
| **Noviembre de 2026** | Se recomienda a los clientes que habiliten de forma opcional el tiempo de ejecución de Java 25 en sus entornos de nube para validar el comportamiento. La adopción temprana maximiza el tiempo para salir a la superficie y resolver los problemas. |
| **Febrero - Mayo de 2027** | Adobe migrará gradualmente entornos más bajos (RDE, Dev) al tiempo de ejecución de Java 25. Los clientes deben validar el comportamiento e informar de problemas inesperados, y se les recomienda que también habiliten los entornos de ensayo y producción. Hay disponible una reversión temporal a Java 21 para resolver cualquier problema. |
| **Junio de 2027** | Todos los tiempos de ejecución del entorno (incluidos ensayo y producción) migran a Java 25. El tiempo de ejecución de Java 21 está fuera de servicio. AEM Cloud Service SDK ya no admitirá Java 21. |

AEM Cloud Service sigue admitiendo la compilación de código de cliente con Java 11, Java 17 y Java 21. Sin embargo, Adobe recomienda crear con Java 25 (una vez disponible en AEM) para aprovechar al máximo las últimas funciones de idioma y mejoras de rendimiento.

### Características de [!DNL Experience Manager] como [!DNL Cloud Service] pionero de la base {#foundation-early-adopter}

#### Funciones de AEM Edge (*Programa Beta* público) {#edge-functions}

[Funciones de AEM Edge](/help/implementing/developing/introduction/edge-functions.md) ahora se encuentra en la versión beta pública, por lo que puede probarlas de forma automática sin ponerse en contacto con Adobe para habilitarlas.

Esta función le permite ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge. Está disponible para proyectos AEM Cloud Service Java Stack y Edge Delivery Services para clientes de AEM Sites.

Los casos de uso comunes incluyen los siguientes:

* Personalización de contenido en función de la geolocalización, el tipo de dispositivo o los atributos del usuario
* Actuación como middleware entre la CDN y su origen
* Modificar el formato de las respuestas de API de terceros (y tal vez añadir las respuestas de varias API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend

Siga [este tutorial](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/edge-functions/overview) para ver una explicación detallada de las variaciones de pila Java de Edge Delivery Services y AEM as a Cloud Service.

*Al usar AEM Edge Functions Beta, reconoce que aún se encuentra en desarrollo y que no debe confiar en el correcto funcionamiento de la tecnología o en la disponibilidad de los datos. Esta función se proporciona tal cual,
puede cambiar sin previo aviso y no está cubierto por los SLA de producción.*

#### Instantáneas para RDE (programa *Public Beta*) {#rde-snapshot-program}

Las instantáneas para entornos de desarrollo rápido (RDE) ya están en versión beta pública, por lo que puede probarlas sin ponerse en contacto con Adobe para habilitarlas.

Los RDE ahora admiten una característica [para tomar una instantánea](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots) del estado actual del código y el contenido, que se puede restaurar más adelante. Esto puede resultar útil al sincronizar código que puede ser necesario revertir o al cambiar entre el desarrollo de distintas características. También es posible restaurar solo el contenido mutable como punto de partida conocido para realizar pruebas.

*Al usar la Beta de instantáneas de RDE, reconoce que aún se encuentra en desarrollo y que no debe confiar en el correcto funcionamiento de la tecnología o en la disponibilidad de los datos. Si bien hemos probado esta característica ampliamente, existe una pequeña posibilidad de que su RDE pueda volverse inestable. Si esto sucede, un restablecimiento lo restaurará a un estado de trabajo.*

#### Resolución de problemas de replicación de IA (programa Beta) {#replication-ai-troubleshooting-beta}

Con el Asistente de IA en AEM Author y otras interfaces, puede solucionar problemas relacionados con la replicación, como colas bloqueadas. Para unirse al programa Beta, envíe un correo electrónico a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com) en el que describa su interés.

#### Implementaciones de producción controladas para probar el código antes de aceptar tráfico en directo (programa Beta) {#canary-beta}

Valide una compilación de producción con tráfico de prueba solamente interno antes de exponerla a los usuarios finales. Realice envíos a producción, dirija solo el tráfico controlado (mediante un encabezado especial), monitorice el comportamiento y, a continuación, promocione al tráfico en directo o revierta el proceso, sin afectar a los clientes.

Envíe un correo electrónico a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acceso y compartir comentarios.

#### Evaluación del código de AEM y corrección automática a través del agente de IA del IDE (Programa Beta) {#ide-ai-aemcode-issues}

Los equipos de AEM Cloud Service apilados en Java que utilizan el desarrollo asistido por IA en herramientas como Cursor, Claude Code, Visual Studio e IntelliJ ahora pueden ir más allá. Una nueva habilidad [del agente IDE de evaluación de código](/help/ai-in-aem/local-development-with-ai-tools.md#use-the-code-assessment-skill) detecta y corrige automáticamente los problemas directamente en la base de código de AEM, lo que reduce los ciclos de revisión y detecta los problemas más temprano en el desarrollo.

Las comprobaciones admitidas incluyen:
* sustitución de API obsoletas
* modernizar la inyección de dependencias del modelo Sling
* actualización de dependencias Maven obsoletas
* añadir los tiempos de espera que faltan a las llamadas HTTP salientes
* consultas ilimitadas delimitadas
* Planificadores de Sling
* agentes de escucha de cambio de recursos en Replicación
* Administración de eventos JCR u OSGi

Esta función está en versión beta. Pruébelo y comparta comentarios con el equipo en [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com).

#### Autenticación de Edge para Edge Delivery Services (programa Beta) {#edge-authentication}

La autenticación de Edge le permite restringir el acceso a las páginas de Edge Delivery Services únicamente a aquellas personas que se hayan autenticado con su proveedor de identidad (IdP). Esto se logra mediante la implementación de un archivo YAML de configuración de OpenID Connect (OIDC).

Si le interesa, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso y cualquier pregunta que pueda tener.

#### OpenTelemetry para la Monitorización del Rendimiento de las Aplicaciones (APM) (Programa Alpha) {#apm-alpha}

AEM as a Cloud Service ahora es compatible con la exportación de telemetría basada en OpenTelemetry, lo que le permite monitorizar AEM junto con el resto de los sistemas en las herramientas de APM que sus equipos ya utilizan.

Utilice esta integración para:

- Investigar solicitudes lentas o fallidas
- Seguimiento del estado de JVM y del uso de recursos a lo largo del tiempo
- Creación de paneles y alertas para sus niveles de AEM
- Correlación del comportamiento de AEM con otros servicios durante los incidentes

Para unirte al alfa, envía un correo electrónico a [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com), donde se describe tu caso de uso.

### [!DNL Experience Manager] as a [!DNL Cloud Service] funciones de Assets Beta {#assets-beta-program-features}

#### Extensibilidad de la IU para la vista Assets {#ui-extensibility-assets-view}

La vista de Assets admite la extensibilidad de la interfaz de usuario, una capacidad que da prioridad al desarrollador y que permite a los clientes adaptar la experiencia predeterminada para satisfacer sus requisitos empresariales específicos.Los clientes pueden aprovechar los puntos de extensión estables existentes siguiendo la documentación para desarrolladores de Adobe para crear e implementar extensiones con un esfuerzo mínimo. En el caso de los casos de uso en los que aún no se dispone de un punto de extensión necesario, Adobe trabaja directamente con los clientes para explorar los requisitos y evaluar la viabilidad técnica de ofrecer nuevas API de extensibilidad adaptadas a sus necesidades, y puede ofrecer nuevas API como **Versiones de Beta**.Además, Adobe ha desarrollado una **herramienta de generación de extensiones con tecnología GenAI** que se encuentra disponible actualmente en una fase interna de adopción temprana. Esta herramienta puede acelerar significativamente el tiempo de desarrollo de la extensión. Los clientes que participen en este programa beta recibirán acceso a la herramienta y se les anima a compartir sus comentarios para ayudar a dar forma a su evolución.Para participar o obtener más información, envía un correo electrónico a `GRP-ASSETSVIEWUIEXTENSIBILITY@adobe.com`.

#### Metadatos según la marca (BAM) {#brand-aware-metadata}

Los AEM Assets ahora admiten metadatos según la marca, una función basada en IA que genera automáticamente metadatos personalizados para los recursos cuando se cargan o vuelven a procesarse. Esto reduce la necesidad de introducir datos manualmente por órdenes de magnitud, lo que ayuda a los equipos a encontrar recursos y ofrecer nuevas experiencias mucho más rápido. Los clientes mantienen una biblioteca de indicadores que definen cómo la IA debe rellenar cualquier campo de metadatos, adaptado a su propio vocabulario y taxonomía de marca. Esta biblioteca de mensajes incluye un área de reproducción para obtener una vista previa de los resultados y un optimizador de mensajes que redacta automáticamente las mejoras sugeridas.

Adobe está ampliando activamente las capacidades de BAM mediante la innovación conjunta directa con sus clientes. Cuando aún no se admite un caso de uso específico, Adobe colabora con los clientes participantes para comprender sus necesidades y puede ofrecer funciones ampliadas a medida que progresa la versión beta. Los clientes de este programa obtienen acceso anticipado a las nuevas funciones a medida que se envían y se les anima a compartir comentarios que modelan directamente la hoja de ruta.

Para participar o obtener más información, envía un correo electrónico a `GRP-AEM-ASSETS-BRANDAWAREMETADATA@adobe.com`.

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

