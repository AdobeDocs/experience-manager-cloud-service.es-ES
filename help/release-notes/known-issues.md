---
title: Problemas conocidos
description: Notas de la versión específicas de los problemas conocidos con Adobe Experience Manager as a Cloud Service.
translation-type: ht
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Problemas conocidos {#known-issues}

Este artículo enumera los problemas conocidos de Adobe Experience Manager as a Cloud Service. La lista se revisa y actualiza con cada versión de Experience Manager.

[Póngase en contacto con el equipo de asistencia](https://helpx.adobe.com/support/experience-manager.html) para obtener más información sobre los problemas conocidos.

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Assets {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Algunos problemas conocidos son:

* **Esquema de metadatos**: la utilidad de clasificación de recursos puede provocar un error de compilación de JSP. Una solución consiste en quitar el componente de clasificación de recursos del esquema de metadatos. <!-- CQ-4282865 -->

Algunas limitaciones de las funciones de Assets son:

* Con AEM Assets as a Cloud Service, la función Recursos conectados se activa cuando AEM 6.5 Sites se implementa en AMS.

### Futuras funciones de Assets {#upcoming-assets-capabilities}

Se espera que algunas funciones de Adobe Experience Manager Assets que dependen de las funciones básicas y que aún no están disponibles como una arquitectura de implementación de Experience Manager as a Cloud Service, se habiliten más adelante:

* La publicación en Brand Portal no está habilitada en este momento. Puede ampliar e integrar la implementación de [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) para casos prácticos de distribución de recursos.
* Por ahora, la función de etiquetado inteligente mejorada que aprovecha los servicios de IA de Adobe I/O no está disponible.
* Funciones no habilitadas en este momento debido a la dependencia de las API del marco de integración comercial:
   * Modelos de flujo de trabajo de sesión fotográfica.
   * La pestaña Información del producto de la interfaz de usuario de las propiedades del recurso no está rellenada.
* Funciones no habilitadas en este momento debido a la dependencia de la integración de InDesign Server:
   * Plantillas y catálogos de recursos.
   * Vista previa de varias páginas de archivos de InDesign.

>[!MORELIKETHIS]
>
>* [Principales cambios en AEM](aem-cloud-changes.md)
>* [Funciones en desuso y eliminadas](deprecated-removed-features.md)
>* [Notas de versión](home.md)

