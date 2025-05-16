---
title: Notas de la versión 2024.4.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2024.4.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 153a3172-676f-4434-94d4-12fab8e17734
feature: Release Information
role: Admin
source-git-commit: 603602dc70f9d7cdf78b91b39e3b7ff5090a6bc0
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 97%

---

# Notas de la versión 2024.4.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2024.4.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2024.4.0) es el 25 de abril de 2024. La siguiente versión con funcionalidades (2024.5.0) está planificada para el 30 de mayo de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de abril de 2024 para ver un resumen de las funciones añadidas en la versión 2024.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3446308?quality=12&captions=spa)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.

**Exploración de recursos en la consola de fragmentos de contenido**

Los autores de contenido ahora pueden examinar, ver y realizar acciones en imágenes y otros recursos sin tener que salir de la consola de fragmento de contenido.

![Examen de recursos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

¿Quiere probar la función y compartir sus comentarios? Puede enviar un correo electrónico a aemcs-waf-adopter@adobe.com desde su ID de correo electrónico oficial para más información acerca del programa de primeros usuarios.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#assets-view-new-features}


**Búsqueda contextual**

Ahora también puede [buscar recursos disponibles en el repositorio definiendo mensajes de texto](/help/assets/search-assets-view.md#contextual-search). Experience Manager Assets transforma automáticamente esos mensajes de texto en filtros de búsqueda y muestra los resultados de la búsqueda. Puede ver y modificar los filtros automáticos mediante el panel Filtros para reducir aún más los resultados de la búsqueda.

![Búsqueda contextual](/help/assets/assets/contextual-search-text-prompt1.png)

**Acciones rápidas de vídeo exprés.**

Experience Manager Assets ahora incluye [herramientas de edición de video sencillas e intuitivas con tecnología de Adobe Express](/help/assets/edit-videos-assets-view.md) para aumentar la reutilización del contenido y acelerar su velocidad. Las opciones de edición incluyen recortar, cambiar el tamaño de un video y convertir también un archivo MP4 a GIF.

![recortar vídeo con Adobe Express](/help/assets/assets/adobe-express-crop-video.png)

**Representaciones dinámicas**

Ahora puede [ver y descargar representaciones dinámicas (incluidos los recortes inteligentes)](/help/assets/renditions.md) en Experience Manager Assets. Las representaciones dinámicas son versiones personalizadas de recursos de imagen creados en tiempo real para satisfacer necesidades específicas, como cambiar el tamaño de las imágenes en función de la resolución del dispositivo o recortarlas para adaptarlas a diferentes relaciones de aspecto. Estas representaciones permiten a las organizaciones ofrecer experiencias personalizadas y optimizadas a las diversas necesidades del público.

![Representaciones dinámicas](/help/assets/assets/preset_smart_crop.png)

**Cambio de nombre in situ de recursos y carpetas**

Experience Manager Assets ahora ofrece una experiencia del usuario simplificada al [brindar la posibilidad de cambiar el nombre de un recurso o una carpeta con un solo clic](/help/assets/manage-organize-assets-view.md).

**Asignar o quitar formulario de metadatos a varias carpetas**

Ahora, puede [asignar o quitar formularios de metadatos a varias carpetas](/help/assets/metadata-assets-view.md#assign-metadata-form-to-a-folder).

### Nuevas funciones de la vista Administrador {#admin-view-new-features}

**Configuración de vínculos compartidos**

Una nueva experiencia de usuario mejorada para [crear vínculos compartidos](/help/assets/share-assets.md) junto con un nuevo conjunto de configuraciones que permiten a los administradores personalizar el comportamiento predeterminado de esta función para los usuarios.

![Configuración de vínculos compartidos](/help/assets/assets/config-email-service.png)



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuevas funciones en AEM Forms {#forms-new-features}

* **Editor de reglas visuales mejorado para formularios adaptables basados en componentes principales**: esta versión aporta una actualización significativa al editor de reglas visuales para formularios adaptables basados en componentes principales. Esta versión aporta una actualización significativa al editor de reglas visuales para formularios adaptables basados en componentes principales. Esta actualización se centra en la optimización de las interacciones con funciones personalizadas, lo que le permite crear formularios más sólidos y eficientes.

  Ahora puede optimizar las interacciones de funciones personalizadas efectuando lo siguiente:

   * [Aprovechar nuevas anotaciones para proporcionar definiciones de funciones más claras](/help/forms/create-and-use-custom-functions.md#supported-javascript-annotations-for-custom-function).
   * [Usar mecanismos de almacenamiento en caché para funciones personalizadas, lo que se traduce en un rendimiento de formulario más rápido.](/help/forms/create-and-use-custom-functions.md#caching-support-for-custom-function)
   * [Trabajar sin problemas con objetos globales dentro de funciones personalizadas](/help/forms/create-and-use-custom-functions.md#field-and-global-scope-objects-in-custom-functions).
   * [Definir y utilizar parámetros opcionales dentro de funciones personalizadas](/help/forms/create-and-use-custom-functions.md#parameter).

  Esta actualización también incorpora las siguientes mejoras en la funcionalidad del editor de reglas. Puede hacer lo siguiente:

   * Implemente una potente lógica [&quot;when-then-else&quot;](/help/forms/rule-editor-core-components.md#when) para la ejecución condicional.
   * Aproveche las funciones modernas de JavaScript como las funciones let y arrow (compatibilidad con ES10).
   * Valide o restablezca no solo campos, sino también paneles y formularios completos, ampliando el control sobre las interacciones de los usuarios.

  Estos avances proporcionan una experiencia más intuitiva y potente para crear reglas y funciones personalizadas dentro del editor de reglas visuales.

* **[Creación de varias versiones de un formulario adaptable](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)**: ahora puede administrar fácilmente las variaciones de los formularios existentes. Esto simplifica el control de versiones y facilita la comparación para la optimización de formularios, todo dentro de un único flujo de trabajo optimizado.

* **[Comparación de formulario adaptable](/help/forms/compare-forms.md)**: ahora puede comparar fácilmente dos formularios para identificar sus diferencias. Facilita una colaboración fluida ya que permite a los miembros del equipo comparar revisiones y discutir cambios de forma eficaz.

* **Mejoras de accesibilidad para el componente Firma manuscrita**: esta actualización aporta mejoras significativas de accesibilidad al componente Firma manuscrita:

  **Navegación por teclado mejorada:**
   * Al presionar la tecla Tab, los usuarios pueden desplazarse por todos los elementos interactivos del cuadro de diálogo de firma.
   * Al firmar con un pincel o teclado y pulsar Intro se cierra el cuadro de diálogo.
   * El foco permanece en el control de firma después de firmar y hacer clic en &quot;Aceptar&quot;.

  **Borrar funcionalidad de firma:**

   * Se puede acceder a un icono cruzado transparente para borrar la firma mediante la tecla Tab.
   * También se puede acceder al cuadro de diálogo &quot;Borrar confirmación de firma&quot; a través de la navegación por pestañas.

  **Etiquetas y controles mejorados:**
   * La etiqueta del botón de firma de teclado es ahora más clara, utilizando &quot;aria-label&quot; para anunciar funcionalidad (como &quot;aria-label=&#39;Sign using Keyboard&#39;&quot;).
   * El contraste mejorado garantiza que todos los controles dentro de la firma manuscrita se puedan distinguir fácilmente.
   * El botón de Aceptar/marca de comprobación indica ahora visualmente cuándo está inactivo.

  **Comentarios sobre firmas para lectores de pantalla:**
   * Cuando se escribe una firma, los usuarios lectores de pantalla pueden oír el texto utilizado para crearla.

Esta actualización garantiza una experiencia más inclusiva para los usuarios con discapacidades al mejorar la navegación, la claridad y los comentarios del componente Firma manuscrita.

### Programa para primeros usuarios {#forms-early-adopter}

* **[Envío de un formulario adaptable a un escenario de Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service ofrece una opción lista para usar para conectar fácilmente un formulario adaptable con Adobe Workfront.  Esto simplifica el proceso de envío de un formulario adaptable a un escenario de Adobe Workfront, permitiéndole activar un escenario de Workfront Fusion al enviar un formulario adaptable.

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Con Adobe Workfront Fusion Connector, puede diseñar flujos de trabajo que se activan automáticamente al enviar un formulario adaptable. Por ejemplo, imagine un escenario en el que se inicia un flujo de trabajo para asignar a un individuo específico la tarea de revisar los datos enviados, lo que permite la aprobación o el rechazo de una solicitud en función de la información capturada a través del formulario adaptable. Esta integración optimizada mejora la eficacia y aporta un nuevo nivel de automatización a los procesos de flujo de trabajo.|

* **[Servicio de extensión de Reader](/help/forms/aem-forms-cloud-service-communications-introduction.md#reader-extension-service)**: las API de comunicación de AEM Forms han incorporado el servicio de extensión de Reader para permitirle añadir funcionalidades como rellenar formularios y hacer comentarios a los PDF habituales, lo que los hace interactivos para los usuarios que tienen Adobe Reader gratuito.

* [Compatibilidad con idiomas de derecha a izquierda](/help/forms/supporting-new-language-localization-core-components.md): los formularios adaptables creados en los componentes principales ahora se pueden presentar en un idioma de derecha a izquierda (RTL) como árabe, persa y urdu.  Más de 2000 millones de personas en todo el mundo hablan los idiomas RTL.  El uso de un formulario en idioma RTL le permite ampliar el alcance de sus formularios adaptables para adaptarse a estas diversas audiencias y seleccionar en los mercados RTL. En ciertas regiones, también es un mandato legal proporcionar formularios en el idioma local.  Al adaptarse a los idiomas locales, no solo abre las puertas a una audiencia más amplia, sino que también garantiza el cumplimiento de las leyes y regulaciones relevantes.

* **[Proteja sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa de protección fortificada no solo protege los datos valiosos de miradas no autorizadas, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos PDF de Adobe que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

  Puede escribir a `aem-forms-ea@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta posibilidad.

* **[Puede aprovechar el servicio de datos de supervisión de uso real (RUM)](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** para habilitar la recopilación del lado del cliente para AEM as a Cloud Service.
El Servicio de datos de monitorización de usuarios reales (RUM) refleja de forma más precisa las interacciones de los usuarios, lo que garantiza una medida fiable de la participación en el sitio web. Es una gran oportunidad para obtener perspectivas avanzadas sobre el rendimiento de su página. Es beneficioso para los clientes que utilizan CDN administrada por Adobe o CDN no administrada por Adobe. Además, para los clientes que utilizan una CDN no administrada por Adobe, ahora se pueden habilitar los informes de tráfico automatizados para ellos, lo que elimina la necesidad de compartir cualquier informe de tráfico con Adobe.

  Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `aemcs-rum-adopter@adobe.com`, junto con su nombre de dominio de cada uno de los entornos en los que desea habilitar RUM desde su dirección de correo electrónico asociada a su Adobe ID. El equipo de productos de Adobe habilitará entonces el servicio de datos de supervisión de uso real (RUM).

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Asignación de dominios {#cdn-config}

Configure el tráfico en la CDN de Adobe de las siguientes maneras:

* [Transformaciones de solicitudes](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations): modifique aspectos de las solicitudes entrantes, incluidas las rutas, los parámetros de consulta y los encabezados HTTP antes de que se dirijan a AEM. 
* [Transformaciones de respuesta](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations): cambie los encabezados HTTP de las respuestas salientes antes de enviarlas al explorador.
* [Selectores de origen](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations#origin-selectors): enrute el tráfico a través de la CDN a sitios y aplicaciones fuera de AEM. 

Una vez declaradas estas reglas en el control de código fuente (Git), puede implementarlas en la CDN mediante la canalización de configuración de Cloud Manager. Consulte también la función de redirecciones del lado del cliente en la siguiente sección de primeros usuarios.

### Páginas de error de la CDN personalizadas {#cdn-error-pages}

En el improbable caso de que la CDN no pueda enrutar el tráfico al origen de AEM, se puede declarar una página de error personalizada que sustituya la versión genérica. [Obtenga más información](/help/implementing/dispatcher/cdn-error-pages.md) sobre cómo ofrecer páginas de error de marca.

### Programa para primeros usuarios {#foundation-early-adopter}

#### Redirecciones del lado del servidor (programa de usuarios pioneros) {#server-side-redirects-early-adopter}

Configure las redirecciones del lado del servidor 301/302 en el control de código fuente e implemente en la CDN. [Obtenga más información](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) y únase al programa de primeros usuarios enviando un correo electrónico a **<aemcs-cdn-config-adopter@adobe.com>**.

#### Alertas de reglas de filtro de tráfico (programa de primeros usuarios) {#traffic-filter-rules-alerts-early-adopter}

Las [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md) recientemente publicadas, que incluyen las reglas del firewall de aplicaciones web ((Web Application Firewall, WAF) con licencia opcional, le permiten configurar qué tráfico se debe permitir o denegar.

Ahora puede enviar un correo electrónico **<aemcs-cdn-config-adopter@adobe.com>** para unirse al programa de primeros usuarios y recibir alertas cada vez que se activen las reglas de filtro de tráfico. Las notificaciones por correo electrónico del Centro de acciones le mantendrán informado cuando se produzcan determinadas condiciones de tráfico para que pueda tomar las medidas adecuadas.

#### Ingesta de mapas de reescritura en tiempo de ejecución de Apache/Dispatcher (programa de primeros usuarios) {#apache-rewritemaps-early-adopter}

De forma similar a la versión AEM 6.5, Apache/Dispatcher introducirá mapas de reescritura colocados en una ubicación específica del repositorio de publicación y los cargará, sin requerir la ejecución de una canalización de niveles web. Esto abre oportunidades para que un usuario empresarial declare redirecciones mediante una interfaz de usuario, como la que ofrece el Administrador de mapas de redirección de ACS Commons. Póngase en contacto con **<aemcs-cdn-config-adopter@adobe.com>** para obtener más información.

#### Edge Side Includes (ESI) para cargar contenido dinámico (programa para primeros usuarios) {#esi-early-adopter}

La red de distribución de contenido (CDN) administrada por Adobe es ahora compatible con Edge Side Includes (ESI), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL más altos, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL menores). Póngase en contacto con **<aemcs-cdn-config-adopter@adobe.com>** para obtener más información.

#### Compatibilidad con RDE para código front-end mediante temas del sitio y plantillas del sitio: (Programa para primeros usuarios) {#rde-frontend-early-adopter}

Los [Entornos de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) admiten ahora código front-end basado en [temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md) y [plantillas del sitio](/help/sites-cloud/administering/site-creation/site-templates.md), para los primeros usuarios. Con los RDE, esto se hace usando una directiva de línea de comandos, en lugar de una [canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Póngase en contacto con **<aemcs-rde-support@adobe.com>** aemcs-rde-support@adobe.com para probarlo y proporcionar comentarios.

#### Registro mejorado para RDE (programa de primeros usuarios) {#rde-logging-early-adopter}

Al depurar código en un [Entorno de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md), los desarrolladores pueden ahora configurar y transmitir registros de forma más eficaz, utilizando la línea de comandos y sin modificar las propiedades OSGI en el control de versiones. Las funciones incluyen:

* declarar niveles de registro en un nivel por paquete o clase
* personalizar el formato de salida del registro
* transmitir varios registros en paralelo

Póngase en contacto con **<aemcs-rde-support@adobe.com>** para probarlo y proporcionar comentarios.

## Guías de [!DNL Experience Manager] {#guides}

### Posibilidad de traducir contenido a varios idiomas utilizando grupos de idiomas preconfigurados

Ahora, Experience Manager Guides permiten crear grupos de idiomas y traducir fácilmente su contenido a varios idiomas. Esta función le ayuda a organizar y administrar las traducciones según las necesidades de su organización.

Por ejemplo, si tiene que traducir el contenido para algunos países de Europa, puede crear un grupo de idiomas para idiomas europeos como el inglés (EN), francés (FR), alemán (DE), español (ES) e italiano (IT).

![panel de traducción](/help/release-notes/assets/guides/translation-languages-2404.png)

*Seleccione los grupos de idiomas o idiomas a los que desee traducir los documentos.*

>[!NOTE]
>
>Si falta la carpeta de destino de un idioma o el idioma de destino es el mismo que el de origen, aparecerá atenuado y mostrará un signo de advertencia.

Como administrador, puede crear grupos de idiomas y configurarlos en varios perfiles de carpeta. Como autor, puede ver los grupos de idiomas configurados en el perfil de la carpeta.


En general, la creación de grupos de idiomas mejora la eficacia y la productividad de los proyectos de traducción y, en última instancia, mejora el proceso de localización en varios idiomas.


Obtenga información sobre cómo [traducir documentos desde el editor web](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/translate-documents-web-editor)

### Experiencia renovada para buscar y filtrar archivos en la vista de repositorio

Ahora tiene una mejor experiencia al filtrar archivos. La funcionalidad renovada para filtrar archivos ofrece una mejor forma de buscar y navegar por los archivos sin esfuerzo.

![búsqueda de archivos en la vista del repositorio](/help/release-notes/assets/guides/repository-filter-search-2404.png)

*Busque los archivos que contienen el texto`general purpose.`*

Disfrute de ventajas como un acceso más rápido a los archivos relevantes y una interfaz de usuario más intuitiva, lo que hace que su experiencia de búsqueda sea más fluida y eficiente.

![filtro de búsqueda rápida ](/help/release-notes/assets/guides/repository-filter-search-quick.png)

*Utilice los filtros rápidos para buscar archivos DITA y no DITA.*

Obtenga más información sobre la función **Filtrar búsqueda** en la sección [Panel izquierdo](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/web-editor-features#id2051EA0M0HS).

### Mejoras en los conectores de fuentes de datos

Se han realizado las siguientes mejoras en los conectores de fuente de datos para la versión 2024.4.0:

#### Conexión a las fuentes de datos de Salsify, Akeneo y Microsoft Azure DevOps Boards (ADO)

Además de los conectores predeterminados existentes, las guías de Experience Manager también proporcionan conectores para fuentes de datos de Salsify, Akeneo y Microsoft Azure DevOps Boards (ADO). Como administrador, puede descargar e instalar estos conectores. A continuación, configure los conectores instalados.

#### Copiar y pegar la consulta de muestra para crear un fragmento de código de contenido o un tema

Puede copiar y pegar fácilmente una consulta de datos de muestra en el generador para crear un fragmento de código de contenido o un tema. Con esta función, no es necesario recordar la sintaxis ni crear una consulta manualmente. En lugar de escribir manualmente la consulta, puede copiar y pegar una consulta de muestra, editarla y utilizarla para recuperar los datos según sus necesidades.

![cuadro de diálogo para insertar fragmento de código de contenido](/help/release-notes/assets/guides/insert-content-snippet.png)

*Copie y edite una consulta de muestra para crear el fragmento de código de contenido.*

#### Conexión a archivos de datos JSON mediante un conector de archivo


Ahora, como administrador, puede configurar un conector de archivo JSON para utilizar archivos de datos JSON como fuente de datos. Utilice el conector para importar los archivos JSON del equipo o de Adobe Experience Manager Assets. A continuación, como autor, puede crear fragmentos de código de contenido o temas mediante los generadores.

Esta función le ayuda a utilizar los datos almacenados en sus archivos JSON y a reutilizarlos en varios fragmentos de código. El contenido también se actualiza dinámicamente cada vez que se actualizan los archivos JSON.

#### Configuración de varias URL de recursos para que un conector cree fragmentos de código de contenido o temas

Como administrador, puede configurar varias URL de recursos para algunos conectores, como Cliente REST genérico, Salsify, Akeneo y Microsoft Azure DevOps Boards (ADO).
A continuación, como autor, conéctese con las fuentes de datos para crear fragmentos de código de contenido o temas mediante los generadores. Esta función es práctica, ya que no tiene que crear una fuente de datos para cada URL. Ayuda a recuperar rápidamente datos de cualquiera de los recursos de una fuente de datos concreta en un solo fragmento de código de contenido o tema. Vea más detalles sobre los conectores de fuentes de datos y cómo [configurar un conector de origen de datos desde la interfaz de usuario](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/install-guide/cs-ig/web-editor-configs-cs/conf-data-source-connector-tools). Obtenga información sobre cómo [utilizar datos de la fuente de datos](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/web-editor-content-snippet).

Para obtener más información acerca de las nuevas características y mejoras, vea [Información sobre las versiones de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
