---
title: Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI
description: Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 1%

---

# Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI {#new-dynaminc-media-apis-frequently-asked-questions}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>La guía de funciones de Dynamic Media con OpenAPI ya está disponible en formato de PDF. Descargue toda la guía y utilice Adobe Acrobat AI Assistant para responder a sus consultas.
>
>[!BADGE PDF de la Guía de Dynamic Media con funciones OpenAPI]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

+++**¿Todos los recursos del repositorio as a Cloud Service de Experience Manager Assets están disponibles para su búsqueda y envío mediante Dynamic Media con capacidades OpenAPI?**

No, solo la [versión aprobada y más reciente de los recursos](/help/assets/approve-assets.md) están disponibles para su búsqueda y envío mediante Dynamic Media con funciones OpenAPI, lo que garantiza la coherencia de la marca en todos los canales y aplicaciones.

+++

+++**¿Cómo pueden los administradores marcar los recursos nuevos y existentes agregados a una carpeta como aprobados?**

El estado de un recurso en Experience Manager Assets se rige por la propiedad `jcr:content/metadata/dam:status`. Los valores de esta propiedad pueden ser:

* Aprobados

* Rechazado

* Cambios solicitados

Experience Manager Assets distingue el estado Aprobado mediante un icono de Aprobado disponible en la tarjeta de recursos, como se muestra en las siguientes imágenes para las vistas Administrador y Recursos:

**Vista de administrador**

![Recursos aprobados en la vista del administrador](/help/assets/assets/approved-assets-thumbs-up.png)

**Vista de Assets**

![Recursos aprobados en la vista de Assets](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


Para aprobar todos los recursos de una carpeta, consulte las instrucciones sobre [cómo aprobar recursos de forma masiva en una carpeta](/help/assets/approve-assets.md#bulk-approve-assets). También hay un vídeo que muestra todo el proceso.

Después de configurar una carpeta para su aprobación masiva, todos los recursos nuevos que se agregan a la carpeta se aprueban automáticamente. Todos los recursos existentes se aprueban después de volver a procesar los recursos. Consulte [Reprocesamiento de recursos digitales](/help/assets/reprocessing.md) para obtener instrucciones sobre cómo reprocesar recursos. Si copia o mueve recursos no aprobados de cualquier otra carpeta, debe [volver a procesar los recursos](/help/assets/reprocessing.md).

El recurso está marcado como `Rejected`, si el administrador especifica `Rejected` o `Changes requested` valores. Experience Manager Assets distingue el estado Rechazado mediante ![Rechazar Assets](/help/assets/assets/do-not-localize/reject-assets.svg) disponible en la tarjeta de recursos en la vista de administración.

Del mismo modo, Experience Manager Assets distingue el estado Rechazado en la vista de Assets mediante el siguiente estado Rechazado en la tarjeta de recursos:

![Recursos rechazados en la vista de Assets](/help/assets/assets/rejected-assets-admin-view.png)


+++

+++**¿Cómo puede obtener el ID de usuario o grupo de Adobe IMS (Servicios de Adobe de Identity Management) para establecer los roles en los recursos en la vista Administrador de Experience Manager, a fin de proteger la experiencia de envío y búsqueda?**

Los usuarios que requieren acceso al entorno de Experience Manager Author se administran como usuarios de IMS de Adobe en el Admin Console de Adobe. Para obtener información sobre qué son los usuarios de IMS de Adobe, y cómo se accede a ellos y se administran en Admin Console, consulte [Usuarios de IMS de Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en).

+++

+++**¿Puede aprobar varios recursos simultáneamente dentro de una carpeta?**

Sí, puede aprobar varios recursos dentro de una carpeta simultáneamente.

Ejecute los siguientes pasos para aprobar varios recursos simultáneamente en [!DNL Experience Manager Assets Admin view]:

1. Seleccione los recursos y haga clic en **[!UICONTROL Propiedades]**.
1. En la ficha **[!UICONTROL Básico]**, desplácese hacia abajo hasta **[!UICONTROL Estado de revisión]**.
1. Cambiar el estado de revisión a **[!UICONTROL Aprobado]**.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

Del mismo modo, para aprobar varios recursos simultáneamente dentro de una carpeta en la vista de Assets:

1. Seleccione los recursos y haga clic en **[!UICONTROL Edición masiva de metadatos]**.

1. Seleccione **[!UICONTROL Aprobado]** en el campo **[!UICONTROL Estado]** disponible en la sección [!UICONTROL Propiedades] del panel derecho.

1. Haga clic en **[!UICONTROL Guardar]**.


+++

+++**¿Cómo puedo asegurar la entrega de recursos y buscar las OpenAPI de Dynamic Media?**

La administración central de recursos en Experience Manager permite a los administradores de DAM o a los administradores de marcas administrar el acceso a los recursos. Pueden restringir el acceso configurando funciones o estableciendo el tiempo de activación y desactivación de los recursos aprobados en el lado de la creación, específicamente en la instancia de autor de AEM as a Cloud Service.

Los usuarios finales que buscan o utilizan direcciones URL de entrega pueden obtener acceso a los recursos restringidos al pasar correctamente el proceso de autorización.

Para obtener más información, consulte [Restringir el acceso a los recursos en Experience Manager](restrict-assets-delivery.md#authoring).

+++

+++**¿Cómo puede obtener permisos para editar el estado de aprobación de un recurso?**

Como usuario de DAM, es posible que no tenga permisos para [aprobar recursos](approve-assets.md#approve-assets). Para obtener permisos para editar el estado de aprobación de un recurso, los administradores pueden editar el esquema de metadatos predeterminado o cualquier otro esquema de metadatos aplicado a la carpeta de recursos para proporcionar permisos de edición en el campo **[!UICONTROL Estado de revisión]**. Para obtener más información, consulte [cómo deshabilitar la edición para el campo Estado de revisión](approve-assets.md#configuration).

+++

+++**¿En qué se diferencia Dynamic Media con las funcionalidades de OpenAPI de la solución Dynamic Media?**

Dynamic Media con funciones OpenAPI y Dynamic Media representan soluciones distintas, cada una de las cuales ofrece sus funciones de envío especializadas. Es imperativo revisar a fondo sus requisitos específicos para determinar la solución más adecuada que se ajuste a sus necesidades.

La guía general del Adobe es aprovechar Dynamic Media con la pila OpenAPI para cualquier caso de uso de integración (aplicaciones de origen o de terceros). Si ya existe una integración con la pila de Dynamic Media, se recomienda no cambiarla, ya que las URL de pila de OpenAPI son diferentes en estructura. Aproveche la pila OpenAPI solo para cualquier caso de uso de integración nuevo de red. Si su caso de uso requiere modificadores avanzados que no están disponibles con la pila de OpenAPI, evite la pila de OpenAPI hasta que el Adobe cierre la brecha. Incluso para la entrega nativa básica de los Cloud Service de AEM Assets, la pila de OpenAPI se puede evaluar siempre y cuando su caso de uso se cubra con los modificadores disponibles con la pila de OpenAPI. En conclusión, Dynamic Media y Dynamic Media con la pila de OpenAPI pueden coexistir, según la naturaleza del caso de uso.

A continuación se indican algunas de las diferencias clave entre Dynamic Media con capacidades OpenAPI y Dynamic Media:

| Dynamic Media con funciones de OpenAPI | Dynamic Media |
|---|---|
| [Disponible solo con Assets as a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | También disponible con Managed Services On-Premise o de Adobe con pasos de configuración y aprovisionamiento adicionales. |
| [Conjunto limitado de modificadores de imagen admitidos, como ancho, alto, giro, voltear, calidad y formato](/help/assets/deliver-assets-apis.md) | Conjunto enriquecido de modificadores de imagen disponibles |
| [Entrega de recursos restringida en función de los usuarios, las funciones, la fecha y la hora](/help/assets/restrict-assets-delivery.md) | Todos los usuarios pueden acceder a los Assets publicados en Dynamic Media |
| La mayoría de los desarrolladores están familiarizados con las especificaciones de OpenAPI. La extensibilidad de los AEM Assets se vuelve muy sencilla con [Micro-Frontend Asset Selector](/help/assets/overview-asset-selector.md). | SOAP Las API basadas en, que se convierten en una barrera al desarrollar personalizaciones de integración. |
| Cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de entrega. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para Dynamic Media con funciones de OpenAPI a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos. | TTL de CDN recomendado de 10 horas. Puede anular el valor TTL mediante la acción de invalidación de la caché. |
| Solo los recursos aprobados están disponibles para su entrega a aplicaciones posteriores, lo que permite utilizar recursos aprobados por la marca en experiencias digitales. | Las actualizaciones de un recurso publicado en Dynamic Media se publican automáticamente sin ningún flujo de trabajo de aprobación, lo que no garantiza que no haya recursos aprobados por la marca en las experiencias digitales. |
| Informes de uso basados en el número de recursos entregados. Esta función estará disponible próximamente. | Los informes de uso no están disponibles. Esta función estará disponible próximamente. |
| Las Assets marcadas como Caducadas en el repositorio as a Cloud Service de Assets ya no están disponibles para las aplicaciones posteriores. | No hay caducidad de recursos inherente. Un recurso permanece público hasta que se elimina del repositorio de AEM as a Cloud Service. |
| No admite ajustes preestablecidos de imagen ni funciones de recorte inteligente de vídeo. | Admite ajustes preestablecidos de imagen y funciones de recorte inteligente de vídeo. |
| Codifica vídeo dinámico, que garantiza que se proporcionen las mejores codificaciones en función del vídeo de entrada. No se requiere ninguna configuración para la entrega de vídeo nativo. | Estándar 3 codifica independientemente del vídeo de entrada (puede afectar al rendimiento de entrega de vídeo). Debe configurar manualmente diferentes codificaciones para diferentes tasas de bits de vídeo. |
| Es difícil adivinar las URL basadas en UID de recursos (permite la ofuscación de URL), pero se optimizó la SEO. | La ofuscación de URL solo está disponible para parámetros de consulta de URL. Los ID de Assets (nombres de recursos) en las direcciones URL son reconocibles. |

+++

+++**¿Cómo Dynamic Media con las capacidades de OpenAPI resuelve las limitaciones de la función de Assets conectado?**

En la tabla siguiente se describen las principales diferencias entre las dos soluciones:

| Dynamic Media con funciones de OpenAPI | Recursos conectados |
|---|---|
| Assets en la implementación remota de DAM está disponible en AEM as a Cloud Service. | Assets en la implementación remota de DAM puede estar disponible en AEM as a Cloud Service o Adobe Managed Services. |
| Los binarios de recursos no se copian cuando los recursos de una implementación remota de DAM están disponibles en una instancia de AEM Sites. | Los binarios de recursos se copian cuando los recursos de una implementación remota de DAM están disponibles en una instancia de AEM Sites. |
| Compatibilidad con todos los tipos de formato de recursos admitidos por los AEM Assets. | No se admiten vídeos. |
| Puede utilizar Dynamic Media en la implementación local de Sites mientras recupera recursos de la implementación remota de DAM. | La implementación de Dynamic Media en sitios locales es de solo lectura. |
| No hay restricciones en el número de instancias de AEM Sites conectadas a una implementación remota de DAM. Puede [restringir el acceso a los recursos de la instancia de Sites configurando los roles](/help/assets/restrict-assets-delivery.md) para los recursos aprobados en el DAM remoto. | Restricción para conectar no más de 4 instancias de AEM Sites a la implementación remota de DAM. Un número mayor requiere pruebas adicionales. |
| Tanto el Selector de recursos como Dynamic Media con capacidades OpenAPI son ampliables para permitir integraciones personalizadas. | Las API de Assets conectadas no son ampliables para permitir integraciones personalizadas. |
| Cualquier cambio realizado en los recursos aprobados disponibles en la implementación remota de DAM, incluidas las actualizaciones de versión y las modificaciones de metadatos, se reflejan automáticamente en la instancia de Sites en un corto tiempo de vida (TTL) de 10 minutos. | Las actualizaciones de recursos en la implementación remota de DAM se gestionan mediante eventos de ciclo vital automáticamente, pero tardan mucho más tiempo que Dynamic Media con las funciones de OpenAPI. |
| Los metadatos de recursos en DAM remoto también están disponibles en la instancia de AEM Sites. | Los metadatos de recursos en DAM remoto no están disponibles en la instancia de AEM Sites. |

+++
