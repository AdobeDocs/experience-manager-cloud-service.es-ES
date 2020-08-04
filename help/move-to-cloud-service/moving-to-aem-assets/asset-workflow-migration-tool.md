---
title: Herramienta de Migración del flujo de trabajo de recursos
description: 'Herramienta de Migración del flujo de trabajo de recursos '
translation-type: tm+mt
source-git-commit: 3a438de3c460d4dc5a8b8617f0ec0eefc56f1665
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 46%

---


# Herramienta de Migración del flujo de trabajo de recursos {#asset-workflow-migration}

La herramienta de migración del flujo de trabajo de recursos se utiliza para migrar automáticamente los flujos de trabajo de procesamiento de recursos de implementaciones on-premise o AMS de AEM a perfiles de procesamiento y configuraciones OSGi para utilizarlos en AEM Assets as a Cloud Service.

## Introducción {#introduction}

En esta sección se describen los recursos y los detalles de implementación de la herramienta de migración del flujo de trabajo de recursos.

Esta utilidad permite a los desarrolladores de AEM migrar los flujos de trabajo de procesamiento de AEM Assets existentes a AEM as a Cloud Service.

## flujos de trabajo admitidos {#migration-support-for-workflows}

Los flujos de trabajo tienen distintos niveles de soporte para la migración. Consulte esta [lista de flujos de trabajo](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)específicos. Los flujos de trabajo se clasifican en las siguientes categorías sobre la base del apoyo prestado. Adobe admite la migración de los flujos de trabajo enumerados en `SUPPORTED`, `REQUIRED`o `OPTIONAL` categorías. No se admiten los pasos del flujo de trabajo mencionados en las otras categorías.

* `SUPPORTED`:: Funcionalidad admitida en [!DNL Experience Manager Assets] calidad de Cloud Service.
* `OPTIONAL`:: Funcionalidad opcional en [!DNL Experience Manager Assets] calidad de Cloud Service.
* `REQUIRED`:: Un paso requerido que se agrega al flujo de trabajo.
* `UNNECESSARY`:: La funcionalidad no es necesaria [!DNL Experience Manager Assets] como Cloud Service.
* `NUI_OOTB`:: Funcionalidad proporcionada por [Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`:: Funcionalidad proporcionada por los [!DNL Dynamic Media] conectores predeterminados.
* `NUI_MIGRATED`:: Se ha migrado a un perfil [de procesamiento para el servicio](/help/assets/asset-microservices-configure-and-use.md)de cómputo de recursos.
* `UNSUPPORTED`:: Actualmente no se admite en [!DNL Experience Manager Assets] como Cloud Service.

## Instalación de la Herramienta de Migración del flujo de trabajo de recursos {#installing-tool}

Consulte el documento **[Recursos de Git: AEM Assets as a Cloud Service: migración del flujo de trabajo](https://github.com/adobe/aem-cloud-migration)**para obtener más información sobre la instalación y la creación de código desde el origen.
