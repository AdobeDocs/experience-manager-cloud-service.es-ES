---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 9eeb47dbca36f1b9f23e3ac4e0bee6594ffb7fda
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 3%

---


# Notas de la versión actuales para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones de documentación recientes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obtener más información sobre las actualizaciones de documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.9.0) es el 6 de octubre de 2021.
La siguiente versión (2021.10.0) es el 28 de octubre de 2021.

## Vídeo de la versión {#release-video}

Consulte el vídeo [Información general de la versión de septiembre de 2021](https://video.tv.adobe.com/v/337381) para ver un resumen de las funciones agregadas.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función en el canal de prelanzamiento [!DNL Sites] {#sites-prerelease-features}

* Los modelos de fragmento de contenido ahora se establecen automáticamente en estado de solo lectura una vez publicados, para evitar dividir de forma involuntaria las consultas de API en vivo después de volver a publicar un modelo editado. Los usuarios reciben una advertencia cuando intentan editar un modelo publicado. La edición es posible tras aceptar la advertencia.

## [!DNL Experience Manager Assets] como  [!DNL Cloud Service] {#assets}

### Nuevas funciones en [!DNL Assets] {#assets-features}

* Los usuarios ahora pueden ordenar los recursos mostrados en los resultados de búsqueda en las vistas Columna y Tarjeta. La ordenación funciona en las columnas Nombre, Creado, Modificado o Ninguno.

   ![Ordene los resultados de búsqueda  [!DNL Assets] en las vistas Columna y Tarjeta](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordene los resultados de búsqueda  [!DNL Assets] en las vistas Columna y Tarjeta.*

<!-- TBD: 'Unpublishing' this feature as suggested by engineering.

* To programmatically invoke processing using asset microservices, a new API is introduced. Developers can now apply an existing folder-level processing profile on one or more specific assets in a folder. The processing profile gets applied based on custom metadata properties updates. See `AssetProcessor` in the [[!DNL Experience Manager] API reference](https://www.adobe.io/experience-manager/reference-materials/). As before, it is possible to [use asset microservices from the user interface](/help/assets/asset-microservices-configure-and-use.md).

-->
<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Uso de funciones de Adobe Sign en un formulario** adaptable: Adobe Sign para los niveles de servicio empresarial y empresarial tiene la opción de ampliar las funciones de los destinatarios del Acuerdo, más allá del Firmante, para que coincidan mejor con sus requisitos de flujo de trabajo. Ahora puede [habilitar a cada destinatario del acuerdo para que configure su función en un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform), siendo Signer la función predeterminada.

* **Analytics para Forms adaptable**: Ahora puede capturar y  [rastrear el comportamiento del usuario final mediante Adobe ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/integrate-aem-forms-with-adobe-analytics.html) Analytics para Adaptive Forms para recopilar perspectivas del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

* **Conecte fácilmente AEM Forms con Microsoft Dynamics y Salesforce**: El servicio proporciona una configuración de origen de datos y modelos de datos predeterminados para Microsoft Dynamics y Salesforce, lo que facilita y  [agiliza la configuración de Microsoft Dynamics y Salesforce como fuentes de datos para un formulario](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en) adaptable.

* **Firme un formulario adaptable por correo electrónico conSign:** [puede utilizarSign para firmar electrónicamente un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/integrate-docusign-adaptive-forms.html). El servicio proporciona una acción de envío personalizada para utilizar ArchiveSign con un formulario adaptable.

### Funciones beta de [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Conector de almacenamiento unificado:** utilice el conector de almacenamiento unificado para externalizar los datos en proceso en repositorios administrados por el cliente. Por ejemplo, puede almacenar datos de flujos de trabajo AEM en proceso (AEM datos de variables de flujo de trabajo) que contengan datos personales confidenciales (SPD) en un repositorio administrado por el cliente.

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [Communication ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) APIShelp permite combinar plantillas XDP y datos XML para generar documentos de impresión en varios formatos. El servicio le permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones que le permitan:
   * Genere documentos rellenando archivos de plantilla con datos XML.
   * Genere formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   * Genere archivos de PDF de impresión desde un PDF de formularios XFA y un formulario de Adobe Acrobat.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* La nueva pestaña &quot;contenido de comercio asociado&quot; del editor de sitios aumenta la eficacia del autor al obtener acceso rápidamente al contenido de producto AEM relevante para el contexto actual

   ![Contenido comercial asociado](/help/assets/CIF/associated-commerce-content.png)

* Interfaz de usuario del selector de productos mejorada para mejorar la experiencia del usuario, la eficacia y la compatibilidad con catálogos de productos complejos

   ![Nuevo selector de productos](/help/assets/CIF/product-picker.png)

* Respetar la propiedad &quot;include_in_menu&quot; en el componente de navegación

### Corrección de errores {#bug-fixes-cif}

* El vaciado de la caché del menú no funciona como se espera

* Errores de JS durante AEM paso de implementación de CS y cuando no se utilizan componentes de cliente

* No se puede crear la configuración de nube del CIF en carpetas que tengan un nodo sling:configs

## [!DNL Experience Manager Screens] como  [!DNL Cloud Service] {#screens}

### Novedades {#what-is-new-screens}

* Las pantallas as a Cloud Service ahora admiten la supervisión básica de la reproducción. El reproductor ahora informará de varias métricas de reproducción con cada ping (el valor predeterminado es de 30 segundos). En función de las métricas, proporciona la capacidad de detectar varios casos extremos (experiencia atascada, pantalla en blanco, problema de programación, etc.). Esta función permite que el equipo supervise de forma remota si un reproductor está reproduciendo contenido correctamente, mejora la reacción a pantallas en blanco o experiencias rotas en el campo y disminuye el riesgo de mostrar una experiencia rota al usuario final.
Consulte [Monitorización de reproducción básica](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) para obtener más información.

* Compatibilidad con miniaturas para vídeos en ahora se admite en Screens as a Cloud Service. Un autor de contenido puede definir una miniatura para los vídeos, de modo que la imagen pueda utilizarse como marcador de posición y probar correctamente la reproducción y el destino del contenido, mientras el equipo adecuado está finalizando el vídeo en sí. También se puede utilizar la imagen en caso de que falle la reproducción del vídeo.
Consulte [Compatibilidad con miniaturas para vídeos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) para obtener más información.

### Corrección de errores {#bug-fixes-screens}

* El reproductor no pudo mostrar contenido de la página integrada y este problema se ha corregido.

* Después de iniciar sesión correctamente, la navegación a la página predeterminada (canales) terminó en una página de error interno del servidor.

* Las entradas de etiquetas asociadas no se eliminaban al quitar listas de reproducción.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Nuevas funciones en [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Redes avanzadas**

>[!INFO]
>
>La función de red avanzada forma parte de la versión 2021.9.0 y estará habilitada para los clientes a mediados de octubre.

[!DNL Adobe Experience Manager] como  [!DNL Cloud Service] ahora ofrece varios tipos de funciones de red avanzadas, entre las que se incluyen:

* Salida de puerto flexible para extraer tráfico de puertos no estándar. Ahora es posible sin ponerse en contacto con el servicio de asistencia al Adobe.
* Dirección IP de salida dedicada para atraer tráfico de AEM as a Cloud Service desde una IP única, ahora compatible con todos los puertos.
* VPN para asegurar el tráfico entre su infraestructura y AEM as a Cloud Service.

Lea la [documentación](/help/security/configuring-advanced-networking.md) para obtener más información, incluido cómo proporcionar redes avanzadas de autoservicio mediante las API de Cloud Manager.

**Optimizaciones de índice**

Para mejorar el rendimiento de las consultas de búsqueda y la indexación, el índice de texto completo lucene-2 ya no se incluye de forma predeterminada en [!DNL Adobe Experience Manager] como [!DNL Cloud Service] en esta versión. Para eliminar este índice de texto completo en entornos AEM de acuerdo con los clientes AEM, Adobe Engineering trabaja de forma individual y proactiva con los clientes para una eliminación suave y sostenible del índice de texto completo de Lucene. Visite la [!DNL Adobe Experience Manager] como [!DNL Cloud Service] [documentación](/help/operations/indexing.md#index-optimizations) para obtener más información y póngase en contacto directamente con nuestro soporte técnico si tiene alguna pregunta.

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.9.0 y 2021.8.0.

## Fecha de la versión {#release-date-cm-sept}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.9.0 es el 9 de septiembre de 2021.
La próxima versión está planificada para el 7 de octubre de 2021.

### Novedades {#what-is-new-cm-sept}

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 30.

* Se han actualizado las tarjetas de programa de la página de aterrizaje de Cloud Manager y la experiencia asociada.

* El registro de pasos de calidad del código ahora incluye información detallada sobre el registro en el proceso de digitalización de OakPal.

* Las opciones del menú de la página Actividad ahora incluirán una opción para **Descargar registro** para las ejecuciones completadas del Generador de códigos. Si selecciona esta opción, se descargará el registro del paso de compilación.

* Al hacer clic directamente en la tarjeta de programa, ahora accederá a la página Información general de Cloud Manager .

### Corrección de errores {#bug-fixes-sept}

* El usuario ahora verá un mensaje más comprensible al intentar agregar una nueva Lista de permitidos IP en un programa que haya alcanzado el número máximo permitido de Listas de permitidos IP que se pueden configurar.

* Se copió una dirección URL incorrecta al seleccionar la opción de menú Copiar URL de la pantalla Repositorios.

## Cloud Acceleration Manager {#cam}

### Fecha de la versión {#release-date-october-cam}

La fecha de versión de Cloud Acceleration Manager es el 4 de octubre de 2021.

### Novedades {#what-is-new-cam}

* Cloud Acceleration Manager ahora proporciona a los usuarios la capacidad de ver los informes de BPA en una vista previa imprimible, lo que permite imprimir o imprimir de forma sencilla a un PDF para facilitar el uso compartido. Consulte los pasos 6 y 7 en [Uso de la tarjeta de análisis de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de versión de la herramienta de transferencia de contenido v1.6.0 es el 4 de octubre de 2021.

### Novedades {#what-is-new-ctt}

* Se ha mejorado la asignación de usuarios con una experiencia de usuario simplificada, que incluye las siguientes funciones que se enumeran a continuación. Para obtener más información, consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).
   * Probar la conexión a la API de administración de usuarios antes de ejecutar la asignación de usuarios
   * Omita correctamente los errores y continúe con la actividad de Asignación de usuarios
   * La asignación de usuarios ya no falla si el token de acceso caduca (después de 24 horas). La asignación de usuarios se puede volver a ejecutar desde donde se detuvo por última vez.

* Para aumentar la solidez de CTT, el contenido se puede ingerir a instancias de Autor o de Publicación a la vez.

* Cuando se incluyen versiones, la ruta `/var/audit` se incluye automáticamente para migrar eventos de auditoría.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa-latest}

La fecha de versión de Best Practices Analyzer v2.1.18 es el 2 de septiembre de 2021.

### Novedades {#what-is-new}

* Capacidad para detectar el recuento total de nodos e informar al respecto.

* Capacidad para detectar y crear informes sobre el tipo y el tamaño del almacén de nodos.

### Corrección de errores {#bug-fixes-bpa}

* La BPA estaba detectando falsamente la presencia del marco de integración comercial.
