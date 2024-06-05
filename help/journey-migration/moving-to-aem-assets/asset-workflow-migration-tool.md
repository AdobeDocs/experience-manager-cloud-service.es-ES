---
title: Herramienta de Migración del flujo de trabajo de recursos
description: Herramienta de Migración del flujo de trabajo de recursos
exl-id: a95caf5e-e6b2-463f-bebd-b791104fd25c
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 72%

---

# Herramienta de Migración del flujo de trabajo de recursos {#asset-workflow-migration}

La herramienta de migración del flujo de trabajo de recursos se utiliza para migrar automáticamente los flujos de trabajo de procesamiento de recursos de implementaciones on-premise o AMS de AEM a perfiles de procesamiento y configuraciones OSGi para utilizarlos en AEM Assets as a Cloud Service.

## Introducción {#introduction}

En esta sección se describen los recursos y los detalles de implementación de la herramienta de migración del flujo de trabajo de recursos.

Esta utilidad permite a los desarrolladores de AEM migrar los flujos de trabajo de procesamiento de AEM Assets existentes a AEM as a Cloud Service.

## Flujos de trabajo admitidos {#migration-support-for-workflows}

Los flujos de trabajo tienen distintos niveles de compatibilidad de migración. Consulte esta [lista de flujos de trabajo específicos](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties). Los flujos de trabajo se clasifican en las siguientes categorías sobre la base de la compatibilidad ofrecida. Adobe admite la migración de los flujos de trabajo enumerados en `SUPPORTED`, `REQUIRED` o en las categorías `OPTIONAL`. No son compatibles los pasos del flujo de trabajo mencionados en las otras categorías.

* `SUPPORTED`: Funcionalidad compatible en [!DNL Experience Manager Assets] as a Cloud Service.
* `OPTIONAL`: Funcionalidad opcional en [!DNL Experience Manager Assets] as a Cloud Service.
* `REQUIRED`: Un paso requerido que se añade al flujo de trabajo.
* `UNNECESSARY`: La funcionalidad no es necesaria en [!DNL Experience Manager Assets] as a Cloud Service.
* `NUI_OOTB`: Funcionalidad proporcionada por [Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`: Funcionalidad proporcionada por los [!DNL Dynamic Media] conectores predeterminados.
* `NUI_MIGRATED`: Se ha migrado a un [perfil de procesamiento para Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `UNSUPPORTED`: Actualmente no es compatible en [!DNL Experience Manager Assets] as a Cloud Service.

## Utilizar la herramienta Migración de flujos de trabajo de recursos {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**: el Adobe recomienda utilizar la herramienta de migración del flujo de trabajo de recursos mediante `aio-cli-plugin-aem-cloud-service-migration` ([!DNL Experience Manager] as a [!DNL Cloud Service] complemento de refactorización de código para [!DNL Adobe I/O] CLI). Para aprender a instalar y utilizar el complemento, consulte [Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction).

* **Utilidad independiente**: la herramienta de migración del flujo de trabajo de recursos también se puede ejecutar como una utilidad independiente. Para obtener más información sobre cómo instalar y generar código desde el origen, consulte [Recurso Git: [!DNL Experience Manager Assets] as a [!DNL Cloud Service] - migración del flujo de trabajo](https://github.com/adobe/aem-cloud-migration).
