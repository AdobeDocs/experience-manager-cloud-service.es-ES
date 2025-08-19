---
title: Cambios importantes del complemento de Commerce integration framework (CIF)
description: Cambios importantes de Commerce integration framework (CIF) en comparación con las versiones de CIF anteriores.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Cambios importantes en el complemento de Commerce integration framework (CIF) {#notable-changes}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades para administrar sus proyectos de AEM. Para obtener más información acerca de estas funcionalidades, siga el vínculo de [cambios en Experience Manager as a Cloud Service.](/help/release-notes/aem-cloud-changes.md)

Este documento destaca las importantes diferencias entre el complemento de Commerce integration framework (CIF) y las versiones de CIF antiguas, conocidas como CIF Classic (Quickstart) y CIF Open-source.

## Instalación y actualizaciones

El complemento AEM CIF se instala mediante Cloud Manager. La instalación requiere un crédito de CIF, excepto en los entornos limitados en los que CIF se puede instalar sin créditos. Los créditos se reciben automáticamente a través de la provisión del complemento CIF en su contrato de AEM.

El complemento se actualiza automáticamente como parte de la actualización normal de AEM as a Cloud Service.

### Versiones anteriores de CIF {#previous-versions-installation}

* CIF Classic: no se necesita instalación, CIF formaba parte de Quickstart. Las actualizaciones de CIF formaban parte de las actualizaciones regulares de AEM o del Service Pack
* CIF Open-source para AEM local: instalación mediante GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.
* CIF Open-source for AEM Adobe Managed Services: Instalación a través del equipo de cuenta de Adobe. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo {#endpoint-configuration}

El extremo se configura y actualiza a través de la interfaz de usuario de Cloud Manager o su CLI.

### Versiones anteriores de CIF {#previous-versions-endpoint}

* CIF Classic: mediante la configuración OSGi en AEM
* CIF Open-source: A través del Explorador de configuración de CIF

## Implementación del proyecto Venia de CIF {#venia-project}

El proyecto está disponible en [repositorio Git de Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) y la implementación se realizó a través de [Cloud Manager.](/help/implementing/deploying/overview.md)

### Versiones anteriores de CIF {#previous-versions-venia}

* CIF Classic: mediante la instalación de paquetes de AEM
* CIF Open-source: A través de [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es)

## Datos del catálogo de productos {#product-catalog-data}

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL requeridas. Estas API admiten el acceso a datos activos o clasificados en cualquier fecha determinada. No se necesita replicación.

### Versiones anteriores de CIF {#previous-versions-catalog}

* CIF Classic: los datos de productos en directo y clasificados se importan y persisten en JCR en AEM Author mediante la importación completa o delta de productos. Los datos del producto activos se replican en AEM Publish.

## Experiencias del catálogo de productos con el procesamiento en AEM {#catalog-experiences}

AEM procesa experiencias de catálogo de productos sobre la marcha mediante plantillas de catálogo de AEM que se han asignado a productos y categorías. No se necesita replicación.

### Versiones anteriores de CIF {#previous-cif-versions}

* CIF Classic: el autor de AEM crea una página de AEM para cada categoría o producto mediante la herramienta de modelo de catálogo. Estas páginas se replican en AEM Publish.

>[!NOTE]
>
>Para obtener documentación adicional sobre cómo usar CIF con AEM Managed Service o AEM On-Premise, consulte [Commerce integration framework.](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
