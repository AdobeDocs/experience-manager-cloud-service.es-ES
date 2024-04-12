---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: af9e30ffb585619d1581db94d3961f561e12df2b
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 34%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2024.3.0) es el viernes, 11 de abril de 2024. La próxima versión con funcionalidades (2024.4.0) está planificada para el viernes, 25 de abril de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the March 2024 Release Overview video for a summary of the features added in the 2024.3.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Experience Manager Sites] {#sites-features}

**AEM Creación de para Edge Delivery Services**

AEM Sites ahora se puede utilizar como fuente de contenido para Edge Delivery Services. AEM Los creadores administran sus sitios web en el uso de la nueva versión del editor universal con la creación wysiwyg en contexto. Esto permite a las empresas crear páginas web de alto rendimiento con Edge Delivery Services AEM y, al mismo tiempo, aprovechar las potentes capacidades de administración de contenido de la red de manera más rápida.

![Creación de AEM](/help/edge/assets/universal_editor_edge_delivery_services.png)

Para obtener más información, consulte la [documentación](/help/edge/overview.md) y observe la [AEM AEM Gems de: introducción a la creación y la creación de Edge Delivery Services](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694#M43905)

**Editor universal para implementaciones sin encabezado**

El editor universal también permite que las aplicaciones web disociadas aprovechen la misma creación WYSIWYG intuitiva en contexto que antes era exclusiva de los sitios tradicionales. Los creadores de contenido ahora pueden componer diseños visualmente mediante fragmentos de contenido con la misma facilidad que los componentes dentro de las páginas.

AEM Lo que distingue al editor universal es su adaptabilidad a diversas arquitecturas web, que permiten el procesamiento tanto del lado del servidor como del lado del cliente, no dependen del marco de trabajo y eliminan la necesidad del alojamiento de los usuarios de forma que puedan acceder al sitio web en cualquier momento. Esto se debe hacer de forma independiente, por lo que se elimina la necesidad del alojamiento de los usuarios. La integración de aplicaciones web existentes con el editor universal para la edición de contenido es sencilla, y requiere principalmente que los desarrolladores incorporen atributos de datos específicos en su marcado.

Con esto, el editor universal garantiza una experiencia de edición uniforme, independientemente de la estructura de contenido o de la pila de tecnología subyacente. Para obtener más información, consulte la [Introducción al editor universal](/help/implementing/universal-editor/introduction.md).

**API abiertas de administración de contenido para fragmentos y modelos de contenido**

Los desarrolladores ahora pueden interactuar mediante programación con los fragmentos de contenido y los modelos de fragmentos de contenido y realizar operaciones CrossID en ellos mediante las API abiertas de administración de contenido. Para obtener más información, consulte [Documentación de API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)

**Compatibilidad con administración de varios sitios para fragmentos de experiencias**

La compatibilidad con la administración de varios sitios se ha ampliado para estructuras de carpetas que almacenan fragmentos de experiencias, lo que permite a los usuarios desplegar una estructura de contenido completa con fragmentos de experiencias.

**Comparar versiones de fragmentos de contenido**

El nuevo Editor de fragmentos de contenido ahora permite a los autores de contenido comparar y ver las diferencias entre la versión actual de un fragmento de contenido y una versión anterior.

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

AEM Aproveche la GenAI mediante la nueva función de la aplicación de datos, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de la cuenta de Adobe para que lo considere en el programa.

**Exploración de recursos en la consola de fragmentos de contenido**

Los autores de contenido ahora pueden examinar, ver y realizar acciones en imágenes y otros recursos sin tener que salir de la consola Fragmento de contenido.

![Exploración de recursos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

¿Quiere probar la función y compartir sus comentarios? Envíe un correo electrónico a aemcs-headless-adopter@adobe.com desde su ID de correo electrónico oficial para obtener más información sobre el programa de usuarios que lo adoptaron por primera vez.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#admin-view}

**Integración nativa con Adobe Express**

AEM Assets se integra de forma nativa con Adobe Express, lo que le permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express. Puede colocar contenido administrado en AEM Assets en el lienzo Express y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets.

![Incluir recursos del complemento Recursos](/help/assets/assets/adobe-express-native-integration.png)

**Previsualizar representaciones para todos los tipos de vídeo admitidos**

Experience Manager Assets ahora genera de forma predeterminada representaciones de previsualización de todos los tipos de vídeo admitidos sin requerir una configuración de perfil de procesamiento.

### Nuevas funcionalidades de la vista Recursos {#assets-view}

**Administración de permisos para colecciones**

Los Assets Essentials permiten a los administradores administrar los niveles de acceso para las colecciones privadas disponibles en el repositorio. Como administrador, puede crear grupos de usuarios y asignar permisos a esos grupos para administrar los niveles de acceso. También puede delegar los privilegios de administración de permisos a grupos de usuarios.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuevas funciones de AEM Forms {#forms-new-features}

* **[Edge Delivery Services de Adobe Experience Manager Forms](/help/edge/docs/forms/overview.md)**: los Edge Delivery Services de AEM Forms son un conjunto de servicios componibles que permiten un entorno de desarrollo rápido en el que los autores pueden actualizar, publicar e iniciar nuevos formularios rápidamente. Estos servicios ofrecen experiencias de formularios excepcionales y de gran impacto que fomentan la participación y las conversiones. Estas experiencias de formulario son fáciles de crear y desarrollar.

  ![Funciones de EDS Forms](/help/edge/assets/eds-forms-features.png)

Estos servicios le permiten:

* Trabaje con varios orígenes de contenido en el mismo sitio de formularios y utilice sus herramientas de creación preferidas, como Microsoft Excel, Hojas de cálculo de Google o Editor de Forms adaptable.
* Ofrezca experiencias de inscripción digital que se carguen y procesen de forma rápida y continua para supervisar el rendimiento de los formularios mediante la supervisión de usuarios reales (RUM).
* Utilice HTML sin formato, CSS moderno y JavaScript de vainilla para crear experiencias excepcionales, evitando la pronunciada curva de aprendizaje de un módulo específico.


### Nuevas funciones del prelanzamiento para AEM Forms {#forms-pre-release}

* **Editor de reglas visuales mejorado para Forms adaptable basado en componentes principales**: Esta versión aporta una actualización significativa al editor de reglas visuales para formularios adaptables basados en componentes principales. Esta versión aporta una actualización significativa al editor de reglas visuales para formularios adaptables basados en componentes principales. Esta actualización se centra en la optimización de las interacciones con funciones personalizadas, lo que le permite crear formularios más sólidos y eficientes.

  Ahora puede optimizar las interacciones de funciones personalizadas mediante lo siguiente:

   * Aprovechamiento de nuevas anotaciones para proporcionar definiciones de funciones más claras.
   * Usar mecanismos de almacenamiento en caché para funciones personalizadas, lo que permite un rendimiento de formulario más rápido.
   * Trabajar sin problemas con objetos globales dentro de funciones personalizadas.
   * Definición y utilización de parámetros opcionales dentro de funciones personalizadas.

  Esta actualización también incorpora las siguientes mejoras en la funcionalidad del editor de reglas. Puede hacer lo siguiente:

   * Implemente una potente lógica &quot;when-then-else&quot; para la ejecución condicional.
   * Aproveche las funciones modernas de JavaScript como las funciones izquierda y flecha (compatibilidad con ES10).
   * Valide o restablezca no solo campos, sino también paneles y formularios completos, lo que expande el control sobre las interacciones del usuario.

  Estos avances proporcionan una experiencia más intuitiva y potente para crear reglas y funciones personalizadas dentro del editor de reglas visuales.

* **Crear varias versiones de un formulario adaptable**: Ahora puede administrar fácilmente las variaciones de los formularios existentes. Esto simplifica el control de versiones y facilita la comparación para la optimización de formularios, todo dentro de un único flujo de trabajo optimizado.

* **Comparar formulario adaptable**: ahora puede comparar fácilmente dos formularios para identificar diferencias entre dos formularios. Facilita una colaboración fluida ya que permite a los miembros del equipo comparar revisiones y discutir cambios de forma eficaz.

* **Mejoras de accesibilidad para el componente Firma manuscrita**: Esta actualización aporta mejoras significativas de accesibilidad al componente Firma manuscrita:

  **Navegación por teclado mejorada:**
   * Al presionar la tecla Tab, los usuarios pueden desplazarse por todos los elementos interactivos del cuadro de diálogo de firma.
   * La firma con un pincel o teclado y la pulsación Intro cierran el cuadro de diálogo.
   * El enfoque permanece en el control de firma después de firmar y hacer clic en &quot;Aceptar&quot;.

  **Borrar funcionalidad de firma:**

   * Se puede acceder a un icono cruzado transparente para borrar la firma mediante el tabulador.
   * También se puede acceder al cuadro de diálogo &quot;Borrar confirmación de firma&quot; a través de la navegación por pestañas.

  **Etiquetas y controles mejorados:**
   * La etiqueta del botón de firma de teclado ahora es más clara, utiliza &quot;aria-label&quot; para anunciar funcionalidades (como &quot;aria-label=&#39;Sign using Keyboard&#39;&quot;).
   * El contraste mejorado garantiza que todos los controles dentro de la firma manuscrita se puedan distinguir fácilmente.
   * El botón OK/check mark ahora indica visualmente cuándo está inactivo.

  **Comentarios sobre firmas para Reader de pantalla:**
   * Cuando se escribe una firma, los usuarios del lector de pantalla pueden oír el texto utilizado para crearla.

Esta actualización garantiza una experiencia más inclusiva para los usuarios con discapacidades al mejorar la navegación, la claridad y los comentarios del componente Firma manuscrita.

### Programa para primeros usuarios {#forms-early-adopter}

* **[Envío de un formulario adaptable a un escenario de Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service ofrece una opción predeterminada para conectar sin esfuerzo un formulario adaptable con Adobe Workfront. Esto simplifica el proceso de envío de un formulario adaptable a un escenario de Adobe Workfront, permitiéndole activar un escenario de Workfront Fusion al enviar un formulario adaptable.

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Con Adobe Workfront Fusion Connector, puede diseñar flujos de trabajo que se activan automáticamente al enviar un formulario adaptable. Por ejemplo, imagine un escenario en el que se inicia un flujo de trabajo para asignar a un individuo específico la tarea de revisar los datos enviados, lo que permite la aprobación o el rechazo de una solicitud en función de la información capturada a través del formulario adaptable. Esta integración optimizada mejora la eficacia y aporta un nuevo nivel de automatización a los procesos de flujo de trabajo.|

* **Servicio de extensión de Reader**: las API de comunicación de AEM Forms han incorporado el servicio de extensión de Reader para permitirle añadir funcionalidades como rellenar formularios y hacer comentarios a los PDF habituales, lo que las hace interactivas para los usuarios con el Adobe Reader gratuito.

* [Compatibilidad con idiomas de derecha a izquierda](/help/forms/supporting-new-language-localization-core-components.md): los formularios adaptables creados en los componentes principales ahora se pueden presentar en un idioma de derecha a izquierda (RTL) como árabe, persa y urdu.  Más de 2000 millones de personas en todo el mundo hablan los idiomas RTL.  El uso de un formulario en idioma RTL le permite ampliar el alcance de sus formularios adaptables para adaptarse a estas diversas audiencias y seleccionar en los mercados RTL. En ciertas regiones, también es un mandato legal proporcionar formularios en el idioma local.  Al adaptarse a los idiomas locales, no solo abre las puertas a una audiencia más amplia, sino que también garantiza el cumplimiento de las leyes y regulaciones relevantes.

* **[Proteja sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa de protección fortificada no solo protege los datos valiosos de miradas no autorizadas, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos PDF de Adobe que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

  Puede escribir a `aem-forms-ea@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta posibilidad.

* **[Puede aprovechar el servicio de datos RUM (Monitorización del usuario real)](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** para habilitar la recopilación del lado del cliente para AEM as a Cloud Service.
El servicio de datos de Monitorización del usuario real (RUM) ofrece un reflejo más preciso de las interacciones del usuario, lo que garantiza una medida fiable de la participación en el sitio web. Es una gran oportunidad para obtener perspectivas avanzadas sobre el rendimiento de su página. Es beneficioso para los clientes que utilizan CDN administrada por Adobe o CDN no administrada por Adobe. Además, para los clientes que utilizan una CDN no administrada por Adobe, ahora se pueden habilitar los informes de tráfico automatizados para ellos, lo que elimina la necesidad de compartir cualquier informe de tráfico con Adobe.

  Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `aemcs-rum-adopter@adobe.com`, junto con su nombre de dominio de cada uno de los entornos en los que desea habilitar RUM desde su dirección de correo electrónico asociada a su Adobe ID. El equipo de productos de Adobe habilitará entonces el servicio de datos RUM (Monitorización del usuario real) para usted.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programas de usuarios pioneros {#foundation-early-adopter}

#### Alertas de reglas de filtro de tráfico (programa de usuario anticipado) {#traffic-filter-rules-alerts-early-adopter}

El recién lanzado [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md), que incluyen las reglas de cortafuegos de aplicaciones web (WAF) con licencia opcional, le permite configurar qué tráfico se debe permitir o denegar.

Ahora puede enviar un correo electrónico **<aemcs-cdn-config-adopter@adobe.com>** para unirse al programa de usuarios que lo adoptaron por primera vez y recibir alertas cada vez que se activen las reglas de filtro de tráfico. Las notificaciones por correo electrónico del Centro de acciones le mantendrán informado cuando se produzcan determinadas condiciones de tráfico para que pueda tomar las medidas adecuadas.

#### Configuración de CDN (programa de adopción anticipada) {#cdn-config-early-adopter}

Además de los lanzamientos recientes [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md), que incluyen las reglas del cortafuegos de aplicaciones web (WAF) con licencia opcional, existe la oportunidad de utilizar la canalización de configuración para declarar e implementar otros tipos de configuración de CDN. [Más información](/help/implementing/dispatcher/cdn-configuring-traffic.md) y únase al programa de usuarios pioneros por correo electrónico **<aemcs-cdn-config-adopter@adobe.com>** para obtener acceso a:

* Redirecciones del lado del cliente 301/302
* AEM solicitudes de proxy en el perímetro de con orígenes arbitrarios (como aplicaciones no)
* transformaciones de URL
* configuración o modificación de encabezados de solicitud o respuesta
* páginas de error personalizadas cuando la CDN no puede llegar a AEM

#### Ingesta de mapas de reescritura en tiempo de ejecución de Apache/Dispatcher (programa de adopción anticipada) {#apache-rewritemaps-early-adopter}

AEM De forma similar a la versión 6.5, Apache/Dispatcher introducirá mapas de reescritura colocados en una ubicación específica del repositorio de publicación y los cargará, sin requerir la ejecución de una canalización de niveles web. Esto abre oportunidades para que un usuario empresarial declare redirecciones mediante una interfaz de usuario, como la que ofrece el Administrador de mapas de redirección de ACS Commons. Póngase en contacto con **<aemcs-cdn-config-adopter@adobe.com>** para obtener más información.

#### Edge Side Includes (ESI) para cargar contenido dinámico (programa para usuarios pioneros) {#esi-early-adopter}

La CDN administrada por Adobe ahora es compatible con Edge Side Includes (ESI), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL más altos, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL menores). Póngase en contacto con **<aemcs-cdn-config-adopter@adobe.com>** para obtener más información.

#### Compatibilidad con RDE para código front-end mediante temas de sitio y plantillas de sitio (programa para usuarios pioneros) {#rde-frontend-early-adopter}

Los [Entornos de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) admiten ahora código front-end basado en [temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md) y [plantillas del sitio](/help/sites-cloud/administering/site-creation/site-templates.md), para los primeros usuarios. Con los RDE, esto se hace usando una directiva de línea de comandos, en lugar de una [canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Póngase en contacto con **<aemcs-rde-support@adobe.com>** para probarlo y proporcionar comentarios.

#### Registro mejorado para RDE (programa de usuarios pioneros) {#rde-logging-early-adopter}

Al depurar código en una [Entorno de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md)Sin embargo, los desarrolladores ahora pueden configurar y transmitir registros de forma más eficaz, utilizando la línea de comandos y sin modificar las propiedades OSGI en el control de versiones. Las funciones incluyen:

* declarar niveles de registro en un nivel por paquete o clase
* personalizar el formato de salida del registro
* transmitir varios registros en paralelo

Póngase en contacto con **<aemcs-rde-support@adobe.com>** para probarlo y proporcionar comentarios.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

