---
title: Eliminación de dependencias externas para instalaciones existentes
description: Eliminación de dependencias externas para instalaciones existentes
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: 80a32672ec018274b0410abfa14fdd761fdb5aba
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 41%

---

# Eliminación de dependencias externas para instalaciones existentes {#remove-external-depedencies}

Adobe recomienda ejecutar los pasos de configuración para las instalaciones de conectores mejoradas existentes para Workfront a fin de eliminar las dependencias de los puntos de distribución de Hoodoo.

>[!NOTE]
>
>Ejecute los pasos de configuración solo si ha instalado el conector mejorado para Workfront antes de marzo de 2022. No existen dependencias en los puntos de distribución de Hoodoo para las nuevas instalaciones de conectores mejoradas para Workfront a partir de marzo de 2022.

Para eliminar las dependencias externas:

1. Quite la siguiente configuración del repositorio Hoodoo del elemento principal `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Quite la siguiente configuración de servidor del archivo `settings.xml`, disponible en `./cloudmanager/maven/settings.xml`:

   ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
   ```

1. Ejecute los [nuevos pasos de instalación](workfront-connector-install.md).


**Consulte también**

* [Traducir recursos](/help/assets/translate-assets.md)
* [API HTTP de recursos](/help/assets/mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](/help/assets/file-format-support.md)
* [Buscar recursos](/help/assets/search-assets.md)
* [Recursos de red](/help/assets/use-assets-across-connected-assets-instances.md)
* [Informes de recurso](/help/assets/asset-reports.md)
* [Esquemas de metadatos](/help/assets/metadata-schemas.md)
* [Descarga de recursos](/help/assets/download-assets-from-aem.md)
* [Administración de metadatos](/help/assets/manage-metadata.md)
* [Administración de plantillas de Dynamic Media](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [Administrar informes](/help/assets/manage-reports-assets-view.md)
* [Facetas de búsqueda](/help/assets/search-facets.md)
* [Administrar colecciones](/help/assets/manage-collections.md)
* [Importación masiva de metadatos](/help/assets/metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

