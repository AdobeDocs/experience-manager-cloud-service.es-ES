---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: c7cba6217ec960219c607b76ab7f2f096af7459a
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 2%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las notas de la versión generales de la versión actual (más reciente) de [!DNL Experience Manager] como Cloud Service.

>[!NOTE]
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021 y así sucesivamente.

>[!NOTE]
>
>Consulte [Actualizaciones de documentación recientes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obtener más información sobre las actualizaciones de documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2021.5.0 es el 27 de mayo de 2021.
La siguiente versión (2021.6.0) se publicará el 24 de junio de 2021.

## Vídeo de la versión {#release-video}

Consulte el vídeo [Información general de la versión de mayo de 2021](https://video.tv.adobe.com/v/333602) para ver un resumen de las funciones agregadas.

## AEM as a Cloud Service Foundation {#foundation}

### Novedades de AEM as a Cloud Service Foundation {#what-is-new-foundation}

* [Canal](/help/release-notes/prerelease.md) previo al lanzamiento: Previsualice las próximas funciones durante un mes completo antes de publicarlas en producción.

* [Desaprobación de API](/help/release-notes/deprecated-apis.md): hay disponible una lista de las API obsoletas más recientes de AEM as a Cloud Service.

* [AEM as a Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html): Actualice sus proyectos de maven a la versión más reciente, que incluye una comprobación de API de Java obsoleta y otras mejoras.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* Pronto podrá verificar el contenido en un nuevo [Nivel de vista previa](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para simular el aspecto y la presentación finales de la experiencia como lo haría en el nivel de publicación. Esto lo habilita el asistente de publicación administrada de AEM Sites, que ahora le permite elegir un destino de publicación entre Publicar o Vista previa. A continuación, se puede acceder a las experiencias en la vista previa a través de una URL dedicada. Después de la validación en la vista previa, el contenido se puede publicar desde Autor en Publicación como de costumbre. La activación del servicio de vista previa en entornos AEM as a Cloud Service se implementará gradualmente en las próximas semanas.

## [!DNL Adobe Experience Manager Assets] como  [!DNL Cloud Service] {#assets}

### Nuevas funciones disponibles en el canal de prelanzamiento {#what-is-new-assets-prerelease}

* Los esquemas de metadatos se pueden aplicar directamente a las propiedades de la carpeta.

   ![Añadir esquema de metadatos de propiedades de carpeta](/help/assets/assets/metadata-schema-folder-properties.png)

* La herramienta Ingesta masiva de recursos permite agregar metadatos durante una ingesta masiva.

* Las mejoras en la experiencia del usuario muestran el número de recursos presentes en una carpeta. Para más de 1000 recursos en una carpeta, [!DNL Assets] muestra más de 1000.

   ![El número de recursos de una carpeta se muestra en la interfaz](/help/assets/assets/browse-folder-number-of-assets.png)

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

* Al cargar archivos muy grandes, se bloquea [!DNL Experience Manager desktop app]. (CQ-4320942)
* Las opciones de la barra de herramientas son diferentes cuando se selecciona la misma colección dentro de una carpeta y cuando se selecciona desde un resultado de búsqueda. (CQ-4321406)

#### Novedades de [!DNL Dynamic Media] {#what-is-new-dm}

* La proporción de píxeles de dispositivos de imágenes inteligentes (DPR) y la optimización del ancho de banda de la red le permiten ofrecer imágenes de la mejor calidad de forma eficaz, en dispositivos con pantallas de alta resolución y ancho de banda de red restringido. Consulte [preguntas frecuentes sobre imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md).

* Se ha introducido compatibilidad con el formato de imagen de próxima generación AVIF en el envío [!DNL Dynamic Media] (`fmt` modificador de URL). Para obtener más información y cronología, consulte [servicio de imágenes y renderización de API fmt](https://experienceleague.corp.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

## [!DNL Adobe Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **Ayuda contextual**: Se ha añadido ayuda contextual para el editor de formularios adaptables, el editor de plantillas y el editor de temas para ayudar a los autores a comprender mejor las distintas funciones de los editores.
* **Mensajes de error en el navegador** de propiedades: Se han añadido mensajes de error para cada propiedad en el explorador de propiedades de Forms adaptable. Estos mensajes ayudan a comprender los valores permitidos para un campo.

### Próxima función beta de [!DNL Forms] {#what-is-new-forms-prerelease}

Output as a Cloud service: El servicio de salida le ayuda a combinar plantillas XDP y datos XML para generar documentos de impresión en varios formatos. El servicio le permite generar documentos en modo por lotes sincrónico y asincrónico. El servicio de salida permite crear aplicaciones que le permitan:

* Genere documentos de formulario finales rellenando archivos de plantilla con datos XML.
* Genere formularios de salida en varios formatos, incluidas secuencias de impresión PDF no interactivas.
* Genere PDFs de impresión a partir de PDFs de formulario XFA.

Puede escribir en formscsbeta@adobe.com para inscribirse en el programa beta.

### Errores corregidos en [!DNL Forms] {#forms-bugs-fixed}

* En el paso Asignar tarea de los flujos de trabajo de AEM Forms, cuando se sustituye el icono predeterminado de los botones de acción por un icono de coral, el flujo de trabajo deja de funcionar y registra una excepción. El flujo de trabajo funciona como se espera cuando se utilizan iconos predeterminados.
* En la capa de diseño, cuando cambie el número de columnas, abra la capa de edición y arrastre algunos componentes en un panel, los cuadros azules cuadrados empezarán a aparecer en el área de contenido del editor de formularios adaptables y el editor no responderá.
* Mensaje de error de una opción de editor de reglas relacionada con el suministro de la URL de un recurso adaptable o externo es demasiado largo y no es fácil de usar.

## Cloud Manager {#cloud-manager}

Esta sección describe las Notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.6.0 y 2021.5.0.

## Fecha de la versión {#release-date-june-cm}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.6.0 es el 10 de junio de 2021.
La próxima versión está planificada para el 15 de julio de 2021.

### Novedades {#what-is-new-junecm}

* El servicio de vista previa se implementará progresivamente en todos los programas. Se notificará al producto a los clientes cuando su programa esté habilitado para el servicio de vista previa. Consulte [Acceso al servicio de vista previa](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) para obtener más información.

* Las dependencias de Maven descargadas durante el paso de compilación ahora se almacenan en caché entre ejecuciones de canalización. Esta función se habilitará para los clientes en las próximas semanas.

* El nombre del programa ahora se puede editar mediante el cuadro de diálogo editar programa .

* El nombre de rama predeterminado utilizado durante la creación del proyecto y en el comando push predeterminado mediante la administración de flujos de trabajo de Git se ha cambiado a `main`.

* Se ha actualizado la edición de la experiencia del programa en la interfaz de usuario.

* La regla de calidad `ImmutableMutableMixCheck` se ha actualizado para clasificar los nodos `/oak:index` como inmutables.

* Las reglas de calidad `CQBP-84` y `CQBP-84--dependencies` se han consolidado en una sola regla. Como parte de esta consolidación, el análisis de dependencias identifica con mayor precisión los problemas en dependencias de terceros que se están implementando en el tiempo de ejecución de AEM.

* Para evitar confusiones, se han consolidado las filas de segmento Publicar AEM y Publicar Dispatcher en la página Detalles del entorno .

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* Se ha agregado una nueva regla de calidad de código para validar la estructura de los índices `damAssetLucene`. Para obtener más información, consulte [Personalización de los índices Oak de DAM Asset Lucene](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) .

* La página de detalles del entorno ahora mostrará varios nombres de dominio para los servicios de publicación y vista previa (según corresponda). Consulte [Detalles del entorno](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obtener más información.

### Corrección de errores {#bug-fixes-junecm}

* Las definiciones de nodo JCR que contenían una nueva línea después del nombre del elemento raíz no se analizaron correctamente.

* La API de repositorios de lista no filtraba los repositorios eliminados.

* Se mostraba un mensaje de error incorrecto cuando se proporcionaba un valor no válido para el paso de programación.

* En ocasiones, el usuario puede ver un estado *activo* verde junto a una Lista de permitidos IP incluso cuando esa configuración no se implementó.

* Algunas secuencias de edición de programas podrían resultar en la incapacidad de crear o editar la canalización de producción.

* Algunas secuencias de edición de programas podrían provocar que la página **Información general** muestre un mensaje engañoso para volver a ejecutar la configuración del programa.


### Fecha de la versión {#release-date-cm-may}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.5.0 es el 6 de mayo de 2021.

### Novedades {#what-is-new-may}

* La regla de calidad PackageOverlaps ahora detecta casos en los que el mismo paquete se implementó varias veces, es decir, en varias ubicaciones incrustadas, en el mismo conjunto de paquetes implementado.

* El extremo del repositorio en la API pública ahora incluye la URL de Git.

* El registro de implementación descargado por un usuario de Cloud Manager será más profundo y ahora incluirá detalles sobre errores y escenarios de éxito.

* Se han resuelto errores intermitentes encontrados al insertar el código en el Git de Adobe.

* Ahora, el complemento Commerce se puede aplicar a los programas de Sandbox durante el flujo de trabajo Editar programa .

* Se ha actualizado la experiencia Editar programa.

* La tabla Nombres de dominio de la página Detalles del entorno mostrará hasta 250 nombres de dominio a través de la paginación.

* La pestaña Soluciones de los flujos de trabajo Añadir programa y Editar programa mostrará la solución, aunque solo haya una solución disponible para el Programa.

* El mensaje de error en el registro de pasos de compilación cuando la compilación no produjo ningún paquete de contenido implementado no estaba claro.

### Corrección de errores {#bug-fixes-cm-may}

* En ocasiones, el usuario puede ver un estado &quot;activo&quot; verde junto a una Lista de permitidos IP incluso cuando esa configuración no se implementó.

* En lugar de eliminar las variables &quot;eliminadas&quot;, la API de variables de canalización solo las marcaría con el estado **DELETED**.

* Algunos problemas de calidad del tipo de hueso de código impactaban incorrectamente en la clasificación de fiabilidad.

* Dado que los dominios comodín no son compatibles, la interfaz de usuario no permitirá que el usuario envíe un dominio comodín.

* Cuando se inició la ejecución de una canalización entre la medianoche y la 01:00 UTC, la versión del artefacto generada por Cloud Manager no estaba buena a la versión creada el día anterior.

* Durante la configuración del programa de espacio aislado, una vez que el proyecto con código de muestra se haya creado correctamente, Administrar Git aparecerá como un vínculo desde la tarjeta promocional en la página Información general .

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de versión de la herramienta de transferencia de contenido v1.4.6 es el 27 de mayo de 2021.

### Novedades {#what-is-new-ctt-latest}

* Se agregó una nueva instrucción de registro al registro de errores de inicio rápido si el usuario no tiene permiso de ejecución en el ejecutable de Java.

* Cuando un usuario elimina un conjunto de migración de la interfaz de usuario de CTT, donde se realizó una extracción, la carpeta `tmp` asociada con ese conjunto de migración se eliminará para ahorrar espacio.

### Corrección de errores {#bug-fixes-ctt-latest}

* Al eliminar un conjunto de migraciones, en ocasiones aparecía un mensaje de error no útil en la interfaz de usuario de CTT. Esto se ha solucionado.

* Al ejecutar la Asignación de usuarios, si los usuarios tenían la misma dirección de correo electrónico en el destino y el host pero nombres de usuario diferentes, se producía un error en toda la ingesta. Esto se ha solucionado. En este caso de conflicto, el usuario o grupo se omite y se registra como conflicto en el archivo de registro.

### Fecha de la versión {#release-date-ctt-may}

La fecha de versión de la herramienta de transferencia de contenido v1.4.0 es el 11 de mayo de 2021.

### Novedades {#what-is-new-ctt-may}

* Esta versión de la herramienta de transferencia de contenido crea representaciones de texto para los recursos que se migran a Cloud Service. Las representaciones de texto son necesarias para admitir la búsqueda de texto completo en recursos ingestados.
* El número máximo de conjuntos de migración de la herramienta de transferencia de contenido que un usuario puede crear ha aumentado de 4 a 10.

### Corrección de errores {#bug-fixes-ctt-may}

* Varias correcciones de errores relacionadas con la función de actualización automática en la interfaz de usuario de la herramienta de transferencia de contenido.
* La herramienta de transferencia de contenido con `wipe=true` daba como resultado un índice de contador incorrecto en el destino. Esto se ha solucionado.

## Complemento de comercio {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Compatibilidad de paginación para contenido asociado en propiedades de la consola del producto

### Corrección de errores {#bug-fixes-commerce}

* Las miniaturas de los recursos no se muestran en la ficha Recurso de las propiedades del producto

* La ruta de navegación restablece los datos de vista previa en la consola del producto
