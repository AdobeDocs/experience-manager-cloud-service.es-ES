---
title: '[!DNL Experience Manager Assets] integración con [!DNL Adobe Workfront]'
description: Introducción a la integración entre [!DNL Assets] y [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 20dbcff249e3fc1beab24600cd54ce1bf4085d38
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] como [!DNL Cloud Service] [!DNL Assets] integración con [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] es una aplicación de administración de trabajo que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. La integración entre [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] permite a las organizaciones mejorar la velocidad de contenido y el tiempo de comercialización conectando intrínsecamente el trabajo con la administración de recursos digitales. En el contexto de la administración de su trabajo en Workfront, los usuarios tienen acceso a los documentos e imágenes necesarios.

ofertas de Adobe a [integrar [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] de forma nativa (compatible con Assets Essentials y Assets as a Cloud Service), con el conector Workfront for AEM o con el conector mejorado de Workfront for Experience Manager](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). En el caso de una integración nativa, no necesita un conector para integrar las dos soluciones.

>[!NOTE]
>
>El Adobe no admite el uso del conector Workfront for AEM o Workfront para el conector mejorado del Experience Manager y la integración del Experience Manager en paralelo.

Con la integración nativa del Experience Manager y [!DNL Workfront for Experience Manager enhanced connector], puede:

| Nativo [!DNL Adobe Experience Manager Assets] características | [!DNL Workfront for Experience Manager enhanced connector] características |
|---|---|
| <ul><li>Configure rápidamente la integración dentro de Workfront.</li><li>Crear automáticamente carpetas vinculadas entre Workfront y Experience Manager.</li><li>Sincronice fácilmente metadatos para recursos vinculados existentes.</li><li>Actualice automáticamente los metadatos del proyecto cuando se cambien en Workfront.</li><li>Conecte sin problemas varios repositorios de Experience Manager Assets a un entorno de Workfront o varios entornos de Workfront a un repositorio de Experience Manager Assets en todos los ID de organización.</li> | <ul><li>Cree automáticamente carpetas de Experience Manager vinculadas en Workfront y organice las carpetas en función de Portfolio, programas y proyectos de Workfront.</li><li>Sincronice los metadatos del proyecto de Workfront con las carpetas de Experience Manager vinculadas.</li><li>Actualizaciones de metadatos de Experience Manager con nuevas versiones.</li><li>Defina los estados de los objetos de Workfront en función de condiciones configurables mediante flujos de trabajo de Experience Manager.</li><li>Publique recursos en el entorno de publicación de Experience Manager o en Brand Portal.</li> |

Consulte la [funciones compatibles a continuación para una comparación](#feature-parity-matrix) entre integración nativa o integración mediante conectores entre las dos soluciones.



Consulte la compatibilidad con la plataforma y [requisitos previos para el conector mejorado](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* El Adobe requiere la implementación y la configuración del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>* Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto ocurre, es posible que se requiera a los clientes que pasen del uso de este conector.
>
>* Adobe admite las versiones 1.7.4 y posteriores del conector mejorado. No se admiten versiones anteriores y personalizadas. Para comprobar la versión mejorada del conector, consulte el paso 5(a) de [instrucciones de instalación del conector mejorado](workfront-connector-install.md).
>
>* Consulte [Examen de certificación de socios para conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información acerca del examen, consulte [Guía de examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Comparar distintas integraciones entre [!DNL Assets] y [!DNL Workfront] {#feature-parity-matrix}

A continuación se detallan las funcionalidades disponibles a través de varios tipos de integraciones entre [!DNL Assets] y [!DNL Workfront].

| Función | Descripción | [!DNL Workfront] y [!DNL Assets Essentials] *Sin conector (OOTB)* | [!DNL Workfront] para [!DNL AEM] connector *Requiere conector* | [!DNL Workfront for Experience Manager enhanced connector] *Requiere conector* | Workfront y [!DNL Experience Manager as a Cloud Service] *Sin conector (OOTB)* |
|----|----|----|------|-----|-----|
| Métodos de implementación | Apropiado para el cual [!DNL Assets] oferta. | Assets Essentials | Cloud Service, Adobe Managed Services, On-Premise | Cloud Service, Adobe Managed Services, On-Premise | Servicio de nube de  |
| **General** |
| Enviar archivos digitales desde [!DNL Workfront] a [!DNL Assets] | La última versión de un documento WF se puede cargar en AEM Assets, que se vinculará como una nueva versión del documento. | ✓ | ✓ | ✓ | ✓ |
| Vincular manualmente AEM carpetas a objetos de Workfront | Las carpetas de AEM existentes se pueden vincular como una carpeta de Workfront y sus recursos secundarios se vinculan como nuevos documentos de Workfront. | ✓ | ✓ | ✓ | ✓ |
| Vínculo [!DNL Assets] a objetos de Workfront | Los recursos existentes en AEM pueden vincularse a un nuevo documento de Workfront o como una nueva versión de un documento existente. | ✓ | ✓ | ✓ | ✓ |
| Los recursos añadidos a carpetas vinculadas se envían automáticamente a AEM | Si el documento se agrega a una carpeta vinculada, el recurso asociado se carga automáticamente en AEM Assets como nuevo recurso. | ✓ | ✓ | ✓ | ✓ |
| Descargar AEM Assets vinculado desde Workfront | Cuando un recurso está vinculado en Workfront, el usuario puede descargar los bytes del recurso. | ✓ | ✓ | ✓ | ✓ |
| Buscar AEM Assets desde Workfront | El selector de AEM Assets en Workfront permite realizar búsquedas de texto completo de los recursos. | ✓ | ✓ | ✓ | ✓ |
| Buscar carpetas AEM desde Workfront | El selector de AEM Assets en Workfront permite realizar búsquedas de texto completo de carpetas. | ✓ | No | ✓ | ✓ |
| Ver y navegar AEM jerarquía de carpetas desde Workfront | El selector de AEM Assets en Workfront permite examinar la jerarquía de AEM Assets limitada por los controles de acceso asociados al usuario y los permisos establecidos en AEM. | ✓ | ✓ | ✓ | ✓ |
| Seguimiento de versiones de recursos en AEM cronologías | Mantener el historial de versiones del documento entre Workfront y AEM. | ✓ | ✓ | ✓ | ✓ |
| Desvincular recursos de AEM Assets en Workfront | Un recurso vinculado existente de AEM se puede desvincular del documento de Workfront asociado. Esto no elimina el recurso original dentro de AEM. | ✓ | ✓ | ✓ | ✓ |
| Añadir recursos de versiones recientes a AEM Assets desde Workfront | Cuando se añade una versión recién añadida a un documento en Workfront, un usuario puede enviar la nueva versión a AEM para reemplazar la versión existente. | ✓ | ✓ | ✓ | ✓ |
| Recursos vinculados en Workfront cuando se hace clic en Direccionar usuario a AEM | Los usuarios son dirigidos a AEM para obtener una vista previa de un recurso vinculado desde Workfront. | ✓ | ✓ | ✓ | Próximos |
| Crear automáticamente carpetas de AEM vinculadas en Workfront | Crear automáticamente carpetas de AEM vinculadas en Workfront mediante los estados del proyecto. Configure automáticamente AEM carpetas en función de Portfolio, programas y proyectos de Workfront. | No | No | ✓ | No |
| Navegar directamente a AEM repositorios desde Workfront | Permita que los usuarios naveguen hasta repositorios de AEM disponibles configurados dentro de Workfront. | ✓ | No | No | ✓ |
| Crear carpetas de AEM vinculadas en Workfront | Cree manualmente carpetas de AEM vinculadas en Workfront mediante la opción disponible en la pestaña Documents . | ✓ | No | No | ✓ |
| Sincronización de comentarios | Sincronizar automáticamente los comentarios de los recursos [!DNL Workfront] a [!DNL Assets] | No | ✓ | ✓ | No |
| Admite varios entornos Workfront que se conectan a un único entorno AEM | Los usuarios de varios entornos Workfront pueden conectarse a un único entorno AEM. | ✓ | No | No | ✓ |
| Admite varios entornos AEM que se conectan a un único entorno de Workfront | Los usuarios de un solo entorno de Workfront pueden enviar o vincular recursos entre varios entornos de AEM. | ✓ | ✓ | ✓ | ✓ |
| **Metadatos** |
| Asignación de metadatos de recursos de Workfront a AEM Assets | El objeto Workfront y las propiedades de formulario personalizadas pueden asignarse a propiedades de metadatos de AEM recurso. Los valores se insertan en el enlace o la carga inicial. | ✓ | ✓ | ✓ | ✓ |
| Crear automáticamente Forms personalizado de documento en Workfront | Adjunte formularios personalizados a documentos, tareas y problemas de Workfront mediante flujos de trabajo AEM. | No | Agregue manualmente el formulario personalizado y la sincronización automatizada funcione | ✓ | No |
| Actualización automática bidireccional de metadatos entre AEM Assets y Workfront | Actualice automáticamente los metadatos entre AEM Assets y Workfront. El recurso debe transferirse inicialmente de Workfront a AEM y los metadatos de recursos de Workfront deben asignarse a AEM recursos para que las actualizaciones de metadatos bidireccionales funcionen correctamente. | No | ✓ | ✓ | No |
| Vista en tiempo real en Workfront para metadatos asignados a AEM | Vea los metadatos asignados actualizados para AEM en los paneles Detalles del documento y Resumen de documento de Workfront. | ✓ | No | No | ✓ |
| Inserción en tiempo real de metadatos de Workfront actualizados a AEM | Actualice automáticamente los metadatos de Workfront asignados a AEM sin tener que volver a asignar reputación a un recurso o a una nueva versión de un recurso. | ✓ | No | No | ✓ |
| Asignación de metadatos de Workfront a carpetas de AEM Assets | Sincronice los metadatos del proyecto de Workfront con las carpetas de AEM vinculadas. | No | No | ✓ | ✓ |
| Actualizaciones de metadatos de AEM con nuevas versiones | Se puede realizar una configuración en AEM para determinar si un recurso con una nueva versión en Workfront también inserta cambios en sus metadatos. | No | No | ✓ | No |
| Actualizar automáticamente AEM metadatos sobre los cambios en el Forms personalizado en Workfront | AEM permite suscribirse a las actualizaciones de los formularios del documento en Workfront. Como resultado, cualquier actualización de los metadatos de formulario personalizados del documento de Workfront modifica los valores de los campos de metadatos de AEM asignados. | No | ✓ | ✓ | No |
| **Flujos de trabajo (predeterminados)** |
| Crear una nueva versión de prueba en recursos vinculados | Al vincular un recurso en Workfront, se puede generar una prueba automáticamente. | No | ✓ | Personalizado | No |
| Definir estado en objetos de Workfront | Definir estados de objetos de Workfront basados en condiciones configurables mediante flujos de trabajo AEM | No | No | ✓ | Próximos |
| Publicar recursos en AEM Publish Environment o Brand Portal | Proporcione a los usuarios de Workfront la opción de publicar automáticamente los recursos vinculados en un entorno de publicación de AEM o Brand Portal. | No | No | ✓ | Próximos |
