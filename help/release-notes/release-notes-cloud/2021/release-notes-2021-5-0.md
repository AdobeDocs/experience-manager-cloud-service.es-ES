---
title: Notas de la versión 2021.5.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2021.5.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 46%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 es el 27 de mayo de 2021.
La de la siguiente versión (2021.6.0) será el 28 de junio de 2021.

## AEM Base as a Cloud Service {#foundation}

### AEM Novedades en la Fundación as a Cloud Service de la {#what-is-new-foundation}

* [Canal de prelanzamiento](/help/release-notes/prerelease.md): Previsualice las próximas funciones durante un mes completo antes de que se activen en la producción.

* [Desaprobación de API](/help/release-notes/deprecated-apis.md)AEM : hay disponible una lista de las API obsoletas más recientes para el as a Cloud Service de la.

* [AEM Complemento Maven de SDK Build Analyzer as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es): Actualice sus proyectos de Maven a la versión más reciente, que incluye una comprobación de API de Java en desuso y otras mejoras.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* Próximamente podrá verificar el contenido de una nueva [Previsualizar nivel](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para simular la apariencia final de la experiencia como lo haría en el nivel de publicación. Esto se habilita mediante el asistente de publicación administrada de AEM Sites, que ahora le permite elegir un destino de publicación entre Publicar o Vista previa. Se puede acceder a las experiencias en Vista previa a través de una dirección URL dedicada. Después de la validación en Vista previa, el contenido se puede publicar de Autor a Publicar como de costumbre. AEM La activación del servicio Vista previa en entornos as a Cloud Service de la se implementará de forma gradual en las próximas semanas.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

* Puede descargar los recursos compartidos mediante la funcionalidad Compartir vínculos. Esta descarga ahora utiliza un servicio asincrónico que ofrece descargas más rápidas e ininterrumpidas, incluso para descargas muy grandes. Consulte [descargar recursos](/help/assets/download-assets-from-aem.md#link-share-download).

  ![Descargar bandeja de entrada](/help/assets/assets/download-inbox.png)

### Nuevas funciones disponibles en el canal de prelanzamiento {#what-is-new-assets-prerelease}

* Los esquemas de metadatos se pueden aplicar directamente a las propiedades de la carpeta.

  ![Añadir esquema de metadatos de las propiedades de carpeta](/help/assets/assets/metadata-schema-folder-properties.png)

* La herramienta Ingestor masivo de datos permite añadir metadatos durante una ingesta masiva.

* Las mejoras en la experiencia del usuario muestran el número de recursos presentes en una carpeta. Para más de 1000 recursos en una carpeta, [!DNL Assets] muestra más de 1000.

  ![El número de recursos de una carpeta se muestra en la interfaz](/help/assets/assets/browse-folder-number-of-assets.png)

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

* Al cargar archivos muy grandes, se bloquea el [!DNL Experience Manager desktop app]. (CQ-4320942)
* Las opciones de la barra de herramientas son diferentes cuando se selecciona la misma colección desde una carpeta y cuando se selecciona desde un resultado de búsqueda. (CQ-4321406)

#### Novedades de Dynamic Media {#what-is-new-dm}

* La RGPD (proporción de píxeles de dispositivo) de imágenes inteligentes y la optimización del ancho de banda de la red le permiten ofrecer imágenes de la mejor calidad de forma eficaz, en dispositivos con pantallas de alta resolución y ancho de banda de red restringido. Para obtener más información, consulte [Preguntas frecuentes sobre imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md) y [Optimización de imágenes con los formatos de imagen de próxima generación WebP y AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* Se ha introducido la compatibilidad con el formato de imagen de próxima generación AVIF en la entrega de Dynamic Media (modificador de URL de fmt).

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **Ayuda contextual**: Se ha agregado ayuda contextual para el editor de formularios adaptables, el editor de plantillas y el editor de temáticas para ayudar a los autores a comprender mejor las distintas características de los editores.
* **Mensajes de error en el explorador de propiedades**: Se han agregado mensajes de error para cada propiedad en el explorador de propiedades de formularios adaptables adaptable. Estos mensajes ayudan a comprender los valores permitidos para un campo.

### Próxima característica beta de [!DNL Forms] {#what-is-new-forms-prerelease}

Output as a Cloud service: El servicio de salida le ayuda a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio le permite generar documentos en los modos sincrónico y asicrónico por lotes. El servicio Output le permite crear aplicaciones con las que puede hacer lo siguiente:

* Generar formularios finales al rellenar archivos de plantilla con datos XML.
* Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
* Generar PDF de impresión a partir de PDF de formularios XFA.

Puede escribir a formscsbeta@adobe.com para inscribirse en el programa beta.

### Errores corregidos en [!DNL Forms] {#forms-bugs-fixed}

* En el paso Asignar tarea de Workflows de AEM Forms, cuando se sustituye el icono predeterminado de los botones de acción por un icono de coral, el flujo de trabajo deja de funcionar y registra una excepción. El flujo de trabajo funciona como se espera cuando se utilizan iconos predeterminados.
* En la capa de diseño, cuando cambia el número de columnas, abre la capa de edición y arrastra algunos componentes en un panel, los cuadros azules aparecen en el área de contenido del editor de formularios adaptables y el editor no responde.
* El mensaje de error de una opción del editor de reglas relacionada con el suministro de la URL de un activo adaptable o externo es demasiado largo y no es fácil de usar.


## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.5.0.

### Fecha de lanzamiento {#release-date-cm-may}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.5.0 es el 6 de mayo de 2021.
La próxima versión está planificada para el 03 de junio de 2021.

### Novedades {#what-is-new-may}

* La regla de calidad PackageOverlaps ahora detecta casos en los que el mismo paquete se implementó varias veces, es decir, en varias ubicaciones incrustadas, en el mismo conjunto de paquetes implementado.

* El extremo del repositorio en la API Public ahora incluye la URL de Git.

* Los registros de implementación descargados por un usuario de Cloud Manager son más profundos e incluyen detalles sobre errores y escenarios de éxito.

* Se han resuelto errores intermitentes encontrados al insertar el código en el Git de Adobe.

* Ahora, el complemento Commerce se puede aplicar a los programas de zonas protegidas durante el flujo de trabajo Editar programa.

* La experiencia Editar programa se ha actualizado.

* La tabla Nombres de dominio de la página Detalles del entorno mostrará hasta 250 nombres de dominio a través de las páginas.

* La pestaña Soluciones de los flujos de trabajo Añadir programa y Editar programa mostrarán la solución, aunque solo haya una solución disponible para el Programa.

* El mensaje de error en el registro de pasos de generación cuando la generación no producía ningún paquete de contenido implementado no estaba claro.

### Correcciones de errores {#bug-fixes-cm-may}

* En ocasiones, el usuario podía ver el estado “activo” verde junto a una Lista de IP permitidas incluso cuando esa configuración no se implementaba.

* En lugar de eliminar las variables “eliminadas”, la API de variables de canalización solo las marcaba con el estado **ELIMINADO**.

* Algunos problemas de calidad del código Smell-type impactaban incorrectamente en la clasificación de fiabilidad.

* Dado que los dominios comodín no son compatibles, la interfaz de usuario no permitía que el usuario enviase un dominio comodín.

* Cuando se iniciaba la ejecución de una canalización entre la medianoche y la 01:00 UTC, la versión del artefacto generada por Cloud Manager no se garantizaba que fuera mayor que la versión creada el día anterior.

* Durante la configuración del programa de zona protegida, una vez que el proyecto con código de muestra se haya creado correctamente, Administrar Git aparecerá como un vínculo desde la tarjeta Hero en la página Información general.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.4.6 es el 27 de mayo de 2021.

### Novedades {#what-is-new-ctt-latest}

* Se agregó una nueva instrucción de registro al registro de errores de inicio rápido si el usuario no tiene permiso de ejecución en el ejecutable Java.

* Cuando un usuario elimina un conjunto de migración de la interfaz de usuario de CTT, donde se realizó una extracción, la variable `tmp` La carpeta asociada con ese conjunto de migración se elimina para ahorrar espacio.

### Correcciones de errores {#bug-fixes-ctt-latest}

* Al eliminar un conjunto de migración, a veces aparecía un mensaje de error no útil en la IU de CTT. Esto se ha corregido.

* Al ejecutar la asignación de usuarios, si los usuarios tuvieran la misma dirección de correo electrónico en el destino y en el host pero nombres de usuario diferentes, se produciría un error en toda la ingesta. Esto se ha corregido. En un escenario tan conflictivo, el usuario/grupo se omite y se registra como un conflicto en el archivo de registro.

### Fecha de lanzamiento {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.4.0 es el 11 de mayo de 2021.

### Novedades {#what-is-new-ctt-may}

* Esta versión de la herramienta de transferencia de contenido crea representaciones de texto para los recursos que se migran a Cloud Service. Las representaciones de texto son necesarias para admitir la búsqueda de texto completo en recursos ingeridos.
* El número máximo de conjuntos de migración de la herramienta de transferencia de contenido que puede crear un usuario ha aumentado de 4 a 10.

### Correcciones de errores {#bug-fixes-ctt-may}

* Varias correcciones de errores relacionadas con la función de actualización automática en la interfaz de usuario de la herramienta de transferencia de contenido.
* Herramienta de transferencia de contenido con `wipe=true` generó un índice de contador incorrecto en el destino. Esto se ha corregido.

## Complemento de Commerce {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Compatibilidad de paginación con contenido asociado en propiedades de la consola de producto

### Correcciones de errores {#bug-fixes-commerce}

* Las miniaturas de recursos no se muestran en la pestaña Recursos de las propiedades del producto

* La ruta restablece los datos de vista previa en la consola del producto
