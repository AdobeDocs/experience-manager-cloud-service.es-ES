---
title: Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI
description: Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: c3bac140c2e0b33cfc206cda7c0591fc75a47a1f
workflow-type: ht
source-wordcount: '1609'
ht-degree: 100%

---

# Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI {#new-dynaminc-media-apis-frequently-asked-questions}

## ¿Están todos los recursos del repositorio de Experience Manager Assets as a Cloud Service disponibles para su búsqueda y entrega mediante Dynamic Media con funciones de OpenAPI? {#assets-available-for-search}

No, solo la [versión aprobada y más reciente de los recursos](/help/assets/approve-assets.md) está disponible para su búsqueda y entrega mediante Dynamic Media con las funciones de OpenAPI, lo que garantiza la uniformidad de la marca en todos los canales y aplicaciones.


## ¿Cómo pueden los administradores marcar los recursos nuevos y existentes que se añadieron a una carpeta como aprobados? {#add-assets-to-folder-as-approved}

El estado de un recurso en Experience Manager Assets se rige por la propiedad `jcr:content/metadata/dam:status`. Los valores de esta propiedad pueden ser:

* Aprobados

* Rechazado

* Cambios solicitados

Experience Manager Assets distingue el estado Aprobado mediante un icono de aprobado disponible en la tarjeta de recursos, como se muestra en las siguientes imágenes para las vistas Administrador y Recursos:

**Vista Administrador**

![Recursos aprobados en la vista Administrador](/help/assets/assets/approved-assets-thumbs-up.png)

**Vista Recursos**

![Recursos aprobados en la vista Recursos](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


Para aprobar todos los recursos de una carpeta, consulte las instrucciones sobre [cómo aprobar recursos de forma masiva en una carpeta](/help/assets/approve-assets.md#bulk-approve-assets). También hay un vídeo que muestra todo el proceso.

Después de configurar una carpeta para su aprobación de forma masiva, todos los recursos nuevos que se añadan a la carpeta se aprobarán automáticamente. Todos los recursos existentes se aprobarán después de volver a procesar los recursos. Consulte [Reprocesamiento de recursos digitales](/help/assets/reprocessing.md) para obtener instrucciones sobre cómo reprocesar recursos. Si copia o mueve recursos no aprobados de cualquier otra carpeta, debe [volver a procesar los recursos](/help/assets/reprocessing.md).

El recurso se marca como `Rejected`, si el administrador especifica los valores `Rejected` o `Changes requested`. Experience Manager Assets distingue el estado Rechazado mediante ![Rechazar recursos](/help/assets/assets/do-not-localize/reject-assets.svg) disponible en la tarjeta de recursos en la vista Administrador.

Del mismo modo, Experience Manager Assets distingue el estado Rechazado en la vista Recursos mediante el siguiente estado Rechazado en la tarjeta de recursos:

![Recursos rechazados en la vista Recursos](/help/assets/assets/rejected-assets-admin-view.png)


## ¿Cómo puede obtener el ID de usuario o grupo de Adobe IMS (servicios de Identity Management de Adobe) para establecer los roles en los recursos en la vista Administrador de Experience Manager, a fin de proteger la experiencia de entrega y búsqueda? {#set-roles-secure-delivery-search}

Los usuarios que necesitan acceder al entorno de creación de Experience Manager se administran como usuarios de Adobe IMS en Admin Console de Adobe. Para obtener información sobre qué son los usuarios de Adobe IMS y cómo se accede a ellos y se administran en Admin Console, consulte [Usuarios de Adobe IMS](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=es).


## ¿Puede aprobar varios recursos simultáneamente dentro de una carpeta? {#approve-multiple-assets-in-folder}

Sí, puede aprobar varios recursos dentro de una carpeta simultáneamente.

Siga estos pasos para aprobar varios recursos simultáneamente en [!DNL Experience Manager Assets Admin view]:

1. Seleccione los recursos y haga clic en **[!UICONTROL Propiedades]**.
1. En la ficha **[!UICONTROL Básico]**, desplácese hacia abajo hasta **[!UICONTROL Estado de revisión]**.
1. Cambiar el estado de revisión a **[!UICONTROL Aprobado]**.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

Del mismo modo, para aprobar varios recursos simultáneamente dentro de una carpeta en la vista Recursos:

1. Seleccione los recursos y haga clic en **[!UICONTROL Edición masiva de metadatos]**.

1. Seleccione **[!UICONTROL Aprobado]** en el campo **[!UICONTROL Estado]** disponible en la sección [!UICONTROL Propiedades] del panel derecho.

1. Haga clic en **[!UICONTROL Guardar]**.


## ¿Cómo puedo asegurar la entrega de recursos y la búsqueda para Dynamic Media con OpenAPI? {#secure-asset-delivery}

La administración central de recursos en Experience Manager permite a los administradores de DAM o a los administradores de marca administrar el acceso a los recursos. Pueden restringir el acceso configurando funciones o estableciendo el tiempo de activación y desactivación de los recursos aprobados en el lado de la creación, específicamente en la instancia de autor de AEM as a Cloud Service.

Los usuarios finales que buscan o utilizan URL de entrega pueden obtener acceso a los recursos restringidos pasando correctamente el proceso de autorización.

Para obtener más información, consulte [Restringir el acceso a los recursos en Experience Manager](restrict-assets-delivery.md#authoring).


## ¿Cómo puede obtener permisos para editar el estado de aprobación de un recurso? {#permissions-edit-approval-status}

Como usuario de DAM, es posible que no tenga permisos para [aprobar recursos](approve-assets.md#approve-assets). Para obtener permisos para editar el estado de aprobación de un recurso, los administradores pueden editar el esquema de metadatos predeterminado o cualquier otro esquema de metadatos aplicado a la carpeta de recursos para proporcionar permisos de edición en el campo **[!UICONTROL Estado de revisión]**. Para obtener más información, consulte [cómo deshabilitar la edición para el campo Estado de revisión](approve-assets.md#configuration).


## ¿Cuál es el tamaño de archivo admitido para los vídeos? {#supported-file-formats-videos}

Las funcionalidades de Dynamic Media con OpenAPI ahora son compatibles con vídeos de formato largo. Los vídeos de formato largo pueden admitir hasta 50 GB y 2 horas.


## ¿En qué se diferencia Dynamic Media con funciones de OpenAPI de la solución Dynamic Media? {#dynamic-media-and-dynamic-media-with-openapi-differences}

Dynamic Media con funciones de OpenAPI y Dynamic Media son soluciones distintas y cada una de ellas ofrece funciones de entrega especializadas. Es imprescindible revisar a fondo sus requisitos específicos para determinar qué solución se ajusta mejor a sus necesidades.

La recomendación general de Adobe es aprovechar la pila de Dynamic Media con OpenAPI para casos de uso de integración (aplicaciones de origen o de terceros). Si ya existe una integración con la pila de Dynamic Media, se recomienda no cambiarla, ya que las URL de pila de OpenAPI son diferentes en estructura. Aproveche la pila de OpenAPI solo para casos de uso de integración de red nuevos. Si su caso de uso requiere modificadores avanzados no disponibles con la pila de OpenAPI, evite la pila OpenAPI hasta que Adobe cubra esta carencia. Incluso para la entrega nativa básica de AEM Assets Cloud Services, la pila de OpenAPI se puede evaluar siempre y cuando su caso de uso se cubra con los modificadores disponibles con la pila de OpenAPI. En conclusión, la pila de Dynamic Media y la de de Dynamic Media con OpenAPI pueden coexistir, según la naturaleza del caso de uso.

A continuación, se indican algunas de las diferencias clave entre Dynamic Media con funciones de OpenAPI y Dynamic Media:

| Funcionalidades de Dynamic Media con OpenAPI | Dynamic Media |
|---|---|
| [Disponible solo con Assets as a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | También disponible con On-Premise o Adobe Managed Services con pasos de configuración y aprovisionamiento adicionales. |
| [Conjunto enriquecido de modificadores de imagen compatibles, como anchura, altura, girar, voltear, calidad y formato](/help/assets/deliver-assets-apis.md) | Conjunto enriquecido de modificadores de imagen disponibles |
| [Entrega restringida de recursos en función de usuarios, funciones, fecha y hora](/help/assets/restrict-assets-delivery.md) | Todos los usuarios pueden acceder a los recursos publicados en Dynamic Media |
| La mayoría de los desarrolladores están familiarizados con las especificaciones de OpenAPI. La extensibilidad de AEM Assets es muy sencilla con [Selector de recursos de Micro-Frontend](/help/assets/overview-asset-selector.md). | Las API basadas en SOAP, que suponen una barrera a la hora de desarrollar personalizaciones de integración. |
| Cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de entrega. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para Dynamic Media con funciones de OpenAPI a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos. | TTL de CDN recomendado de 10 horas. Puede anular el valor de TTL mediante la acción de invalidación de la caché. |
| Solo los recursos aprobados están disponibles para su envío a aplicaciones descendentes, lo que permite utilizar recursos de marca aprobados en experiencias digitales. | Las actualizaciones de un recurso publicado en Dynamic Media se publican automáticamente sin ningún flujo de trabajo de aprobación, lo que no garantiza que haya recursos de marca aprobados en las experiencias digitales. |
| Informes de uso basados en el número de recursos entregados. Esta función estará disponible en breve. | Los informes de uso no están disponibles. Esta función estará disponible en breve. |
| Los recursos marcados como Caducados en el repositorio de Assets as a Cloud Service ya no están disponibles para las aplicaciones descendentes. | No hay caducidad de recursos inherente. Un recurso permanece público hasta que se elimina del repositorio de AEM as a Cloud Service. |
| No admite funciones de recorte inteligente de vídeo. | Admite funciones de recorte inteligente de vídeo. |
| Codificaciones de vídeo dinámicas, que garantizan que se proporcionan las mejores codificaciones en función del vídeo de entrada. No se requiere ninguna configuración para el envío de vídeo nativo. | Codificaciones de norma 3 independientemente del vídeo de entrada (puede afectar al rendimiento del envío de vídeo). Debe configurar manualmente diferentes codificaciones para diferentes tasas de bits de vídeo. |
| Habilita URL seguras y ocultas mediante UID de recursos sin poner en riesgo el SEO. | La ofuscación de URL solo está disponible para parámetros de consulta de URL. Los ID de los recursos (nombres de los recursos) en las URL son reconocibles. |


## ¿Cómo aborda Dynamic Media con funciones de OpenAPI las limitaciones de la función de Recursos de red? {#dynamic-media-openapi-addresses-connected-assets-limitations}

En la tabla siguiente se describen las principales diferencias entre las dos soluciones:

| Funcionalidades de Dynamic Media con OpenAPI | Recursos de red |
|---|---|
| Los recursos de la implementación remota de DAM están disponibles en AEM as a Cloud Service. | Los recursos de la implementación remota de DAM pueden estar disponibles en AEM as a Cloud Service o en Adobe Managed Services. |
| Los binarios de recursos no se copian cuando los recursos de una implementación remota de DAM están disponibles en una instancia de AEM Sites. | Los binarios de recursos se copian cuando los recursos de una implementación remota de DAM están disponibles en una instancia de AEM Sites. |
| Compatibilidad con todos los tipos de formato de recursos admitidos por AEM Assets. | No admite vídeos. |
| Puede utilizar Dynamic Media en la implementación local de Sites mientras recupera recursos de la implementación remota de DAM. | Dynamic Media en la implementación local de Sites es de solo lectura. |
| No hay restricciones en el número de instancias de AEM Sites conectadas a una implementación remota de DAM. Puede [restringir el acceso a los recursos de la instancia de Sites configurando los roles](/help/assets/restrict-assets-delivery.md) para los recursos aprobados en la implementación remota de DAM. | Restricción para conectar no más de 4 instancias de AEM Sites a la implementación remota de DAM. Un número mayor requiere pruebas adicionales. |
| Tanto el Selector de recursos como Dynamic Media con funciones de OpenAPI se pueden ampliar para permitir integraciones personalizadas. | Las API de Assets conectadas no se pueden ampliar para permitir integraciones personalizadas. |
| Cualquier cambio realizado en los recursos aprobados disponibles en la implementación remota de DAM, incluidas las actualizaciones de versión y las modificaciones de metadatos, se reflejan automáticamente en la instancia de Sites en un corto tiempo de vida (TTL) de 10 minutos. | Las actualizaciones de recursos en la implementación remota de DAM se gestionan mediante eventos de ciclo vital automáticamente, pero tardan mucho más tiempo que Dynamic Media con funciones de OpenAPI. |
| Los metadatos de recursos en la implementación remota de DAM también están disponibles en la instancia de AEM Sites. | Los metadatos de recursos en la implementación remota de DAM no están disponibles en la instancia de AEM Sites. |

## Algunos modificadores están marcados como Disponibilidad limitada. ¿Cómo puedo empezar a usarlos? {#use-limited-availability-modifiers}

Para habilitar el uso de producción de [modificadores en Disponibilidad limitada](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) en su cuenta:

1. [Cree un caso de soporte de Adobe con Admin Console](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

1. Mencione los siguientes detalles en el caso de asistencia de Adobe:

   * Organización de IMS

   * Lista de modificadores que se van a habilitar


## ¿Cómo puedo probar los modificadores experimentales? {#modifiers-not-generally-available}

Puede probar cualquier modificador, lo cual no suele estar disponible a través de API experimentales. Por ejemplo, &lt;/adobe/experimental/advancemodifiers-expires-YYYYMMDD/assets>
Haga clic aquí para obtener más información sobre cómo usar las [API experimentales](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/#experimental-apis) y la [lista completa de modificadores](https://developer.adobe.com/experience-cloud/experience-manager-apis/).
