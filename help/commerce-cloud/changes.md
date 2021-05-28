---
title: Cambios importantes del complemento Commerce Integration Framework (CIF)
description: Cambios importantes del marco de integración comercial (CIF) en comparación con las versiones anteriores del CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 5%

---

# Cambios importantes en el complemento Commerce Integration Framework (CIF){#notable-changes}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades para gestionar sus Proyectos AEM. Para obtener más información sobre estas funcionalidades, siga el enlace para [cambios a Experience Manager como Cloud Service](/help/release-notes/aem-cloud-changes.md).

Este documento destaca las importantes diferencias entre el complemento Commerce Integration Framework (CIF) y las versiones anteriores del CIF, conocidas principalmente como CIF Classic (Quickstart) y CIF Open-source.

## Instalación y actualizaciones

El complemento AEM CIF se instala mediante Cloud Manager. La instalación requiere un crédito CIF, excepto para los entornos limitados en los que CIF puede instalarse sin créditos. Los créditos se reciben automáticamente mediante el aprovisionamiento del complemento CIF en su contrato AEM.

El complemento se actualiza automáticamente como parte del AEM normal como actualizaciones de Cloud Service.

**Versiones anteriores del CIF**

* CIF Classic: No se necesita instalación, CIF era parte de Quickstart. Las actualizaciones del CIF formaban parte de actualizaciones AEM o service pack normales
* CIF Código abierto para AEM locales: Instalación a través de GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.
* CIF Open-source para AEM Adobe Managed Services: Instalación mediante Customer Success Manager. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo

El extremo se configura y actualiza a través de la interfaz de usuario de Cloud Manager o su CLI.

**Versiones anteriores del CIF**

* CIF Classic: A través de la configuración OSGi en AEM
* CIF Open-source: A través del navegador de configuración del CIF

## Implementación del proyecto CIF Venia

Proyecto disponible en [Repositorio Git de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) e implementación realizada mediante [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html)

**Versiones anteriores del CIF**

* CIF Classic: A través de AEM instalación del paquete
* CIF Open-source: A través de [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es)

## Datos del catálogo de productos

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL necesarias. Estas API admiten el acceso a los datos activos o por etapas en cualquier fecha determinada. No se necesita replicación.

**Versiones anteriores del CIF**

* CIF Classic: Los datos de productos activos y por etapas se importan y persisten en JCR en AEM Author mediante la importación completa o delta de productos. Los datos del producto activo se replican en AEM Publish.

## Experiencias del catálogo de productos con AEM renderización

AEM procesa las experiencias del catálogo de productos sobre la marcha mediante AEM plantillas de catálogo que se han asignado a productos y categorías. No se necesita replicación.

**Versiones anteriores del CIF**

* CIF Classic: AEM Author crea una página AEM para cada categoría o producto con la herramienta de modelo del catálogo. Estas páginas se replican en AEM Publish.

>[!NOTE]
>
>Para obtener documentación adicional sobre cómo utilizar CIF con AEM servicio administrado o AEM local, consulte [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
