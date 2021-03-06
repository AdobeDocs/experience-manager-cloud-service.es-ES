---
title: Notas de la versión 2021.10.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión 2021.10.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 48%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2021.10.0) es el 4 de noviembre de 2021.
La siguiente versión (2021.11.0) es el 2 de diciembre de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general sobre la versión de octubre de 2021](https://video.tv.adobe.com/v/338253) vídeo para ver un resumen de las funciones añadidas.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función de [!DNL Sites] {#sites-features}

* Los modelos de fragmento de contenido ahora se establecen automáticamente en estado de solo lectura una vez publicados, para evitar que se rompan de forma involuntaria las consultas de API en directo después de volver a publicar un modelo editado. Los usuarios reciben una advertencia cuando intentan editar un modelo publicado. La edición es posible tras aceptar la advertencia.

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] ahora admite la generación automática de transcripciones de texto desde los recursos de audio y vídeo compatibles, utilizando un conector integrado para [!DNL Azure Media Services]. La variable [tipos de archivo compatibles](/help/assets/file-format-support.md#audio-video-transcription-formats) se transcriben automáticamente y el texto se almacena en formato WebVTT. Los subtítulos WebVTT se utilizan para realizar búsquedas, subtítulos o traducciones más eficaces. Además, la función mejora la accesibilidad, la capacidad de detección y la localización de los recursos.

### Nueva función en la [!DNL Assets] canal de prelanzamiento {#assets-prerelease-features}

* [!DNL Dynamic Media]El recorte inteligente y la muestra de la imagen de ahora cuenta con la tecnología de los últimos servicios de Sensei, que generan recortes y muestras mejorados. Además, se ha lanzado una mejora para generar diferentes contenidos de recorte, para la misma proporción de aspecto pero en diferentes resoluciones. Además, las ediciones manuales se conservarán en el reprocesamiento si no hay cambios en la anchura y la altura del perfil de imagen.

* Las etiquetas inteligentes se aplican automáticamente a los recursos mediante microservicios de recursos, en lugar de los servicios de contenido inteligente. El modelo subyacente se actualiza para mejorar los resultados de etiquetado y reducir los sesgos. <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics para Forms adaptable**: Ahora puede capturar y rastrear el comportamiento de inicio de sesión y no inicio de sesión (Anonymous) mediante Adobe Analytics for Adaptive Forms para recopilar perspectivas del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Externalización de los datos de flujo de trabajo de AEM para un procesamiento seguro**: puede almacenar datos de flujos de trabajo AEM en el proceso (datos de variables de flujo de trabajo de AEM) que contengan elementos de datos personales sensibles (SPD) en un repositorio administrado por el cliente para un procesamiento seguro. Los elementos de datos y las variables de flujo de trabajo no se almacenan en el repositorio de AEM y se recuperan a petición de un repositorio administrado por el cliente mientras se procesa el flujo de trabajo.

### Funciones beta de [!DNL Forms] {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=es) le ayudan a combinar una plantilla y los datos XML para generar documentos de impresión en distintos formatos. El servicio le permite generar documentos en modos sincrónico y por lotes. Las API le permiten crear aplicaciones con las que puede:

   * Generar documentos rellenando archivos de plantilla (PDF y XDP) con datos XML.
   * Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.

Puede escribir en [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* El complemento CIF es compatible con la última versión de Commerce v2.4.3 con las nuevas API y esquemas de GraphQL

* Los autores pueden agregar vínculos a páginas de productos y catálogos en campos de texto utilizando el editor de texto enriquecido (RTE). Se ha agregado un icono del CIF a la barra de herramientas de RTE que abrirá los selectores para buscar y seleccionar rápidamente el producto o la categoría sin abandonar el contexto.

* El carro de compras emergente y el cierre de compra existentes se han sustituido por páginas dedicadas AEM carro de compras y de cierre de compra. Los componentes de estas páginas se crean utilizando los componentes Peregrine ampliables de Adobe Commerce

* Los comerciantes pueden ocultar ciertas categorías de catálogo de productos en la navegación mediante el servidor de Commerce. El componente principal de navegación del CIF respeta la configuración del back-end de comercio &quot;incluir en menú&quot; para mostrar u ocultar categorías en la navegación

* AEM Tienda Venia devuelve el error HTTP 404 si no se encuentra la categoría o la página de producto

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.10.0.

### Fecha de la versión {#release-date-cm-nov}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.11.0 es el 4 de noviembre de 2021.
La próxima versión está planificada para el 9 de diciembre de 2021.

### Novedades {#what-is-new-cm-nov}

* Los usuarios ahora pueden aprovechar las nuevas canalizaciones front-end para implementar exclusivamente el código front-end de forma acelerada. Consulte [Canalizaciones principales de Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obtener más información.

   >[!IMPORTANT]
   >Debe estar en AEM versión `2021.10.5933.20211012T154732Z` para aprovechar las nuevas canalizaciones front-end.

* La duración de la canalización Calidad del código se reduce significativamente al realizar el análisis del código de una manera más eficiente sin necesidad de crear una imagen de AEM completa. Este cambio se implementará progresivamente durante las semanas siguientes a la publicación.

* El ID de confirmación de Git ahora se mostrará en los detalles de ejecución de la canalización, lo que facilita el seguimiento del código creado.

* La creación de programas ya está disponible a través de una API expuesta públicamente.

* La creación de entornos ya está disponible a través de una API expuesta públicamente.

* El encabezado de respuesta `x-request-id` ahora está visible en el sitio de pruebas de API en [www.adobe.io](https://www.adobe.io/). Este encabezado es útil cuando se envían problemas de servicio de atención al cliente para la resolución de problemas.

* Como usuario, veo que la tarjeta de canalización con cero canalizaciones me proporciona la guía adecuada.

* Ya está disponible una nueva página Actividad donde se pueden ver actividades como las ejecuciones de canalización y código junto con los detalles asociados. Con el tiempo, las actividades enumeradas en esta página se ampliarán en alcance junto con los detalles proporcionados.

* Ya está disponible una nueva página de canalizaciones con una ventana emergente de estado al pasar el ratón por encima para facilitar la vista del resumen de detalles. Las ejecuciones de canalización se pueden ver junto con los detalles asociados.

* La API Editar canalización ahora admite el cambio del entorno utilizado en las fases de implementación.

* Se ha introducido una optimización en el proceso de digitalización de OakPal para paquetes grandes.

* El archivo CSV del problema de calidad ahora contendrá la marca de tiempo para cada problema de calidad.

### Corrección de errores {#bug-fixes-nov}

* Algunas configuraciones de compilación no ortodoxas tuvieron como resultado que se almacenaran archivos innecesarios en la caché de artefactos Maven de la canalización, lo que resultó en I/O de red superfluas al iniciar y detener el contenedor de compilación.

* La API PATCH de canalización falla si la fase de implementación no existe.

* La regla de calidad `ClientlibProxyResourceCheck` producía problemas de falsos positivos cuando había bibliotecas de cliente con rutas base comunes.

* El mensaje de error cuando se ha alcanzado el número máximo de repositorios no especificaba el motivo del error.

* En casos excepcionales, las canalizaciones fallaban debido a la gestión inadecuada de reintentos de ciertos códigos de respuesta.


## Fecha de la versión {#release-date-cm-oct}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.10.0 es el 14 de octubre de 2021.

### Novedades {#what-is-new-cm-oct}

* A fin de prepararse para algunos cambios, ahora se hará referencia a las canalizaciones de implementación existentes y se etiquetarán en la interfaz de usuario como **Pila completa** canalizaciones.

* La tarjeta de canalización se ha actualizado para que ahora muestre una sola cara integrada que muestre tanto las canalizaciones de producción como las que no son de producción, y el usuario puede seleccionar Ejecutar/Pausar/Reanudar directamente en el menú de acción asociado con cada canalización.

* Un usuario con la función de administrador de implementación ahora puede eliminar la canalización de producción de forma autoservicio mediante la interfaz de usuario.

* Se han actualizado las experiencias de adición y edición de canalización para que ahora utilicen modelos modernos y conocidos.

* Los usuarios de Cloud Manager ahora pueden enviar comentarios directamente desde la interfaz de usuario a través de la **Comentarios** en la parte superior derecha de la página de aterrizaje.

* Los gráficos SLA anuales ahora se pueden descargar desde la interfaz de usuario de Cloud Manager.

* La calidad del código y las ejecuciones de canalizaciones que no sean de producción ahora utilizarán un proceso de clonación superficial más eficiente durante el paso de compilación, lo que conllevará un tiempo de compilación más rápido para los clientes con repositorios Git especialmente grandes.

* El asistente para agregar Lista de permitidos de IP ahora informará al usuario si se ha alcanzado el número máximo permitido de Listas de permitidos de IP.

* La documentación de la API de Cloud Manager ahora incluye un área de reproducción interactiva que permite a los usuarios que iniciaron sesión experimentar con la API desde su explorador. Consulte [Reproducción de la API de Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) para obtener más información.

* La información del objeto de la tarjeta de programa será más descriptiva si se desactiva una opción de selección en &quot;Navegar a&quot;. Ahora muestra &quot;Un entorno de producción no existe&quot;.

### Corrección de errores {#bug-fixes-cm-oct}

* En raras ocasiones, cuando el personal de un Adobe restauraba el entorno de un cliente, la restauración se consideraba completa antes de que el entorno fuera completamente operativo.

* Algunas solicitudes internas realizadas durante la creación del entorno no se estaban reintentando.

* Si se produce un error de implementación tras la verificación del nombre de dominio, se ha corregido el mensaje de error para solicitar al cliente que se ponga en contacto con su representante de Adobe.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa-latest}

La fecha de versión de Best Practices Analyzer v2.1.20 es el 5 de octubre de 2021.

### Novedades {#what-is-new}

* Capacidad para detectar y crear informes sobre la longitud del nombre del nodo.

* Capacidad para detectar el tamaño total del índice e informar al respecto.

* Capacidad para detectar y crear informes sobre los recursos que no tienen su representación original.
