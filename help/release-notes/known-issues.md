---
title: Problemas conocidos
description: Notas de la versión específicas de los problemas conocidos con Adobe Experience Manager as a Cloud Service.
translation-type: ht
source-git-commit: ce82d7c9ca1fd8fe3d6f61213cfee360fc6496fd

---


# Problemas conocidos {#known-issues}

Este artículo enumera los problemas conocidos de Adobe Experience Manager as a Cloud Service. La lista se revisa y actualiza con cada versión de Experience Manager.

[Comuníquese con soporte técnico](https://helpx.adobe.com/support/experience-manager.html) para obtener más información sobre los problemas conocidos.

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Assets {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Algunos problemas conocidos son:

* **Esquema de metadatos**: la utilidad de clasificación de recursos solía causar un error de compilación de JSP. Se eliminó del esquema de metadatos. <!-- CQ-4282865, CQ-4284633 -->

### Futuras funciones de Assets {#upcoming-assets-capabilities}

Se espera que algunas funciones de Adobe Experience Manager Assets que dependen de las funciones básicas y que aún no están disponibles como una arquitectura de implementación de Experience Manager as a Cloud Service, se habiliten más adelante:

* Por ahora, la función de etiquetado inteligente mejorada que aprovecha los servicios de IA de Adobe I/O no está disponible.
* Funciones no habilitadas en este momento debido a la dependencia de las API del marco de integración comercial:
   * Modelos de flujo de trabajo de sesión fotográfica.
   * La pestaña Información del producto de la interfaz de usuario de las propiedades del recurso no se completó.
* Funciones no habilitadas en esta etapa debido a la dependencia de la integración de InDesign Server:
   * Plantillas y catálogos de recursos.
   * Vista previa de varias páginas de archivos de InDesign.

>[!MORELIKETHIS]
>
>* [Principales cambios en AEM](aem-cloud-changes.md)
>* [Funciones en desuso y eliminadas](deprecated-removed-features.md)
>* [Notas de la versión](home.md)

