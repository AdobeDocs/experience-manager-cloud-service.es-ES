---
title: Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI
description: Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI {#new-dynaminc-media-apis-frequently-asked-questions}

+++**¿Todos los recursos del repositorio as a Cloud Service de Experience Manager Assets están disponibles para la búsqueda y la entrega mediante Dynamic Media con funciones OpenAPI?**

No, sólo [aprobado y la última versión de los recursos](/help/assets/approved-assets.md) están disponibles para su búsqueda y envío mediante Dynamic Media con funciones de OpenAPI, lo que garantiza la coherencia de la marca en todos los canales y aplicaciones.

+++

+++**¿Cómo pueden los administradores marcar los recursos nuevos y existentes agregados a una carpeta como aprobados?**

El estado de un recurso en Experience Manager Assets se rige por `jcr:content/metadata/dam:status` propiedad. Los valores de esta propiedad pueden ser:

* Aprobados

* Rechazado

* Cambios solicitados

Experience Manager Assets distingue el estado Aprobado mediante ![Aprobar recursos](assets/thumbs-up-icon.svg) disponible en la tarjeta de recursos, como se muestra en la siguiente imagen:

![Icono para recursos aprobados](/help/assets/assets/approved-assets-thumbs-up.png)

Para aprobar todos los recursos de una carpeta, consulte las instrucciones sobre [cómo aprobar recursos de forma masiva en una carpeta](/help/assets/approved-assets.md#bulk-approve-assets). También hay un vídeo que muestra todo el proceso.

Después de configurar una carpeta para su aprobación masiva, todos los recursos nuevos que se agregan a la carpeta se aprueban automáticamente. Todos los recursos existentes se aprueban después de volver a procesar los recursos. Consulte [Reprocesamiento de recursos digitales](/help/assets/reprocessing.md) para obtener instrucciones sobre cómo volver a procesar los recursos. Si copia o mueve recursos no aprobados de cualquier otra carpeta, debe [volver a procesar los recursos](/help/assets/reprocessing.md).

El recurso está marcado como `Rejected`, si el administrador especifica `Rejected` o `Changes requested` valores. Experience Manager Assets distingue el estado Rechazado mediante ![Rechazar recursos](/help/assets/assets/do-not-localize/reject-assets.svg) disponible en la tarjeta de recursos.

+++

+++**¿Cómo puede obtener el ID de usuario o grupo de Adobe IMS (Adobe Identity Management Services) para configurar las funciones en los recursos en la vista de administrador de Experience Manager, a fin de proteger la experiencia de entrega y búsqueda?**

Los usuarios que requieren acceso al entorno de Experience Manager Author se administran como usuarios de IMS de Adobe en el Admin Console de Adobe. Para obtener información sobre qué son los usuarios de IMS de Adobe, y cómo se accede a ellos y se administran en Admin Console, consulte [Usuarios de IMS de Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en).

+++

+++**¿Puede aprobar varios recursos simultáneamente dentro de una carpeta?**

Sí, puede aprobar varios recursos dentro de una carpeta simultáneamente.

Ejecute los siguientes pasos para aprobar varios recursos simultáneamente en [!DNL Experience Manager Assets]:

1. Seleccione los recursos y haga clic en **[!UICONTROL Propiedades]**.
1. En el **[!UICONTROL Básico]** pestaña, desplazarse hacia abajo hasta **[!UICONTROL Estado de revisión]**.
1. Cambiar el estado de revisión a **[!UICONTROL Aprobado]**.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

+++

+++**¿Cómo puedo asegurar la entrega de recursos y la búsqueda de las API abiertas de Dynamic Media?**

La administración central de recursos en Experience Manager permite a los administradores de DAM o a los administradores de marcas administrar el acceso a los recursos. AEM Pueden restringir el acceso configurando funciones para los recursos aprobados en el lado de la creación, específicamente en la instancia de autor as a Cloud Service.

Los usuarios finales que buscan o utilizan direcciones URL de entrega pueden obtener acceso a los recursos restringidos al pasar correctamente el proceso de autorización.

Para obtener más información, consulte [Restringir el acceso a los recursos en Experience Manager](restrict-assets-delivery.md#authoring).

+++

+++**¿Cómo puede obtener permisos para editar el estado de aprobación de un recurso?**

Como usuario de DAM, es posible que no tenga permisos para [aprobar recursos](approved-assets.md#approve-assets). Para obtener permisos para editar el estado de aprobación de un recurso, los administradores pueden editar el esquema predeterminado o cualquier otro esquema de metadatos aplicado a la carpeta de recursos para proporcionar permisos de edición al **[!UICONTROL Estado de revisión]** field. Para obtener más información, consulte [Obtenga información sobre cómo deshabilitar la edición para el estado de revisión](approved-assets.md#configuration) field.

+++

+++**¿En qué se diferencian las capacidades de Dynamic Media con OpenAPI de la solución Dynamic Media?**

Dynamic Media con funciones OpenAPI y Dynamic Media representan soluciones distintas, cada una de las cuales ofrece sus funciones de envío especializadas. Es imperativo revisar a fondo sus requisitos específicos para determinar la solución más adecuada que se ajuste a sus necesidades.

A continuación se indican algunas de las diferencias clave entre Dynamic Media con capacidades OpenAPI y Dynamic Media:

| Dynamic Media con funciones de OpenAPI | Dynamic Media |
|---|---|
| [Disponible solo con recursos as a Cloud Service](/help/assets/new-dynamic-media-overview.md#prerequisites-new-dynaminc-media-apis) | También disponible con Managed Services On-Premise o de Adobe con pasos de configuración y aprovisionamiento adicionales. |
| [Conjunto limitado de modificadores de imagen admitidos, como anchura, altura, rotación, volteo, calidad y formato](/help/assets/deliver-assets-apis.md) | Conjunto enriquecido de modificadores de imagen disponibles |
| [Entrega de recursos restringida en función de usuarios y funciones](/help/assets/restrict-assets-delivery.md) | Todos los usuarios pueden acceder a los recursos publicados en Dynamic Media |
| Admite recorte inteligente de imagen | Admite recorte inteligente de imagen y vídeo |
| Pila basada en especificaciones de OpenAPI, con las que la mayoría de los desarrolladores están familiarizados. La extensibilidad de AEM Assets se vuelve muy sencilla mediante [Selector de recursos de Micro FrontEnd](/help/assets/asset-selector.md). | API basadas en SOAP, que se convierten en una barrera al desarrollar personalizaciones de integración. |
| Cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de entrega. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para Dynamic Media con funciones de OpenAPI a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos. | TTL de CDN recomendado de 10 horas. Puede anular el valor TTL mediante la acción de invalidación de la caché. |
| Solo los recursos aprobados están disponibles para su entrega a aplicaciones posteriores, lo que permite utilizar recursos aprobados por la marca en experiencias digitales. AEM Los recursos entregados respetan el estado de caducidad del recurso en la instancia de autor repositorio as a Cloud Service. | Las actualizaciones de un recurso publicado en Dynamic Media se publican automáticamente sin ningún flujo de trabajo de aprobación, lo que no garantiza que no haya recursos aprobados por la marca en las experiencias digitales. No hay caducidad de recursos inherente. AEM Un recurso permanece público hasta que se elimina del repositorio as a Cloud Service de la base de datos de. |
| Informes de uso basados en el número de recursos entregados. | Los informes de uso no están disponibles. |

+++

+++**¿Cómo Dynamic Media con las capacidades de OpenAPI aborda las limitaciones de la función Recursos conectados?**

En la tabla siguiente se describen las principales diferencias entre las dos soluciones:

| Dynamic Media con funciones de OpenAPI | Recursos conectados |
|---|---|
| AEM Los recursos de la implementación remota de DAM están disponibles en el as a Cloud Service de la. | AEM Los recursos de la implementación remota de DAM pueden estar disponibles en Managed Services de Adobe o as a Cloud Service de la aplicación de la. |
| Los binarios de recursos no se copian cuando los recursos de una implementación remota de DAM están disponibles en una instancia de AEM Sites. | Los binarios de recursos se copian cuando los recursos de una implementación remota de DAM están disponibles en una instancia de AEM Sites. |
| Compatibilidad con todos los tipos de formato de recursos compatibles con AEM Assets. | No se admiten vídeos. |
| Admite recorte inteligente de imagen. | Compatibilidad con recortes inteligentes de imagen de Dynamic Media y ajustes preestablecidos de imagen. |
| Puede utilizar Dynamic Media en la implementación local de Sites mientras recupera recursos de la implementación remota de DAM. | La implementación de Dynamic Media en sitios locales es de solo lectura. |
| No hay restricciones en el número de instancias de AEM Sites conectadas a una implementación remota de DAM. Puede [restringir el acceso a los recursos de la instancia de Sites configurando funciones](/help/assets/restrict-assets-delivery.md) para recursos aprobados en DAM remoto. | Restricción para conectar no más de 4 instancias de AEM Sites a la implementación remota de DAM. Un número mayor requiere pruebas adicionales. |
| Tanto el Selector de recursos como Dynamic Media con capacidades OpenAPI son ampliables para permitir integraciones personalizadas. | Las API de recursos conectadas no son ampliables para permitir integraciones personalizadas. |
| Cualquier cambio realizado en los recursos aprobados disponibles en la implementación remota de DAM, incluidas las actualizaciones de versión y las modificaciones de metadatos, se reflejan automáticamente en la instancia de Sites en un corto tiempo de vida (TTL) de 10 minutos. | Las actualizaciones de recursos en la implementación remota de DAM se gestionan mediante eventos de ciclo vital automáticamente, pero tardan mucho más tiempo que Dynamic Media con las funciones de OpenAPI. |
| Los metadatos de recursos en DAM remoto también están disponibles en la instancia de AEM Sites. | Los metadatos de recursos en DAM remoto no están disponibles en la instancia de AEM Sites. |

+++



