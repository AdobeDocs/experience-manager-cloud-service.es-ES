---
title: '[!DNL Experience Manager Assets] integración con [!DNL Adobe Workfront]'
description: Introducción a la integración entre [!DNL Assets] y [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] integración con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | Este artículo |

[!DNL Adobe Workfront] es una aplicación de administración de trabajo que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. La integración entre [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] permite a las organizaciones mejorar la velocidad del contenido y el tiempo de salida al mercado conectando intrínsecamente el trabajo con la administración de recursos digitales. En el contexto de la administración de su trabajo en Workfront, los usuarios tienen acceso a los documentos e imágenes necesarios.

ofertas de Adobe a [integrar [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] de forma nativa (compatible con Assets Essentials y Assets as a Cloud Service) o mediante el conector mejorado de Workfront para Experience Manager](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). Si se trata de una integración nativa, no necesita un conector para integrar las dos soluciones.

>[!NOTE]
>
>El Adobe no admite el uso del conector mejorado de Workfront para Experience Manager y la integración de Experience Manager en paralelo.

Con la integración nativa de Experience Manager y [!DNL Workfront for Experience Manager enhanced connector], puede:

| Nativo [!DNL Adobe Experience Manager Assets] características | [!DNL Workfront for Experience Manager enhanced connector] características |
|---|---|
| <ul><li>Configure rápidamente la integración dentro de Workfront.</li><li>Crea automáticamente carpetas vinculadas entre Workfront y Experience Manager.</li><li>Sincronice fácilmente los metadatos de los recursos vinculados existentes.</li><li>Actualizar automáticamente los metadatos del proyecto cuando se modifiquen en Workfront.</li><li>Conecte sin problemas varios repositorios de Experience Manager Assets a un entorno de Workfront o varios entornos de Workfront a un repositorio de Experience Manager Assets en los ID de organización.</li> | <ul><li>Cree automáticamente carpetas de Experience Manager vinculados en Workfront y organícelas en función de Portfolio, programas y proyectos de Workfront.</li><li>Sincronice los metadatos del proyecto de Workfront con las carpetas de Experience Manager vinculadas.</li><li>Experience Manager de actualizaciones de metadatos con nuevas versiones.</li><li>Establezca los estados de objetos de Workfront en función de condiciones configurables mediante flujos de trabajo de Experience Manager.</li><li>Publique recursos en el entorno de publicación de Experience Manager o en Brand Portal.</li> |

Consulte la [funciones compatibles a continuación para ver una comparación](#feature-parity-matrix) entre la integración nativa o una integración mediante conectores entre las dos soluciones.



Consulte la compatibilidad con la plataforma y [requisitos previos para el conector mejorado](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* A partir de junio de 2022, Adobe lanzó una nueva integración nativa para conectar Workfront con Adobe Experience Manager Assets as a Cloud Service. Esta integración se ha convertido en el método requerido para conectar estas dos soluciones. Cualquier nueva implementación futura del conector mejorado (1.9.8 y posterior) para conectar Workfront con AEM Assets as a Cloud Service está bloqueada. Para obtener más información sobre cómo configurar esta integración, consulte [Configuración de la integración as a Cloud Service de Experience Manager Assets](workfront-connector-configure.md).
>
>* El Adobe requiere la implementación y la configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con el Adobe.
>
>* El Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* El Adobe admite las versiones de conector mejoradas 1.7.4 y posteriores. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, consulte el paso 5(a) de [instrucciones de instalación del conector mejorado](workfront-connector-install.md).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener más información sobre el examen, consulte [Guía del examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Comparar diferentes integraciones entre [!DNL Assets] y [!DNL Workfront] {#feature-parity-matrix}

A continuación se describen las funcionalidades disponibles a través de varios tipos de integraciones entre [!DNL Assets] y [!DNL Workfront].

| Funcionalidad | Descripción | [!DNL Workfront] y [!DNL Assets Essentials] *Sin conector (OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *Requiere conector* | WORKFRONT y [!DNL Experience Manager as a Cloud Service] *Sin conector (OOTB)* |
|----|----|----|-----|-----|
| Métodos de implementación | Apropiado para lo cual [!DNL Assets] oferta. | Assets Essentials | Adobe Managed Services, On-Premise | Servicio de nube de  |
| **General** |
| Envío de archivos digitales desde [!DNL Workfront] hasta [!DNL Assets] | La última versión de un documento WF se puede cargar en AEM Assets, que está vinculado como una nueva versión del documento. | ✓ | ✓ | ✓ |
| AEM Vinculación manual de carpetas de recursos a objetos de Workfront | AEM Las carpetas existentes se pueden vincular como carpetas de Workfront y sus recursos secundarios se vinculan como nuevos documentos de Workfront. | ✓ | ✓ | ✓ |
| Vínculo [!DNL Assets] a objetos de Workfront | AEM Los recursos existentes en la se pueden vincular a un nuevo documento de Workfront o como una nueva versión de un documento existente. | ✓ | ✓ | ✓ |
| AEM Los recursos agregados a las carpetas vinculadas se envían automáticamente a los recursos de la | Si se agrega el documento a una carpeta vinculada, el recurso asociado se cargará automáticamente en AEM Assets como un nuevo recurso. | ✓ | ✓ | ✓ |
| Descargar AEM Assets vinculado desde Workfront | Cuando un recurso está vinculado en Workfront, el usuario puede descargar los bytes del recurso. | ✓ | ✓ | ✓ |
| Busque AEM Assets desde Workfront | El selector de AEM Assets en Workfront permite búsquedas de texto completo para recursos. | ✓ | ✓ | ✓ |
| AEM Buscar carpetas de la desde Workfront | El selector de AEM Assets en Workfront permite búsquedas de texto completo en carpetas. | ✓ | ✓ | ✓ |
| AEM Ver y navegar por la jerarquía de carpetas desde Workfront | El selector de AEM Assets en Workfront permite explorar la jerarquía de AEM Assets AEM limitada por los controles de acceso asociados al usuario y los permisos establecidos en la. | ✓ | ✓ | ✓ |
| AEM Seguimiento de versiones de recursos en cronologías de | Mantener el historial de versiones del documento entre Workfront AEM y la. | ✓ | ✓ | ✓ |
| Desvincular recursos de AEM Assets en Workfront | AEM Un recurso vinculado existente de la lista de recursos se puede desvincular del documento de Workfront asociado. AEM Esto no elimina el recurso original dentro de la. | ✓ | ✓ | ✓ |
| Añadir recurso con nueva versión a AEM Assets desde Workfront | Cuando se agrega una versión recién agregada a un documento en Workfront AEM, un usuario puede enviar la nueva versión a para que la sustituya, a fin de que se pueda usar la versión existente. | ✓ | ✓ | ✓ |
| Recursos vinculados en Workfront AEM al hacer clic en el usuario directo para obtener el acceso a los | AEM Los usuarios son dirigidos a los recursos para obtener una vista previa de un recurso vinculado desde Workfront. | ✓ | ✓ | Próximamente |
| AEM Crear automáticamente carpetas enlazadas de la en Workfront | AEM Cree automáticamente carpetas de recursos enlazados en Workfront mediante los estados de proyecto. AEM Configuración automática de carpetas de recursos basadas en Portfolio, programas y proyectos de Workfront. | No | ✓ | No |
| AEM Navegue directamente a repositorios de desde Workfront | AEM Permite que los usuarios naveguen a los repositorios de datos disponibles configurados en Workfront. | ✓ | No | ✓ |
| AEM Creación de carpetas de carpetas enlazadas en Workfront | AEM Cree manualmente carpetas de recursos enlazadas en Workfront mediante la opción disponible en la pestaña Documentos. | ✓ | No | ✓ |
| Sincronización de comentarios | Sincronizar automáticamente los comentarios de los recursos de [!DNL Workfront] hasta [!DNL Assets] | No | ✓ | No |
| Compatibilidad con varios entornos de Workfront AEM que se conectan a un solo entorno de | Los usuarios de varios entornos de Workfront AEM pueden conectarse a un único entorno de. | ✓ | No | ✓ |
| AEM Compatibilidad con varios entornos de que se conectan a un solo entorno de Workfront | Los usuarios dentro de un solo entorno de Workfront AEM pueden enviar o vincular recursos entre varios entornos de. | ✓ | ✓ | ✓ |
| **Metadatos** |
| Asignar metadatos de recursos de Workfront a AEM Assets | Las propiedades de objeto de Workfront AEM y de formulario personalizado se pueden asignar a propiedades de metadatos de recursos de. Los valores se insertan en la carga o el vínculo inicial. | ✓ | ✓ | ✓ |
| Crear automáticamente un documento de Forms personalizado en Workfront | Adjuntar formularios personalizados a documentos, tareas y problemas de Workfront AEM mediante flujos de trabajo de la. | No | ✓ | No |
| Actualización automática bidireccional de metadatos entre AEM Assets y Workfront | Actualizar automáticamente los metadatos entre AEM Assets y Workfront. El recurso debe insertarse inicialmente desde Workfront AEM a la red de recursos, y los metadatos del recurso de Workfront AEM deben asignarse a los recursos de la red de recursos para que las actualizaciones de metadatos bidireccionales funcionen correctamente. | No | ✓ | No |
| Vista en tiempo real en Workfront AEM para metadatos asignados a los usuarios de la red de área de datos | AEM Vea los metadatos asignados actualizados a los paneles Detalles del documento y Resumen del documento de Workfront para su uso. | ✓ | No | ✓ |
| Inserción en tiempo real de metadatos de Workfront AEM actualizados para su | Actualice automáticamente los metadatos de Workfront AEM asignados a sin volver a cargar un recurso o una nueva versión de un recurso. | ✓ | No | ✓ |
| Asignación de metadatos de Workfront a carpetas de AEM Assets | Sincronice los metadatos del proyecto de Workfront AEM con las carpetas enlazadas de la. | No | ✓ | ✓ |
| AEM Actualizaciones de metadatos con nuevas versiones de | AEM Se puede realizar una configuración en la para determinar si un recurso con una nueva versión en Workfront también se inserta junto con los cambios realizados en sus metadatos. | No | ✓ | No |
| AEM Actualizar automáticamente los metadatos de los cambios de los datos de la a Forms personalizada en Workfront | AEM le permite suscribirse a las actualizaciones de los formularios de documentos en Workfront. Como resultado, cualquier actualización de los metadatos del formulario personalizado del documento de Workfront AEM modifica los valores de los campos de metadatos de la asignados. | No | ✓ | No |
| **Flujos de trabajo (predeterminados)** |
| Crear nueva versión de prueba en recursos vinculados | Al vincular un recurso en Workfront, se puede generar una prueba automáticamente. | No | Personalizado | No |
| Definir estado en objetos de Workfront | Definición de estados de objetos de Workfront AEM basados en condiciones configurables mediante flujos de trabajo de | No | ✓ | Próximamente |
| Publicar recursos en el entorno de publicación de AEM o Brand Portal | Dé a los usuarios de Workfront la opción de publicar automáticamente los recursos vinculados en un entorno de publicación de AEM o Brand Portal. | No | ✓ | Próximamente |
