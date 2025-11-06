---
title: Notas de la versión 2023.8.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.8.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a0ffa6cf-64ae-468c-93f4-ac6805ef907e
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 100%

---

# Notas de la versión 2023.8.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funcionalidades de la versión 2023.8.0 de [!DNL Experience Manager] as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.8.0) fue el 31 de agosto de 2023. La próxima versión con funcionalidades (2023.9.0) se planificó para el 28 de septiembre de 2023.

## Vídeo de la versión {#release-video}

Echa un vistazo al vídeo Información general sobre la versión de agosto de 2023 para ver un resumen de las funciones añadidas en la versión 2023.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Experience Manager Sites] {#sites-features}

* La [Consola de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=es) ahora permite a los usuarios ver etiquetas y buscar por etiquetas aplicadas como metadatos a fragmentos de contenido. Los usuarios ya no tendrán que cambiar a la IU de Assets para esta capacidad, lo que reduce el cambio de contexto y mejora la eficacia.

  ![Etiquetado en la consola de fragmentos de contenido](/help/assets/content-fragments-console-tags.png)
* El nuevo Editor de fragmentos de contenido ya está disponible en AEM as a Cloud Service. Permite a los autores de contenido ser más productivos al optimizar sus tareas de creación y al reducir la necesidad de cambiar entre distintas aplicaciones mientras editan contenido.
  ![Nuevo editor de fragmentos de contenido](/help/release-notes/assets/newCFEditor.png)

El nuevo editor de fragmentos de contenido ofrece las siguientes ventajas que no están disponibles en el editor original:

* Guardado automático para mejorar la eficacia de la creación y evitar la pérdida accidental de ediciones.
* Vista jerárquica de un fragmento de contenido y sus referencias mediante el árbol de estructura para una navegación rápida dentro de un fragmento profundamente estructurado.
  ![Árbol de estructura en el editor de fragmentos de contenido](/help/release-notes/assets/newCFEditor_StructureTree.png)

* Carga en línea de recursos como referencias de contenido sin tener que cargarlos primero en el DAM de recursos
* Vista previa ad hoc de la experiencia representada por el fragmento de contenido para ayudar a los autores a visualizar la apariencia del contenido en la aplicación de front-end
* Publicación y cancelación de la publicación del fragmento de contenido desde el editor con un solo clic
* Visualización y navegación a copias de idioma al editar un fragmento de contenido
  ![Copias de idioma en el editor de fragmentos de contenido](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* Visualización de versiones para realizar un seguimiento de la cronología de un fragmento de contenido

  ![Versiones en el editor de fragmentos de contenido](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* Ver referencias principales para ayudar a los autores a comprender el impacto de sus ediciones

  ![Referencias principales en el editor de fragmentos de contenido](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **Importación masiva de recursos desde fuentes de datos**: los administradores ahora tienen la [capacidad de importar un gran número de recursos](/help/assets/bulk-import-assets-view.md) de una fuente de datos a AEM Assets. Los administradores ya no tienen que cargar archivos o carpetas individuales a AEM Assets. Las fuentes de datos admitidas para la importación masiva son Azure, AWS, Google Cloud y Dropbox.

  ![Importación masiva de recursos desde una fuente de datos](/help/release-notes/assets/bulk-import.png)

* **Herramientas de edición de imágenes con tecnología Adobe Express**: herramientas de edición de [imágenes sencillas e intuitivas con tecnología Adobe Express](/help/assets/edit-images-assets-view.md) disponibles directamente en AEM Assets para aumentar la reutilización de contenidos y acelerar la velocidad del contenido.

  ![Edición de imágenes con Adobe Express](/help/release-notes/assets/edit-adobe-express.png)

* **Flexibilidad a la hora de anclar elementos para el Acceso rápido de Mi espacio de trabajo**: capacidad para seleccionar y fijar elementos para usted, para toda su organización o para una lista de grupos, de modo que aparezcan en la sección [Acceso rápido de Mi espacio de trabajo](/help/assets/my-workspace-assets-view.md) en función de su selección.

  ![Fijar elementos para grupos](/help/release-notes/assets/pin-items-for-groups.png)

### Nuevas funciones de la vista Recursos {#admin-view-features}

**Mejoras de búsqueda**

* Los administradores ahora pueden [configurar el tamaño del lote de recursos](/help/assets/search-assets.md#configure-asset-batch-size) que se muestran al realizar una búsqueda. Los resultados de la búsqueda de recursos se muestran en múltiplos del número de tamaños de lotes configurados al desplazarse hacia abajo para cargar los resultados. Puede seleccionar entre los tamaños de lote disponibles de 200, 500 y 1000 recursos. Configurar un número de tamaño de lote menor resulta en tiempos de respuesta de búsqueda más rápidos.

  ![Configuración de tamaño del lote de recursos](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets ahora incluye la nueva versión 9 del índice de `damAssetLucene`. `damAssetLucene-9` cambia el comportamiento del recuento de facetas de Oak Query [ para dejar de evaluar el control de acceso en los recuentos de facetas ](/help/assets/search-assets.md) devueltos por el índice de búsqueda subyacente, lo que resulta en tiempos de respuesta de búsqueda más rápidos.

### Funciones de versión preliminar disponibles en [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [compatibilidad con subtítulos y pistas de audio múltiples para vídeos en Dynamic Media](/help/assets/dynamic-media/video.md#about-msma). Ahora se pueden añadir fácilmente varios subtítulos y pistas de audio a un vídeo principal. Esta posibilidad significa que los vídeos son accesibles para todo el público global. Puede personalizar un solo vídeo principal publicado para un público global en varios idiomas y seguir las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

  ![Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.](/help/release-notes/assets/msma-aem-cs.png)*Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.*

* **Assets**: capacidad para seleccionar archivos ZIP administrados en Experience Manager y [ extracción de los archivos directamente en Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) sin descargarlos.

  ![Fijar elementos para grupos](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Soporte Google reCAPTCHA Enterprise**](/help/forms/captcha-adaptive-forms.md): utilice Google reCAPTCHA Enterprise en un formulario adaptable para obtener una protección mejorada contra la actividad fraudulenta, el correo no deseado y una experiencia de usuario más segura. Con un análisis de riesgos avanzado y una integración optimizada, los usuarios compradores pueden enviar fácilmente formularios mientras los bots están bloqueados de manera efectiva.


### Funciones de versión preliminar disponibles en [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* **Adobe Analytics con automatización de la configuración de Experience Cloud para Forms**: ahora se puede habilitar Adobe Analytics con la automatización de la configuración de Experience Cloud con un par de botones. Esto permite conectar AEM Forms as a Cloud Service con las etiquetas de Experience Platform y Adobe Analytics para capturar y rastrear las métricas de rendimiento de los formularios publicados.

* **Plantilla de informe de Adobe Analytics para formularios adaptables**: Forms as a Cloud Service ahora proporciona un informe listo para usar de Adobe Analytics. Le ayuda a comprender fácilmente el rendimiento de sus formularios. Las métricas de nivel de formulario proporcionan una perspectiva del rendimiento del formulario en varios indicadores clave de rendimiento (KPI) como representaciones, visitantes, envíos o tiempo promedio de cumplimentación. Al rastrear el comportamiento del usuario y los comentarios, usted puede identificar las áreas del formulario que están causando frustración o confusión, lo que guía las mejoras en el diseño y la funcionalidad del formulario.

  ![Informe de Adobe Analytics de participación del usuario del formulario adaptable](/help/forms/assets/forms-analytics-report.png)

* **[Fragmentos de formulario adaptables basados en componentes principales](/help/forms/adaptive-form-fragments-core-components.md)**: Despídase de la duplicación, optimice su inventario digital y mejore la colaboración a medida que mejora su experiencia de creación de formularios con fragmentos de formularios. Estos componentes reutilizables se integran a la perfección en múltiples formularios, agilizando la creación de formularios coherentes y de aspecto profesional. Los fragmentos de formulario garantizan la reutilización, la estandarización y la coherencia de la marca mediante la funcionalidad “cambiar una vez y reflejar en todas partes”. Experimente una mayor capacidad de mantenimiento y eficacia, ya que las actualizaciones realizadas en un solo lugar se propagan automáticamente a todos los formularios que utilizan estos fragmentos.

* **[Paso del flujo de trabajo de Adobe Sign mejorado](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: este se ha mejorado e incluye lo siguiente:
   * **Autenticación basada en documentos de identidad oficiales para Adobe Sign**: la autenticación basada en documentos de identidad oficiales de Adobe Acrobat Sign ofrece un nivel adicional de verificación al permitir a los usuarios autenticarse con documentos de identidad emitidos por el gobierno (licencia de conducir, identificación nacional, pasaporte). Al utilizar documentos de identificación de confianza, esta mejora añade un nivel adicional de confianza al proceso de firma, lo que lo hace ideal para situaciones que requieren una mayor seguridad, conformidad y validación del usuario.

   * **Pista de auditoría para documentos de Adobe Sign**: utilice la función Pista de auditoría para obtener información detallada sobre el ciclo de vida de los documentos de Adobe Sign. Con la pista de auditoría, se puede mantener un registro completo de todas las acciones e interacciones relacionadas con los documentos. Esto incluye detalles como quién vio, editó o firmó el documento, junto con marcas de tiempo para cada evento. Esta mejora es crucial para mantener el cumplimiento, resolver disputas y garantizar la integridad de los acuerdos digitales.

   * **Nuevas funciones para los destinatarios del acuerdo más allá del firmante**: Adobe Acrobat Sign tiene la opción de ampliar las funciones de los destinatarios del acuerdo más allá del firmante para que coincidan mejor con sus requisitos de flujo de trabajo. Cuando se habilita, cada destinatario de un acuerdo tiene su función que se configura de forma individual, siendo la de Firmante la predeterminada.

* **[Proteja sus documentos con las API de verificación de documentos (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de verificación de documentos permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se convierte a un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan acceder. Esta capa de protección fortificada no solo protege los datos valiosos de miradas no autorizadas, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos PDF de Adobe que distribuye y recibe. Este servicio utiliza firmas digitales y certificaciones para garantizar que solo los destinatarios autorizados puedan modificar los documentos.

* **Compatibilidad con recuentos de páginas en las API de comunicación**: ahora, junto con recuperar el documento a través de las API de comunicación, también puede recibir información valiosa sobre el número de páginas que contiene el documento.

* **[Tratamiento de errores con controladores de error personalizados en el editor de reglas](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: ahora se puede invocar una función personalizada en respuesta a un error devuelto por un servicio externo y proporcionar una respuesta adaptada a los usuarios finales. Por ejemplo, puede invocar un flujo de trabajo personalizado en el back-end para códigos de error específicos o informar al cliente de que el servicio está inactivo.


### Formularios adaptables sin encabezado, programa para primeros usuarios {#forms-early-adopter}

Utilice los [Formularios adaptables sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es) para que los desarrolladores puedan crear, publicar y gestionar formularios interactivos a los que se pueda acceder y con los que se pueda interactuar a través de API, en lugar de a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

* crear formularios multicanal de alta calidad en el lenguaje de programación que desee
* integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
* reutilizar los componentes de IU propios con aplicaciones de formularios
* aprovechar la potencia de Adobe Experience Manager Forms

Puede enviar un correo electrónico a `aem-forms-headless@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Registros de la CDN {#cdn-logs}

Se pueden descargar los registros de la CDN de Cloud Manager, lo que resulta útil para optimizar la proporción de visitas en caché y aumentar la visibilidad del flujo de entrega de contenido. [Más información](/help/implementing/developing/introduction/logging.md#cdn-log) sobre el formato de registro de la CDN. Esta funcionalidad se implementará gradualmente para los clientes a principios de septiembre.

### Programa de adopción temprana de reglas CDN y WAF {#waf-early-adopter}

Filtre el tráfico en la red de distribución de contenido (CDN) en función de lo siguiente:

* encabezados y propiedades de solicitud (por ejemplo, dirección IP)
* patrones de tráfico asociados a tráfico malintencionado

¿Quiere probar la función y compartir sus comentarios? Puede enviar un correo electrónico a **aemcs-waf-adopter@adobe.com** desde su ID de correo electrónico oficial para más información acerca del programa de primeros usuarios. El espacio es limitado.

Obtenga más información acerca de la funcionalidad en este [artículo](/help/security/traffic-filter-rules-including-waf.md).


## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
