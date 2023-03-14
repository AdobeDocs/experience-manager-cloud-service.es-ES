---
title: Notas de la versión 2021.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2021.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 38%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] la versión actual (2021.9.0) es el 6 de octubre de 2021.
La de la siguiente versión (2021.10.0) es el 4 de noviembre de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general de la versión de septiembre de 2021](https://video.tv.adobe.com/v/337381) para ver un resumen de las funciones añadidas.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función en la [!DNL Sites] canal de prelanzamiento {#sites-prerelease-features}

* Los modelos de fragmento de contenido ahora se establecen automáticamente en estado de solo lectura una vez publicados, para evitar romper de forma involuntaria consultas de API activas después de volver a publicar un modelo editado. Los usuarios recibirán una advertencia cuando intenten editar un modelo publicado. Es posible realizar la edición tras aceptar la advertencia.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Ahora puede ordenar los recursos mostrados en los resultados de búsqueda en las vistas Columna y Tarjeta. El orden funciona en las columnas Nombre, Creada, Modificada o Ninguna.

   ![Ordenar los resultados de búsqueda en [!DNL Assets] en las vistas Columna y Tarjeta](/help/assets/assets/sort-searched-assets.png)
   *Imagen: ordenación de los resultados de búsqueda en [!DNL Assets] en las vistas Columna y Tarjeta.*

* Para invocar el procesamiento mediante programación utilizando los microservicios de recursos, se introduce una nueva API. Los desarrolladores ahora pueden aplicar un perfil de procesamiento de nivel de carpeta existente a uno o varios recursos específicos de una carpeta. El perfil de procesamiento se aplica en función de las actualizaciones de propiedades de metadatos personalizadas. Consulte `AssetProcessor` en el [[!DNL Experience Manager] Referencia de API](https://www.adobe.io/experience-manager/reference-materials/). Como antes, es posible [uso de microservicios de recursos desde la interfaz de usuario](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Utilizar funciones de Adobe Sign en un formulario adaptable**: Adobe Sign para el nivel de servicio empresarial tiene la opción de ampliar las funciones de los destinatarios del contrato, más allá del firmante, para que coincidan mejor con los requisitos del flujo de trabajo. Ahora puede [permitir que cada destinatario del acuerdo configure su función en un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform), siendo la de firmante la función predeterminada.

* **Analytics para formularios adaptables**: Ahora puede capturar y hacer un seguimiento del comportamiento del usuario final mediante Adobe Analytics para que el formulario adaptable recopile información del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

* **Conecte fácilmente AEM Forms con Microsoft Dynamics y Salesforce**: El servicio proporciona una configuración de origen de datos y modelos de datos predeterminados para Microsoft Dynamics y Salesforce, lo que lo hace [más rápido y fácil para los desarrolladores configurar Microsoft Dynamics y Salesforce como fuentes de datos para un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en).

* **Firme electrónicamente un formulario adaptable mediante el uso de DocuSign:** Puede utilizar DocuSign para firmar electrónicamente un formulario adaptable. El servicio proporciona una acción de envío personalizada para utilizar DocuSign con un formulario adaptable. Puede instalar el paquete disponible en Distribución de software para importar la acción de envío.

### Características beta de [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Conector de almacenamiento unificado:** Utilice el conector de almacenamiento unificado para externalizar los datos en proceso en repositorios que administre el cliente. Por ejemplo, puede
   * Habilitar la funcionalidad de guardar y reanudar el portal de Forms y almacenar borradores de formularios adaptables en un repositorio de datos que administre el cliente.
   * Almacenar datos de los flujos de trabajo de AEM en proceso (datos de variables de flujo de trabajo de AEM) que contengan datos personales confidenciales (SPD) en un repositorio que administre el cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) le ayudan a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio le permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:
   * Generar documentos rellenando archivos de plantilla con datos XML.
   * Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   * Genere archivos de PDF imprimibles desde un PDF de formularios XFA y un formulario de Adobe Acrobat.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* AEM La nueva pestaña &quot;Contenido de comercio asociado&quot; del editor de Sites aumenta la eficacia del autor al obtener acceso rápidamente al contenido de producto relevante para el contexto actual

   ![Contenido de comercio asociado](/help/assets/CIF/associated-commerce-content.png)

* Se ha mejorado la interfaz de usuario del selector de productos para mejorar la experiencia del usuario, aumentar la eficacia y admitir catálogos de productos complejos

   ![Nuevo selector de productos](/help/assets/CIF/product-picker.png)

* Respetar la propiedad &quot;include_in_menu&quot; en el componente de navegación

### Correcciones de errores {#bug-fixes-cif}

* El vaciado de caché del menú no funciona como se esperaba

* AEM Errores de JS durante el paso de implementación de CS y durante el uso de componentes del lado del cliente

* No se puede crear la configuración de nube del CIF en carpetas que tengan un nodo sling:configs

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### Novedades {#what-is-new-screens}

* Pantallas as a Cloud Service ahora admite la monitorización básica de la reproducción. El reproductor ahora informará de varias métricas de reproducción con cada ping (el valor predeterminado es de 30 segundos). En función de las métricas, permite detectar varios casos extremos (experiencia atascada, pantalla en blanco, problema de programación, etc.). Esta función permite al equipo monitorizar de forma remota si un reproductor está reproduciendo el contenido correctamente, mejora la reacción ante pantallas en blanco o experiencias rotas en el campo y reduce el riesgo de mostrar una experiencia rota al usuario final.
Consulte [Monitorización de reproducción básica](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) para obtener más información.

* Ahora se admite la compatibilidad con miniaturas para vídeos en Pantallas as a Cloud Service. Un autor de contenido puede definir una miniatura para los vídeos, de modo que la imagen pueda utilizarse como marcador de posición y probar correctamente la reproducción y la segmentación del contenido, mientras el equipo correspondiente finaliza el vídeo real. También se puede utilizar la imagen en caso de que falle la reproducción del vídeo.
Consulte [Compatibilidad con miniaturas para vídeos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) para obtener más información.

### Correcciones de errores {#bug-fixes-screens}

* El reproductor no ha podido mostrar contenido de la página incrustada y este problema ya está solucionado.

* Después de un inicio de sesión correcto, la navegación a la página predeterminada (canales) terminó en una página de error interno del servidor.

* Las entradas de etiquetas asociadas no se eliminaban al eliminar las listas de reproducción.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Nuevas funciones de [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Redes avanzadas**

>[!INFO]
>
>La función de red avanzada forma parte de la versión 2021.9.0 y se habilitará para clientes a mediados de octubre.

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] ahora ofrece varios tipos de funciones de red avanzadas, entre las que se incluyen:

* Salida de puerto flexible para recibir tráfico de puertos no estándar. Ahora es posible sin ponerse en contacto con el Soporte de Adobe.
* AEM La dirección IP de salida dedicada para extraer tráfico de la salida as a Cloud Service desde una dirección IP única, ahora es compatible con todos los puertos de salida de la red.
* AEM VPN para proteger el tráfico entre su infraestructura y el as a Cloud Service.

Lea el [documentación](/help/security/configuring-advanced-networking.md) para obtener más información, incluido cómo aprovisionar de forma automática redes avanzadas mediante las API de Cloud Manager.

**Optimizaciones de índice**

Para mejorar el rendimiento de las consultas de búsqueda y la indexación, el índice de texto completo lucene-2 ya no se utiliza de forma predeterminada en [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] de esta versión. AEM AEM Con el fin de eliminar este índice de texto completo en entornos de de acuerdo con los clientes, Adobe Engineering trabaja de forma individual y proactiva con los clientes para eliminar de forma suave y sostenible el índice de texto completo de Lucene. Visite la [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [documentación](/help/operations/indexing.md#index-optimizations) para obtener más información y póngase en contacto con nuestro servicio de asistencia directamente si tiene alguna pregunta.

## Cloud Manager {#cloud-manager}

AEM Esta sección describe las notas de la versión para Cloud Manager en las versiones 2021.9.0 y 2021.8.0 de as a Cloud Service.

## Fecha de lanzamiento {#release-date-cm-sept}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.9.0 es el 9 de septiembre de 2021.
La próxima versión está planificada para el 7 de octubre de 2021.

### Novedades {#what-is-new-cm-sept}

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 30.

* Se han actualizado las tarjetas de programa de la página de aterrizaje de Cloud Manager y la experiencia asociada.

* El registro de pasos de calidad del código ahora incluye información detallada sobre el registro en el proceso de digitalización de OakPal.

* Las opciones del menú de la página Actividad ahora incluyen una opción para **Descargar el registro** para ejecuciones completadas del generador de códigos. Si selecciona esta opción, se descargará el registro del paso de generación.

* Al hacer clic directamente en la tarjeta de programa, ahora accederá a la página de Información general de Cloud Manager.

### Correcciones de errores {#bug-fixes-sept}

* El usuario ahora verá un mensaje más comprensible al intentar agregar una nueva lista de IP permitidas en un programa que haya alcanzado el número máximo permitido de listas de IP permitidas que se pueden configurar.

* Se copió una dirección URL incorrecta al seleccionar la opción de menú Copiar URL de la pantalla Repositorios.

## Cloud Acceleration Manager {#cam}

### Fecha de lanzamiento {#release-date-october-cam}

La fecha de lanzamiento de Cloud Acceleration Manager es el 4 de octubre de 2021.

### Novedades {#what-is-new-cam}

* Cloud Acceleration Manager ahora permite a los usuarios ver los informes de BPA en una vista previa imprimible, lo que permite hacer una impresión simple o una impresión en el PDF para compartir fácilmente. Consulte los pasos 6 y 7 en [Tarjeta de análisis de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de versión de la herramienta de transferencia de contenido v1.6.0 es el 4 de octubre de 2021.

### Novedades {#what-is-new-ctt}

* Asignación de usuarios mejorada con una experiencia de usuario simplificada que incluye las siguientes funciones enumeradas a continuación. Para obtener más información, consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=es#using-user-mapping-tool).
   * Probar la conexión a la API de administración de usuarios antes de ejecutar la asignación de usuarios
   * Omitir correctamente los errores y continuar con la actividad de asignación de usuarios
   * La asignación de usuarios ya no falla si caduca el token de acceso (después de 24 horas). La asignación de usuarios se puede volver a ejecutar desde la última vez que se detuvo.

* Para aumentar la solidez de CTT, el contenido se puede ingerir en una instancia de autor o de publicación a la vez.

* Cuando se incluyen versiones, la ruta `/var/audit` para migrar eventos de auditoría.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa-latest}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.18 es el 2 de septiembre de 2021.

### Novedades {#what-is-new}

* Capacidad para detectar e informar sobre el recuento total de nodos.

* Capacidad para detectar y crear informes sobre el tipo y el tamaño del almacén de nodos.

### Correcciones de errores {#bug-fixes-bpa}

* BPA detectaba falsamente la presencia de Commerce Integration Framework.
