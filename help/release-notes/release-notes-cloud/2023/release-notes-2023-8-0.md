---
title: Notas de la versión 2023.8.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.8.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a0ffa6cf-64ae-468c-93f4-ac6805ef907e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 20%

---

# Notas de la versión 2023.8.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.8.0 de [!DNL Experience Manager] as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] La versión de la funcionalidad actual (2023.8.0) es el 31 de agosto de 2023. La próxima versión de la funcionalidad (2023.9.0) está planificada para el 28 de septiembre de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de agosto de 2023 para ver un resumen de las funciones añadidas en la versión 2023.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Experience Manager Sites] {#sites-features}

* El [Consola de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=es) ahora permite a los usuarios ver etiquetas y buscar por etiquetas aplicadas como metadatos a fragmentos de contenido. Los usuarios ya no tendrán que cambiar a la IU de Assets para esta capacidad, lo que reduce el cambio de contexto y mejora la eficacia.

  ![Etiquetado en la consola de fragmentos de contenido](/help/assets/content-fragments-console-tags.png)
* AEM El nuevo Editor de fragmentos de contenido ya está disponible en el as a Cloud Service de la. Permite a los autores de contenido ser más productivos al optimizar sus tareas de creación y reducir la necesidad de cambiar entre distintas aplicaciones mientras editan contenido.
  ![Nuevo editor de fragmentos de contenido](/help/release-notes/assets/newCFEditor.png)

El nuevo editor de fragmentos de contenido ofrece las siguientes ventajas que no están disponibles en el editor original:
* Guardado automático para mejorar la eficacia de la creación y evitar la pérdida accidental de ediciones.
* Vista jerárquica de un fragmento de contenido y sus referencias mediante el árbol de estructura para una navegación rápida dentro de un fragmento profundamente estructurado.
  ![Árbol de estructura en el editor de fragmentos de contenido](/help/release-notes/assets/newCFEditor_StructureTree.png)

* Carga en línea de recursos como referencias de contenido sin tener que cargarlos primero en el DAM de recursos
* Vista previa ad hoc de la experiencia representada por el fragmento de contenido para ayudar a los autores a visualizar el aspecto del contenido en la aplicación de front-end
* 1 clic en publicación y cancelación de la publicación del fragmento de contenido desde el editor
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

* **Importación masiva de recursos desde fuentes de datos**: Los administradores ahora tienen el [capacidad para importar un gran número de recursos](/help/assets/bulk-import-assets-view.md) de una fuente de datos a AEM Assets. Los administradores ya no tienen que cargar archivos o carpetas individuales a AEM Assets. Las fuentes de datos admitidas para la importación masiva son Azure, AWS, Google Cloud y Dropbox.

  ![Importación masiva de recursos desde una fuente de datos](/help/release-notes/assets/bulk-import.png)

* **Herramientas de edición de imágenes con tecnología de Adobe Express**: Fácil e intuitivo [herramientas de edición de imágenes con tecnología de Adobe Express](/help/assets/edit-images-assets-view.md) disponible directamente en AEM Assets para aumentar la reutilización del contenido y acelerar la velocidad de contenido.

  ![Edición de imágenes con Adobe Express](/help/release-notes/assets/edit-adobe-express.png)

* **Flexibilidad al fijar elementos para el acceso rápido de Mi espacio de trabajo**: capacidad para seleccionar y anclar elementos para usted, para toda su organización o para una lista de grupos para que se muestren en el [Sección Acceso rápido de Mi espacio de trabajo](/help/assets/my-workspace-assets-view.md) en función de su selección.

  ![Fijar elementos para grupos](/help/release-notes/assets/pin-items-for-groups.png)

### Nuevas funciones en la vista de administración {#admin-view-features}

**Mejoras de búsqueda**

* Los administradores ahora pueden [configurar el tamaño del lote de recursos](/help/assets/search-assets.md#configure-asset-batch-size) que se muestran al realizar una búsqueda. Los resultados de la búsqueda de recursos se muestran en múltiplos del número de tamaño de lote configurado al desplazarse hacia abajo para cargar los resultados. Puede seleccionar entre los tamaños de lote disponibles de 200, 500 y 1000 recursos. Configurar un número de tamaño de lote menor resulta en tiempos de respuesta de búsqueda más rápidos.

  ![Configuración de tamaño de lote de recursos](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets ahora incluye una nueva versión 9 de `damAssetLucene` índice. `damAssetLucene-9` cambia el comportamiento del recuento de facetas de Oak Query a [ya no se evalúa el control de acceso en los recuentos de facetas](/help/assets/search-assets.md) devuelto por el índice de búsqueda subyacente, lo que resulta en tiempos de respuesta de búsqueda más rápidos.

### Funciones previas al lanzamiento disponibles en [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Compatibilidad con subtítulos múltiples y pistas de audio múltiple para vídeos en Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): ahora se pueden añadir fácilmente varios subtítulos y varias pistas de audio a un vídeo principal. Esta capacidad significa que los vídeos son accesibles para toda la audiencia global. Puede personalizar un solo vídeo principal publicado a una audiencia global en varios idiomas y adherirse a las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

  ![Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.](/help/release-notes/assets/msma-aem-cs.png)*Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.*

* **Assets**: capacidad para seleccionar archivos ZIP administrados en Experience Manager y [extracción de los archivos directamente en el Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) sin descargarlos.

  ![Fijar elementos para grupos](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Soporte empresarial de Google reCAPTCHA**](/help/forms/captcha-adaptive-forms.md): utilice Google reCAPTCHA Enterprise en un formulario adaptable para proporcionar una protección mejorada contra la actividad fraudulenta y el correo no deseado, lo que ofrece una experiencia de usuario más segura. Con un análisis de riesgo avanzado y una integración perfecta, los usuarios genuinos pueden enviar fácilmente formularios mientras los bots están bloqueados de manera efectiva.


### Funciones previas al lanzamiento disponibles en [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* **Adobe Analytics con automatización de la configuración de Experience Cloud para Forms**: Ahora puede habilitar Adobe Analytics con la automatización de la configuración de Experience Cloud con un par de botones. Permite conectar AEM Forms as a Cloud Service con etiquetas de Experience Platform y Adobe Analytics para capturar y realizar un seguimiento de las métricas de rendimiento de los formularios publicados.

* **Plantilla de informe de Adobe Analytics para Forms adaptable**: Forms as a Cloud Service ahora proporciona un informe OOTB de Adobe Analytics. Le ayuda a comprender fácilmente el rendimiento de sus formularios. Las métricas de nivel de formulario proporcionan una perspectiva del rendimiento del formulario en varios indicadores clave de rendimiento (KPI) como, representaciones, visitantes, envíos o tiempo medio de cumplimentación. Al realizar un seguimiento del comportamiento y los comentarios de los usuarios, se pueden identificar las áreas del formulario que causan confusión y guiar las mejoras en el diseño y la funcionalidad del formulario.

  ![Informe de Adobe Analytics de participación del usuario del formulario adaptable](/help/forms/assets/forms-analytics-report.png)

* **[Fragmento de formulario en Forms adaptable basado en componentes principales](/help/forms/adaptive-form-fragments-core-components.md)**: Diga adiós a la duplicación, optimice su inventario digital y mejore la colaboración a medida que eleva su experiencia de creación de formularios con fragmentos de formularios. Estos componentes reutilizables se integran perfectamente en varios formularios, lo que optimiza la creación de formularios coherentes y de aspecto profesional. Los fragmentos de formulario garantizan la reutilización, la estandarización y la coherencia de la marca mediante la funcionalidad &quot;cambiar una vez y reflejar en todas partes&quot;. Experimente una mayor capacidad de mantenimiento y eficacia, ya que las actualizaciones realizadas en un solo lugar se propagan automáticamente a todos los formularios que utilizan estos fragmentos.

* **[Paso de flujo de trabajo de Adobe Sign mejorado](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: El paso del flujo de trabajo de Adobe Sign se ha mejorado para incluir lo siguiente:
   * **Autenticación basada en documentos de identidad oficiales para Adobe Sign**: la autenticación basada en documentos de identidad oficiales de Adobe Acrobat Sign ofrece un nivel adicional de verificación al permitir a los usuarios autenticarse con documentos de identidad emitidos por el gobierno (licencia de conducir, identificación nacional, pasaporte). Al utilizar documentos de identificación de confianza, esta mejora añade un nivel adicional de confianza al proceso de firma, lo que lo hace ideal para situaciones que requieren una mayor seguridad, conformidad y validación del usuario.

   * **Pista de auditoría para documentos de Adobe Sign**: utilice la función Pista de auditoría para obtener información detallada sobre el ciclo de vida de los documentos de Adobe Sign. Con la pista de auditoría, ahora puede mantener un registro completo de todas las acciones e interacciones relacionadas con sus documentos. Esto incluye detalles como quién vio, editó o firmó el documento, junto con marcas de tiempo para cada evento. Esta mejora es crucial para mantener el cumplimiento, resolver disputas y garantizar la integridad de los acuerdos digitales.

   * **Nuevas funciones para los destinatarios del acuerdo más allá del firmante**: Adobe Acrobat Sign tiene la opción de ampliar las funciones de los destinatarios del acuerdo más allá del firmante para que coincidan mejor con sus requisitos de flujo de trabajo. Cuando se habilita, cada destinatario de un acuerdo tiene su función configurable individualmente, con firmante como predeterminado.

* **[Protect carga sus documentos con las API de Document Assurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de Document Assurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa reforzada de protección no solo protege los datos valiosos de los ojos no autorizados, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos de Adobe PDF que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

* **Compatibilidad con recuentos de páginas en las API de comunicación**: Ahora, junto con recuperar el documento a través de las API de comunicación, también puede recibir la información valiosa sobre el número de páginas que contiene el documento.

* **[Tratamiento de errores con controladores de error personalizados en el editor de reglas](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: Ahora puede invocar una función personalizada en respuesta a un error devuelto por un servicio externo y proporcionar una respuesta personalizada a los usuarios finales. Por ejemplo, puede invocar un flujo de trabajo personalizado en el back-end para códigos de error específicos o informar al cliente de que el servicio está inactivo.


### Formularios adaptables sin encabezado, programa para primeros usuarios {#forms-early-adopter}

Utilice los [Formularios adaptables sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es) para que los desarrolladores puedan crear, publicar y gestionar formularios interactivos a los que se pueda acceder y con los que se pueda interactuar a través de API, en lugar de a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

* crear formularios multicanal de alta calidad en el lenguaje de programación que desee
* integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
* reutilizar los componentes de IU propios con aplicaciones de formularios
* aprovechar la potencia de Adobe Experience Manager Forms

Puede enviar un correo electrónico a `aem-forms-headless@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Registros de CDN {#cdn-logs}

Descargue los registros de CDN de Cloud Manager, lo que resulta útil para optimizar la proporción de visitas en caché y aumentar la visibilidad del flujo de entrega de contenido. [Más información](/help/implementing/developing/introduction/logging.md#cdn-log) el formato de registro de CDN. Esta función se implementará gradualmente para los clientes a principios de septiembre.

### Programa de adopción temprana de reglas CDN y WAF {#waf-early-adopter}

Filtre el tráfico en la CDN en función de lo siguiente:
* encabezados y propiedades de solicitud (por ejemplo, dirección IP)
* patrones de tráfico asociados a tráfico malintencionado

¿Quiere probar la función y compartir sus comentarios? Envíe un correo electrónico a **aemcs-waf-adopter@adobe.com** desde su ID de correo electrónico oficial para obtener más información sobre el programa de usuarios que lo adoptaron por primera vez. El espacio es limitado.

Obtenga más información acerca de la función en el artículo [aquí](/help/security/traffic-filter-rules-including-waf.md).


## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
