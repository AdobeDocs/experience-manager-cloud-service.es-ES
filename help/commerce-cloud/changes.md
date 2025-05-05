---
title: Cambios importantes en el complemento de Commerce integration framework CIF ()
description: Cambios importantes del Commerce integration framework CIF CIF () en comparación con las versiones antiguas del.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Cambios importantes en el complemento de Commerce integration framework CIF (){#notable-changes}

Adobe Experience Manager as a Cloud Service AEM ofrece muchas nuevas funciones y posibilidades para administrar sus proyectos de. Para obtener más información acerca de estas funcionalidades, siga el vínculo de [cambios en el Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

En este documento se destacan las importantes diferencias entre el complemento de Commerce integration framework CIF CIF CIF CIF () y las versiones de antiguas, conocidas como Clásicas de la (Quickstart) y de código abierto (Open-source).

## Instalación y actualizaciones

AEM CIF El complemento de se instala mediante Cloud Manager. CIF CIF La instalación requiere un crédito de, excepto para las zonas protegidas, en las que se pueden instalar los entornos limitados sin que haya créditos. CIF AEM Los créditos se reciben automáticamente a través de la provisión del complemento de la en su contrato de la compañía.

El complemento se actualiza automáticamente como parte de la actualización normal de AEM as a Cloud Service.

CIF **Versiones anteriores**

* CIF CIF Clásico: no se necesita instalación, ya que el inicio rápido era parte de la instalación de, por lo tanto, no se requiere instalación. CIF AEM Las actualizaciones de la versión de la aplicación de datos formaban parte de las actualizaciones regulares de los paquetes de servicio o de la
* CIF AEM Código abierto para la instalación local de la: instalación a través de GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.
* CIF AEM Código abierto para la instalación de Managed Services de Adobe de: Instalación a través del equipo de cuenta de Adobe. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo

El extremo se configura y actualiza a través de la interfaz de usuario de Cloud Manager o su CLI.

CIF **Versiones anteriores**

* CIF AEM Clásico: configuración mediante OSGi en el
* CIF CIF Código abierto: A través del explorador de configuración de la

## CIF Implementación del proyecto Venia de la

El proyecto está disponible en [repositorio Git de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html?lang=es) y la implementación se realizó a través de [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=es)

CIF **Versiones anteriores**

* CIF AEM Clásico: A través de la instalación del paquete de la
* CIF Código abierto: A través de [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es)

## Datos del catálogo de productos

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL requeridas. Estas API admiten el acceso a datos activos o clasificados en cualquier fecha determinada. No se necesita replicación.

CIF **Versiones anteriores**

* CIF AEM Clásico: los datos de producto en vivo y clasificados se importan y persisten en JCR en el autor de la a través de la importación completa o delta del producto. AEM Los datos del producto activo se replican en Publish de forma.

## AEM Experiencias del catálogo de productos con procesamiento de la

AEM AEM La función de procesamiento de experiencias de catálogo de productos se procesa sobre la marcha utilizando plantillas de catálogo de productos que se han asignado a productos y categorías, y que se pueden usar para crear experiencias de catálogo de productos. No se necesita replicación.

CIF **Versiones anteriores**

* CIF AEM AEM Clásico de la: Autor de la publicación crea una página de la publicación para cada categoría / producto usando la herramienta de modelo del catálogo. AEM Estas páginas se replican en Publish de forma.

>[!NOTE]
>
>CIF AEM AEM Para obtener documentación adicional sobre cómo usar la con el servicio administrado por el usuario o el servicio administrado por el usuario, consulte [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
