---
title: Cambios importantes en el complemento del marco de integración comercial (CIF)
description: Cambios importantes del Commerce Integration Framework (CIF) en comparación con las versiones anteriores del CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 3%

---

# Cambios importantes en el complemento Commerce Integration Framework (CIF){#notable-changes}

Adobe Experience Manager as a Cloud Service AEM ofrece muchas nuevas funciones y posibilidades para administrar sus proyectos de. Para obtener más información acerca de estas funcionalidades, siga el vínculo de [cambios en Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Este documento destaca las importantes diferencias entre el complemento Commerce Integration Framework (CIF) y las versiones antiguas del CIF, conocidas como CIF clásico (Quickstart) y CIF de código abierto.

## Instalación y actualizaciones

AEM El complemento CIF de la aplicación se instala a través de Cloud Manager. La instalación requiere un crédito CIF, excepto para los entornos limitados en los que CIF se puede instalar sin créditos. AEM Los créditos se reciben automáticamente a través del suministro del complemento CIF en su contrato de.

AEM El complemento se actualiza automáticamente como parte de la actualización regular y as a Cloud Service de la.

**Versiones anteriores del CIF**

* CIF clásico: no se necesita instalación, CIF era parte de Quickstart. AEM Las actualizaciones del CIF formaban parte de las actualizaciones regulares de los paquetes de servicio o de los programas de servicio
* AEM CIF de código abierto para la instalación local de la: instalación a través de GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.
* AEM CIF de código abierto para Adobe Managed Services: instalación a través del equipo de cuenta de Adobe. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo

El extremo se configura y actualiza a través de la interfaz de usuario de Cloud Manager o su CLI.

**Versiones anteriores del CIF**

* AEM CIF clásico: a través de la configuración OSGi en el
* CIF Open-source: a través del explorador de configuración del CIF

## Implementación del proyecto CIF Venia

Proyecto disponible en [Repositorio de Git de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html) e implementación realizada mediante [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=es)

**Versiones anteriores del CIF**

* AEM CIF Classic: a través de la instalación del paquete de la
* CIF de código abierto: a través de [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es)

## Datos del catálogo de productos

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL requeridas. Estas API admiten el acceso a datos activos o clasificados en cualquier fecha determinada. No se necesita replicación.

**Versiones anteriores del CIF**

* CIF clásico: los datos de productos en vivo y clasificados se importan y persisten en JCR en AEM Author a través de la importación completa o delta de productos. Los datos del producto activos se replican en AEM Publish.

## AEM Experiencias del catálogo de productos con procesamiento de la

AEM AEM La función de procesamiento de experiencias de catálogo de productos se procesa sobre la marcha utilizando plantillas de catálogo de productos que se han asignado a productos y categorías, y que se pueden usar para crear experiencias de catálogo de productos. No se necesita replicación.

**Versiones anteriores del CIF**

* AEM CIF clásico: AEM Author crea una página de para cada categoría/producto mediante la herramienta de modelo de catálogo. Estas páginas se replican en AEM Publish.

>[!NOTE]
>
>AEM AEM Para obtener documentación adicional sobre cómo utilizar CIF con el servicio administrado por el usuario o el servicio administrado por el usuario en el sitio web, consulte el artículo sobre el uso de CIF con el servicio administrado por el usuario o el servicio administrado en el sitio web de [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
