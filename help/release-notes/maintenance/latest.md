---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fd687498a8c72bf5d47b7b97aadf22d7d1e8dd2b
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 30%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 16799 {#release-16799}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 16799, que se publicó el miércoles, 18 de junio de 2024. La versión de mantenimiento anterior fue la 16544.

La activación de funcionalidades 2024.6.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-16799}

* ASSETS-31977: operaciones mejoradas de movimiento, copia y eliminación de recursos.
* ASSETS-33618: transcripción y traducción automáticas para vídeos en Dynamic Media.
* ASSETS-35185: Acción de aprobación para ContentHub y DM y añadir propiedades a las propiedades damAssetLucene.
* ASSETS-35533: agregue propiedades DRM y CAI al índice damAssetLucene.
* ASSETS-37280: Gestión secuencial de trabajos de traducción cuando el subtítulo de origen (vtt) aún se está procesando.
* ASSETS-37559: evento de eliminación de recursos mejorado.
* ASSETS-37723: Implementar el evento de publicación de recursos.
* ASSETS-37724: Implementar el evento de cancelación de publicación de recursos.
* ASSETS-38614: mejoras en la IU de Vínculo compartido.
* ASSETS-39601: aplique la regex de validación automáticamente al nombre de LiveCopy del recurso.
* ASSETS-39454: Actualice a la versión 2024.5.0 de visores en Quickstart.
* CNTBF-184: Rutas de soporte debajo `/conf` en Reflujo de contenido.

### Problemas solucionados {#fixed-issues-16799}

* ASSETS-37335: Al Editar El Panel Buscar En El Filtro, Se Desactivan Todas Las Casillas.
* AEM ASSETS-38069: Problema de vista previa del PDF de DAM en la selección de filtros de la cronología.
* ASSETS-38215: el botón de licencia de Adobe Stock AEM aparece atenuado en la as a Cloud Service para la suscripción de empresa de la.
* ASSETS-38578: hipervínculos incorrectos en el informe de uso compartido de vínculos de Assets.
* ASSETS-38678: vea la configuración dañada en los detalles de la colección.
* ASSETS-39071: La entrega optimizada para la web puede producir una excepción si el tipo MIME de la representación original es nulo.
* ASSETS-39316: La ordenación por nombre no funciona en Colecciones.
* ASSETS-39377: La importación masiva desde OneDrive puede fallar al recibir contrapresión desde la API remota.
* ASSETS-39428: Problemas de procesamiento en la IU de Administración de derechos de autor.
* CQ-4357150: Guava en el paquete cq-content-sync.
* GRANITE-52573: Solicitudes que contienen una barra doble `//` se rechazan con el código de estado 400.
* SCRNS-4194: Elimine la dependencia de las API de Google Guava.
* SCRNS-4360: falta el botón Administrar publicación y publicación rápida para usuarios no administradores en el proveedor de contenido para canales.
* SCRNS-4323: Ocultar/deshabilitar inicios desde screens.html.

### Problemas conocidos {#known-issues-16799}

>[!NOTE]
> AEM AEM El departamento de ingeniería ha identificado una regresión para la funcionalidad de los lanzamientos que afecta a las versiones actuales de los lanzamientos de la, empezando por 16461. Debido a esta regresión, los nuevos lanzamientos (creados después de aplicar nuevas versiones) que incluyen páginas no profundas no se promocionarán correctamente debido a la falta de configuraciones.
> En caso de que sus entornos se vean afectados, encontrará un script shell disponible para identificar y actualizar las configuraciones que faltan a través de la asistencia al cliente (referencia interna SITES-22457).
> Se pondrá a disposición una corrección a más largo plazo que garantizará que se creen nuevos lanzamientos con todas las configuraciones correctas. Hasta entonces, también está disponible una versión de parche interna bajo demanda.

#### Formularios

1. Si un usuario descarga la versión del SDK de AEM Forms mayor que `AEM Forms add-on v2024.05.04.00-240400`Sin embargo, el archivo por lotes no puede iniciar el servicio Docker. Para resolver este problema:
   1. Descargue la [carpeta](/help/forms/assets/sdk_hotfix.zip).
   1. Extraiga el contenido de la carpeta descargada y copie el `sdk.sh` y `sdk.bat` archivos.
   1. Reemplazar el existente `sdk.sh` y `sdk.bat` archivos en el SDK de AEM Forms con los nuevos archivos.

### Aviso de cambio {#change-notice-16799}

* Esta versión incluye las siguientes versiones nuevas del índice de productos:
   * **damAssetLucene-11**
   * **fragmentos-11**

  Las versiones personalizadas de las versiones de índice anteriores se combinarán automáticamente con la nueva versión del índice del producto. Aplique más actualizaciones personalizadas a la versión combinada.

* A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-16799}

Para saber qué es lo que está en desuso o se ha eliminado en AEM as a Cloud Service, consulte [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-16799}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
